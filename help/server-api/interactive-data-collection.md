---
title: Collecte de données interactive
description: Découvrez comment l’API Adobe Experience Platform Edge Network Server effectue la collecte de données interactive.
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: f8434746c4a023ec895d23a59e04fca4baecfc36
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 15%

---

# Collecte de données interactive

## Vue d’ensemble {#overview}

Les points de terminaison de collecte de données interactives reçoivent un seul événement et sont utilisés lorsque le client s’attend à ce qu’une réponse soit renvoyée par le serveur Adobe Experience Platform Edge Network. Ces points de terminaison peuvent également renvoyer du contenu d’autres services Edge Network lors de la collecte de données.

>[!IMPORTANT]
>
>Le point d’entrée `/interact` est principalement conçu pour être utilisé par les SDK Experience Platform. Ce point de terminaison est sujet à des modifications additive et son comportement peut évoluer sans préavis. Par exemple, de nouveaux éléments pourront être ajoutés ultérieurement à la charge utile de la réponse.

La réponse du serveur comprend un ou plusieurs objets `Handle`, comme illustré ci-dessous.

## Exemple d’appel API

### Format d’API {#format}

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
   "event": {
      "xdm": {
         "identityMap": {
            "Email_LC_SHA256": [
               {
                  "id": "0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary": true
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
   }
}'
```

| Paramètre | Type | Obligatoire | Description |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Oui. | Identifiant de la banque de données. |
| `requestId` | `String` | Non | Fournissez un ID aléatoire client pour les demandes de serveur interne corrélées. Si aucun n’est fourni, le Edge Network en génère un et le renvoie dans la réponse. |

### Réponse {#response}

Une réponse réussie renvoie un état HTTP `200 OK`, avec un ou plusieurs objets `Handle`, selon les services Edge en temps réel activés dans la configuration de la chaîne de données.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
