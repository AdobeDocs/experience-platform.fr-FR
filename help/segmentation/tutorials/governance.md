---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Appliquer la conformité d’utilisation des données aux segments de  '
topic: tutorial
translation-type: tm+mt
source-git-commit: 97ba7aeb8a67735bd65af372fbcba5e71aee6aae

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
   - [Stratégies](../../data-governance/policies/overview.md)d’utilisation des données : Configurations indiquant les actions marketing autorisées sur les données classées par des étiquettes d’utilisation de données particulières.
   - [Application](../../data-governance/enforcement/overview.md)des règles : Permet d’appliquer des stratégies d’utilisation des données et d’empêcher les opérations de données qui constituent des violations de stratégies.
- [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

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

## Rechercher une stratégie de fusion pour une définition de segment {#merge-policy}

Ce flux de travaux commence par l’accès à un segment   connu. Les segments qui sont activés pour une utilisation dans le de clients en temps réel contiennent un ID de stratégie de fusion dans leur définition de segment. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui à son tour contiennent les étiquettes d’utilisation de données applicables.

A l’aide de l’API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentation, vous pouvez rechercher une définition de segment par son identifiant afin de trouver sa stratégie de fusion associée.

**Format API**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | ID de la définition de segment que vous souhaitez rechercher. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

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

## Rechercher les jeux de données source à partir de la stratégie de fusion {#datasets}

Les stratégies de fusion contiennent des informations sur leurs jeux de données source, qui contiennent à leur tour des libellés d’utilisation des données. Vous pouvez rechercher les détails d’une stratégie de fusion en fournissant l’ID de stratégie de fusion dans une requête GET à l’API .

**Format API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | ID de la stratégie de fusion obtenue à l’étape [](#merge-policy)précédente. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

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

## Evaluer les jeux de données pour les violations de stratégie

>[!NOTE]  Cette étape suppose que vous disposez d’au moins une stratégie d’utilisation des données active qui empêche l’exécution d’actions marketing spécifiques sur des données contenant certaines étiquettes. Si vous ne disposez d’aucune stratégie d’utilisation applicable pour les jeux de données évalués, suivez le didacticiel [de création de](../../data-governance/policies/create.md) stratégies pour en créer une avant de poursuivre cette étape.

Une fois que vous avez obtenu les ID des jeux de données source de la stratégie de fusion, vous pouvez utiliser l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE Policy Service pour évaluer ces jeux de données par rapport à des actions marketing spécifiques afin de vérifier les violations de la stratégie d’utilisation des données.

Pour évaluer les jeux de données, vous devez indiquer le nom de l’action marketing dans le chemin d’une requête POST, tout en fournissant les ID de jeu de données dans le corps de la requête, comme illustré dans l’exemple ci-dessous.

**Format API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing associée à la stratégie d’utilisation des données par laquelle vous évaluez les jeux de données. Selon que la stratégie a été définie par Adobe ou votre organisation, vous devez utiliser `/marketingActions/core` ou `/marketingActions/custom`, respectivement. |

**Requête**

La requête suivante teste l’action `exportToThirdParty` marketing par rapport aux jeux de données obtenus à l’étape [](#datasets)précédente. La charge utile de requête est un tableau contenant les ID de chaque jeu de données.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780"
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df"
    }
  ]'
```

| Propriété | Description |
| --- | --- |
| `entityType` | Chaque élément du tableau de charge utile doit indiquer le type d&#39;entité en cours de définition. Dans ce cas d’utilisation, la valeur sera toujours &quot;dataSet&quot;. |
| `entityID` | Chaque élément du tableau de charge doit fournir l’identifiant unique d’un jeu de données. |

**Réponse**

Une réponse réussie renvoie l’URI de l’action marketing, les étiquettes d’utilisation des données collectées à partir des jeux de données fournis et un de toute stratégie d’utilisation des données violée suite au test de l’action par rapport à ces étiquettes. Dans cet exemple, la stratégie &quot;Exporter les données vers un tiers&quot; s’affiche dans le `violatedPolicies` tableau, indiquant que l’action marketing a déclenché une violation de la stratégie.

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{IMS_ORG}",
  "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
  "duleLabels": [
    "C1",
    "C2",
    "C4",
    "C5"
  ],
  "discoveredLabels": [
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C2",
            ],
            "path": "/properties/_customer"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/geoUnit"
          },
          {
            "labels": [
              "C1"
            ],
            "path": "/properties/identityMap"
          }
        ]
      }
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/createdByBatchID"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/faxPhone"
          }
        ]
      }
    }
  ],
  "violatedPolicies": [
    {
      "name": "Export Data to Third Party",
      "status": "ENABLED",
      "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
      ],
      "description": "Conditions under which data cannot be exported to a third party",
      "deny": {
        "operator": "OR",
        "operands": [
          {
            "label": "C1"
          },
          {
            "operator": "AND",
            "operands": [
              {
                "label": "C3"
              },
              {
                "label": "C7"
              }
            ]
          }
        ]
      },
      "imsOrg": "{IMS_ORG}",
      "created": 1565651746693,
      "createdClient": "{CREATED_CLIENT}",
      "createdUser": "{CREATED_USER",
      "updated": 1565723012139,
      "updatedClient": "{UPDATED_CLIENT}",
      "updatedUser": "{UPDATED_USER}",
      "_links": {
        "self": {
          "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
      },
      "id": "5d51f322e553c814e67af1a3"
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `duleLabels` | de libellés d’utilisation des données extraits des jeux de données fournis. |
| `discoveredLabels` |  des jeux de données fournis dans la charge utile de la demande, affichant les étiquettes au niveau du jeu de données et au niveau du champ trouvées dans chacun d’eux. |
| `violatedPolicies` | Tableau répertoriant toutes les stratégies d’utilisation des données qui ont été violées en testant l’action marketing (spécifiée dans `marketingActionRef`) par rapport aux stratégies fournies `duleLabels`. |

En utilisant les données renvoyées dans la réponse de l’API, vous pouvez configurer des protocoles dans votre application d’expérience afin d’appliquer correctement les violations de stratégie lorsqu’elles se produisent.

## Filtrage des champs de données

Si votre segment   ne réussit pas l’évaluation, vous pouvez ajuster les données incluses dans le segment par l’une des deux méthodes décrites ci-dessous.

### Mettre à jour la stratégie de fusion de la définition de segment

La mise à jour de la stratégie de fusion d’une définition de segment ajustera les jeux de données et les champs qui seront inclus lors de l’exécution de la tâche de segment. Pour plus d’informations, consultez la section sur la [mise à jour d’une stratégie](../../profile/api/merge-policies.md#update) de fusion existante dans le didacticiel sur la stratégie de fusion des API.

### Limiter des champs de données spécifiques lors de l’exportation du segment

Lors de l’exportation d’un segment vers un jeu de données à l’aide de l’API  client en temps réel, vous pouvez filtrer les données incluses dans l’exportation à l’aide du `fields` paramètre. Tous les champs de données ajoutés à ce paramètre seront inclus dans l’exportation, tandis que tous les autres champs de données seront exclus.

Prenons l’exemple d’un segment dont les champs de données sont nommés &quot;A&quot;, &quot;B&quot; et &quot;C&quot;. Si vous ne souhaitez exporter que le champ &quot;C&quot;, le `fields` paramètre contiendra le champ &quot;C&quot; seul. Ainsi, les champs &quot;A&quot; et &quot;B&quot; seraient exclus lors de l’exportation du segment.

Pour plus d’informations, voir la section sur l’ [exportation d’un segment](./evaluate-a-segment.md#export) dans le didacticiel de segmentation.

## Étapes suivantes

En suivant ce didacticiel, vous avez recherché les libellés d’utilisation des données associés à un segment  de et les avez testés pour détecter les violations de stratégie par rapport à des actions marketing spécifiques. Pour plus d’informations sur la gouvernance des données dans la plateforme d’expérience, voir l’aperçu [de la gouvernance des](../../data-governance/home.md)données.
