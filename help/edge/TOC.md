---
solution: Data Collection
audience: user
user-guide-title: Aide du SDK web d’Adobe Experience Platform
breadcrumb-title: Guide du SDK web
user-guide-description: Interagissez avec les services Experience Cloud via le réseau Edge.
feature: Web SDK
source-git-commit: 95d7b16efb638c37d8db3f56b0f3fbf6aa9d15df
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 96%

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
* Identité {#identity}
   * [Aperçu](identity/overview.md)
   * [Identifiants d’appareils propriétaires](identity/first-party-device-ids.md)
   * [Partage d’identifiants entre appareils mobiles et domaines](identity/id-sharing.md)
* Collecte de données {#data-collection}
   * [Informations collectées automatiquement](data-collection/automatic-information.md)
   * [Suivi des liens](data-collection/track-links.md)
   * [Collecte de données commerciales, de produits et de commandes](data-collection/collect-commerce-data.md)
   * Adobe Analytics {#adobe-analytics}
      * [Utiliser Adobe Analytics avec le SDK Web Platform](data-collection/adobe-analytics/analytics-overview.md)
      * [Mappage des variables Analytics](data-collection/adobe-analytics/manually-mapping-variables.md)
      * [Variables mappées automatiquement](data-collection/adobe-analytics/automatically-mapped-vars.md)
      * [Envoi de données à Analytics](data-collection/adobe-analytics/sending-data-to-analytics.md)
* Personnalisation {#personalization}
   * [Rendu de contenu personnalisé](personalization/rendering-personalization-content.md)
   * [Personnalisation via une implémentation hybride](personalization/hybrid-personalization.md)
   * [Gestion du scintillement](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [Aperçu](personalization/adobe-target/target-overview.md)
      * [Implémentation d’applications d’une seule page](personalization/adobe-target/spa-implementation.md)
      * [Accès aux jetons de réponse](personalization/adobe-target/accessing-response-tokens.md)
      * [Utiliser un ID mBox tiers](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [Comparer la bibliothèque at.js au SDK Web](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Connexion Analytics for Target (A4T) {#a4t}
         * [Aperçu](personalization/adobe-target/analytics-logging/overview.md)
         * [Côté client côté serveur](personalization/adobe-target/analytics-logging/client-side.md)
         * [Connexion côté serveur](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer Decisioning {#offer-decisioning}
      * [Aperçu](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [Aperçu](personalization/ajo/overview.md)
* Consentement {#consent}
   * [Prise en charge du consentement](consent/supporting-consent.md)
   * IAB Transparency and Consent Framework 2.0 {#iab-tcf}
      * [Aperçu](consent/iab-tcf/overview.md)
      * [Intégration avec des balises](consent/iab-tcf/with-launch.md)
      * [Intégration sans balises](consent/iab-tcf/without-launch.md)
* [Extension de balises du SDK Web](web-sdk-tag-extension-overview.md)
* [Notes de mise à jour](release-notes.md)
* [Questions fréquentes](web-sdk-faq.md)
* [Ressources](resources.md)
