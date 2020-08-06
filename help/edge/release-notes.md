---
title: Notes de mise à jour du SDK Web Adobe Experience Platform
seo-title: Notes de mise à jour du SDK Web Adobe Experience Platform
description: Notes de mise à jour du SDK Web Adobe Experience Platform.
seo-description: Notes de mise à jour du SDK Web Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c1cb64dc297d9133a8e3ef18c97cbd5fac5b0cd6
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 3%

---


# Notes de mise à jour

## Version 2.1.0

* Prise en charge de la norme de consentement IAB 2.0.
* Prise en charge de la transmission d’identifiants supplémentaires dans la `setConsent` commande.
* Prendre en charge le remplacement de la `datasetId` dans la `sendEvent` commande.
* Supprimez la `syncIdentity` commande et prenez en charge la transmission de ces identifiants dans la `sendEvent` commande.
* Moniteurs d&#39;allocation de support ([en savoir plus](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Transmettre `environment: browser` les données contextuelles des détails de l’implémentation.
