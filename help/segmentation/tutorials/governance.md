---
solution: Experience Platform
title: Application de la conformité à l’utilisation des données pour un segment ciblé à l’aide d’API
type: Tutorial
description: Ce tutoriel décrit les étapes à suivre pour appliquer les définitions de segment de conformité d’utilisation des données à l’aide d’API.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 42%

---

# Application de la conformité d’utilisation des données pour une définition de segment à l’aide d’API

Ce tutoriel décrit les étapes à suivre pour appliquer la conformité d’utilisation des données aux définitions de segment à l’aide des API.

## Prise en main

Ce tutoriel nécessite une connaissance pratique des composants suivants de [!DNL Adobe Experience Platform] :

- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : [!DNL Real-Time Customer Profile] est un magasin d’entités de recherche générique qui est utilisé pour gérer les données [!DNL Experience Data Model (XDM)] dans [!DNL Experience Platform]. Profile fusionne les données de divers actifs de données d’entreprise et permet d’accéder à ces données dans une présentation unifiée.
   - [Politiques de fusion](../../profile/api/merge-policies.md) : règles utilisées par les [!DNL Real-Time Customer Profile] pour déterminer quelles données peuvent être fusionnées en une vue unifiée sous certaines conditions. Les politiques de fusion peuvent être configurées à des fins de gouvernance des données.
- [[!DNL Segmentation]](../home.md) : comment [!DNL Real-Time Customer Profile] un grand groupe d’individus contenu dans la banque de profils en plus petits groupes qui partagent des caractéristiques similaires et qui réagiront de la même manière aux stratégies marketing.
- [Gouvernance des données](../../data-governance/home.md) : la gouvernance des données fournit l’infrastructure pour l’étiquetage et l’application de l’utilisation des données, à l’aide des composants suivants :
   - [Libellés d’utilisation des données](../../data-governance/labels/user-guide.md) : libellés utilisés pour décrire les jeux de données et les champs en fonction du niveau de sensibilité avec lequel traiter leurs données respectives.
   - [Politiques d’utilisation des données](../../data-governance/policies/overview.md) : configurations indiquant quelles actions marketing sont autorisées sur les données classées selon des libellés d’utilisation de données particulières.
   - [Application des politiques](../../data-governance/enforcement/overview.md) : permet d’appliquer les politiques d’utilisation des données et d’empêcher les opérations de données en violation avec les politiques.
