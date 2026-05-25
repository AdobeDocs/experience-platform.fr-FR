---
title: Notes de mise à jour de l’extension Adobe Target v2
description: Notes de mise à jour les plus récentes pour l’extension de balise Adobe Target v2 dans Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
TQID: https://experienceleague.adobe.com/kl8KpQrBUAsTy4XJD4BDCZa0oaf0sx72YZCO6uWJaQ0
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: eb9732ab-8232-4b21-bc4c-89de86dbe4d7
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
  - id: fc7979f3-56c3-43ca-9784-f1ea3dc69c4b
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: df62f171-ac37-440f-8f0f-f41a72ebdd34
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 853
ht-degree: 99%

---

# Notes de mise à jour de l’extension Adobe Target v2

## v0.20.3 (23 janvier 2024)

- Mise à jour pour prendre en charge `at.js` 2.11.4.
- Correction d’un bug afin d’empêcher l’envoi de données géographiques non valides à l’API de diffusion.

## v0.20.2 (29 novembre 2023)

- Mise à jour pour la prise en charge d’`at.js` 2.11.3
- Correction d’un bug qui empêchait l’envoi des jetons de réponse sur les événements at-content-rendering-failed.

## v0.20.1 (3 novembre 2023)

- Mise à jour pour la prise en charge d’`at.js` 2.11.2.
- Correction d’un bug qui provoquait des incohérences dans les jetons de réponse envoyés sur des événements personnalisés.

## v0.20.0 (9 octobre 2023)

- Mise à jour pour la prise en charge d’`at.js` 2.11.0.
- Ajout de la prise en charge de la définition des sandboxId et sandboxName Adobe Experience Platform personnalisés dans targetGlobalSettings, qui seront transmis à l’API Delivery lors des appels getOffer/getOffers.
- Correctif DOM fantôme pour le chaînage de :eq() dans le sélecteur.

## v0.19.3 (18 septembre 2023)

- Mise à jour pour la prise en charge d’`at.js` v2.10.3.
- Correction d’un problème qui déclenchait à tort l’événement personnalisé at-content-rendering-succeeded, alors qu’aucune offre n’était générée. L’événement correct, at-content-rendering-no-offer, est maintenant déclenché.
- Ajout d’eventToken et de responseTokens à l’objet d’erreur pour l’événement personnalisé at-content-rendering-failed.

## v0.19.2 (14 février 2023)

- Correction d’un problème en raison duquel le délai d’expiration était défini sur un élément de données.

## v0.19.1 (3 février 2023)

- Mise à jour pour la prise en charge de `at.js` v2.10.1.
- Les paramètres mBox personnalisés des clientes et clients prennent désormais correctement en charge la notation par points
- Les appels de diffusion ne sont plus effectués dans le VEC

## v0.19.0 (19 septembre 2022)

- Mise à jour pour la prise en charge de `at.js` v2.10.0.
- Ajout de la prise en charge du suivi interdomaine.

## v0.18.0 (1er juin 2022)

- Mise à jour pour la prise en charge de `at.js` v2.9.0.
- Ajout de la prise en charge des indices clients d’agent utilisateur.

## v0.17.1 (28 janvier 2022)

- Mise à jour pour la prise en charge de `at.js` v2.8.1.
- Correction d’un problème en raison duquel `pageLoad` n’était pas mappée à `target-global-mbox` en mode d’exécution hybride ODD.
- Correction d’un problème lié aux détails des analyses pour la requête de `mbox`.
- Mise à niveau des dépendances de développement pour corriger les vulnérabilités de sécurité.

## v0.17.0 (7 janvier 2022)

- Mise à jour afin de prendre en charge `at.js` v2.8.0, qui collecte désormais des données télémétriques sur l’utilisation des fonctionnalités et les performances.  Les données personnelles ne sont pas collectées. Pour indiquer votre opt-out pour cette fonctionnalité, définissez `telemetryEnabled` sur `false` dans `targetGlobalSettings`.

## v0.16.0 (28 octobre 2021)

- Mise à jour pour la prise en charge de `at.js` v2.7.0, désormais disponible en téléchargement depuis Adobe Target.

## v0.15.2 (16 août 2021)

- Mise à jour pour la prise en charge d’`at.js` 2.6.1.
- Initialisez la prise de décision sur le périphérique au démarrage, indépendamment de l’événement de chargement de page.
- La prise de décision sur le périphérique peut désormais être utilisée lors de la première visite, une fois l’artefact téléchargé.

## v0.15.1 (20 juillet 2021)

- Correction d’un problème lié à un conflit de nom de fonction `stringify`, en raison duquel des valeurs UUID incorrectes étaient générées pour `sessionId`, `requestId`, etc.

## v0.15.0 (16 juillet 2021)

