---
solution: Data Collection
audience: user
user-guide-title: Aide du SDK web d’Adobe Experience Platform
breadcrumb-title: Guide du SDK web
user-guide-description: Interagissez avec les services Experience Cloud via le réseau Edge.
feature: Web SDK
source-git-commit: b53be9f2f2d55d5f9e8081fb0ca6732dcc2a8c11
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 77%

---


# SDK web Adobe Experience Platform {#edge}

* [Présentation du SDK web de Platform](home.md)
* Notions fondamentales {#fundamentals}
   * [Cas d’utilisation pris en charge](fundamentals/supported-use-cases.md)
   * [Conditions préalables](fundamentals/prerequisite.md)
   * [Installation du SDK](fundamentals/installing-the-sdk.md)
   * [Configuration du SDK](fundamentals/configuring-the-sdk.md)
   * [Exécution des commandes](fundamentals/executing-commands.md)
   * [Suivi des événements](fundamentals/tracking-events.md)
   * [Débogage](fundamentals/debugging.md)
   * [Configuration d’un fichier CSP](fundamentals/configuring-a-csp.md)
   * [Interaction avec plusieurs propriétés](fundamentals/interacting-with-multiple-properties.md)
   * [Conseils sur le client User-Agent](fundamentals/user-agent-client-hints.md)
* Flux de données {#datastreams}
   * [Présentation](./datastreams/overview.md)
   * [Configurer un flux de données](./datastreams/configure.md)
   * [Préparation des données pour la collecte de données](./datastreams/data-prep.md)
   * Enrichissement des données {#data-enrichment}
      * [Données météo par canal météo](./datastreams/data-enrichment/weather.md)
      * [Mappages des champs de données météo](./datastreams/data-enrichment/weather-reference.md)
* Identité {#identity}
   * [Présentation](identity/overview.md)
   * [Identifiants d’appareils propriétaires](identity/first-party-device-ids.md)
   * [Partage d’identifiants entre appareils mobiles et domaines](identity/id-sharing.md)
* Collecte de données {#data-collection}
   * [Informations collectées automatiquement](data-collection/automatic-information.md)
   * [Suivi des liens](data-collection/track-links.md)
   * [Collecte de données sur les produits et le commerce](data-collection/collect-commerce-data.md)
   * Adobe Analytics {#adobe-analytics}
      * [Utilisation d’Adobe Analytics avec le SDK Web Platform](data-collection/adobe-analytics/analytics-overview.md)
      * [Mappage des variables Analytics](data-collection/adobe-analytics/manually-mapping-variables.md)
      * [Variables mappées automatiquement](data-collection/adobe-analytics/automatically-mapped-vars.md)
      * [Envoi de données à Analytics](data-collection/adobe-analytics/sending-data-to-analytics.md)
* Personnalisation {#personalization}
   * [Rendu de contenu personnalisé](personalization/rendering-personalization-content.md)
   * [Personnalisation via une implémentation hybride](personalization/hybrid-personalization.md)
   * [Gestion du scintillement](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [Présentation](personalization/adobe-target/target-overview.md)
      * [Implémentation d’applications d’une seule page](personalization/adobe-target/spa-implementation.md)
      * [Accès aux jetons de réponse](personalization/adobe-target/accessing-response-tokens.md)
      * [Utilisation de l’ID tiers de mbox](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [Comparaison de la bibliothèque at.js avec le SDK Web](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Journalisation d’Analytics for Target (A4T) {#a4t}
         * [Aperçu](personalization/adobe-target/analytics-logging/overview.md)
         * [Côté client connexion](personalization/adobe-target/analytics-logging/client-side.md)
         * [Journalisation côté serveur](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer Decisioning {#offer-decisioning}
      * [Présentation](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [Présentation](personalization/ajo/overview.md)
* Consentement {#consent}
   * [Prise en charge du consentement](consent/supporting-consent.md)
   * IAB の透明性および同意フレームワーク 2.0 {#iab-tcf}
      * [Présentation](consent/iab-tcf/overview.md)
      * [Intégration avec des balises](consent/iab-tcf/with-launch.md)
      * [Intégration sans balises](consent/iab-tcf/without-launch.md)
* Extension de balises du SDK web {#extension}
   * [Extension SDK web](extension/web-sdk-extension-configuration.md)
   * [Types d’événements](extension/event-types.md)
   * [Types d’actions](extension/action-types.md)
   * [Types d’éléments de données](extension/data-element-types.md)
   * [Accès à l’ECID](extension/accessing-the-ecid.md)
   * [Notes de mise à jour de l’extension SDK web](extension/web-sdk-ext-release-notes.md)
* [Notes de mise à jour](release-notes.md)
* [Questions fréquentes](web-sdk-faq.md)
* [Ressources](resources.md)
