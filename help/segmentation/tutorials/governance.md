---
keywords: Experience Platform;accueil;rubriques les plus consultées;conformité de l’utilisation des données;application;application de la conformité de l’utilisation des données;service de segmentation;segmentation;segmentation;segmentation
solution: Experience Platform
title: Application de la conformité de l’utilisation des données à un segment d’audience à l’aide d’API
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel décrit les étapes à suivre pour appliquer la conformité de l’utilisation des données pour les segments ciblés de profils client en temps réel à l’aide d’API.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 55%

---

# Application de la conformité de l’utilisation des données à un segment ciblé à l’aide d’API

Ce tutoriel décrit les étapes à suivre pour appliquer la conformité de l’utilisation des données à [!DNL Real-time Customer Profile] segments d’audience à l’aide d’API.

## Prise en main

Ce tutoriel nécessite une compréhension pratique des composants suivants de [!DNL Adobe Experience Platform]:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): [!DNL Real-time Customer Profile] est un magasin d’entités de recherche générique utilisé pour gérer les [!DNL Experience Data Model (XDM)] données dans [!DNL Platform]. Profile fusionne les données de divers actifs de données d’entreprise et permet d’accéder à ces données dans une présentation unifiée.
   - [Stratégies de fusion](../../profile/api/merge-policies.md)[!DNL Real-time Customer Profile] : stratégies utilisées par pour déterminer quelles données peuvent être fusionnées en une vue unifiée dans certains cas. Les stratégies de fusion peuvent être configurées à des fins de gouvernance des données.
- [[!DNL Segmentation]](../home.md)[!DNL Real-time Customer Profile] : manière dont divise un grand groupe d’individus inclus dans la banque de profils en groupes plus petits partageant des caractéristiques et réagissant de la même manière aux stratégies marketing.
- [Gouvernance des données](../../data-governance/home.md): La gouvernance des données fournit l’infrastructure pour l’étiquetage et l’application de l’utilisation des données, à l’aide des composants suivants :
   - [Libellés d’utilisation des données](../../data-governance/labels/user-guide.md) : libellés utilisés pour décrire les jeux de données et les champs en fonction du niveau de sensibilité avec lequel traiter leurs données respectives.
   - [Stratégies d’utilisation des données](../../data-governance/policies/overview.md) : configurations indiquant quelles actions marketing sont autorisées sur les données classées selon des libellés d’utilisation de données particulières.
   - [Application des stratégies](../../data-governance/enforcement/overview.md): Permet d’appliquer des stratégies d’utilisation des données et d’empêcher les opérations de données qui constituent des violations de stratégie.
