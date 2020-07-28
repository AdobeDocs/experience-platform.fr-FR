---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Application de la conformité de l’utilisation des données aux segments ciblés
topic: tutorial
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 46%

---


# Application de la conformité de l’utilisation des données à un segment ciblé à l’aide d’API

This tutorial covers the steps for enforcing data usage compliance for [!DNL Real-time Customer Profile] audience segments using APIs.

## Prise en main

This tutorial requires a working understanding of the following components of [!DNL Adobe Experience Platform]:

- [!DNL Real-time Customer Profile](../../profile/home.md): [!DNL Real-time Customer Profile] est un magasin d’entités de recherche générique, qui est utilisé pour gérer les données [!DNL Experience Data Model] (XDM) dans [!DNL Platform]. Profile fusionne les données de divers actifs de données d’entreprise et permet d’accéder à ces données dans une présentation unifiée.
   - [Stratégies de fusion](../../profile/api/merge-policies.md)[!DNL Real-time Customer Profile] : stratégies utilisées par pour déterminer quelles données peuvent être fusionnées en une vue unifiée dans certains cas. Merge policies can be configured for [!DNL Data Governance] purposes.
- [!DNL Segmentation](../home.md)[!DNL Real-time Customer Profile] : manière dont divise un grand groupe d’individus inclus dans la banque de profils en groupes plus petits partageant des caractéristiques et réagissant de la même manière aux stratégies marketing.
- [!DNL Data Governance](../../data-governance/home.md): [!DNL Data Governance] fournit l’infrastructure pour l’étiquetage et l’application des données (DULE), en utilisant les composants suivants :
   - [Libellés d’utilisation des données](../../data-governance/labels/user-guide.md) : libellés utilisés pour décrire les jeux de données et les champs en fonction du niveau de sensibilité avec lequel traiter leurs données respectives.
   - [Stratégies d’utilisation des données](../../data-governance/policies/overview.md) : configurations indiquant quelles actions marketing sont autorisées sur les données classées selon des libellés d’utilisation de données particulières.
   - [Application des](../../data-governance/enforcement/overview.md)politiques : Permet d’appliquer des stratégies d’utilisation des données et d’empêcher les opérations de données qui constituent des violations de stratégies.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully make calls to the [!DNL Platform] APIs.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Look up a merge policy for a segment definition {#merge-policy}

Ce workflow commence par l’accès à un segment connu. Segments that are enabled for use in [!DNL Real-time Customer Profile] contain a merge policy ID within their segment definition. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui à leur tour contiennent les libellés d’utilisation de données applicables.

Using the [!DNL Segmentation] API, you can look up a segment definition by its ID to find its associated merge policy.

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

Les stratégies de fusion contiennent des informations sur leurs jeux de données source, qui contiennent à leur tour des étiquettes d’utilisation des données. You can lookup the details of a merge policy by providing the merge policy ID in a GET request to the [!DNL Profile] API. Vous trouverez plus d’informations sur les stratégies de fusion dans le guide [des points de terminaison des stratégies de](../../profile/api/merge-policies.md)fusion.

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
            "order" : ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
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

## Evaluer les jeux de données en cas de violation de stratégie

>[!NOTE]
>
> Cette étape suppose que vous disposez d’au moins une stratégie d’utilisation des données active qui empêche l’exécution d’actions marketing spécifiques sur les données contenant certaines étiquettes. Si vous ne disposez d’aucune stratégie d’utilisation applicable pour les jeux de données évalués, suivez le didacticiel [de création de](../../data-governance/policies/create.md) stratégies pour en créer un avant de poursuivre cette étape.

Une fois que vous avez obtenu les ID des jeux de données source de la stratégie de fusion, vous pouvez utiliser l&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE Policy Service pour évaluer ces jeux de données par rapport à des actions marketing spécifiques afin de vérifier les violations de la stratégie d&#39;utilisation des données.

Pour évaluer les jeux de données, vous devez indiquer le nom de l’action marketing dans le chemin d’une requête de POST, tout en indiquant les ID de jeu de données dans le corps de la requête, comme indiqué dans l’exemple ci-dessous.

**Format d’API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing associée à la stratégie d’utilisation des données par laquelle vous évaluez les jeux de données. Selon que la stratégie a été définie par Adobe ou par votre organisation, vous devez utiliser `/marketingActions/core` ou `/marketingActions/custom`, respectivement. |

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
| `entityType` | Chaque élément du tableau de payload doit indiquer le type d’entité en cours de définition. Dans ce cas d’utilisation, la valeur sera toujours « dataSet ». |
| `entityID` | Chaque élément du tableau de payload doit fournir l’identifiant unique d’un jeu de données. |

**Réponse**

Une réponse réussie renvoie l’URI de l’action marketing, les étiquettes d’utilisation des données collectées à partir des jeux de données fournis et une liste de toute stratégie d’utilisation des données qui a été violée suite au test de l’action par rapport à ces étiquettes. In this example, the &quot;Export Data to Third Party&quot; policy is shown in the `violatedPolicies` array, indicating that the marketing action triggered a policy violation.

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
| `duleLabels` | liste d’étiquettes d’utilisation des données extraites des jeux de données fournis. |
| `discoveredLabels` | Liste des jeux de données fournis dans le payload de la requête affichant les libellés au niveau du jeu de données et au niveau du champ trouvées dans chaque jeu. |
| `violatedPolicies` | An array listing any data usage policies that were violated by testing the marketing action (specified in `marketingActionRef`) against the provided `duleLabels`. |

En utilisant les données renvoyées dans la réponse de l’API, vous pouvez configurer des protocoles dans votre application d’expérience afin d’appliquer de manière appropriée les violations de stratégie lorsqu’elles se produisent.

## Filtrage des champs de données

Si votre segment d’audience ne réussit pas l’évaluation, vous pouvez ajuster les données incluses dans le segment par l’une des deux méthodes décrites ci-dessous.

### Mise à jour de la stratégie de fusion de la définition de segment

La mise à jour de la stratégie de fusion d’une définition de segment modifie les jeux de données et les champs qui seront inclus dans l’exécution de la tâche de segmentation. See the section on [updating an existing merge policy](../../profile/api/merge-policies.md#update) in the API merge policy tutorial for more information.

### Restriction des champs de données spécifiques lors de l’exportation du segment

When exporting a segment to a dataset using the [!DNL Segmentation] API, you can filter the data that is included in the export by using the `fields` parameter. Tous les champs de données ajoutés à ce paramètre seront inclus dans l’exportation, tandis que tous les autres champs de données en seront exclus.

Prenons l’exemple d’un segment dont les champs de données sont nommés « A », « B » et « C ». Si vous ne souhaitez exporter que le champ « C », le `fields` paramètre contiendra seulement le champ « C ». Ainsi, les champs « A » et « B » seront exclus lors de l’exportation du segment.

Pour plus d’informations, consultez la section sur l’[exportation d’un segment](./evaluate-a-segment.md#export) dans le tutoriel sur la segmentation.

## Étapes suivantes

Dans ce tutoriel, vous avez cherché les libellés d’utilisation des données associés à un segment ciblé et les avez testés pour détecter des violations de stratégie en fonction d’actions marketing spécifiques. Pour plus d&#39;informations sur [!DNL Data Governance] dans [!DNL Experience Platform], veuillez lire l&#39;aperçu pour [!DNL Data Governance](../../data-governance/home.md).
