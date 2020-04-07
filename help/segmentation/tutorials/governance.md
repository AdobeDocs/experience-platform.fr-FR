---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Appliquer la conformité d’utilisation des données aux segments de  '
topic: tutorial
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07

---


# Appliquer la conformité à l’utilisation des données pour un segment   à l’aide d’API

Ce didacticiel décrit les étapes à suivre pour faire respecter la conformité de l’utilisation des données pour les de clients en temps réel   les segments de à l’aide des API.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [](../../profile/home.md)du client en temps réel : Le de clients en temps réel est un magasin d’entités de recherche générique et est utilisé pour gérer les données du modèle de données d’expérience (XDM) dans la plateforme.  fusionne les données dans divers actifs de données d’entreprise et permet d’accéder à ces données dans une présentation unifiée.
   - [Fusionner les stratégies](../../profile/api/merge-policies.md): Règles utilisées par le du client en temps réel pour déterminer quelles données peuvent être fusionnées dans un unifié  dans certaines conditions. Les stratégies de fusion peuvent être configurées à des fins de gouvernance des données.
- [Segmentation](../home.md): La manière dont le du client en temps réel divise un grand groupe d’individus contenus dans le magasin de  de en groupes plus petits qui partagent des caractéristiques similaires et réagissent de la même manière aux stratégies marketing.
- [Gouvernance](../../data-governance/home.md)des données : La gouvernance des données fournit l’infrastructure pour l’étiquetage et l’application de l’utilisation des données (DULE), en utilisant les composants suivants :
   - [Libellés](../../data-governance/labels/user-guide.md)d’utilisation des données : Étiquettes utilisées pour décrire les jeux de données et les champs en fonction du niveau de sensibilité avec lequel traiter leurs données respectives.
   - [Stratégies](../../data-governance/api/getting-started.md)d’utilisation des données : Configurations indiquant les actions marketing autorisées sur les données classées par des étiquettes d’utilisation de données particulières.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir effectuer des appels aux API de plateforme.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Recherche d’une stratégie de fusion pour une définition de segment

Ce flux de travaux commence par l’accès à un segment   connu. Les segments qui sont activés pour une utilisation dans le de clients en temps réel contiennent un ID de stratégie de fusion dans leur définition de segment. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui à son tour contiennent les étiquettes d’utilisation de données applicables.

A l’aide de l’API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentation, vous pouvez rechercher une définition de segment par son identifiant afin de trouver la stratégie de fusion associée.

**Format API**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | ID de la définition de segment à rechercher. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Répondre**

