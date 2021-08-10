---
title: Suivi des liens à l’aide du SDK Web de Adobe Experience Platform
description: Découvrez comment envoyer des données de lien à Adobe Analytics avec le SDK Web Experience Platform
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;interaction web;pages vues;suivi des liens;liens;suivre les liens;cliquer sur la collection;cliquer sur la collection;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: d6460e442a136bf9bd26582f228017a6fb52138c
workflow-type: tm+mt
source-wordcount: '340'
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
            "value": 1
        }
      },
      "name": "My Custom Link", // Name that shows up in the custom links report
      "URL": "https://myurl.com", // The URL of the link
      "type": "other" // values: other, download, exit
    }
  }
});
```

Le type de lien peut correspondre à l’une des trois valeurs suivantes :

* **`other`:** lien personnalisé
* **`download`:** lien de téléchargement
* **`exit`:** lien de sortie

Ces valeurs sont [mappées automatiquement](adobe-analytics/automatically-mapped-vars.md) dans Adobe Analytics si [configuré](adobe-analytics/analytics-overview.md) pour cela.

## Suivi automatique des liens {#automaticLinkTracking}

Par défaut, le SDK Web capture, étiquette et enregistre les clics sur les balises de lien admissibles. Les clics sont capturés avec un écouteur d’événement de clic [capture](https://www.w3.org/TR/uievents/#capture-phase) joint au document.

Le suivi automatique des liens peut être désactivé en [configurant](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) le SDK Web.

```javascript
clickCollectionEnabled: false
```

### Quelles balises remplissent les critères du suivi des liens ?{#qualifyingLinks}

Le suivi automatique des liens est effectué pour les balises `A` et `AREA` d’ancrage. Toutefois, ces balises ne sont pas prises en compte pour le suivi des liens si elles sont accompagnées d’un gestionnaire `onclick`.

### Comment les liens sont-ils étiquetés ?{#labelingLinks}

Les liens sont étiquetés comme lien de téléchargement si la balise d’ancrage inclut un attribut de téléchargement ou si le lien se termine par une extension de fichier populaire. Le qualificateur de lien de téléchargement peut être [configuré](../fundamentals/configuring-the-sdk.md) avec une expression régulière :

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Les liens sont étiquetés comme lien de sortie si le domaine cible du lien diffère de la `window.location.hostname` actuelle.

Les liens qui ne sont pas qualifiés de liens de téléchargement ou de sortie sont étiquetés comme &quot;autres&quot;.

### Comment les valeurs de suivi des liens peuvent-elles être filtrées ?

Les données collectées avec le suivi automatique des liens peuvent être inspectées et filtrées en fournissant une fonction de rappel [onBeforeEventSend](../fundamentals/tracking-events.md#modifying-events-globally).

Le filtrage des données de suivi des liens peut s’avérer utile lors de la préparation des données pour la création de rapports Analytics. Le suivi automatique des liens capture le nom du lien et l’URL du lien. Dans les rapports Analytics, le nom du lien a la priorité sur l’URL du lien. Si vous souhaitez signaler l’URL du lien, le nom du lien doit être supprimé. L’exemple suivant illustre une fonction `onBeforeEventSend` qui supprime le nom du lien pour les liens de téléchargement :

```javascript
alloy("configure", {
  onBeforeEventSend: function(options) {
    if (options
      && options.xdm
      && options.xdm.web
      && options.xdm.web.webInteraction) {
        if (options.xdm.web.webInteraction.type === "download") {
          options.xdm.web.webInteraction.name = undefined;
        }
    }
  }
});
```

