---
title: Notes de mise à jour de l’extension Adobe Target v2
description: Notes de mise à jour les plus récentes pour l’extension de balise Adobe Target v2 dans Adobe Experience Platform.
source-git-commit: ae6b69ecea54942c1bbf8a2765768bac50a8b930
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 62%

---

# Notes de mise à jour de l’extension Adobe Target v2

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

## 20 juillet 2021

### Extension 0.15.1 d’Adobe Target v2

- Correction d’un problème lié à un conflit de nom de fonction `stringify`, en raison duquel des valeurs UID incorrectes étaient générées pour `sessionId`, `requestId`, etc.

## 16 juillet 2021

### Extension 0.15.0 d’Adobe Target v2

- Ajoutez un attribut sécurisé aux cookies chaque fois que les paramètres at.js secureOnly sont définis sur true
- Les jetons de réponse sont désormais disponibles lors de l’utilisation de `triggerView()`
- Correction d’un bogue lié à l’événement `CONTENT_RENDERING_NO_OFFERS` . Désormais, il se déclenche correctement lorsqu’aucun contenu n’est renvoyé par Target.
- Les détails des mesures de clics A4T sont correctement renvoyés lors de l’utilisation de requêtes de prérécupération
- La génération de l’UUID n’utilise plus `Math.random()`, mais repose sur `window.crypto`
- `sessionId` l’expiration du cookie est correctement étendue à chaque appel réseau.
- L’initialisation du cache de l’affichage SPA est désormais correctement gérée et respecte les paramètres `viewsEnable`

## 2 juin 2021

### Extension 0.14.2 d’Adobe Target v2

- Correction d’un bogue en raison duquel le lot final de Launch contient deux versions d’at.js, l’une avec la prise de décision sur l’appareil et l’autre sans.

## 19 mai 2021

### Extension 0.14.1 d’Adobe Target v2

- Correction d’une régression introduite avec la version v0.14 où l’action Charger Target déclenchait des appels de mbox globaux.

## 14 mai 2021

### Extension 0.14 d’Adobe Target v2

- Ajout d’une nouvelle action Charger Target avec la fonction de [prise de décision sur l’appareil](./overview.md#load-target-with-on-device-decisioning), qui charge at.js 2.5 avec les fonctionnalités de prise de décision sur l’appareil.
- Mise à jour du fichier at.js vers la version 2.5


## 25 mars 2021

### Extension 0.13.7 d’Adobe Target v2

- Correction dʼun problème en raison duquel le paramètre `targetPageParams` était inclus dans les requêtes mbox. Le paramètre `targetPageParams` ne doit être inclus que dans les requêtes `pageLoad`.
- Correction d’un problème lié aux objets globaux document et window dans l’extension de balise en remplaçant les dépendances d’objets globaux par des références directes.
- Mise à jour du fichier at.js vers la version 2.4.1.

## 25 janvier 2021

### Extension 0.13.6 d’Adobe Target v2

- Ajoute la prise en charge de l’identifiant unifié de profil/plateforme pour les identifiants de client de l’API de diffusion
- Correction d’une injection de balise de style non valide
- Mise à jour dʼAdobe Target at.s vers la version 2.4.0
- Correction dʼun problème en raison duquel des paramètres non définis pouvaient générer des demandes de diffusion incorrectes.

## 25 novembre 2020

### Extension 0.13.4 d’Adobe Target v2

- Correction d’un bug en raison duquel les paramètres de mbox ne s’affichaient pas dans l’interface utilisateur.
- Mises à jour du branding
- Mise à jour du fichier at.js vers la version 2.3.3

## 24 juillet 2020

### Extension 0.13.3 d’Adobe Target v2

- Correction d’un bug en raison duquel les liens du mode AQ ne fonctionnaient pas pour les activités inactives.
- Correction d’un bug en cas d’échec de l’extension si un script ou un code ajoute la propriété `default` à la `window` ou au `document`.

## 15 juin 2020

### Extension 0.13.2 d’Adobe Target v2

- Correction d’un problème lors de l’utilisation du remplacement CNAME et Edge, en raison duquel at.js 1.x pouvait créer un domaine de serveur incorrect, entraînant ainsi l’échec de la demande de Target.
- Correction d’un problème en raison duquel, lors de l’utilisation de l’extension de balise v2 pour Target et l’extension de balise Adobe Analytics, Target retardait l’appel sendBeacon d’Analytics.
- Amélioration du paramètre `deviceIdLifetime` en le rendant remplaçable via `targetGlobalSettings`

## 25 mars 2020

### Extension 0.13.0 d’Adobe Target v2

- Mise à jour d’at.js vers la version 2.3.
- Ajout de la prise en charge de Target Global Mbox dans l’API adobe.target.getOffer.
- Correction d’un problème qui entraînait un mauvais traitement des paramètres et des paramètres de chargement des pages.

## 10 octobre 2019

### Extension 0.12.0 d’Adobe Target v2

- Mise à jour d’at.js vers la version 2.2.
- Amélioration des performances pour les intégrations entre la bibliothèque d’Experience Cloud ID (ECID) version 4.4 et at.js version 2.2.
- Auparavant, la bibliothèque ECID effectuait deux appels de blocage avant qu’at.js puisse récupérer des expériences. Cela a été réduit à un seul appel, ce qui améliore considérablement les performances.

>[!NOTE]
>Mettez à niveau votre extension de balise ECID vers la version 4.4.1 pour tirer parti de cette amélioration des performances.

## 31 juillet 2019

### Extension 0.11.1 d’Adobe Target v2

- Version d’extension mise à jour pour utiliser at.js 2.1.1.
- Ajout d’un correctif pour la gestion des paramètres.

## 3 juin 2019

### Extension 0.11.0 d’Adobe Target v2

- Nouvelle extension de balise pour la prise en charge d’at.js 2.1
