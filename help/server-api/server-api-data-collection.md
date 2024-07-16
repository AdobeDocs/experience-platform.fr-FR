---
title: Collecte de données
description: Découvrez comment l’API Adobe Experience Platform Edge Network Server structure les données collectées.
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 8%

---


# Collecte de données

[!DNL Server API] offre deux types de points de terminaison de collecte de données :

* [Points de terminaison de collecte de données interactives](interactive-data-collection.md), utilisés lorsque le client s’attend à ce qu’une réponse soit renvoyée par le serveur. Ces points de terminaison peuvent également renvoyer du contenu d’autres services Edge Network lors de la collecte de données.
* [Collecte de données d’événement non interactif](non-interactive-data-collection.md), utilisée lorsqu’aucune réponse n’est attendue du serveur. Ces points de terminaison sont utilisés uniquement pour la collecte de données.

## Objet `Event` {#event-object}

Les données collectées par [!DNL Server API] sont structurées dans l’objet `Event`. La structure de cet objet est décrite ci-dessous.

```json
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
            "name":"home-demo-Home Page",
            "pageViews":{
               "value":1
            }
         }
      },
      "placeContext":{
         "localTime":"2021-08-09T17:09:20.859+03:00",
         "localTimezoneOffset":-180
      },
      "timestamp":"2021-08-09T14:09:20.859Z"
   },
   "data":{
      "prop1":"custom value",
      "var10":"search (organic)"
   }
}
```

| Attribut | Type | Description |
| --- | --- | --- |
| `xdm` | Objet | *Obligatoire*. Objet JSON contenant des données au format XDM, correspondant au schéma du jeu de données. |
| `data` | Objet | *Facultatif*. Objet JSON contenant des données de formulaire libre, qui peuvent être mappées à XDM par l’Edge Network. |

