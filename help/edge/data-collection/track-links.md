---
title: Suivi des liens avec Adobe Analytics
seo-title: Liaison du suivi à Adobe Analytics avec le SDK Web Adobe Experience Platform
description: Découvrez comment envoyer des données de lien vers l'Adobe Analytics avec le SDK Web Experience Platform
seo-description: Découvrez comment envoyer des données de lien vers l'Adobe Analytics avec le SDK Web Experience Platform
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;vues de page;suivi des liens;liens;suivi des liens;clicCollection;clic collection;clic collection;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# Suivi des liens

Les liens peuvent être définis manuellement ou suivis [automatiquement](#automaticLinkTracking). Le suivi manuel est effectué en ajoutant les détails sous la partie `web.webInteraction` du schéma. Il existe trois variables obligatoires :

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

Par défaut, le kit SDK Web capture, étiquette et enregistre les clics sur les balises de lien éligibles. Les clics sont capturés avec un écouteur de événement de clics [capture](https://www.w3.org/TR/uievents/#capture-phase) attaché au document.

Le suivi automatique des liens peut être désactivé en [configurant](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) le SDK Web.

```javascript
clickCollectionEnabled: false
```

### Quelles balises sont admissibles pour le suivi des liens ?{#qualifyingLinks}

Le suivi automatique des liens est effectué pour les balises d&#39;ancrage `A` et `AREA`. Cependant, ces balises ne sont pas prises en compte pour le suivi des liens si elles comportent un gestionnaire `onclick` associé.

### Comment les liens sont-ils étiquetés ?{#labelingLinks}

Les liens sont étiquetés comme lien de téléchargement si la balise d’ancrage comporte un attribut de téléchargement ou si le lien se termine par une extension de fichier populaire. Le qualificateur de lien de téléchargement peut être [configuré](../fundamentals/configuring-the-sdk.md) avec une expression régulière :

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Les liens sont étiquetés comme lien de sortie si le domaine de cible de liens diffère de l’élément `window.location.hostname` actuel.

Les liens qui ne sont pas considérés comme des liens de téléchargement ou de sortie sont étiquetés comme &quot;autres&quot;.