- Ajout dʼun attribut sécurisé aux cookies chaque fois que les paramètres secureOnly d’`at.js` sont définis sur « true ».
- Des jetons de réponse sont désormais disponibles lors de l’utilisation de `triggerView()`
- Correction d’un bug lié à l’événement `CONTENT_RENDERING_NO_OFFERS`. Désormais, il se déclenche correctement chaque fois que Target ne renvoie aucun contenu
- Les informations détaillées des mesures de clics A4T sont correctement renvoyées lors de l’utilisation de requêtes de prérécupération
- La génération de l’UUID n’utilise plus `Math.random()`, mais repose sur `window.crypto`
- L’expiration du cookie `sessionId` est correctement étendue à chaque appel réseau
- L’initialisation du cache de l’affichage SPA est désormais correctement gérée et respecte les paramètres `viewsEnable`

## v0.14.2 (2 juin 2021)

- Correction d’un bug en raison duquel l’offre groupée finale contenait deux versions d’`at.js`, l’une avec la prise de décision sur l’appareil et l’autre sans.

## v0.14.1 (19 mai 2021)

- Correction d’une régression introduite avec la version v0.14 où l’action Charger Target déclenchait des appels de mbox globaux.

## v0.14 (14 mai 2021)

- Ajout d’une nouvelle action Charger Target avec la fonction de [prise de décision sur l’appareil](./overview.md#load-target-with-on-device-decisioning), qui charge `at.js` 2.5 avec les fonctionnalités de prise de décision sur l’appareil.
- Mise à jour d’`at.js` vers la version 2.5.


## v0.13.7 (25 mars 2021)

- Correction dʼun problème en raison duquel le paramètre `targetPageParams` était inclus dans les requêtes mbox. Le paramètre `targetPageParams` ne doit être inclus que dans les requêtes `pageLoad`.
- Correction d’un problème lié aux objets globaux de document et de fenêtre dans l’extension de balise en remplaçant les dépendances d’objets globaux par des références directes vers ces objets.
- Mise à jour d’`at.js` vers la version 2.4.1.

## v0.13.6 (25 janvier 2021)

- Ajoute la prise en charge de l’identifiant unifié de profil/plateforme pour les identifiants de client de l’API de diffusion
- Correction d’une injection de balise de style non valide
- Mise à jour dʼAdobe Target at.s vers la version 2.4.0
- Correction dʼun problème en raison duquel des paramètres non définis pouvaient générer des demandes de diffusion incorrectes.

## v0.13.4 (25 novembre 2020)

- Correction d’un bug en raison duquel les paramètres de mbox ne s’affichaient pas dans l’interface utilisateur.
- Mises à jour du branding
- Mise à jour d’`at.js` vers la version 2.3.3.

## v0.13.3 (24 juillet 2020)

- Correction d’un bug en raison duquel les liens du mode AQ ne fonctionnaient pas pour les activités inactives.
- Correction d’un bug en cas d’échec de l’extension si un script ou un code ajoute la propriété `default` à la `window` ou au `document`.

## v0.13.2 (15 juin 2020)

- Correction d’un problème lors de l’utilisation du remplacement CNAME et Edge, en raison duquel `at.js` 1.x pouvait créer un domaine de serveur incorrect, entraînant ainsi l’échec de la requête de Target.
- Correction dʼun problème lors de lʼutilisation de lʼextension de balise v2 pour Target et de lʼextension de balise Adobe Analytics au cours duquel Target retardait lʼappel Analytics sendBeacon.
- Amélioration du paramètre `deviceIdLifetime` en le rendant remplaçable via `targetGlobalSettings`

## v0.13.0 (25 mars 2020)

- Mise à jour d’`at.js` vers la version 2.3.
- Ajout de la prise en charge de Target Global Mbox dans l’API adobe.target.getOffer.
- Correction d’un problème qui entraînait un mauvais traitement des paramètres et des paramètres de chargement des pages.

## v0.12.0 (10 octobre 2019)

- Mise à jour d’`at.js` vers la version 2.2.
- Amélioration des performances pour les intégrations entre la bibliothèque d’Experience Cloud ID (ECID) version 4.4 et `at.js` version 2.2.
- Auparavant, la bibliothèque ECID effectuait deux appels de blocage avant qu’`at.js` puisse récupérer des expériences. Cela a été réduit à un seul appel, ce qui améliore considérablement les performances.

>[!NOTE]
>Mettez à niveau votre extension de balise ECID vers la version 4.4.1 pour profiter de cette amélioration des performances.

## v0.11.1 (31 juillet 2019)

- Version d’extension mise à jour pour utiliser `at.js` 2.1.1.
- Ajout d’un correctif pour la gestion des paramètres

## v0.11.0 (3 juin 2019)

- Nouvelle extension de balise pour la prise en charge dʼ`at.js` 2.1.
