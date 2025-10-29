---
solution: Data Collection
audience: user
user-guide-title: Aide du SDK web d’Adobe Experience Platform
breadcrumb-title: Guide du SDK web
user-guide-description: Interagissez avec les services Experience Cloud via le réseau Edge.
feature: Web SDK
role: Developer
source-git-commit: 84faff58bac199c1113d7451f8cc865b6a870680
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 46%

---


# SDK Web Adobe Experience Platform {#web-sdk}

* [Présentation du SDK web](home.md)
* [Notes de mise à jour](release-notes.md)
* Installation de Web SDK {#install}
   * [Vue d’ensemble](install/overview.md)
   * [Installation de Web SDK à l’aide de l’extension de balise](install/extension.md)
   * [Installation de Web SDK à l’aide de la bibliothèque JavaScript](install/library.md)
   * [Installer le SDK Web à l’aide du package NPM](install/npm.md)
   * [Créer une version SDK Web personnalisée à l’aide du package NPM](install/create-custom-build.md)
* Commands {#commands}
   * configure {#configure}
      * [Vue d’ensemble](commands/configure/overview.md)
      * [autoCollectPropositionInteractions](commands/configure/autocollectpropositioninteractions.md)
      * [clickCollectionEnabled](commands/configure/clickcollectionenabled.md)
      * [clickCollection](commands/configure/clickcollection.md)
      * [contexte](commands/configure/context.md)
      * [datastreamId](commands/configure/datastreamid.md)
      * [debugEnabled](commands/configure/debugenabled.md)
      * [defaultConsent](commands/configure/defaultconsent.md)
      * [downloadLinkQualifier](commands/configure/downloadlinkqualifier.md)
      * [edgeBasePath](commands/configure/edgebasepath.md)
      * [edgeDomain](commands/configure/edgedomain.md)
      * [idMigrationEnabled](commands/configure/idmigrationenabled.md)
      * [streamingMedia](commands/configure/streamingmedia.md)
      * [onBeforeEventSend](commands/configure/onbeforeeventsend.md)
      * [onBeforeLinkClickSend](commands/configure/onbeforelinkclicksend.md)
      * [orgId](commands/configure/orgid.md)
      * [prehidingStyle](commands/configure/prehidingstyle.md)
      * [notifications push](commands/configure/pushnotifications.md)
      * [targetMigrationEnabled](commands/configure/targetmigrationenabled.md)
      * [thirdPartyCookiesEnabled](commands/configure/thirdpartycookiesenabled.md)
   * sendEvent {#sendevent}
      * [Vue d’ensemble](commands/sendevent/overview.md)
      * [data](commands/sendevent/data.md)
      * [documentUnloading](commands/sendevent/documentunloading.md)
      * [personnalisation](commands/sendevent/personalization.md)
      * [renderDecisions](commands/sendevent/renderdecisions.md)
      * [type](commands/sendevent/type.md)
      * [xdm](commands/sendevent/xdm.md)
   * [appendIdentityToUrl](commands/appendidentitytourl.md)
   * [applyPropositions](commands/applypropositions.md)
   * [applyResponse](commands/applyresponse.md)
   * [createMediaSession](commands/createmediasession.md)
   * [getIdentity](commands/getidentity.md)
   * [getLibraryInfo](commands/getlibraryinfo.md)
   * [getMediaAnalyticsTracker](commands/getmediaanalyticstracker.md)
   * [setConsent](commands/setconsent.md)
   * [setDebug](commands/setdebug.md)
   * [sendMediaEvent](commands/sendmediaevent.md)
   * [sendPushSubscription](commands/sendpushsubscription.md)
   * [subscribeRulesetItems](commands/subscriberulesetitems.md)
   * [Configurer les remplacements de trains de données](commands/datastream-overrides.md)
   * [Réponses aux commandes](commands/command-responses.md)

* Identité {#identity}
   * [Aperçu](identity/overview.md)
   * [Identifiants d’appareils propriétaires](identity/first-party-device-ids.md)
   * [Partage d’identifiants entre appareils mobiles et domaines](identity/id-sharing.md)

* Personnalisation {#personalization}
   * [Gestion des événements d’affichage](personalization/display-events.md)
   * [Rendu de contenu personnalisé](personalization/rendering-personalization-content.md)
   * [Personnalisation via une implémentation hybride](personalization/hybrid-personalization.md)
   * [Gestion du scintillement](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [Aperçu](personalization/adobe-target/target-overview.md)
      * [Implémentation d’applications d’une seule page](personalization/adobe-target/spa-implementation.md)
      * [Accès aux jetons de réponse](personalization/adobe-target/accessing-response-tokens.md)
      * [Utiliser un ID mBox tiers](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [Comparer la bibliothèque at.js au SDK Web](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Journalisation Analytics for Target (A4T) {#a4t}
         * [Vue d’ensemble](personalization/adobe-target/analytics-logging/overview.md)
         * [Journalisation côté client](personalization/adobe-target/analytics-logging/client-side.md)
         * [Connexion côté serveur](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer Decisioning {#offer-decisioning}
      * [Vue d’ensemble](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [Aperçu](personalization/ajo/overview.md)
      * [Implémentation d’applications d’une seule page](personalization/ajo/web-spa-implementation.md)
      * [Configuration de la prise en charge de la messagerie web in-app dans Web SDK](personalization/web-in-app-messaging.md)

* Consentement {#consent}
   * Transparence et cadre de consentement 2.0 de l&#39;IAB {#iab-tcf}
      * [Aperçu](consent/iab-tcf/overview.md)
      * [Intégration avec des balises](consent/iab-tcf/with-tags.md)
      * [Intégration sans balises](consent/iab-tcf/without-tags.md)

* Cas d’utilisation {#use-cases}
   * [Vue d’ensemble](use-cases/overview.md)
   * [Envoyer des données à Adobe Analytics à l’aide de Web SDK](use-cases/adobe-analytics.md)
   * [Indications du client de l’agent utilisateur](use-cases/client-hints.md)
   * [Collecter des données commerciales](use-cases/collect-commerce-data.md)
   * [Configuration d’un fichier CSP](use-cases/configuring-a-csp.md)
   * [Méthodes de débogage](use-cases/debugging.md)
   * [Utilisation de plusieurs instances Web SDK](use-cases/multiple-instances.md)
   * [Configurer les événements des pages supérieure et inférieure](use-cases/top-bottom-page-events.md)
* [Crochets de surveillance](monitoring-hooks.md)
* [Questions fréquentes](faq.md)
* [Ressources](resources.md)
