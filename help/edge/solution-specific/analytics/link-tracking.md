---
title: Suivi des pages et des liens avec Adobe Analytics
seo-title: Liaison du suivi à Adobe Analytics avec le SDK Web Adobe Experience Platform
description: Découvrez comment envoyer des données de lien vers l'Adobe Analytics avec le SDK Web Experience Platform
seo-description: Découvrez comment envoyer des données de lien vers l'Adobe Analytics avec le SDK Web Experience Platform
translation-type: tm+mt
source-git-commit: ab73e4d793cf39c29ddca385487bf027002db883
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---


# Envoi de données à Adobe Analytics

Alors que dans le passé il y avait différentes fonctions pour distinguer entre une vue de page et un lien (par exemple, `s.t(), s.tl()`), dans le SDK Web il n&#39;y a que la `sendEvent` commande. Les données envoyées avec un événement déterminent s’il doit s’agir d’une vue de page ou d’un lien.

## Envoi d’une vue de page

Vous pouvez spécifier une vue de page en définissant la `web.webPageDetails.pageViews.value=1` variable.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetailsr": {
        "pageViews": {
            "value":1
      }
    }
  }
});
```

Bien qu’Analytics enregistre techniquement une vue de page même si cette variable n’est pas définie, il est recommandé de définir cette variable chaque fois que vous souhaitez enregistrer une vue de page pour qu’elle soit explicite dans vos données et pour que votre implémentation soit à l’épreuve de l’avenir.

## Suivi des liens

Les liens peuvent être définis en ajoutant les détails sous la `web.webInteraction` partie du schéma. Il existe trois variables obligatoires : `web.webInteraction.name`, `web.webInteraction.type` et `web.webInteraction.linkClicks.value`.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value":1
      },
      "name":"My Custom Link", //Name that shows up in the custom links report
      "URL":"https://myurl.com", //the URL of the link
      "type":"other", // values: other, download, exit
    }
  }
});
```

Le type de lien peut être l’une des trois valeurs suivantes :

* **`other`:** Un lien personnalisé
* **`download`:** Un lien de téléchargement (qui peut être suivi automatiquement par la bibliothèque)
* **`exit`:** Un lien de sortie

### Suivi automatique des liens

Le SDK Web peut automatiquement effectuer le suivi de tous les clics sur les liens en activant [clickCollection](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled).

Les liens de téléchargement sont automatiquement détectés en fonction des types de fichiers courants. La logique de classification des téléchargements est configurable.
