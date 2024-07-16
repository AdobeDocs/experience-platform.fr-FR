---
title: Vue d’ensemble de la personnalisation
description: Découvrez comment utiliser l’API Adobe Experience Platform Edge Network Server pour récupérer du contenu personnalisé à partir des solutions de personnalisation d’Adobe.
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: ae6c6d21b1eea900d01be3287827296071429d30
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 10%

---

# Vue d’ensemble de la personnalisation

Avec [!DNL Server API], vous pouvez récupérer du contenu personnalisé à partir des solutions de personnalisation d’Adobe, y compris [Adobe Target](https://business.adobe.com/fr/products/target/adobe-target.html), [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/ajo-home) et [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=fr).

En outre, le [!DNL Server API] optimise les fonctionnalités de personnalisation de la même page et de la page suivante par le biais de destinations de personnalisation Adobe Experience Platform, telles que [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) et la [connexion de personnalisation personnalisée](../destinations/catalog/personalization/custom-personalization.md). Pour savoir comment configurer Experience Platform pour la personnalisation de la même page et de la page suivante, consultez le [guide dédié](../destinations/ui/activate-edge-personalization-destinations.md).

Lors de l’utilisation de l’API serveur, vous devez intégrer la réponse fournie par le moteur de personnalisation à la logique utilisée pour effectuer le rendu du contenu sur votre site. Contrairement au [SDK Web](../web-sdk/home.md), [!DNL Server API] ne dispose pas d’un mécanisme pour appliquer automatiquement le contenu renvoyé par les solutions de personnalisation d’Adobe.

## Terminologie {#terminology}

Avant d’utiliser des solutions de personnalisation d’Adobe, veillez à comprendre les concepts suivants :

* **Offre** : une offre est un message marketing auquel des règles peuvent être associées et qui spécifie qui est éligible pour voir l&#39;offre.
* **Décision** : une décision (précédemment appelée activité d’offre) informe la sélection d’une offre.
* **Schéma** : le schéma d’une décision informe le type d’offre renvoyé.
* **Portée** : la portée de la décision.
   * Dans Adobe Target, il s’agit du [!DNL mbox]. [!DNL global mbox] est la portée `__view__`
   * Pour [!DNL Offer Decisioning], il s’agit des chaînes encodées Base64 de JSON contenant les identifiants d’activité et d’emplacement que le service d’offer decisioning doit utiliser pour proposer des offres.

## Objet `query` {#query-object}

La récupération de contenu personnalisé nécessite un objet de requête de requête explicite pour un exemple de requête. Le format de l’objet de requête est le suivant :

```json
{
  "query": {
    "personalization": {
      "schemas": [
        "https://ns.adobe.com/personalization/html-content-item",
        "https://ns.adobe.com/personalization/json-content-item",
        "https://ns.adobe.com/personalization/redirect-item",
        "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes": [
        "alloyStore",
        "siteWide",
        "__view__",
        "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
      ],
      "surfaces": [
        "web://mywebpage.html/",
        "web://mywebpage.html/#sample-json-content"
      ]
    }
  }
}
```



| Attribut | Type | Obligatoire / Facultatif | Description |
| --- | --- | --- | ---|
| `schemas` | `String[]` | Requis pour la personnalisation de Target. Facultatif pour l’Offer decisioning. | Liste des schémas utilisés dans la décision, pour sélectionner le type d&#39;offres renvoyé. |
| `scopes` | `String[]` | Facultatif | Liste des portées de décision. 30 maximum par demande. |

## Objet handle {#handle}

Le contenu personnalisé récupéré à partir des solutions de personnalisation est présenté dans un pseudo `personalization:decisions`, qui a le format suivant pour sa payload :

```json
{
   "type":"personalization:decisions",
   "payload":[
      {
         "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
         "scope":"__view__",
         "scopeDetails":{
            "decisionProvider":"TGT",
            "activity":{
               "id":"131010"
            },
            "experience":{
               "id":"0"
            },
            "strategies":[
               {
                  "algorithmID":"0",
                  "trafficType":"0"
               }
            ]
         },
         "items":[
            {
               "id":"0",
               "schema":"https://ns.adobe.com/personalization/dom-action",
               "meta":{
                  "offer.name":"Default Content",
                  "experience.id":"0",
                  "activity.name":"Luma target reporting",
                  "activity.id":"131010",
                  "experience.name":"Experience A",
                  "option.id":"2",
                  "offer.id":"0"
               },
               "data":{
                  "type":"setHtml",
                  "format":"application/vnd.adobe.target.dom-action",
                  "content":"Customer Service not chrome",
                  "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                  "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
               }
            }
         ]
      }
   ]
}
```

| Attribut | Type | Description |
| --- | --- | --- |
| `payload.id` | Chaîne | ID de décision. |
| `payload.scope` | Chaîne | Portée de décision qui a abouti aux offres proposées. |
| `payload.scopeDetails.decisionProvider` | Chaîne | Définissez cette variable sur `TGT` lors de l’utilisation d’Adobe Target. |
| `payload.scopeDetails.activity.id` | Chaîne | Identifiant unique de l’activité d’offre. |
| `payload.scopeDetails.experience.id` | Chaîne | Identifiant unique de l’emplacement de l’offre. |
| `items[].id` | Chaîne | Identifiant unique de l’emplacement de l’offre. |
| `items[].data.id` | Chaîne | L’identifiant de l’offre proposée. |
| `items[].data.schema` | Chaîne | Le schéma du contenu associé à l’offre proposée. |
| `items[].data.format` | Chaîne | Format du contenu associé à l’offre proposée. |
| `items[].data.language` | Chaîne | Tableau de langues associées au contenu de l’offre proposée. |
| `items[].data.content` | Chaîne | Contenu associé à l’offre proposée au format d’une chaîne. |
| `items[].data.selector` | Chaîne | Sélecteur d’HTML utilisé pour identifier l’élément DOM cible pour une offre d’action DOM. |
| `items[].data.prehidingSelector` | Chaîne | Sélecteur d’HTML utilisé pour identifier l’élément DOM à masquer lors de la gestion d’une offre d’action DOM. |
| `items[].data.deliveryUrl` | Chaîne | Contenu de l&#39;image associé à l&#39;offre proposée au format d&#39;une URL. |
| `items[].data.characteristics` | Chaîne | Caractéristiques associées à l’offre proposée au format d’un objet JSON. |

## Exemple d’appel API {#sample-call}

**Format d’API**

```http
POST /ee/v2/interact
```

### Requête {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event":{
      "xdm":{
         "identityMap":{
            "Email_LC_SHA256":[
               {
                  "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary":true
               }
            ]
         },
         "eventType":"web.webpagedetails.pageViews",
         "web":{
            "webPageDetails":{
               "URL":"https://alloystore.dev/",
               "name":"home-demo-Home Page"
            }
         },
         "timestamp":"2021-08-09T14:09:20.859Z"
      }
   },
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}'
```

| Paramètre | Type | Obligatoire | Description |
| --- | --- | --- | --- |
| `configId` | Chaîne | Oui | Identifiant de la banque de données. |
| `requestId` | Chaîne | Non | Fournissez un identifiant de suivi de requête externe. Si aucun n’est fourni, l’Edge Network en génère un pour vous et le renvoie dans le corps/les en-têtes de réponse. |

### Réponse {#response}

Renvoie un état `200 OK` et un ou plusieurs objets `Handle`, en fonction des services Edge activés dans la configuration du flux de données.

```json
{
   "requestId":"da20d11d-adac-458c-91ac-15bf4e420a15",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"__view__",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"131010"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ]
               },
               "items":[
                  {
                     "id":"0",
                     "schema":"https://ns.adobe.com/personalization/dom-action",
                     "meta":{
                        "offer.name":"Default Content",
                        "experience.id":"0",
                        "activity.name":"Luma target reporting",
                        "activity.id":"131010",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"0"
                     },
                     "data":{
                        "type":"setHtml",
                        "format":"application/vnd.adobe.target.dom-action",
                        "content":"Customer Service not chrome",
                        "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                        "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions"
      }
   ]
}
```

## Notifications {#notifications}

Les notifications doivent être déclenchées lorsqu’un contenu ou une vue prérécupéré a été visité ou rendu à l’utilisateur final. Pour que les notifications soient déclenchées pour la portée appropriée, veillez à suivre le `id` correspondant pour chaque portée.

Les notifications avec le `id` approprié pour les portées correspondantes doivent être déclenchées pour que les rapports soient correctement reflétés.

**Format d’API**

```http
POST /ee/v2/collect
```

### Requête {#notifications-request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "events":[
      {
         "xdm":{
            "identityMap":{
               "Email_LC_SHA256":[
                  {
                     "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                     "primary":true
                  }
               ]
            },
            "eventType":"web.webpagedetails.pageViews",
            "web":{
               "webPageDetails":{
                  "URL":"https://alloystore.dev/",
                  "name":"home-demo-Home Page"
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z",
            "_experience":{
               "decisioning":{
                  "propositions":[
                     {
                        "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                        "scope":"__view__",
                        "items":[
                           {
                              "id":"0"
                           }
                        ]
                     }
                  ]
               }
            }
         }
      }
   ]
}'
```

| Paramètre | Type | Obligatoire | Description |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Oui | L’identifiant du flux de données utilisé par le point de terminaison de la collecte de données. |
| `requestId` | `String` | Non | ID de suivi de requête externe externe. Si aucun n’est fourni, l’Edge Network en génère un pour vous et le renvoie dans le corps/les en-têtes de réponse. |
| `silent` | `Boolean` | Non | Paramètre booléen facultatif indiquant si l’Edge Network doit renvoyer une réponse `204 No Content` avec une charge utile vide. Les erreurs critiques sont signalées à l’aide du code d’état HTTP et de la charge utile correspondants. |

### Réponse {#notifications-response}

Une réponse réussie renvoie l’un des états suivants, et `requestID` si aucun état n’a été fourni dans la requête.

* `202 Accepted` lorsque la requête a été traitée avec succès ;
* `204 No Content` lorsque la requête a été traitée avec succès et que le paramètre `silent` a été défini sur `true` ;
* `400 Bad Request` lorsque la requête n’a pas été correctement formée (par exemple, l’identité principale obligatoire est introuvable).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
