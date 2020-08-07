---
title: Notes de mise à jour du SDK Web Adobe Experience Platform
seo-title: Notes de mise à jour du SDK Web Adobe Experience Platform
description: Notes de mise à jour du SDK Web Adobe Experience Platform.
seo-description: Notes de mise à jour du SDK Web Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: e9a49c20f30d06fa125185865b4963c8472fa5e5
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 3%

---


# Notes de mise à jour

## Version 2.1.0

* Supprimez la `syncIdentity` commande et prenez en charge la transmission de ces identifiants dans la `sendEvent` commande.
* Prise en charge de la norme de consentement IAB 2.0.
* Prise en charge de la transmission d’identifiants supplémentaires dans la `setConsent` commande.
* Prendre en charge le remplacement de la `datasetId` dans la `sendEvent` commande.
* Moniteurs d’allocation de support ([en savoir plus](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Transmettre `environment: browser` les données contextuelles des détails de l’implémentation.
