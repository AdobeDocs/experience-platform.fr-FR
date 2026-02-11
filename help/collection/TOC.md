---
audience: user
solution: Data Collection
user-guide-title: Collecte de données
breadcrumb-title: Collecte de données
user-guide-description: Découvrez comment envoyer des données à Adobe Experience Platform.
feature: Data Collection
role: Developer
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 38%

---


# Collecte de données {#collection}

+ [Vue d’ensemble](home.md)
+ [Autorisations](permissions.md)
+ BrightScript {#brightscript}
   + [Présentation de BrightScript](brightscript/brs-overview.md)
+ JavaScript {#js}
   + [Présentation de Web SDK JavaScript](js/js-overview.md)
   + [Notes de mise à jour](js/release-notes.md)
   + Installation {#install}
      + [Présentation de l’installation](js/install/overview.md)
      + [Code de base](js/install/base-code.md)
      + [Bibliothèque](js/install/library.md)
      + [NPM](js/install/npm.md)
      + [Version personnalisée](js/install/create-custom-build.md)
   + Commands {#commands}
      + [appendIdentityToUrl](js/commands/appendidentitytourl.md)
      + [applyPropositions](js/commands/applypropositions.md)
      + [applyResponse](js/commands/applyresponse.md)
      + configure {#configure}
         + [Vue d’ensemble](js/commands/configure/overview.md)
         + [autoCollectPropositionInteractions](js/commands/configure/autocollectpropositioninteractions.md)
         + [clickCollection](js/commands/configure/clickcollection.md)
         + [clickCollectionEnabled](js/commands/configure/clickcollectionenabled.md)
         + [contexte](js/commands/configure/context.md)
         + [conversation](js/commands/configure/conversation.md)
         + [datastreamId](js/commands/configure/datastreamid.md)
         + [debugEnabled](js/commands/configure/debugenabled.md)
         + [defaultConsent](js/commands/configure/defaultconsent.md)
         + [downloadLinkQualifier](js/commands/configure/downloadlinkqualifier.md)
         + [edgeBasePath](js/commands/configure/edgebasepath.md)
         + [edgeConfigOverrides](js/commands/configure/edgeconfigoverrides.md)
         + [edgeDomain](js/commands/configure/edgedomain.md)
         + [idMigrationEnabled](js/commands/configure/idmigrationenabled.md)
         + [onBeforeEventSend](js/commands/configure/onbeforeeventsend.md)
         + [onBeforeLinkClickSend](js/commands/configure/onbeforelinkclicksend.md)
         + [orgId](js/commands/configure/orgid.md)
         + [prehidingStyle](js/commands/configure/prehidingstyle.md)
         + [notifications push](js/commands/configure/pushnotifications.md)
         + [streamingMedia](js/commands/configure/streamingmedia.md)
         + [targetMigrationEnabled](js/commands/configure/targetmigrationenabled.md)
         + [thirdPartyCookiesEnabled](js/commands/configure/thirdpartycookiesenabled.md)
      + [createMediaSession](js/commands/createmediasession.md)
      + [getIdentity](js/commands/getidentity.md)
      + [getLibraryInfo](js/commands/getlibraryinfo.md)
      + [getMediaAnalyticsTracker](js/commands/getmediaanalyticstracker.md)
      + sendEvent {#sendevent}
         + [Vue d’ensemble](js/commands/sendevent/overview.md)
         + [data](js/commands/sendevent/data.md)
         + [documentUnloading](js/commands/sendevent/documentunloading.md)
         + [edgeConfigOverrides](js/commands/sendevent/edgeconfigoverrides.md)
         + [eventType](js/commands/sendevent/eventtype.md)
         + [personnalisation](js/commands/sendevent/personalization.md)
         + [renderDecisions](js/commands/sendevent/renderdecisions.md)
         + [xdm](js/commands/sendevent/xdm.md)
      + [sendMediaEvent](js/commands/sendmediaevent.md)
      + [sendPushSubscription](js/commands/sendpushsubscription.md)
      + [setConsent](js/commands/setconsent.md)
      + [setDebug](js/commands/setdebug.md)
      + [subscribeRulesetItems](js/commands/subscriberulesetitems.md)
      + [Réponses aux commandes](js/commands/command-responses.md)
   + [Crochets de surveillance](js/monitoring-hooks.md)
   + [Questions fréquentes](js/faq.md)
+ JavaScript côté client des balises {#tags}
   + [Vue d’ensemble](tags/overview.md)
   + [buildInfo](tags/buildinfo.md)
   + [entreprise](tags/company.md)
   + [_conteneur](tags/container.md)
   + [cookie](tags/cookie.md)
   + [environment](tags/environment.md)
   + [getVar](tags/getvar.md)
   + [getVisitorId](tags/getvisitorid.md)
   + [logger](tags/logger.md)
   + [_moniteurs](tags/monitors.md)
   + [setDebug](tags/setdebug.md)
   + [setVar](tags/setvar.md)
   + [suivre](tags/track.md)
+ Cas d’utilisation {#use-cases}
   + [Vue d’ensemble](use-cases/overview.md)
   + [Client hints](use-cases/client-hints.md)
   + [État du client](use-cases/client-state.md)
   + [Collecter des données commerciales](use-cases/collect-commerce-data.md)
   + [Configuration d’un fichier CSP](use-cases/configuring-a-csp.md)
   + [Débogage](use-cases/debugging.md)
   + [Déduplication des événements](use-cases/event-duplication.md)
   + Identité {#identity}
      + [Vue d’ensemble](use-cases/identity/id-overview.md)
      + [Identifiants d’appareils propriétaires](use-cases/identity/first-party-device-ids.md)
      + [Partage d’identifiants](use-cases/identity/id-sharing.md)
   + [Plusieurs instances SDK](use-cases/multiple-instances.md)
   + Personnalisation {#personalization}
      + [Vue d’ensemble](use-cases/personalization/pers-overview.md)
      + [Afficher les événements](use-cases/personalization/display-events.md)
      + [Gestion du scintillement](use-cases/personalization/manage-flicker.md)
      + [Rendu du contenu personnalisé](use-cases/personalization/rendering-personalization-content.md)
      + [Événements des pages supérieure et inférieure](use-cases/personalization/top-bottom-page-events.md)
