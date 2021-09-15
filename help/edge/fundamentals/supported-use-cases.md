---
title: Cas d’utilisation pris en charge avec le SDK Web de Adobe Experience Platform
description: Découvrez les cas d’utilisation pris en charge avec le SDK Web de Adobe Experience Platform.
keywords: sdk web;cas d’utilisation
exl-id: e0643c2c-ceb3-4ea2-aafa-1e18e0c66453
source-git-commit: ed092b85d74eaa0fdc29f3a8d28f84fe81ccca17
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 20%

---

# Cas d’utilisation pris en charge

Cette page répertorie les cas d’utilisation pris en charge pour le SDK Web, avec des liens vers des informations supplémentaires.

## General (Général)

| Exemple d’utilisation | Plus d’informations |
| --- | --- |
| SDK simplifié unique |  |
| Réseau de collecte de données global |  |
| Consentement acquis du cours |  |
| Collecter le consentement des clients selon diverses normes | <ul><li>[Prise en charge du consentement Adobe 2.0](../../landing/governance-privacy-security/consent/adobe/overview.md)</li><li>[Prise en charge du TCF 2.0 de l’IAB](../../landing/governance-privacy-security/consent/iab/overview.md)</li><li>[Intégration du SDK pour envoyer des signaux de consentement au réseau Edge](../../landing/governance-privacy-security/consent/sdk.md)</li></ul> |
| Prise en charge ECID | Pour plus d’informations sur la récupération de l’ECID, consultez notre documentation [ici](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#first-party-identity) et [ici](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/accessing-the-ecid.html?lang=en#extension) |
| Collecter plusieurs entités |  |
| Prise en charge de Device Graph (public/privé) | [Documentation](https://experienceleague.adobe.com/docs/analytics/components/cda/device-graph.html?lang=en) |
| Envoi de données à plusieurs organisations sur la page | [Documentation](./interacting-with-multiple-properties.md) |
| Rapports et logs d’erreur détaillés |  |
| Demandes de suivi côté client et côté serveur |  |
| extension de balise | [Documentation sur l’extension SDK Web](../../tags/extensions/web/sdk/overview.md) |
| Outils de débogage disponibles | [Extension Debugger ](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) et  [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon) |

{style=&quot;table-layout:auto&quot;}

## Adobe Experience Platform

| Exemple d’utilisation | Plus d’informations |
| --- | --- |
| Envoi d’événements d’expérience |  |
| Offer Decisioning | [Documentation](../personalization/offer-decisioning/offer-decisioning-overview.md) |
| Si le jeu de données est activé pour le profil, possibilité d’envoyer des données à Real-time Customer Data Profile en temps réel |  |
| Envoi de données à Customer Journey Analytics en temps réel |  |
| Consentement en écriture sur le profil | [Documentation](../../landing/governance-privacy-security/consent/sdk.md) |
| Transfert des données côté serveur en temps réel vers des tiers | [Documentation](../../tags/ui/event-forwarding/overview.md) |
| Prise en charge des espaces de noms d’identité |  |

{style=&quot;table-layout:auto&quot;}

## Adobe Analytics

| Exemple d’utilisation | Plus d’informations |
| --- | --- |
| Analytics for Target (A4T) |  |
| Aucune latence Analytics for Target (A4T) |  |
| Balisage multisuite |  |
| Filtrage des robots |  |
| Props, eVars et événements |  |
| Prise en charge de ListVar pour Adobe Analytics |  |
| Version du système d’exploitation et du navigateur |  |
| Variables d’usine | [Variables mappées automatiquement](../data-collection/adobe-analytics/automatically-mapped-vars.md) |
| Règles VISTA/règles de traitement |  |
| Prise en charge des attributs du visiteur |  |
| Prise en charge des liens de sortie |  |
| Liens personnalisés/liens de téléchargement |  |
| Tracking de l’état et de l’action |  |
| Sérialisation d’événements pour les événements standard |  |
| Variable products | [Documentation](../data-collection/collect-commerce-data.md#actions-related-to-products) |

{style=&quot;table-layout:auto&quot;}

## Adobe Target

| Exemple d’utilisation | Plus d’informations |
| --- | --- |
| Tous les types d’activité |  |
| Prise en charge du compositeur d’expérience visuelle natif et SPA | [Documentation](../personalization/adobe-target/spa-implementation.md) |
| Compositeur d’après les formulaires |  |
| Prise en charge de la mbox globale | [Documentation](../personalization/rendering-personalization-content.md#automatically-rendering-content) |
| Mbox personnalisées | [Documentation](../personalization/rendering-personalization-content.md#manually-rendering-content) |
| Analytics for Target (A4T) |  |
| Prise en charge de l’environnement |  |
| Prise en charge de Workspace |  |
| Liens d’assurance qualité dans Adobe Target |  |
| Ciblage basé sur la géo/l’appareil dans Adobe Target |  |
| Prise en charge des attributs du visiteur |  |
| Scripts de profil |  |
| XDM devient des paramètres de mbox |  |
| Offres de redirection prises en charge par les rapports A4T | [Documentation](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en) |
| Mise à jour du profil Target | [Documentation](../personalization/adobe-target/target-overview.md#single-profile-update) |
| Recommandations |  |
| Identifiant tiers mBox |  |
| Jetons de réponse | [Documentation](../personalization/adobe-target/accessing-response-tokens.md) |

{style=&quot;table-layout:auto&quot;}

## Adobe Audience Manager

| Exemple d’utilisation | Plus d’informations |
| --- | --- |
| Audience Analytics |  |
| Partage de segments vers Adobe Analytics |  |
| Prise en charge des attributs du visiteur |  |
| Synchronisations des partenaires |  |
| Destinations d’URL |  |
| Destinations de cookie |  |
| Prise en charge de l’environnement |  |
| Synchronisation des espaces de noms Adobe Experience Platform avec les sources de données d’Audience Manager |  |
| Identifiants authentifiés ou connus |  |

{style=&quot;table-layout:auto&quot;}
