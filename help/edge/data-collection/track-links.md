---
title: Suivi des liens avec Adobe Analytics
seo-title: Liaison du suivi à Adobe Analytics avec le SDK Web Adobe Experience Platform
description: Découvrez comment envoyer des données de lien vers l'Adobe Analytics avec le SDK Web Experience Platform
seo-description: Découvrez comment envoyer des données de lien vers l'Adobe Analytics avec le SDK Web Experience Platform
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: ab1618a9d8c6cc60407d301dad03983ce432bbbe
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 4%

---


# Suivi des liens

Les liens peuvent être définis manuellement ou suivis [automatiquement](#automaticLinkTracking). Le suivi manuel est effectué en ajoutant les détails sous la `web.webInteraction` partie du schéma. Il existe trois variables obligatoires :

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

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
  }
});
```

Le type de lien peut être l’une des trois valeurs suivantes :

* **`other`:** Un lien personnalisé
* **`download`:** Un lien de téléchargement
* **`exit`:** Un lien de sortie

## Suivi automatique des liens {#automaticLinkTracking}

Par défaut, le SDK Web capture, [étiquette](#labelingLinks)et [enregistre les clics sur les balises de lien](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) qualifiantes [](#qualifyingLinks) . Les clics sont capturés à l’aide d’un écouteur de événement de [capture](https://www.w3.org/TR/uievents/#capture-phase) de clics attaché au document.

Vous pouvez désactiver le suivi automatique des liens en [configurant](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) le SDK Web.

```javascript
clickCollectionEnabled: false
```

### Quelles balises remplissent les critères du suivi des liens ?{#qualifyingLinks}

Le suivi automatique des liens est effectué pour les balises d’ancrage `A` et `AREA` . Cependant, ces balises ne sont pas prises en compte pour le suivi des liens si elles disposent d’un `onclick` gestionnaire associé.

### Comment les liens sont-ils étiquetés ?{#labelingLinks}

Les liens sont étiquetés comme lien de téléchargement si la balise d’ancrage comporte un attribut de téléchargement ou si le lien se termine par une extension de fichier populaire. Le qualificateur de lien de téléchargement peut être [configuré](../fundamentals/configuring-the-sdk.md) avec une expression régulière :

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Les liens sont étiquetés comme lien de sortie si le domaine de la cible des liens diffère de celui `window.location.hostname`en cours.

Les liens qui ne sont pas considérés comme des liens de téléchargement ou de sortie sont étiquetés comme &quot;autres&quot;.
