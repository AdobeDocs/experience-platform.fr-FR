---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un segment
topic: tutorial
translation-type: tm+mt
source-git-commit: a6a1ecd9ce49c0a55e14b0d5479ca7315e332904

---


# Création d’un segment

Ce fournit un didacticiel pour le développement, le test, la prévisualisation et l’enregistrement d’une définition de segment à l’aide de l’API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentation.

Pour plus d’informations sur la création de segments à l’aide de l’interface utilisateur, consultez le guide [Créateur de](../ui/overview.md)segments.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans la création de  segments  de. Avant de commencer ce didacticiel, veuillez consulter la documentation des services suivants :

- [](../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
- [Adobe Experience Platform Segmentation Service](../home.md): Permet de créer  segments  à partir de données de client en temps réel.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plateforme organise les données d’expérience client.

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

## Développement d’une définition de segment

La première étape de la segmentation consiste à définir un segment, représenté dans un concept appelé définition **de** segment. Une définition de segment est un objet qui encapsule un écrit dans le langage de  de (PQL). Cet objet est également appelé prédicat **PQL**. Les prédicats PQL définissent les règles du segment en fonction des conditions liées aux données d’enregistrement ou de série chronologique que vous fournissez au client en temps réel. Consultez le guide [](../pql/overview.md) PQL pour en savoir plus sur l’écriture de  PQL.

Vous pouvez créer une nouvelle définition de segment en envoyant une requête POST au point de `/segment/definitions` fin dans l’API  client en temps réel. L’exemple suivant montre comment formater une demande de définition, y compris les informations requises pour qu’un segment soit défini avec succès.

Les définitions de segment peuvent être évaluées de deux manières : segmentation par lot et segmentation en flux continu. La segmentation par lot évalue les segments en fonction d’un calendrier prédéfini ou lorsque l’évaluation est déclenchée manuellement, tandis que la segmentation en flux continu évalue les segments dès que les données sont assimilées dans la plateforme. Ce didacticiel utilisera la segmentation **par** lot. Pour plus d’informations sur la segmentation en flux continu, veuillez lire la [présentation sur la segmentation](../api/streaming-segmentation.md)en flux continu.

**Format API**

```http
POST /segment/definitions
```

**Requête**

La requête suivante crée une nouvelle définition de segment pour un appelé &quot;MonProfil&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "My Sample Cart Abandons Segment Definition",
        "schema": {
            "name": "MyProfile",
        },
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "xEvent.metrics.commerce.abandons.value > 0",
        },
        "mergePolicyId": "mpid1",
        "description": "This Segment represents those users who have abandoned a cart"
    }'
```

| Propriété | Description |
| --------- | ------------ | 
| `name` | **Obligatoire.** Nom unique par lequel faire référence au segment. |
| `schema` | **Obligatoire.** associé aux entités du segment. Se compose d’un champ `id` ou `name` . |
| `expression` | **Obligatoire.** Entité qui contient des informations sur les champs concernant la définition de segment. |
| `expression.type` | Indique le type de  de . Actuellement, seul PQL est pris en charge. |
| `expression.format` | Indique la structure du   en valeur. Actuellement, le format suivant est pris en charge : <ul><li>`pql/text`: Représentation textuelle d’une définition de segment, selon la grammaire PQL publiée.  Par exemple : `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Un   conforme au type indiqué dans `expression.format`. |
| `mergePolicyId` | Identifiant de la stratégie de fusion à utiliser pour les données exportées. Pour plus d&#39;informations, veuillez lire le configuration de la stratégie de [fusion](../../profile/api/merge-policies.md). |
| `description` | Description lisible de la définition. |

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle définition de segment, y compris sa définition générée par le système et en lecture seule `id` qui sera utilisée plus loin dans ce didacticiel.

```json
{
    "id": "1234",
    "name": "My Sample Cart Abandons Segment Definition",
    "description": "This Segment represents those users who have abandoned a cart",
    "type": "PQL",
    "format": "pql/text",
    "expression": "xEvent.metrics.commerce.abandons.value > 0",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/core/ups/segment/definitions/1234"
        }
    }
}
```

## Estimation et d&#39;un  de

Au fur et à mesure que vous développez votre définition de segment, vous pouvez utiliser les outils d’estimation et de  dans le client en temps réel pourobtenir des informations au niveau du résumé, afin de vous assurer que vous isolez le de attendu. Les estimations fournissent des informations statistiques sur une définition de segment, telles que la taille   prévue et l’intervalle de confiance. Les  de fournissent un paginé de l’ admissible pour une définition de segment, ce qui vous permet de comparer les résultats avec ce que vous attendez.

En estimant et en prévisualisant vos  de , vous pouvez tester et optimiser vos prédicats PQL jusqu’à ce qu’ils produisent un résultat désirable, où ils peuvent ensuite être utilisés dans une définition de segment mise à jour.

Deux étapes sont nécessaires pour  ou obtenir une estimation de votre segment :

