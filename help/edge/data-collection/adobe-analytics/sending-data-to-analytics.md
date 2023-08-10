---
title: Envoi de données à Adobe Analytics à l’aide du SDK Web de Adobe Experience Platform
description: Découvrez comment envoyer des données à Adobe Analytics à l’aide du SDK Web de Adobe Experience Platform.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;interaction web;pages vues;suivi des liens;liens;suivre les liens;cliquer sur la collection;cliquer sur la collection;
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Envoi de données à Adobe Analytics

Alors que dans le passé, il existait différentes fonctions pour distinguer une page vue d’un lien (par exemple, `s.t(), s.tl()`), dans le SDK Web, il n’y a que la variable `sendEvent` . Les données envoyées avec un événement déterminent s’il doit s’agir d’une page vue ou d’un lien. [En savoir plus sur les liens de suivi](../track-links.md).

## Envoi d’une page vue

Vous pouvez spécifier une page vue en définissant la variable `web.webPageDetails.pageViews.value=1` Variable .

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        "pageViews": {
            "value":1
         }
      }
    }
  }
});
```

Bien qu’Analytics enregistre techniquement une page vue même si cette variable n’est pas définie, il est recommandé de définir cette variable chaque fois que vous souhaitez enregistrer une page vue afin d’être explicite dans vos données et de BAT futur de votre implémentation.
