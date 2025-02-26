---
keywords: Champs de mappage Analytics;mappage Analytics
solution: Experience Platform
title: Champs de mappage pour le connecteur Source Adobe Analytics
description: Mappez les champs Adobe Analytics aux champs XDM à l’aide du connecteur Source Analytics.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: ae8a54f8e9fafe782cb24e54e5b638d83d468e3a
workflow-type: tm+mt
source-wordcount: '2415'
ht-degree: 70%

---

# Mappages de champs Analytics

Adobe Experience Platform vous permet d’ingérer des données Adobe Analytics par le biais de la source Analytics. Certaines des données ingérées par l’intermédiaire d’ADC peuvent être mappées directement des champs Analytics aux champs du modèle de données d’expérience (XDM), tandis que d’autres données nécessitent des transformations et des fonctions spécifiques pour être mappées avec succès.

![](../images/analytics-data-experience-platform.png)

## Champs de mappage direct

Certains champs sont directement mappés d’Adobe Analytics au modèle de données d’expérience (XDM, Experience Data Model).

| Champ Analytics | Champ XDM | Type XDM | Description |
| --------------- | --------- | -------- | ---------- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | chaîne | eVars d’analyse personnalisées. Chaque organisation peut utiliser des eVars différemment. |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | Chaîne | Props Analytics personnalisées. Chaque organisation peut utiliser des props différemment. |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | entier | Numéro d’identifiant du navigateur. |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | entier | Hauteur du navigateur, en pixels. |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | entier | Largueur du navigateur, en pixels. |
| `m_campaign` | `marketing.trackingCode` | chaîne | Variable utilisée dans la dimension Code de suivi. |
| `m_channel` | `web.webPageDetails.siteSection` | chaîne | Variable utilisée dans la dimension Sections du site. |
| `m_domain` | `environment.domain` | chaîne | Variable utilisée dans la dimension Domaine. Il est basé sur le fournisseur de services Internet (FAI) de l’utilisateur. |
| `m_geo_city` | `placeContext.geo.city` | chaîne | Nom de la ville de l’accès. Il est basé sur l’adresse IP de l’accès. |
| `m_geo_dma` | `placeContext.geo.dmaID` | entier | Identifiant numérique de la zone démographique pour l’accès. Il est basé sur l’adresse IP de l’accès. |
| `m_geo_region` | `placeContext.geo.stateProvince` | chaîne | Nom de l’état ou de la région de l’accès. Il est basé sur l’adresse IP de l’accès. |
| `m_geo_zip` | `placeContext.geo.postalCode` | chaîne | Code postal de l’accès. Il est basé sur l’adresse IP de l’accès. |
| `m_keywords` | `search.keywords` | chaîne | Variable utilisée dans la dimension Mot-clé. |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | entier | Identifiant numérique représentant le système d’exploitation du visiteur. Dépend de la colonne user_agent. |
| `m_page_url` | `web.webPageDetails.URL` | chaîne | URL de l’accès à la page. |
| `m_pagename` | `web.webPageDetails.pageViews.value` | Chaîne | Est égal à 1 sur les accès ayant un nom de page. Ceci est similaire à la mesure Pages vues d’Adobe Analytics. |
| `m_referrer` | `web.webReferrer.URL` | chaîne | URL de la page précédente. |
| `m_search_page_num` | `search.pageDepth` | entier | Variable utilisée par la dimension Classification globale des pages de recherche. Indique la page des résultats de recherche sur laquelle votre site est apparu avant que l’utilisateur n’ait cliqué sur votre site. |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | chaîne | Variable d’état. |
| `m_user_server` | `web.webPageDetails.server` | chaîne | Variable utilisée dans la dimension Serveur. |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | chaîne | Variable utilisée pour remplir la dimension Code postal. |
| `accept_language` | `environment.browserDetails.acceptLanguage` | chaîne | Liste de tous les langages acceptés, comme indiqué dans l’en-tête HTTP Accept-Language. |
| `homepage` | `web.webPageDetails.isHomePage` | booléen | N’est plus utilisé. Indique si l’URL active est la page d’accueil du navigateur. |
| `ipv6` | `environment.ipV6` | chaîne |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | chaîne | Version de JavaScript prise en charge par le navigateur. |
| `user_agent` | `environment.browserDetails.userAgent` | chaîne | Chaîne de l’agent utilisateur envoyée dans l’en-tête HTTP. |
| `mobileappid` | `application.name` | chaîne | Identifiant de l’application mobile, stocké au format suivant : `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | chaîne | Nom de l’appareil mobile. Sous iOS, il est stocké sous la forme d’une chaîne de 2 chiffres séparés par des virgules. Le premier chiffre représente la génération de l’appareil, le second représente la famille d’appareils. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | chaîne | Utilisé par les services mobiles. Représente le point ciblé. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | nombre | Utilisé par les services mobiles. Représente la distance du point ciblé. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | nombre | Collecté à partir de la variable de données contextuelles a.loc.acc. Indique la précision du GPS en mètres au moment de la collecte. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | chaîne | Collecté à partir de la variable de données contextuelles a.loc.category. Décrit la catégorie d’un emplacement spécifique. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | chaîne | Collecté à partir de la variable a.loc.id des données de contexte. Identifiant d’un point ciblé donné. |
| `video` | `media.mediaTimed.primaryAssetReference.`<br/>`_id` | chaîne | Nom de la vidéo. |
| `videoad` | `advertising.adAssetReference._id` | chaîne | Identifiant de la ressource publicitaire. |
| `videocontenttype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastContentType` | chaîne | Type de contenu vidéo. Défini automatiquement sur « Vidéo » pour toutes les consultations vidéo. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | chaîne | Capsule dans laquelle se trouve la publicité vidéo. |
| `videoadinpod` | `advertising.adAssetViewDetails.index` | entier | Position de la publicité vidéo dans la capsule. |
| `videoplayername` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`playerName` | chaîne | Nom du lecteur vidéo. |
| `videochannel` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastChannel` | chaîne | Canal vidéo. |
| `videoadplayername` | `advertising.adAssetViewDetails.playerName` | chaîne | Nom du lecteur de publicité vidéo. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._id` | chaîne | Nom du chapitre vidéo. |
| `videoname` | `media.mediaTimed.primaryAssetReference.`<br/>`_dc.title` | chaîne | Nom de la vidéo. |
| `videoadname` | `advertising.adAssetReference._dc.title` | chaîne | Nom de la publicité vidéo. |
| `videoshow` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Series._iptc4xmpExt.Name` | chaîne | Affichage de la vidéo. |
| `videoseason` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Season._iptc4xmpExt.Name` | chaîne | Saison de la vidéo. |
| `videoepisode` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Episode._iptc4xmpExt.Name` | chaîne | Épisode de la vidéo. |
| `videonetwork` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastNetwork` | chaîne | Réseau de la vidéo. |
| `videoshowtype` | `media.mediaTimed.primaryAssetReference.`<br/>`showType` | chaîne | Type d’affichage de la vidéo. |
| `videoadload` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`adLoadType` | chaîne | Chargements des publicités vidéo. |
| `videofeedtype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sourceFeed` | chaîne | Type de flux vidéo. |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | nombre | Relais Mobile Services majeur. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | nombre | Relais Mobile Services mineur. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | chaîne | UUID du relais Mobile Services. |
| `videosessionid` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`_id` | chaîne | Identifiant de session vidéo. |
| `videogenre` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Genre` | tableau | Genre de la vidéo. | {title (Object), description (Object), type (Object), meta:xdmType (Object), items (string), meta:xdmField (Object)} |
| `mobileinstalls` | `application.firstLaunches` | Objet | Il est déclenché lors de la première exécution suivant l’installation ou la réinstallation | {id (string), value (number)} |
| `mobileupgrades` | `application.upgrades` | objet | Indique le nombre de mises à niveau d’application. Se déclenche lors de la première exécution après mise à niveau ou dès que le numéro de version change. | {id (string), value (number)} |
| `mobilelaunches` | `application.launches` | objet | Nombre de fois où l’application a été lancée. | {id (string), value (number)} |
| `mobilecrashes` | `application.crashes` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `mobilemessageclicks` | `directMarketing.clicks` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videotime` | `media.mediaTimed.timePlayed` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videostart` | `media.mediaTimed.impressions` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videocomplete` | `media.mediaTimed.completes` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videosegmentviews` | `media.mediaTimed.mediaSegmentViews` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videoadstart` | `advertising.impressions` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videoadcomplete` | `advertising.completes` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videoadtime` | `advertising.timePlayed` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videochapterstart` | `media.mediaTimed.mediaChapter.`<br/>`impressions` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videochaptercomplete` | `media.mediaTimed.mediaChapter.`<br/>`completes` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videochaptertime` | `media.mediaTimed.mediaChapter.`<br/>`timePlayed` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videoplay` | `media.mediaTimed.starts` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videototaltime` | `media.mediaTimed.totalTimePlayed` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | objet | Temps jusqu’au début de la qualité vidéo. | {id (string), value (number)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | objet | Nombre de mémoires tampons de la qualité vidéo. | {id (string), value (number)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | objet | Période tampon de la qualité vidéo. | {id (string), value (number)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | objet | Nombre de changements de la qualité vidéo. | {id (string), value (number)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | objet | Débit moyen de la qualité vidéo. | {id (string), value (number)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | objet | Nombre d’erreurs de la qualité vidéo. | {id (string), value (number)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress10` | `media.mediaTimed.progress10` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress25` | `media.mediaTimed.progress25` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress50` | `media.mediaTimed.progress50` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress75` | `media.mediaTimed.progress75` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress95` | `media.mediaTimed.progress95` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videoresume` | `media.mediaTimed.resumes` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videopausecount` | `media.mediaTimed.pauses` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videopausetime` | `media.mediaTimed.pauseTime` | objet | <!-- MISSING --> | {id (string), value (number)} |
| `videosecondssincelastcall` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sessionTimeout` | Entier |

{style="table-layout:auto"}

## Champs de mappage partagé

Ces champs ont une source unique, mais ils sont mappés à **plusieurs** emplacements XDM.

| Champ Analytics | Champ XDM | Type XDM | Description |
| --------------- | --------- | -------- | ---------- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | entier | Identifiant numérique représentant la résolution du moniteur. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | chaîne | Version du système d’exploitation mobile. |
| `videoadlength` | `advertising.adAssetReference._xmpDM.duration` | entier | Durée de la publicité vidéo. |

{style="table-layout:auto"}

## Champs de mappage générés

Certains champs provenant d’ADC doivent être transformés, ce qui nécessite la génération d’une logique au-delà d’une copie directe d’Adobe Analytics dans XDM.

| Champ Analytics | Champ XDM | Type XDM | Description |
| --------------- | --------- | -------- | ----------- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objet | Props Analytics personnalisées, configurées pour être des props de liste. Il contient une liste délimitée de valeurs. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | objet | Utilisé par les variables de hiérarchie. Il contient une liste délimitée de valeurs. | {values (array), delimiter (string)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | tableau | Variables de liste Analytics personnalisées. Contient une liste délimitée de valeurs. | {value (string), key (string)} |
| `m_color` | `device.colorDepth` | Entier | Identifiant de profondeur de couleur, qui est basé sur la valeur de la colonne c_color. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | booléen | Variable utilisée dans la dimension Prise en charge des cookies. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | objet | Événements de commerce standard déclenchés à l’accès. | {id (string), value (number)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | objet | Événements personnalisés déclenchés à l’accès. | {id (Object), value (Object)} |
| `m_geo_country` | `placeContext.geo.countryCode` | Chaîne | Abréviation du pays d’où provient l’accès, basé sur l’adresse IP. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | nombre | <!-- MISSING --> |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | nombre | <!-- MISSING --> |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | Booléen | Indicateur qui signale si Java™ est activé. |
| `m_latitude` | `placeContext.geo._schema.latitude` | nombre | <!-- MISSING --> |
| `m_longitude` | `placeContext.geo._schema.longitude` | nombre | <!-- MISSING --> |
| `m_page_event_var1` | `web.webInteraction.URL` | chaîne | Variable utilisée uniquement dans les demandes d’image de suivi de liens. Cette variable contient l’URL du lien de téléchargement, de sortie ou personnalisé sur lequel a cliqué l’utilisateur. |
| `m_page_event_var2` | `web.webInteraction.name` | chaîne | Variable utilisée uniquement dans les demandes d’image de suivi de liens. Répertorie le nom personnalisé du lien, s’il est spécifié. |
| `m_page_type` | `web.webPageDetails.isErrorPage` | booléen | Variable utilisée pour remplir la dimension Pages introuvables. Cette variable doit être vide ou contenir « ErrorPage ». |
| `m_pagename_no_url` | `web.webPageDetails.name` | nombre | Nom de la page (s’il est défini). Si aucune page n’est spécifiée, cette valeur reste vide. |
| `m_paid_search` | `search.isPaid` | booléen | Indicateur défini si l’accès correspond à la détection des référencements payants. |
| `m_product_list` | `productListItems[].items` | tableau | Liste de produits, telle qu’elle est transmise par l’intermédiaire de la variable des produits. | {SKU (string), quantity (integer), priceTotal (number)} |
| `m_ref_type` | `web.webReferrer.type` | chaîne | Identifiant numérique représentant le type de référence pour l’accès.<br/>`1` : À l&#39;intérieur de votre site <br/>`2` : Autres sites Web <br/>`3` : Moteurs de recherche <br/>`4` : Disque dur <br/>`5` : USENET <br/>`6` : Typed/Bookmarked (pas de référent)<br/>`7` : e-mail <br/>`8` : Pas de JavaScript <br/>`9` : Réseaux sociaux |
| `m_search_engine` | `search.searchEngine` | chaîne | Identifiant numérique représentant le moteur de recherche qui a renvoyé le visiteur sur votre site. |
| `post_currency` | `commerce.order.currencyCode` | chaîne | Code de devise utilisé pendant la transaction. |
| `post_cust_hit_time_gmt` | `timestamp` | chaîne | Utilisé uniquement dans les jeux de données horodatés. Il s’agit de l’horodatage envoyé avec l’accès, basé sur l’heure UNIX®. |
| `post_cust_visid` | `identityMap` | objet | Identifiant visiteur du client. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | booléen | Identifiant visiteur du client. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | chaîne | Identifiant visiteur du client. |
| `post_visid_high` + `visid_low` | `identityMap` | objet | Identifiant unique d’une visite. |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | chaîne | Identifiant unique d’une visite. |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | Booléen | Utilisé avec `visid_low` pour identifier de manière unique une visite. |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | Chaîne | Utilisé avec `visid_low` pour identifier de manière unique une visite. |
| `post_visid_low` | `identityMap` | objet | Utilisé avec visid_high pour identifier de manière unique une visite. |
| `hit_time_gmt` | `receivedTimestamp` | Chaîne | Date et heure de l’accès, basées sur l’heure UNIX®. |
| `hitid_high` + `hitid_low` | `_id` | chaîne | Identifiant unique permettant d’identifier un accès. |
| `hitid_low` | `_id` | Chaîne | Utilisé avec hitid_high pour identifier de manière unique un accès. |
| `ip` | `environment.ipV4` | chaîne | Adresse IP, basée sur l’en-tête HTTP de la demande d’image. |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | booléen | Version de JavaScript utilisée. |
| `mcvisid_high` + `mcvisid_low` | identityMap | objet | Identifiant visiteur Experience Cloud. |
| `mcvisid_high` + `mcvisid_low` | endUserIDs._experience.mcid.id | chaîne | L’Experience Cloud ID (ECID) est également appelé MCID et est parfois utilisé dans les espaces de noms. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | Booléen | L’Experience Cloud ID (ECID) est également appelé MCID et est parfois utilisé dans les espaces de noms. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | Chaîne | L’Experience Cloud ID (ECID) est également appelé MCID et est parfois utilisé dans les espaces de noms. |
| `mcvisid_low` | `identityMap` | objet | Identifiant visiteur Experience Cloud. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | chaîne | Identifiant d’assemblage d’accès. Le champ d’analyse sdid_high et sdid_low correspond à l’identifiant de données supplémentaire utilisé pour associer deux (ou plusieurs) accès entrants. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | chaîne | Proximité du relais Mobile Services. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._xmpDM.duration` | entier | Nom de chapitre vidéo. |
| `videolength` | `media.mediaTimed.primaryAssetReference.`<br/>`_xmpDM.duration` | entier | Durée de la vidéo. |

{style="table-layout:auto"}

## Champs de mappage avancé

Certains champs (appelés « valeurs de publication ») contiennent des données après l’ajustement de leurs valeurs par Adobe à l’aide des règles de traitement, des règles VISTA et des tables de recherche. La plupart des valeurs post ont un équivalent prétraité.

Le connecteur source Analytics envoie des données prétraitées dans un jeu de données dans Experience Platform. Vous pouvez transformer ces données en données correspondantes post-traitées à l’aide de transformations. Pour en savoir plus sur l’exécution de ces transformations à l’aide de Query Service, consultez [Fonctions définies par Adobe](/help/query-service/sql/adobe-defined-functions.md) dans le guide d’utilisation de Query Service.

Pour en savoir plus sur l’exécution de ces transformations à l’aide de Query Service, consultez [Fonctions définies par Adobe](/help/query-service/sql/adobe-defined-functions.md) dans le guide d’utilisation de Query Service.

| Champ Analytics | Champ XDM | Type XDM | Description |
| --------------- | --------- | -------- | ---------- |
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | chaîne | eVars d’analyse personnalisées. Chaque organisation peut utiliser des eVars différemment. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | Chaîne | Props Analytics personnalisées. Chaque organisation peut utiliser des props différemment. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | entier | Hauteur du navigateur, en pixels. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | entier | Largueur du navigateur, en pixels. |
| `post_campaign` | `marketing.trackingCode` | chaîne | Variable utilisée dans la dimension Code de suivi. |
| `post_channel` | `web.webPageDetails.siteSection` | chaîne | Variable utilisée dans la dimension Sections du site. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | chaîne | Identifiant visiteur personnalisé, le cas échéant. |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | chaîne | URL de la première page atteinte par le visiteur. |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | chaîne | Variable utilisée dans la dimension Page d’accès originale. Nom de page de la page d’accès du visiteur. |
| `post_keywords` | `search.keywords` | chaîne | Mots-clés collectés pour l’accès. |
| `post_page_url` | `web.webPageDetails.URL` | chaîne | URL de l’accès à la page. |
| `post_pagename` | `web.webPageDetails.pageViews.value` | Chaîne | Est égal à 1 sur les accès ayant un nom de page. Ceci est similaire à la mesure Pages vues d’Adobe Analytics. |
| `post_purchaseid` | `commerce.order.purchaseID` | chaîne | Variable utilisée pour identifier de manière unique les achats. |
| `post_referrer` | `web.webReferrer.URL` | chaîne | URL de la page précédente. |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | chaîne | Variable d’état. |
| `post_user_server` | `web.webPageDetails.server` | chaîne | Variable utilisée dans la dimension Serveur. |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | chaîne | Variable utilisée pour remplir la dimension Code postal. |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | entier | Identifiant numérique du navigateur. |
| `domain` | `environment.domain` | chaîne | Variable utilisée dans la dimension Domaine. Il est basé sur le fournisseur de services Internet (FAI) de l’utilisateur. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | chaîne | Première URL de référence du visiteur. |
| `geo_city` | `placeContext.geo.city` | chaîne | Nom de la ville de l’accès. Il est basé sur l’adresse IP de l’accès. |
| `geo_dma` | `placeContext.geo.dmaID` | entier | Identifiant numérique de la zone démographique pour l’accès. Il est basé sur l’adresse IP de l’accès. |
| `geo_region` | `placeContext.geo.stateProvince` | chaîne | Nom de l’état ou de la région de l’accès. Il est basé sur l’adresse IP de l’accès. |
| `geo_zip` | `placeContext.geo.postalCode` | chaîne | Code postal de l’accès. Il est basé sur l’adresse IP de l’accès. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | entier | Identifiant numérique représentant le système d’exploitation du visiteur. Dépend de la colonne user_agent. |
| `search_page_num` | `search.pageDepth` | entier | Cette variable est utilisée par la dimension Classification globale des pages de recherche et indique sur quelle page de résultats de recherche est apparu votre site | avant que l’utilisateur n’ait cliqué sur celui-ci. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | chaîne | Variable utilisée dans la dimension Mots-clés de recherche. |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | entier | Variable utilisée dans la dimension Nombre de visites. Commence à 1 et est incrémenté chaque fois qu’une nouvelle visite est entamée (par utilisateur). |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | entier | Variable utilisée dans la dimension Détail des accès. Cette valeur augmente de 1 pour chaque accès généré par l’utilisateur et est réinitialisée après chaque visite. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | chaîne | Premier référent de la visite. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | entier | Premier nom de page de la visite. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objet | Props Analytics personnalisées, configurées pour être des props de liste. Il contient une liste délimitée de valeurs. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | objet | Utilisé par les variables de hiérarchie et contient une liste délimitée de valeurs. | {values (array), delimiter (string)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | tableau | Liste de valeurs variables. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. | {value (string), key (string)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | booléen | Variable utilisée dans la dimension Prise en charge des cookies. |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | objet | Événements de commerce standard déclenchés à l’accès. | {id (string), value (number)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | objet | Événements personnalisés déclenchés à l’accès. | {id (Object), value (Object)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | Booléen | Indicateur qui signale si Java™ est activé. |
| `post_latitude` | `placeContext.geo._schema.latitude` | nombre | <!-- MISSING --> |
| `post_longitude` | `placeContext.geo._schema.longitude` | nombre | <!-- MISSING --> |
| `post_page_event` | `web.webInteraction.type` | chaîne | Le type d’accès qui est envoyé dans la demande d’image (accès standard, lien de téléchargement, lien de sortie ou lien personnalisé sur lequel le visiteur a cliqué). |
| `post_page_event` | `web.webInteraction.linkClicks.value` | nombre | Est égal à 1 si l’accès est un clic sur un lien. Ceci est similaire à la mesure Événements de page dans Adobe Analytics. |
| `post_page_event_var1` | `web.webInteraction.URL` | chaîne | Variable utilisée uniquement dans les demandes d’image de suivi de liens. Il s’agit de l’URL du lien de téléchargement, du lien de sortie ou du lien personnalisé sur lequel l’utilisateur a cliqué. |
| `post_page_event_var2` | `web.webInteraction.name` | chaîne | Variable utilisée uniquement dans les demandes d’image de suivi de liens. Il s’agit du nom personnalisé du lien. |
| `post_page_type` | `web.webPageDetails.isErrorPage` | booléen | Utilisé pour remplir la dimension Pages introuvables. Cette variable doit être vide ou contenir « ErrorPage ». |
| `post_pagename_no_url` | `web.webPageDetails.name` | nombre | Nom de la page (s’il est défini). Si aucune page n’est spécifiée, cette valeur reste vide. |
| `post_product_list` | `productListItems[].items` | tableau | Liste de produits, telle qu’elle est transmise par l’intermédiaire de la variable des produits. | {SKU (string), quantity (integer), priceTotal (number)} |
| `post_search_engine` | `search.searchEngine` | chaîne | Identifiant numérique représentant le moteur de recherche qui a renvoyé le visiteur sur votre site. |
| `mvvar1_instances` | `.list.items[]` | objet | Liste de valeurs variables. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. |
| `mvvar2_instances` | `.list.items[]` | objet | Liste de valeurs variables. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. |
| `mvvar3_instances` | `.list.items[]` | objet | Liste de valeurs variables. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. |
| `color` | `device.colorDepth` | entier | Identifiant de profondeur de la couleur, basé sur la valeur de la colonne c_color. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | Chaîne | Identifiant numérique, représentant le type de référent du premier référent du visiteur. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | Entier | Horodatage du premier accès du visiteur en temps UNIX®. |
| `geo_country` | `placeContext.geo.countryCode` | chaîne | Abréviation du pays d’où provient l’accès, selon l’adresse IP. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | nombre | <!-- MISSING --> |
| `geo_longitude` | `placeContext.geo._schema.longitude` | nombre | <!-- MISSING --> |
| `paid_search` | `search.isPaid` | booléen | Indicateur défini si l’accès correspond à la détection des référencements payants. |
| `ref_type` | `web.webReferrer.type` | chaîne | Identifiant numérique représentant le type de référence pour l’accès. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | booléen | Indicateur (1=payant, 0=non payant) signalant si le premier accès de la visite provient d’un accès de référencement payant. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | chaîne | Identifiant numérique, représentant le type de référent du premier référent du visiteur. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | chaîne | Identifiant numérique du premier moteur de recherche de la visite. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | Entier | Date et heure du premier accès de la visite à l’heure UNIX®. |

{style="table-layout:auto"}