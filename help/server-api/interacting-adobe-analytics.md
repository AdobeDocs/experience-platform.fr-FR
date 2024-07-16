---
title: Interagir avec Adobe Analytics
description: Découvrez comment utiliser l’API du serveur Edge Network pour interagir avec Adobe Analytics.
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: 5de1ec17b78c97be21c0d2afd6f0b119a6074b6f
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---

# Interagir avec Adobe Analytics

## Vue d’ensemble {#overview}

La collecte de données Adobe Analytics fonctionne en traduisant les données XDM dans un format compréhensible par Adobe Analytics. Plusieurs champs XDM sont [ automatiquement mappés](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html) aux variables Analytics. Vous pouvez également mapper manuellement les valeurs XDM aux variables Analytics héritées.

Pour permettre à Adobe Analytics de recevoir des données de l’API du serveur, vous devez [configurer votre flux de données](../datastreams/overview.md#adobe-analytics-settings) pour transférer des événements vers Adobe Analytics, en saisissant l’identifiant de suite de rapports dans la page de configuration du flux de données.

![Configuration Adobe Analytics Datastream](assets/analytics-datastream.png)

## Interagir avec Adobe Analytics {#interacting-analytics}

### Format d’API {#format}

```http
POST /ee/v2/interact?dataStreamId={DATASTREAM_ID}
```

### Requête {#request}

L’exemple ci-dessous inclut plusieurs valeurs mappées automatiquement à partir du groupe de champs `_experience.analytics`. Elle comprend également des couches de données basées sur JSON. Bien que ces couches de données ne puissent pas être mappées automatiquement, il est possible d’utiliser [Préparation de données pour la collecte de données](../datastreams/data-prep.md) pour mapper ces valeurs à un schéma qui contient des groupes de champs référencés ci-dessus.

Toutes les valeurs que les utilisateurs mappent à ces champs sont automatiquement associées aux valeurs Analytics appropriées, comme si elles étaient incluses dans la requête API.

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" \
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" \
-d '{
   "event": {
      "xdm": {
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev",
               "name": "Home Page"
            },
            "webReferrer": {
               "URL": ""
            }
         },
         "device": {
            "screenHeight": 1440,
            "screenWidth": 3440,
            "screenOrientation": "landscape"
         },
         "environment": {
            "type": "browser",
            "browserDetails": {
               "viewportWidth": 3440,
               "viewportHeight": 1440
            }
         },
         "placeContext": {
            "localTime": "2022-03-22T22:45:21.193-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-23T04:45:21.193Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "2.8.0+2.9.0",
            "environment": "browser"
         },
         "_experience": {
            "analytics": {
               "customDimensions": {
                  "eVars": {
                     "eVar14": "eVar14"
                  }
               },
               "event1to100": {
                  "event13": {
                     "value": 1
                  },
                  "event14": {
                     "value": 2
                  }
               }
            }
         }
      }
   },
   "data": {
      "page": {
         "pageInfo": {
            "pageName": "Promotions",
            "siteSection": "Home"
         },
         "promos": {
            "heroPromos": "purse,shoes,sunglasses"
         },
         "customVariables": {
            "testGroup": "orange/black theme"
         },
         "events": {
            "homePage": true
         },
         "products": [
            {
               "productSKU": "abc123",
               "productName": "shirt"
            }
         ]
      }
   }
}'
```

### Réponse {#response}

```json
{
   "requestId": "d2ad6364-5675-4a86-ba41-50e7a4c4a299",
   "handle": []
}
```
