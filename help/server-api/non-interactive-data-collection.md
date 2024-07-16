---
title: Collecte de données non interactive
description: Découvrez comment l’API Adobe Experience Platform Edge Network Server effectue une collecte de données non interactive.
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 5%

---


# Collecte de données non interactive

## Vue d’ensemble {#overview}

Les points de terminaison de collecte de données d’événement non interactifs sont utilisés pour envoyer plusieurs événements à des jeux de données ou à d’autres sources Experience Platform.

L’envoi d’événements par lots est recommandé lorsque les événements d’utilisateur final sont placés en file d’attente localement pendant une courte période (par exemple, lorsqu’il n’y a aucune connexion réseau).

Les événements de lot ne doivent pas nécessairement appartenir au même utilisateur final, ce qui signifie que les événements peuvent contenir différentes identités dans leur objet `identityMap`.

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
| `dataStreamId` | `String` | Oui | L’identifiant du flux de données utilisé par le point de terminaison de la collecte de données. |
| `requestId` | `String` | Non | Fournissez un identifiant de suivi de requête externe. Si aucun n’est fourni, l’Edge Network en génère un pour vous et le renvoie dans le corps/les en-têtes de réponse. |
| `silent` | `Boolean` | Non | Paramètre booléen facultatif indiquant si l’Edge Network doit renvoyer une réponse `204 No Content` avec une charge utile vide ou non. Les erreurs critiques sont signalées à l’aide du code d’état HTTP et de la charge utile correspondants. |

### Réponse {#response}

Une réponse réussie renvoie l’un des états suivants, et `requestID` si aucun état n’a été fourni dans la requête.

* `202 Accepted` lorsque la requête a été traitée avec succès ;
* `204 No Content` lorsque la requête a été traitée avec succès et que le paramètre `silent` a été défini sur `true` ;
* `400 Bad Request` lorsque la requête n’a pas été correctement formée (par exemple, l’identité principale obligatoire est introuvable).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
