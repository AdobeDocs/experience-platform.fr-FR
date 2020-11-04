---
title: Notes de mise à jour du SDK web Adobe Experience Platform
seo-title: Notes de mise à jour du SDK web Adobe Experience Platform
description: Notes de mise à jour du SDK web Adobe Experience Platform.
seo-description: Notes de mise à jour du SDK web Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 77c1e693668bc50a81713d02cfe4b0fabc661404
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 14%

---


# Notes de mise à jour

## Version 2.3.0

* Prise en charge des nonce Ajoutée pour permettre des stratégies de sécurité du contenu plus strictes.
* Prise en charge de la personnalisation Ajoutée pour les applications d’une seule page.
* Amélioration de la compatibilité avec d’autres codes JavaScript sur la page susceptibles de remplacer `window.console` les API.
* Correctif : `sendBeacon` n’était pas utilisé lorsque `documentUnloading` était défini sur `true` ou lorsque les clics sur les liens étaient automatiquement suivis.
* Correctif : Un lien ne serait pas automatiquement suivi si l’élément d’ancrage contenait du contenu HTML.
* Correctif : Certaines erreurs de navigateur contenant une propriété en lecture seule `message` n’ont pas été gérées correctement, d’où une autre erreur exposée au client.
* Correctif : L’exécution du SDK dans un iframe provoquerait une erreur si la page HTML de l’iframe provenait d’un sous-domaine différent de celui de la page HTML de la fenêtre parent.

## Version 2.2.0

* Correctif : L’objet Opt-in empêchait Alloy d’effectuer des appels en `idMigrationEnabled` `true`l’état.
* Correctif : Sensibilisez Alloy aux demandes qui doivent renvoyer des offres de personnalisation afin d’éviter un problème de scintillement.

## Version 2.1.0

* Supprimez la `syncIdentity` commande et prenez en charge la transmission de ces identifiants dans la `sendEvent` commande.
* Prise en charge de la norme de consentement IAB 2.0.
* Prise en charge de la transmission d’identifiants supplémentaires dans la `setConsent` commande.
* Prendre en charge le remplacement de la `datasetId` dans la `sendEvent` commande.
* Moniteurs d’allocation de support ([en savoir plus](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Transmettre `environment: browser` les données contextuelles des détails de l’implémentation.