Une réponse réussie renvoie les détails de la définition de segment.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{IMS_ORG}",
    "name": "Cart abandons in CA",
    "description": "",
    "expression": {
        "type": "PQL", 
        "format": "pql/text", 
        "value": "homeAddress.countryISO = 'US'"
    },
    "mergePolicyId": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1556094486000,
    "updateEpoch": 1556094486000,
    "updateTime": 1556094486000
  }
}
```

| Propriété | Description |
| -------- | ----------- |
| `mergePolicyId` | ID de la stratégie de fusion utilisée pour la définition de segment. Elle sera utilisée à l’étape suivante. |

## Rechercher les jeux de données source à partir de la stratégie de fusion

Les stratégies de fusion contiennent des informations sur leurs jeux de données source, qui contiennent à leur tour des libellés DULE. Vous pouvez rechercher les détails d’une stratégie de fusion en fournissant l’ID de stratégie de fusion dans une requête GET à l’API .

**Format API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | ID de la stratégie de fusion obtenue à l’étape [](#lookup-a-merge-policy-for-a-segment-definition)précédente. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Répondre**

Une réponse réussie renvoie les détails de la stratégie de fusion.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence", 
        "data": {
            "order" : ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Propriété | Description |
| -------- | ----------- |
| `schema.name` | Nom du associé à la stratégie de fusion. |
| `attributeMerge.type` | Type de configuration de priorité des données pour la stratégie de fusion. Si la valeur est `dataSetPrecedence`, les jeux de données associés à cette stratégie de fusion sont répertoriés sous `attributeMerge > data > order`. Si la valeur est `timestampOrdered`définie, tous les jeux de données associés au référencé dans `schema.name` sont utilisés par la stratégie de fusion. |
| `attributeMerge.data.order` | Si la valeur `attributeMerge.type` est `dataSetPrecedence`, cet attribut sera un tableau contenant les ID des jeux de données utilisés par cette stratégie de fusion. Ces identifiants sont utilisés à l’étape suivante. |

## Rechercher les libellés d’utilisation des données pour les jeux de données source

Une fois que vous avez rassemblé les ID des jeux de données source de la stratégie de fusion, vous pouvez utiliser ces ID pour rechercher les libellés d’utilisation des données configurés pour les jeux de données eux-mêmes et les champs de données spécifiques qu’ils contiennent.

L’appel suivant à l’API [du service de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) catalogue récupère les libellés d’utilisation des données associés à un seul jeu de données en indiquant son ID dans le chemin d’accès à la requête :

**Format API**

```http
GET /dataSets/{DATASET_ID}/dule
```

| Propriété | Description |
| -------- | ----------- |
| `{DATASET_ID}` | ID du jeu de données dont vous souhaitez rechercher les étiquettes d’utilisation des données. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b95b155419ec801e6eee780/dule \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Répondre**

Une réponse réussie renvoie un de libellés d’utilisation des données associés au jeu de données dans son ensemble, ainsi que tous les champs de données spécifiques associés au source.

```json
{
    "connection": {},
    "dataset": {
        "identity": [],
        "contract": [
            "C3"
        ],
        "sensitive": [],
        "contracts": [
            "C3"
        ],
        "identifiability": [],
        "specialTypes": []
    },
    "fields": [],
    "schemaFields": [
        {
            "path": "/properties/personalEmail/properties/address",
            "identity": [
                "I1"
            ],
            "contract": [
                "C2",
                "C9"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C9"
            ],
            "identifiability": [
                "I1"
            ],
            "specialTypes": []
        }
    ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `dataset` | Objet contenant les libellés d’utilisation des données appliqués au jeu de données dans son ensemble. |
| `schemaFields` | Tableau d’objets représentant des champs de  spécifiques auxquels des libellés d’utilisation des données sont appliqués. |
| `schemaFields.path` | Chemin d’accès du champ de  dont les libellés d’utilisation des données sont répertoriés dans le même objet. |

## Filtrage des champs de données

>[!NOTE] Cette étape est facultative. Si vous ne souhaitez pas ajuster les données incluses dans votre segment en fonction des résultats de l’étape précédente de [recherche des étiquettes](#lookup-data-usage-labels-for-the-source-datasets)d’utilisation des données, vous pouvez passer à l’étape finale de l’ [évaluation des données en cas de violation](#evaluate-data-for-policy-violations)de stratégie.

Si vous souhaitez ajuster les données incluses dans votre segment  de , vous pouvez le faire en utilisant l’une des deux méthodes suivantes :

### Mettre à jour la stratégie de fusion de la définition de segment

La mise à jour de la stratégie de fusion d’une définition de segment ajustera les jeux de données et les champs qui seront inclus lors de l’exécution de la tâche de segment. Pour plus d’informations, voir la section sur la [mise à jour d’une stratégie](../../profile/api/merge-policies.md) de fusion existante dans le didacticiel sur la stratégie de fusion.

### Limiter des champs de données spécifiques lors de l’exportation du segment

Lors de l’exportation d’un segment vers un jeu de données à l’aide de l’API  client en temps réel, vous pouvez filtrer les données incluses dans l’exportation à l’aide du `fields` paramètre. Tous les champs de données ajoutés à ce paramètre seront inclus dans l’exportation, tandis que tous les autres champs de données seront exclus.

Prenons l’exemple d’un segment dont les champs de données sont nommés &quot;A&quot;, &quot;B&quot; et &quot;C&quot;. Si vous ne souhaitez exporter que le champ &quot;C&quot;, le `fields` paramètre contiendra le champ &quot;C&quot; seul. Ainsi, les champs &quot;A&quot; et &quot;B&quot; seraient exclus lors de l’exportation du segment.

Pour plus d’informations, voir la section sur l’ [exportation d’un segment](./evaluate-a-segment.md#export-a-segment) dans le didacticiel de segmentation.

## Évaluer les données en cas de violation de stratégie

Maintenant que vous avez rassemblé les libellés d’utilisation des données associés à votre segment  de , vous pouvez tester ces libellés par rapport aux actions marketing afin d’évaluer les violations de la stratégie d’utilisation des données. Pour obtenir des instructions détaillées sur la manière d’effectuer des évaluations de stratégie à l’aide de l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)DULE Policy Service, reportez-vous au  sur l’évaluation [des](../../data-governance/enforcement/overview.md)stratégies.

## Étapes suivantes

En suivant ce didacticiel, vous avez recherché les libellés d’utilisation des données associés à un segment  de et les avez testés pour détecter les violations de stratégie par rapport à des actions marketing spécifiques. Pour plus d’informations sur la gouvernance des données dans la plateforme d’expérience, voir l’aperçu [de la gouvernance des](../../data-governance/home.md)données.