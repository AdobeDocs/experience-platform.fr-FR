---
title: Collecte de données non interactive
description: Découvrez comment l’API Adobe Experience Platform Edge Network Server effectue une collecte de données non interactive
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs non-interactive data collection
keywords: collecte de données;collection;réseau adobe experience platform edge;api;collecte de données non interactives
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 5%

---

# Collecte de données non interactive

## Présentation {#overview}

Les points de terminaison de collecte de données d’événement non interactifs sont utilisés pour envoyer plusieurs événements à des jeux de données ou à d’autres sources Experience Platform.

L’envoi d’événements par lots est recommandé lorsque les événements d’utilisateur final sont placés en file d’attente localement pendant une courte période (par exemple, lorsqu’il n’y a aucune connexion réseau).

Les événements de lot ne doivent pas nécessairement appartenir au même utilisateur final, ce qui signifie que les événements peuvent contenir différentes identités dans leur `identityMap` .


<!-- However, when an `ECID` identity is sent via a cookie or metadata (in Edge Network accepted format), the Edge Network will read it and associate it with each event in the batch.

Each event should include the corresponding `XDM` content that needs to be collected.

>[!NOTE]
>
>[Experience Edge Identity Protocol](visitor-identification.md#experience-edge-identity-protocol) (`ECID` generation) is not applicable for data collection requests, meaning that events sent to this API should already have at least one identity associated to them. For server datastreams (calls to `server.adobedc.net`), the API requires that each event contains an identity **explicitly set as primary**. For device datastreams, the Edge Network will attempt to set the `ECID` as primary, when it is present, and no other primary identity is explicitly set.

-->

## Exemple d’appel API non interactif {#example}

### Format d’API {#api-format}

```http
POST /ee/v2/collect
```

### Requête {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "events": [
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "79bf8e83-f708-414b-b1ed-5789ff33bf0b",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webpagedetails.pageViews",
            "web": {
               "webPageDetails": {
                  "URL": "https://alloystore.dev/",
                  "name": "home-demo-Home Page"
               }
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         },
         "data": {
            "prop1": "custom value"
         }
      },
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "871e8460-a329-4e96-a5b6-ff359fb0afb9",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webinteraction.linkClicks",
            "web": {
               "webInteraction": {
                  "linkClicks": {
                     "value": 1
                  }
               },
               "name": "My Custom Link",
               "URL": "https://myurl.com"
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         }
      }
   ]
}'
```

| Paramètre | Type | Obligatoire | Description |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Oui | Identifiant du flux de données utilisé par le point de terminaison de la collecte de données. |
| `requestId` | `String` | Non | Fournissez un identifiant de suivi de requête externe. Si aucun n’est fourni, le réseau Edge en génère un pour vous et le renvoie dans le corps/les en-têtes de réponse. |
| `silent` | `Boolean` | Non | Paramètre booléen facultatif indiquant si le réseau Edge doit renvoyer une valeur `204 No Content` réponse avec un payload vide ou non. Les erreurs critiques sont signalées à l’aide du code d’état HTTP et de la charge utile correspondants. |


### Réponse {#response}

Une réponse réussie renvoie l’un des états suivants, et un `requestID` si aucun n’a été fourni dans la requête.

* `202 Accepted` lorsque la requête a été traitée avec succès ;
* `204 No Content` lorsque la requête a été traitée avec succès et que la variable `silent` a été défini sur `true`;
* `400 Bad Request` lorsque la requête n’a pas été correctement formée (par exemple, l’identité Principale obligatoire est introuvable).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