- [Sandbox](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin afin de passer avec succès des appels aux API [!DNL Experience Platform].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Recherche d’une politique de fusion pour une définition de segment {#merge-policy}

Ce workflow commence par accéder à une définition de segment connue. Les définitions de segment qui sont activées pour une utilisation dans [!DNL Real-Time Customer Profile] contiennent un ID de politique de fusion dans leur définition de segment. Cette politique de fusion contient des informations sur les jeux de données à inclure dans la définition de segment, qui à leur tour contiennent tous les libellés d’utilisation des données applicables.

À l’aide de l’API [!DNL Segmentation], vous pouvez rechercher une définition de segment par son identifiant pour trouver sa politique de fusion associée.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrgId": "{ORG_ID}",
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
| `mergePolicyId` | L’identifiant de la politique de fusion utilisée pour la définition de segment. Cela sera utile pour l’étape suivante. |

## Recherche des jeux de données source à partir de la politique de fusion {#datasets}

Les politiques de fusion contiennent des informations sur leurs jeux de données sources, qui à leur tour contiennent des libellés d’utilisation des données. Vous pouvez rechercher les détails d’une politique de fusion en fournissant l’identifiant de la politique de fusion dans une requête GET à l’API [!DNL Profile]. Vous trouverez plus d’informations sur les politiques de fusion dans le guide [point d’entrée des politiques de fusion](../../profile/api/merge-policies.md).

**Format d’API**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | Identifiant de la politique de fusion obtenue à l’[étape précédente](#merge-policy). |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de la politique de fusion.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{ORG_ID}",
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
| `schema.name` | Nom du schéma associé à la politique de fusion. |
| `attributeMerge.type` | Type de configuration de priorité des données de la politique de fusion. Si la valeur est `dataSetPrecedence`, les jeux de données associés à cette politique de fusion sont répertoriés sous `attributeMerge > data > order`. Si la valeur est `timestampOrdered`, tous les jeux de données associés au schéma référencés dans `schema.name` sont utilisés par la politique de fusion. |
| `attributeMerge.data.order` | Si la valeur `attributeMerge.type` est `dataSetPrecedence`, cet attribut sera un tableau contenant les identifiants des jeux de données utilisés par cette politique de fusion. Ces identifiants sont utilisés à l’étape suivante. |

## Évaluation des jeux de données pour les violations de politique

>[!NOTE]
>
> Cette étape suppose que vous disposez d’au moins une politique d’utilisation des données active qui empêche l’exécution d’actions marketing spécifiques sur les données contenant certains libellés. Si vous ne disposez d’aucune politique d’utilisation applicable pour les jeux de données évalués, suivez le [tutoriel sur la création de politiques](../../data-governance/policies/create.md) pour en créer une avant de poursuivre cette étape.

Une fois que vous avez obtenu les identifiants des jeux de données source de la politique de fusion, vous pouvez utiliser l’[API Policy Service](https://www.adobe.io/experience-platform-apis/references/policy-service/) pour évaluer ces jeux de données par rapport à des actions marketing spécifiques afin de vérifier les violations de la politique d’utilisation des données.

Pour évaluer les jeux de données, vous devez fournir le nom de l’action marketing dans le chemin d’accès d’une requête POST, tout en fournissant les identifiants du jeu de données dans le corps de la requête, comme illustré dans l’exemple ci-dessous.

**Format d’API**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Paramètre | Description |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Nom de l’action marketing associée à la politique d’utilisation des données selon laquelle vous évaluez les jeux de données. Selon que la politique a été définie par Adobe ou votre organisation, vous devez utiliser `/marketingActions/core` ou `/marketingActions/custom`, respectivement. |

**Requête**

La requête suivante teste l’action marketing `exportToThirdParty` par rapport aux jeux de données obtenus à l’[étape précédente](#datasets). La payload de la requête est un tableau contenant les identifiants de chaque jeu de données.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Une réponse réussie renvoie l’URI de l’action marketing, les libellés d’utilisation des données collectés à partir des jeux de données fournis et une liste de toutes les politiques d’utilisation des données enfreintes suite au test de l’action en fonction de ces libellés. Dans cet exemple, la politique « Exporter des données vers un tiers » s’affiche dans le tableau `violatedPolicies`, indiquant que l’action marketing a déclenché une violation de la politique.

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{ORG_ID}",
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
      "imsOrg": "{ORG_ID}",
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
| `violatedPolicies` | Tableau répertoriant toutes les politiques d’utilisation des données enfreintes lors du test de l’action marketing (spécifiée dans `marketingActionRef`) en fonction des `duleLabels` fournies. |

En utilisant les données renvoyées dans la réponse de l’API, vous pouvez configurer des protocoles dans votre application d’expérience afin d’appliquer de manière appropriée les violations de politique lorsqu’elles se produisent.

## Filtrage des champs de données

Si votre définition de segment n’est pas évaluée, vous pouvez ajuster les données incluses dans la définition de segment par l’une des deux méthodes décrites ci-dessous.

### Mise à jour de la politique de fusion de la définition de segment

La mise à jour de la politique de fusion d’une définition de segment modifie les jeux de données et les champs qui seront inclus dans l’exécution de la tâche de segmentation. Pour plus d’informations, reportez-vous à la section [Mise à jour d’une politique de fusion existante](../../profile/api/merge-policies.md#update) dans le tutoriel sur la politique de fusion des API.

### Limiter les champs de données spécifiques lors de l’exportation de la définition de segment

Lors de l’exportation d’une définition de segment vers un jeu de données à l’aide de l’API [!DNL Segmentation], vous pouvez filtrer les données incluses dans l’exportation à l’aide du paramètre `fields` . Tous les champs de données ajoutés à ce paramètre seront inclus dans l’exportation, tandis que tous les autres champs de données en seront exclus.

Prenons une définition de segment qui comporte des champs de données nommés « A », « B » et « C ». Si vous ne souhaitez exporter que le champ « C », le `fields` paramètre contiendra seulement le champ « C ». Ce faisant, les champs « A » et « B » sont exclus lors de l’exportation de la définition de segment.

Pour plus d’informations, reportez-vous à la section [exportation d’une définition de segment](./evaluate-a-segment.md#export) dans le tutoriel sur la segmentation.

## Étapes suivantes

En suivant ce tutoriel, vous avez recherché les libellés d’utilisation des données associés à une définition de segment et les avez testés pour les violations de politique par rapport à des actions marketing spécifiques. Pour plus d’informations sur la gouvernance des données dans [!DNL Experience Platform], consultez la présentation de la [gouvernance des données](../../data-governance/home.md).
