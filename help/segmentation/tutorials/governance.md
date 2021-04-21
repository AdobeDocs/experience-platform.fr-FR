---
keywords: Experience Platform ; accueil ; rubriques populaires ; conformité à l’utilisation des données ; appliquer ; appliquer la conformité à l’utilisation des données ; Service de segmentation ; segmentation ; Segmentation ;
solution: Experience Platform
title: Appliquer la conformité à l’utilisation des données pour un segment d’Audience à l’aide d’API
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel décrit les étapes à suivre pour appliquer la conformité de l’utilisation des données pour les segments ciblés de profils client en temps réel à l’aide d’API.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 50%

---

# Application de la conformité de l’utilisation des données à un segment ciblé à l’aide d’API

Ce didacticiel décrit les étapes à suivre pour appliquer la conformité de l&#39;utilisation des données aux segments d&#39;audience [!DNL Real-time Customer Profile] à l&#39;aide des API.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants de [!DNL Adobe Experience Platform] :

- [[!DNL Real-time Customer Profile]](../../profile/home.md):  [!DNL Real-time Customer Profile] est un magasin d’entités de recherche générique, qui est utilisé pour gérer  [!DNL Experience Data Model (XDM)] les données au sein  [!DNL Platform]. Profile fusionne les données de divers actifs de données d’entreprise et permet d’accéder à ces données dans une présentation unifiée.
   - [Stratégies de fusion](../../profile/api/merge-policies.md)[!DNL Real-time Customer Profile] : stratégies utilisées par pour déterminer quelles données peuvent être fusionnées en une vue unifiée dans certains cas. Les stratégies de fusion peuvent être configurées à des fins [!DNL Data Governance].
- [[!DNL Segmentation]](../home.md)[!DNL Real-time Customer Profile] : manière dont divise un grand groupe d’individus inclus dans la banque de profils en groupes plus petits partageant des caractéristiques et réagissant de la même manière aux stratégies marketing.
- [[!DNL Data Governance]](../../data-governance/home.md):  [!DNL Data Governance] fournit l’infrastructure pour l’étiquetage et l’application des données, en utilisant les composants suivants :
   - [Libellés d’utilisation des données](../../data-governance/labels/user-guide.md) : libellés utilisés pour décrire les jeux de données et les champs en fonction du niveau de sensibilité avec lequel traiter leurs données respectives.
   - [Stratégies d’utilisation des données](../../data-governance/policies/overview.md) : configurations indiquant quelles actions marketing sont autorisées sur les données classées selon des libellés d’utilisation de données particulières.
   - [Application des](../../data-governance/enforcement/overview.md) politiques : Permet d’appliquer des stratégies d’utilisation des données et d’empêcher les opérations de données qui constituent des violations de stratégies.