- [Environnements de test](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à la fonction [!DNL Platform] API.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, voir la section concernant la [lecture d&#39;exemples d&#39;appels d&#39;API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d&#39;abord suivre le [tutoriel d&#39;authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les environnements de test dans [!DNL Platform], consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Recherche d’une stratégie de fusion pour une définition de segment {#merge-policy}

Ce workflow commence par l’accès à un segment connu. Segments activés pour une utilisation dans [!DNL Real-time Customer Profile] contiennent un identifiant de stratégie de fusion dans leur définition de segment. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui à leur tour contiennent les libellés d’utilisation de données applicables.

En utilisant la variable [!DNL Segmentation] API, vous pouvez rechercher une définition de segment par son identifiant pour trouver sa stratégie de fusion associée.

**Format d’API**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | L’identifiant de la définition de segment que vous souhaitez rechercher. |

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
| `mergePolicyId` | L’identifiant de la stratégie de fusion utilisée pour la définition de segment. Cela sera utile pour l’étape suivante. |

## Recherche des jeux de données source à partir de la stratégie de fusion {#datasets}

Les stratégies de fusion contiennent des informations sur leurs jeux de données source, qui à leur tour contiennent des libellés d’utilisation des données. Vous pouvez rechercher les détails d’une stratégie de fusion en fournissant l’ID de stratégie de fusion dans une requête de GET à la variable [!DNL Profile] API. Vous trouverez plus d’informations sur les stratégies de fusion dans la section [guide de point de terminaison des stratégies de fusion](../../profile/api/merge-policies.md).

**Format d’API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | Identifiant de la stratégie de fusion obtenue à l’[étape précédente](#merge-policy). |

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
            "order": ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Propriété | Description |
| -------- | ----------- |
| `schema.name` | Nom du schéma associé à la stratégie de fusion. |
| `attributeMerge.type` | Type de configuration de priorité des données de la stratégie de fusion. Si la valeur est `dataSetPrecedence`, les jeux de données associés à cette stratégie de fusion sont répertoriés sous `attributeMerge > data > order`. Si la valeur est `timestampOrdered`, tous les jeux de données associés au schéma référencés dans `schema.name` sont utilisés par la stratégie de fusion. |
| `attributeMerge.data.order` | Si la valeur `attributeMerge.type` est `dataSetPrecedence`, cet attribut sera un tableau contenant les identifiants des jeux de données utilisés par cette stratégie de fusion. Ces identifiants sont utilisés à l’étape suivante. |

## Évaluation des jeux de données en cas de violation de stratégie

>[!NOTE]
>
> Cette étape suppose que vous disposez au moins d’une stratégie d’utilisation des données principale qui empêche l’exécution d’actions marketing spécifiques sur les données contenant certains libellés. Si vous ne disposez d’aucune stratégie d’utilisation applicable pour les jeux de données évalués, veuillez suivre la [tutoriel sur la création de stratégies](../../data-governance/policies/create.md) pour en créer un avant de poursuivre cette étape.

Une fois que vous avez obtenu les identifiants des jeux de données source de la stratégie de fusion, vous pouvez utiliser la variable [API Policy Service](https://www.adobe.io/experience-platform-apis/references/policy-service/) pour évaluer ces jeux de données par rapport à des actions marketing spécifiques afin de rechercher les violations de stratégie d’utilisation des données.

Pour évaluer les jeux de données, vous devez fournir le nom de l’action marketing dans le chemin d’une requête de POST, tout en fournissant les identifiants des jeux de données dans le corps de la requête, comme illustré dans l’exemple ci-dessous.

**Format d’API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing associée à la stratégie d’utilisation des données que vous évaluez les jeux de données. Selon que la stratégie a été définie par Adobe ou par votre organisation, vous devez utiliser `/marketingActions/core` ou `/marketingActions/custom`, respectivement. |

**Requête**

La requête suivante teste la variable `exportToThirdParty` action marketing par rapport aux jeux de données obtenus dans la variable [étape précédente](#datasets). Le payload de requête est un tableau contenant les identifiants de chaque jeu de données.

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
| `entityType` | Chaque élément du tableau de payload doit indiquer le type d’entité en cours de définition. Dans ce cas d’utilisation, la valeur sera toujours « dataSet ». |
| `entityID` | Chaque élément du tableau de payload doit fournir l’ID unique d’un jeu de données. |

**Réponse**

Une réponse réussie renvoie l’URI de l’action marketing, les libellés d’utilisation des données collectés à partir des jeux de données fournis et une liste de toutes les stratégies d’utilisation des données violées suite au test de l’action en fonction de ces libellés. Dans cet exemple, la stratégie &quot;Export Data to Third Party&quot; s’affiche dans la variable `violatedPolicies` , indiquant que l’action marketing a déclenché une violation de stratégie.

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
| `duleLabels` | Liste des libellés d’utilisation des données extraits des jeux de données fournis. |
| `discoveredLabels` | Liste des jeux de données fournis dans le payload de la requête affichant les libellés au niveau du jeu de données et au niveau du champ trouvées dans chaque jeu. |
| `violatedPolicies` | Un tableau répertoriant toutes les stratégies d’utilisation des données violées lors du test de l’action marketing (spécifiée dans `marketingActionRef`) par rapport au fourni `duleLabels`. |

En utilisant les données renvoyées dans la réponse de l’API, vous pouvez configurer des protocoles dans votre application d’expérience afin d’appliquer correctement les violations de stratégie lorsqu’elles se produisent.

## Filtrage des champs de données

Si votre segment d’audience ne réussit pas l’évaluation, vous pouvez ajuster les données incluses dans le segment à l’aide de l’une des deux méthodes décrites ci-dessous.

### Mise à jour de la stratégie de fusion de la définition de segment

La mise à jour de la stratégie de fusion d’une définition de segment modifie les jeux de données et les champs qui seront inclus dans l’exécution de la tâche de segmentation. Voir la section sur [mise à jour d’une stratégie de fusion existante](../../profile/api/merge-policies.md#update) pour plus d’informations, consultez le tutoriel sur les stratégies de fusion d’API .

### Restriction des champs de données spécifiques lors de l’exportation du segment

Lors de l’exportation d’un segment vers un jeu de données à l’aide de la variable [!DNL Segmentation] API, vous pouvez filtrer les données incluses dans l’exportation à l’aide de la variable `fields` . Tous les champs de données ajoutés à ce paramètre seront inclus dans l’exportation, tandis que tous les autres champs de données en seront exclus.

Prenons l’exemple d’un segment dont les champs de données sont nommés « A », « B » et « C ». Si vous ne souhaitez exporter que le champ « C », le `fields` paramètre contiendra seulement le champ « C ». Ainsi, les champs « A » et « B » seront exclus lors de l’exportation du segment.

Pour plus d’informations, consultez la section sur l’[exportation d’un segment](./evaluate-a-segment.md#export) dans le tutoriel sur la segmentation.

## Étapes suivantes

Dans ce tutoriel, vous avez cherché les libellés d’utilisation des données associés à un segment ciblé et les avez testés pour détecter des violations de stratégie en fonction d’actions marketing spécifiques. Pour plus d’informations sur la gouvernance des données dans [!DNL Experience Platform], veuillez lire la présentation de [Gouvernance des données](../../data-governance/home.md).
