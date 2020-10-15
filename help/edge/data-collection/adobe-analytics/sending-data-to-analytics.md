---
title: Suivi des pages et des liens avec Adobe Analytics
seo-title: Liaison du suivi à Adobe Analytics avec le SDK Web Adobe Experience Platform
description: Découvrez comment envoyer des données de lien vers l'Adobe Analytics avec le SDK Web Experience Platform
seo-description: Découvrez comment envoyer des données de lien vers l'Adobe Analytics avec le SDK Web Experience Platform
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 9e1ad05285b27a9fc8b56db903609add3fef144e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Envoi de données à Adobe Analytics

Alors que dans le passé il y avait différentes fonctions pour distinguer entre une vue de page et un lien (par exemple, `s.t(), s.tl()`), dans le SDK Web il n&#39;y a que la `sendEvent` commande. Les données envoyées avec un événement déterminent s’il doit s’agir d’une vue de page ou d’un lien. [En savoir plus sur le suivi des liens](../track-links.md)

## Envoi d’une vue de page

Vous pouvez spécifier une vue de page en définissant la `web.webPageDetails.pageViews.value=1` variable.

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

Bien qu’Analytics enregistre techniquement une vue de page même si cette variable n’est pas définie, il est recommandé de définir cette variable chaque fois que vous souhaitez enregistrer une vue de page pour qu’elle soit explicite dans vos données et pour votre implémentation future BAT.
