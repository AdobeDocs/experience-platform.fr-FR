---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un segment
topic: tutorial
translation-type: tm+mt
source-git-commit: 822f43b139b68b96b02f9a5fe0549736b2524ab7
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 2%

---


# Création d’un segment

Ce document fournit un didacticiel pour le développement, le test, la prévisualisation et l’enregistrement d’une définition de segment à l’aide de l’API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentation.

Pour plus d’informations sur la création de segments à l’aide de l’interface utilisateur, consultez le guide [du créateur de](../ui/overview.md)segments.

## Prise en main

Ce didacticiel nécessite une bonne compréhension des différents services d’Adobe Experience Platform impliqués dans la création de segments d’audience. Avant de commencer ce didacticiel, consultez la documentation relative aux services suivants :

- [Profil](../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [Service](../home.md)de segmentation des Adobes Experience Platform : Permet de créer des segments d’audience à partir des données du Profil client en temps réel.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les API Platform.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de l’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour passer des appels aux API Platform, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API Experience Platform, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de l&#39;Experience Platform sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes aux API Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Développement d’une définition de segment

La première étape de la segmentation consiste à définir un segment, représenté dans un concept appelé définition **de** segment. Une définition de segment est un objet qui encapsule une requête écrite dans le langage PQL (Profil Requête Language). Cet objet est également appelé prédicat **** PQL. Les prédicats PQL définissent les règles du segment en fonction des conditions liées à tout enregistrement ou série chronologique que vous fournissez au Profil client en temps réel. Consultez le guide [](../pql/overview.md) PQL pour en savoir plus sur l’écriture de requêtes PQL.

Vous pouvez créer une nouvelle définition de segment en adressant une requête POST au point de `/segment/definitions` terminaison dans l’API Profil client en temps réel. L&#39;exemple suivant montre comment formater une demande de définition, y compris les informations requises pour qu&#39;un segment soit défini avec succès.

Les définitions de segment peuvent être évaluées de deux manières : la segmentation par lot et la segmentation en flux continu. La segmentation par lot évalue les segments en fonction d’un calendrier prédéfini ou lorsque l’évaluation est déclenchée manuellement, tandis que la segmentation en flux continu évalue les segments dès que les données sont saisies dans Platform. Ce didacticiel utilisera la segmentation **par** lot. Pour plus d’informations sur la segmentation en flux continu, veuillez lire l’ [aperçu sur la segmentation](../api/streaming-segmentation.md)en flux continu.

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

La requête suivante crée une nouvelle définition de segment pour un schéma appelé &quot;MonProfil&quot;.

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
| `name` | **Obligatoire.** Nom unique auquel faire référence au segment. |
| `schema` | **Obligatoire.** schéma associé aux entités du segment. Se compose d’un champ `id` ou `name` d’un champ. |
| `expression` | **Obligatoire.** Entité qui contient des informations de champs sur la définition de segment. |
| `expression.type` | Indique le type d’expression. Actuellement, seul &quot;PQL&quot; est pris en charge. |
| `expression.format` | Indique la structure de l’expression en valeur. Actuellement, le format suivant est pris en charge : <ul><li>`pql/text`: Représentation textuelle d’une définition de segment, selon la grammaire PQL publiée.  Par exemple : `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | expression conforme au type indiqué dans `expression.format`. |
| `mergePolicyId` | Identifiant de la stratégie de fusion à utiliser pour les données exportées. Pour plus d&#39;informations, consultez le document [de configuration de la stratégie de](../../profile/api/merge-policies.md)fusion. |
| `description` | Description lisible de la définition. |

**Réponse**

Une réponse positive renvoie les détails de la nouvelle définition de segment, y compris sa définition générée par le système et en lecture seule `id` qui sera utilisée plus loin dans ce didacticiel.

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

## Estimation et prévisualisation d&#39;une audience {#estimate-and-preview-an-audience}

Au fur et à mesure que vous développez votre définition de segment, vous pouvez utiliser les outils d’estimation et de prévisualisation du Profil client en temps réel pour vue des informations de synthèse afin de vous assurer que vous isolez l’audience attendue. Les estimations fournissent des informations statistiques sur une définition de segment, telles que la taille d’audience estimée et l’intervalle de confiance. Les Prévisualisations fournissent des listes paginées de profils qualifiants pour une définition de segment, ce qui vous permet de comparer les résultats à ce que vous attendez.

En estimant et en prévisualisant votre audience, vous pouvez tester et optimiser vos prédicats PQL jusqu’à ce qu’ils produisent un résultat désirable, où ils peuvent ensuite être utilisés dans une définition de segment mise à jour.

Deux étapes sont nécessaires pour prévisualisation ou obtenir une estimation de votre segment :

1. [Création d’une tâche de prévisualisation](#create-a-preview-job)
2. [Estimation de la Vue ou prévisualisation](#view-an-estimate-or-preview) à l&#39;aide de l&#39;ID de la tâche de prévisualisation

### Génération des estimations

Les exemples de données servent à évaluer les segments et à estimer le nombre de profils admissibles. De nouvelles données sont chargées en mémoire chaque matin (entre 12h00 et 2h00 heure du Pacifique, soit entre 7 et 9h00 heure du Pacifique) et toutes les requêtes de segmentation sont estimées à l’aide des données d’exemple de cette journée. Par conséquent, les nouveaux champs ajoutés ou les données supplémentaires recueillies seront pris en compte dans les estimations le lendemain.

La taille de l’échantillon dépend du nombre total d’entités dans votre magasin de profils. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités dans le magasin de profils | Taille d’exemple |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

Les estimations durent généralement entre 10 et 15 secondes, en commençant par une estimation approximative et en se raffinant au fur et à mesure de la lecture d&#39;un plus grand nombre d&#39;enregistrements.

### Création d’une tâche de prévisualisation

Vous pouvez créer une tâche de prévisualisation en adressant une requête POST au point de `/preview` terminaison.

**Format d’API**

```http
POST /preview
```

**Requête**

La requête suivante crée une tâche de prévisualisation. Le corps de la demande contient les informations de requête relatives au segment.

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
| `predicateExpression` | expression PQL de requête des données par. |
| `predicateModel` | Nom du schéma XDM sur lequel reposent les données du Profil. |

**Réponse**

Une réponse positive renvoie les détails de la tâche de prévisualisation nouvellement créée, y compris son identifiant et l’état de traitement actuel.

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
| `state` | Etat actuel de la tâche de prévisualisation. Il sera à l’état &quot;EN COURS&quot; jusqu’à ce que le traitement soit terminé, puis devient &quot;RESULT_READY&quot; ou &quot;FAILED&quot;. |
| `previewId` | ID de la tâche de prévisualisation, à utiliser à des fins de recherche lors de l&#39;affichage d&#39;une estimation ou d&#39;une prévisualisation, comme indiqué dans la section suivante. |

### Vue d’une estimation ou d’une prévisualisation

Les processus d’estimation et de prévisualisation sont exécutés de manière asynchrone, car différentes requêtes peuvent prendre différentes longueurs de temps. Une fois qu&#39;une requête a été lancée, vous pouvez utiliser des appels d&#39;API pour récupérer (GET) l&#39;état actuel de l&#39;estimation ou de la prévisualisation au fur et à mesure qu&#39;elle progresse.

A l’aide de l’API Profil client en temps réel, vous pouvez rechercher l’état actuel d’une tâche de prévisualisation en fonction de son identifiant. Si l&#39;état est &quot;RESULT_READY&quot;, vous pouvez vue les résultats. Selon que vous souhaitez vue une estimation ou une prévisualisation, chacun possède son propre point de terminaison dans l&#39;API. Vous trouverez ci-dessous des exemples de ces deux types d&#39;utilisation.

### Vue d’une estimation

**Format d’API**

```http
GET /estimate/{PREVIEW_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{PREVIEW_ID}` | ID de la tâche de prévisualisation à vue. |

**Requête**

La requête suivante récupère une estimation, à l&#39;aide de l&#39; `previewId` étape précédente.

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
| `state` | Etat actuel de la tâche de prévisualisation. Sera &quot;EN COURS&quot; jusqu&#39;à ce que le traitement soit terminé, à ce moment-là il devient &quot;RESULT_READY&quot; ou &quot;FAILED&quot;. |
| `_links.preview` | Lorsque l&#39;état actuel de la tâche de prévisualisation est &quot;RESULT_READY&quot;, cet attribut fournit une URL pour la vue de l&#39;estimation. |

### Vue d’une prévisualisation

**Format d’API**

```http
GET /preview/{PREVIEW_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{PREVIEW_ID}` | ID de la tâche de prévisualisation à vue. |

**Requête**

La requête suivante récupère une prévisualisation à l’aide de la requête `previewId` créée à l’étape précédente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/preview/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de la prévisualisation.

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

Une fois que vous avez développé, testé et enregistré votre définition de segment, vous pouvez créer une tâche de segment afin de créer une audience à l’aide de l’API Profil client en temps réel. Consultez le didacticiel sur l’ [évaluation et l’accès aux résultats](./evaluate-a-segment.md) des segments pour obtenir des instructions détaillées sur la façon d’y parvenir.