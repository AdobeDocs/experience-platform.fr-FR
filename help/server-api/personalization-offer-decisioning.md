---
title: Personnalisation via Offer Decisioning
description: Découvrez comment utiliser l’API serveur pour diffuser et générer des expériences personnalisées via Offer Decisioning.
exl-id: 5348cd3e-08db-4778-b413-3339cb56b35a
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---

# Personnalisation via Offer Decisioning

## Vue d’ensemble {#overview}

L’API du serveur Edge Network peut fournir des expériences personnalisées gérées dans [Offer decisioning](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=fr) au canal web.

[!DNL Offer Decisioning] prend en charge une interface non visuelle pour créer, activer et diffuser vos activités et expériences de personnalisation.

## Conditions préalables {#prerequisites}

Personalization via [!DNL Offer Decisioning] nécessite que vous ayez accès à [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=fr) avant de configurer votre intégration.

## Configuration de votre flux de données {#configure-your-datastream}

Avant de pouvoir utiliser l’API serveur conjointement avec Offer Decisioning, vous devez activer la personnalisation Adobe Experience Platform sur votre configuration de flux de données et activer l’option **[!UICONTROL Offer decisioning]** .

Pour plus d’informations sur l’activation de l’Offer decisioning, reportez-vous au [guide sur l’ajout de services à un flux de données](../datastreams/overview.md#adobe-experience-platform-settings).

![Image de l’interface utilisateur montrant l’écran de configuration du service de flux de données, avec Offer decisioning sélectionné](assets/aep-od-datastream.png)

## Création d’audiences {#audience-creation}

[!DNL Offer Decisioning] repose sur le service de segmentation Adobe Experience Platform pour la création d’audiences. Vous trouverez la documentation de [!DNL Segmentation Service] [ici](../segmentation/home.md).

## Définition des portées de décision {#creating-decision-scopes}

[!DNL Offer Decision Engine] utilise les données Adobe Experience Platform et les [ profils clients en temps réel ](../profile/home.md), ainsi que le [!DNL Offer Library], pour diffuser des offres aux bons clients et aux bons canaux au bon moment.

Pour en savoir plus sur [!DNL Offer Decisioning Engine], consultez la [documentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=fr) dédiée.

Après avoir [configuré votre flux de données](#configure-your-datastream), vous devez définir les portées de décision à utiliser dans votre campagne de personnalisation.

[Les portées de décision](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html#add-decision-scopes) sont les chaînes JSON codées en base64 contenant les identifiants d’activité et d’emplacement que vous souhaitez que le [!DNL Offer Decisioning Service] utilise lors de la proposition d’offres.

**JSON d’étendue de décision**

```json
{
   "activityId":"xcore:offer-activity:11cfb1fa93381aca",
   "placementId":"xcore:offer-placement:1175009612b0100c"
}
```

**Chaîne codée en Base64 du périmètre de décision**

```shell
"eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
```

Après avoir créé vos offres et collections, vous devez définir une [portée de décision](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html#add-decision-scopes).

Copiez la portée de décision codée en Base64. Vous l’utiliserez dans l’objet `query` de la requête d’API de serveur.

![Image de l’interface utilisateur affichant l’interface utilisateur de l’Offer decisioning, mettant en évidence la portée de la décision.](assets/decision-scope.png)

```json
"query":{
   "personalization":{
      "decisionScopes":[
         "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
      ]
   }
}
```

## Exemple d’appel API {#api-example}

**Format d’API**

```http
POST /ee/v2/interact
```

### Requête {#request}

Vous trouverez ci-dessous une requête complète comprenant un objet XDM, un objet de données et une requête d’Offer decisioning.

>[!NOTE]
>
>Les objets `xdm` et `data` sont facultatifs et ne sont nécessaires à l’Offer decisioning que si vous avez créé des segments avec des conditions qui utilisent des champs dans l’un de ces objets.

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
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
                "version": "1.0",
                "environment": "serverapi"
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
            },
            "__adobe.target": {
                "profile.eyeColor": "brown",
                "profile.hairColor": "brown"
            }
        }
    },
    "query": {
        "personalization": {
            "decisionScopes": [
                "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
            ]
        }
    }
}'
```

### Réponse {#response}

L’Edge Network renvoie une réponse similaire à celle ci-dessous.

```json
{
   "requestId":"b375077d-7e1d-4c18-b7d3-e4da0fb4fbc5",
   "handle":[
      {
         "payload":[
            
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "id":"120d5db7-181c-42c5-8653-88b3cd3e1e69",
               "scope":"eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9",
               "activity":{
                  "id":"xcore:offer-activity:14efca8941895181",
                  "etag":"1"
               },
               "placement":{
                  "id":"xcore:offer-placement:12d544ae54e7e7db",
                  "etag":"1"
               },
               "items":[
                  {
                     "id":"xcore:personalized-offer:14efc848a3577d92",
                     "etag":"2",
                     "schema":"https://ns.adobe.com/experience/offer-management/content-component-json",
                     "data":{
                        "id":"xcore:personalized-offer:14efc848a3577d92",
                        "format":"application/json",
                        "language":[
                           "en-us"
                        ],
                        "content":"{\n\t\"ODEFirstTest\" : \"Personalizaton Content\"\n}",
                        "characteristics":{
                           "reporting":"testRequest"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCLr6xb39LxgBKgNPUjLwAbr6xb39Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Si le visiteur est admissible pour une activité de personnalisation basée sur les données envoyées à [!DNL Offer Decisioning], le contenu de l’activité pertinente se trouve sous l’objet `handle`, où le type est `personalization:decisions`.

D’autres contenus seront également renvoyés sous l’objet `handle`. D’autres types de contenu ne sont pas pertinents pour la personnalisation [!DNL Offer Decisioning]. Si le visiteur est admissible pour plusieurs activités, elles sont contenues dans un tableau .

Le tableau ci-dessous explique les éléments clés de cette partie de la réponse.

| Propriété | Description | Exemple |
|---|---|---|
| `scope` | Portée de décision associée aux offres proposées qui ont été renvoyées. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | Identifiant unique de l’activité d’offre. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | Identifiant unique de l’emplacement de l’offre. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | L’identifiant unique de l’offre proposée. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Le schéma du contenu associé à l’offre proposée. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | L’identifiant unique de l’offre proposée. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Format du contenu associé à l’offre proposée. | `"format": "text/html"` |
| `language` | Tableau de langues associées au contenu de l’offre proposée. | `"language": [ "en-US" ]` |
| `content` | Contenu associé à l’offre proposée au format d’une chaîne. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenu de l&#39;image associé à l&#39;offre proposée au format d&#39;une URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Objet JSON contenant les caractéristiques associées à l’offre proposée. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
