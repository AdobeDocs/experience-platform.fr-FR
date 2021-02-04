---
title: Suivi des pages et des liens avec Adobe Analytics
seo-title: Liaison du suivi à Adobe Analytics avec le SDK Web Adobe Experience Platform
description: Découvrez comment envoyer des données de lien vers l'Adobe Analytics avec le SDK Web Experience Platform
seo-description: Découvrez comment envoyer des données de lien vers l'Adobe Analytics avec le SDK Web Experience Platform
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;vues de page;suivi des liens;liens;suivi des liens;clicCollection;clic collection;clic collection;
translation-type: tm+mt
source-git-commit: c9d777f4350f0b039608c4f9b01d5206994e2572
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Envoi de données à Adobe Analytics

Alors que dans le passé il y avait différentes fonctions pour distinguer une vue de page d&#39;un lien (par exemple, `s.t(), s.tl()`), dans le SDK Web il n&#39;y a que la commande `sendEvent`. Les données envoyées avec un événement déterminent s’il doit s’agir d’une vue de page ou d’un lien. [En savoir plus sur le suivi des liens](../track-links.md).

## Envoi d’une vue de page

Vous pouvez spécifier une vue de page en définissant la variable `web.webPageDetails.pageViews.value=1`.

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
