---
title: Envoi de données à Adobe Analytics à l’aide du SDK Web Adobe Experience Platform
description: Découvrez comment envoyer des données à Adobe Analytics à l’aide du kit Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;vues de page;suivi des liens;liens;suivi des liens;clicCollection;clic collection;clic collection;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '162'
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