1. [Création d’une tâche de](#create-a-preview-job)
2. [d’estimation ou de](#view-an-estimate-or-preview) à l’aide de l’ID de la tâche d’

### Génération des estimations

Les exemples de données sont utilisés pour évaluer les segments et estimer le nombre de  admissibles. Les nouvelles données sont chargées en mémoire chaque matin (entre 12h00 et 2h00 heure du Pacifique, soit entre 7 et 9h00 heure du Pacifique) et tous les de segmentation sont estimés à l’aide des données d’exemple de cette journée. Par conséquent, les nouveaux champs ajoutés ou les données supplémentaires recueillies seront pris en compte dans les estimations le lendemain.

La taille de l’échantillon dépend du nombre total d’entités dans votre  de stockage de. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités dans le magasin  | Taille d’échantillon |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

Les estimations durent généralement entre 10 et 15 secondes, en commençant par une estimation approximative et en les affinant au fur et à mesure de la lecture d&#39;un plus grand nombre de documents.

### Création d’une tâche de 

Vous pouvez créer une tâche de  de en exécutant une requête POST sur le point de `/preview` fin.

**Format API**

```http
POST /preview
```

**Requête**

La requête suivante crée une tâche de . Le corps de la requête contient les informations  du relatives au segment.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "simple",
        "mergeStrategy": "simple"
    }'
```

| Propriété | Description |
| --------- | ----------- |
| `predicateExpression` | Le PQL   de des données par. |
| `predicateModel` | Le nom du XDM  les données  du est basé sur. |

**Réponse**

Une réponse réussie renvoie les détails de la tâche de  de nouvellement créée, y compris son ID et l’état de traitement actuel.

```json
{
   "state": "RUNNING",
   "previewQueryId": "4a45e853-ac91-4bb7-a426-150937b6af5c",
   "previewQueryStatus": "RUNNING",
   "previewId": "MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg",
   "previewExecutionId": 42
}
```

| Propriété | Description |
| -------- | ----------- |
| `state` | Etat actuel de la tâche de  du. Il sera à l’état &quot;EN COURS&quot; jusqu’à ce que le traitement soit terminé, puis devient &quot;RESULT_READY&quot; ou &quot;FAILED&quot;. |
| `previewId` | ID de la tâche de  de, à utiliser à des fins de recherche lors de l’affichage d’une estimation ou d’un  de, comme indiqué dans la section suivante. |

###  une estimation ou un 

Les processus d’estimation et de  sont exécutés de manière asynchrone, car les différents  de peuvent prendre plusieurs temps. Une fois qu’un  a été lancé, vous pouvez utiliser des appels d’API pour récupérer (GET) l’état actuel de l’estimation ou du  au fur et à mesure qu’il progresse.

A l’aide de l’API  de client en temps réel, vous pouvez rechercher l’état actuel d’une tâche  par son identifiant. Si l’état est &quot;RESULT_READY&quot;, vous pouvez  les résultats. Selon que vous souhaitez  une estimation ou un  de, chacun possède son propre point de terminaison dans l’API. Vous trouverez ci-dessous des exemples de ces deux types de mesures.

###  une estimation

**Format API**

```http
GET /estimate/{PREVIEW_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{PREVIEW_ID}` | ID de la tâche de  de à. |

**Requête**

La requête suivante récupère une estimation, à l’aide de l’ `previewId` étape précédente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive renvoie les détails de l’estimation.

```json
{
    "estimatedSize": 45,
    "state": "RESULT_READY",
    "profilesReadSoFar": 83834,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 46,
    "totalRows": 82473,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview?previewQueryId=f88bc056-ee48-40d5-9ddb-8865d7d6a0e0"
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `state` | Etat actuel de la tâche de  du. Sera &quot;EN COURS&quot; jusqu&#39;à ce que le traitement soit terminé, puis devient &quot;RESULT_READY&quot; ou &quot;FAILED&quot;. |
| `_links.preview` | Lorsque l’état actuel de la tâche  est &quot;RESULT_READY&quot;, cet attribut fournit une URL pour  l’estimation. |

###  un

**Format API**

```http
GET /preview/{PREVIEW_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{PREVIEW_ID}` | ID de la tâche de  de à. |

**Requête**

La requête suivante récupère un , à l’aide de la requête `previewId` créée à l’étape précédente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/preview/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails du  du.

```json
{
   "results": [{
         "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
               "XID_COOKIE_ID_1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
               },
               "XID_PROFILE_ID_1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
               }
            }
         }
      },
      {
         "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
               "XID_COOKIE_ID_2-1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

               },
               "XID_PROFILE_ID_2": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
               }
            }
         },
         "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
         },
         "state": "RESULT_READY",
         "links": {
            "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
            "next": "",
            "prev": ""
         }
      }
   ],
   "page": {
      "offset": 0,
      "size": 3
   }
}
```

## Étapes suivantes

Une fois que vous avez développé, testé et enregistré votre définition de segment, vous pouvez créer une tâche de segment afin de créer un   à l’aide de l’API de client en temps réel. Consultez le didacticiel sur l’ [évaluation et l’accès aux résultats](./evaluate-a-segment.md) des segments pour obtenir des instructions détaillées sur la manière d’y parvenir.