- [Sandbox](../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les API [!DNL Platform].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Rechercher une stratégie de fusion pour une définition de segment {#merge-policy}

Ce workflow commence par l’accès à un segment connu. Les segments qui sont activés pour une utilisation dans [!DNL Real-time Customer Profile] contiennent un ID de stratégie de fusion dans leur définition de segment. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui à leur tour contiennent les libellés d’utilisation de données applicables.

À l&#39;aide de l&#39;API [!DNL Segmentation], vous pouvez rechercher une définition de segment par son identifiant afin de trouver la stratégie de fusion associée.

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

Les stratégies de fusion contiennent des informations sur leurs jeux de données source, qui contiennent à leur tour des étiquettes d’utilisation des données. Vous pouvez rechercher les détails d&#39;une stratégie de fusion en fournissant l&#39;ID de stratégie de fusion dans une demande de GET à l&#39;API [!DNL Profile]. Pour plus d&#39;informations sur les stratégies de fusion, consultez le [guide du point de terminaison des stratégies de fusion](../../profile/api/merge-policies.md).

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
> Cette étape suppose que vous disposez d’au moins une stratégie d’utilisation des données principale qui empêche l’exécution d’actions marketing spécifiques sur les données contenant certaines étiquettes. Si vous n&#39;avez pas de règles d&#39;utilisation applicables pour les jeux de données évalués, suivez le [didacticiel de création de stratégies](../../data-governance/policies/create.md) pour en créer une avant de poursuivre cette étape.

Une fois que vous avez obtenu les ID des jeux de données source de la stratégie de fusion, vous pouvez utiliser l&#39;[API du service de stratégie](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) pour évaluer ces jeux de données par rapport à des actions marketing spécifiques afin de vérifier les violations de la stratégie d&#39;utilisation des données.

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

La requête suivante teste l&#39;action marketing `exportToThirdParty` par rapport aux jeux de données obtenus à l&#39;étape [précédente](#datasets). La charge utile de requête est un tableau contenant les ID de chaque jeu de données.

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

Une réponse positive renvoie l’URI de l’action marketing, les étiquettes d’utilisation des données collectées à partir des jeux de données fournis et une liste de toute stratégie d’utilisation des données qui a été violée suite au test de l’action par rapport à ces étiquettes. Dans cet exemple, la stratégie &quot;Exporter les données vers un tiers&quot; est affichée dans la baie `violatedPolicies`, ce qui indique que l&#39;action marketing a déclenché une violation de la stratégie.

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
| `duleLabels` | Liste d’étiquettes d’utilisation des données extraites des jeux de données fournis. |
| `discoveredLabels` | Liste des jeux de données fournis dans le payload de la requête affichant les libellés au niveau du jeu de données et au niveau du champ trouvées dans chaque jeu. |
| `violatedPolicies` | Tableau répertoriant toutes les stratégies d&#39;utilisation des données qui ont été violées en testant l&#39;action marketing (spécifiée dans `marketingActionRef`) par rapport au `duleLabels` fourni. |

En utilisant les données renvoyées dans la réponse de l’API, vous pouvez configurer des protocoles dans votre application d’expérience afin d’appliquer de manière appropriée les violations de stratégie lorsqu’elles se produisent.

## Filtrage des champs de données

Si votre segment d’audience ne réussit pas l’évaluation, vous pouvez ajuster les données incluses dans le segment par l’une des deux méthodes décrites ci-dessous.

### Mise à jour de la stratégie de fusion de la définition de segment

La mise à jour de la stratégie de fusion d’une définition de segment modifie les jeux de données et les champs qui seront inclus dans l’exécution de la tâche de segmentation. Pour plus d&#39;informations, consultez la section [mise à jour d&#39;une stratégie de fusion existante](../../profile/api/merge-policies.md#update) dans le didacticiel de stratégie de fusion d&#39;API.

### Restriction des champs de données spécifiques lors de l’exportation du segment

Lors de l’exportation d’un segment vers un jeu de données à l’aide de l’API [!DNL Segmentation], vous pouvez filtrer les données incluses dans l’exportation à l’aide du paramètre `fields`. Tous les champs de données ajoutés à ce paramètre seront inclus dans l’exportation, tandis que tous les autres champs de données en seront exclus.

Prenons l’exemple d’un segment dont les champs de données sont nommés « A », « B » et « C ». Si vous ne souhaitez exporter que le champ « C », le `fields` paramètre contiendra seulement le champ « C ». Ainsi, les champs « A » et « B » seront exclus lors de l’exportation du segment.

Pour plus d’informations, consultez la section sur l’[exportation d’un segment](./evaluate-a-segment.md#export) dans le tutoriel sur la segmentation.

## Étapes suivantes

Dans ce tutoriel, vous avez cherché les libellés d’utilisation des données associés à un segment ciblé et les avez testés pour détecter des violations de stratégie en fonction d’actions marketing spécifiques. Pour plus d&#39;informations sur [!DNL Data Governance] dans [!DNL Experience Platform], veuillez lire l&#39;aperçu pour [[!DNL Data Governance]](../../data-governance/home.md).
