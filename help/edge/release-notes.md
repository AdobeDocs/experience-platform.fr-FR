---
title: Notes de mise à jour du SDK web Adobe Experience Platform
description: Notes de mise à jour les plus récentes pour le SDK Web Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK ; Platform Web SDK ; Web SDK ; notes de mise à jour ;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 10%

---


# Notes de mise à jour

## Version 2.3.0

* Prise en charge des nonce Ajoutée pour permettre des stratégies de sécurité du contenu plus strictes.
* Prise en charge de la personnalisation Ajoutée pour les applications d’une seule page.
* Amélioration de la compatibilité avec d’autres codes JavaScript sur la page susceptibles de remplacer les API `window.console`.
* Correctif : `sendBeacon` n&#39;était pas utilisé lorsque `documentUnloading` était défini sur `true` ou lorsque les clics sur les liens étaient automatiquement suivis.
* Correctif : Un lien ne serait pas automatiquement suivi si l’élément d’ancrage contenait du contenu HTML.
* Correctif : Certaines erreurs de navigateur contenant une propriété `message` en lecture seule n&#39;ont pas été gérées correctement, ce qui a provoqué une autre erreur exposée au client.
* Correctif : L’exécution du SDK dans un iframe provoquerait une erreur si la page HTML de l’iframe provenait d’un sous-domaine différent de celui de la page HTML de la fenêtre parent.

## Version 2.2.0

* Correctif : L’objet d’inclusion empêchait Alloy d’effectuer des appels lorsque `idMigrationEnabled` est `true`.
* Correctif : Sensibilisez Alloy aux demandes qui doivent renvoyer des offres de personnalisation afin d’éviter un problème de scintillement.

## Version 2.1.0

* Supprimez la commande `syncIdentity` et prenez en charge la transmission de ces identifiants dans la commande `sendEvent`.
* Prise en charge de la norme de consentement IAB 2.0.
* Prise en charge de la transmission d’identifiants supplémentaires dans la commande `setConsent`.
* Prise en charge du remplacement de `datasetId` dans la commande `sendEvent`.
* Moniteurs d’alliage d’assistance ([En savoir plus](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Transmettez `environment: browser` dans les données contextuelles des détails d’implémentation.
