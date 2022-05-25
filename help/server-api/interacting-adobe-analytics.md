---
title: Interaction avec Adobe Analytics
description: Découvrez comment utiliser l’API Edge Network Server pour interagir avec Adobe Analytics
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Analytics
keywords: la collecte de données; le point d'exutoire; les analyses; API réseau Adobe Experience Platform Edge;analytics
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: 08b1924c518a76873051b4038d8a1fe38dc7ddac
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# Interaction avec Adobe Analytics

## Présentation {#overview}

La collecte de données Adobe Analytics fonctionne en traduisant les données XDM dans un format compréhensible par Adobe Analytics. Plusieurs champs XDM [mappé automatiquement](../edge/data-collection/adobe-analytics/automatically-mapped-vars.md) aux variables Analytics.

Vous pouvez également [mappage manuel des valeurs XDM](../edge/data-collection/adobe-analytics/manually-mapping-variables.md) aux variables Analytics héritées.

Pour permettre à Adobe Analytics de recevoir des données de l’API serveur, vous devez [configuration de votre flux de données](../edge/datastreams/overview.md#adobe-analytics-settings) pour transférer des événements vers Adobe Analytics, en saisissant l’identifiant de suite de rapports dans la page de configuration de la chaîne de données.

![Configuration des flux de données Adobe Analytics](assets/analytics-datastream.png)

## Interaction avec Adobe Analytics {#interacting-analytics}

### Format d’API {#format}

```http
POST https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}
```

### Requête {#request}

L’exemple ci-dessous comprend plusieurs valeurs mappées automatiquement à partir de la variable `_experience.analytics` groupe de champs. Elle comprend également des couches de données basées sur JSON. Bien que ces couches de données ne puissent pas être mappées automatiquement, il est possible d’utiliser [Préparation de données pour la collecte de données](../edge/datastreams/data-prep.md) pour mapper ces valeurs à un schéma qui contient des groupes de champs référencés ci-dessus.

Toutes les valeurs que les utilisateurs mappent à ces champs sont automatiquement associées aux valeurs Analytics appropriées, comme si elles étaient incluses dans la requête API.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}" \
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
