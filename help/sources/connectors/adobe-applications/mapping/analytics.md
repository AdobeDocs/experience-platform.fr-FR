---
keywords: Experience Platform;accueil;rubriques populaires;champs de mappage Analytics;mappage analytics
solution: Experience Platform
title: Mappage des champs pour le connecteur source Adobe Analytics
description: Adobe Experience Platform vous permet d’ingérer des données Adobe Analytics par le biais de la source Analytics. Certaines données ingérées par ADC peuvent être mappées directement des champs Analytics aux champs du modèle de données d’expérience (XDM), tandis que d’autres nécessitent des transformations et des fonctions spécifiques pour être mappées avec succès.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '3419'
ht-degree: 97%

---

# Mappages de champs Analytics

Adobe Experience Platform vous permet d’ingérer des données Adobe Analytics par le biais de la source Analytics. Certaines données ingérées par ADC peuvent être mappées directement des champs Analytics aux champs du modèle de données d’expérience (XDM), tandis que d’autres nécessitent des transformations et des fonctions spécifiques pour être mappées avec succès.

![](../images/analytics-data-experience-platform.png)

## Champs de mappage direct

Certains champs sont directement mappés d’Adobe Analytics au modèle de données d’expérience (XDM, Experience Data Model).

Le tableau suivant comprend des colonnes qui indiquent le nom du champ Analytics (*Champ Analytics*), le champ XDM correspondant (*Champ XDM*) et son type (*Type XDM*), ainsi qu’une description du champ (*Description*).

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Champ Analytics | Champ XDM | Type XDM | Description |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | chaîne | Variable personnalisée, qui peut être comprise entre 1 et 250. Chaque organisation peut utiliser ces eVars personnalisées différemment. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | chaîne | Variables de trafic personnalisées, qui peuvent être comprises entre 1 et 75. |
| m_browser | _experience.analytics.environment.browserID | entier | Numéro d’identifiant du navigateur. |
| m_browser_height | environment.browserDetails.viewportHeight | entier | Hauteur du navigateur, en pixels. |
| m_browser_width | environment.browserDetails.viewportWidth | entier | Largueur du navigateur, en pixels. |
| m_campaign | marketing.trackingCode | chaîne | Variable utilisée dans la dimension Code de suivi. |
| m_channel | web.webPageDetails.siteSection | chaîne | Variable utilisée dans la dimension Sections du site. |
| m_domain | environment.domain | chaîne | Variable utilisée dans la dimension Domaine. Dépend du fournisseur d’accès à Internet (FAI) de l’utilisateur. |
| m_geo_city | placeContext.geo.city | chaîne | Nom de la ville de l’accès. Dépend de l’adresse IP de l’accès. |
| m_geo_dma | placeContext.geo.dmaID | entier | Identifiant numérique de la zone démographique pour l’accès. Dépend de l’adresse IP de l’accès. |
| m_geo_region | placeContext.geo.stateProvince | chaîne | Nom de l’état ou de la région de l’accès. Dépend de l’adresse IP de l’accès. |
| m_geo_zip | placeContext.geo.postalCode | chaîne | Code postal de l’accès. Dépend de l’adresse IP de l’accès. |
| m_keywords | search.keywords | chaîne | Variable utilisée dans la dimension Mot-clé. |
| m_os | _experience.analytics.environment.operatingSystemID | entier | Identifiant numérique représentant le système d’exploitation du visiteur. Dépend de la colonne user_agent. |
| m_page_url | web.webPageDetails.URL | chaîne | URL de l’accès à la page. |
| m_pagename_no_url | web.webPageDetails.</span>name | chaîne | Variable utilisée pour remplir la dimension Pages. |
| m_referrer | web.webReferrer.URL | chaîne | URL de la page précédente. |
| m_search_page_num | search.pageDepth | entier | Variable utilisée par la dimension Classification globale des pages de recherche. Indique la page des résultats de recherche sur laquelle votre site est apparu avant que l’utilisateur n’ait cliqué sur votre site. |
| m_state | _experience.analytics.customDimensions.stateProvince | chaîne | Variable d’état. |
| m_user_server | web.webPageDetails.server | chaîne | Variable utilisée dans la dimension Serveur. |
| m_zip | _experience.analytics.customDimensions.postalCode | chaîne | Variable utilisée pour remplir la dimension Code postal. |
| accept_language | environment.browserDetails.acceptLanguage | chaîne | Liste de tous les langages acceptés, comme indiqué dans l’en-tête HTTP Accept-Language. |
| homepage | web.webPageDetails.isHomePage | booléen | N’est plus utilisé. Indique si l’URL active est la page d’accueil du navigateur. |
| ipv6 | environment.ipV6 | chaîne |
| j_jscript | environment.browserDetails.javaScriptVersion | chaîne | Version de JavaScript prise en charge par le navigateur. |
| user_agent | environment.browserDetails.userAgent | chaîne | Chaîne de l’agent utilisateur envoyée dans l’en-tête HTTP. |
| mobileappid | application.</span>name | chaîne | Identifiant de l’application mobile, stocké au format suivant : `[AppName][BundleVersion]`. |
| mobiledevice | device.model | chaîne | Nom de l’appareil mobile. Sous iOS, il est stocké sous la forme d’une chaîne de 2 chiffres séparés par des virgules. Le premier chiffre représente la génération de l’appareil, le second représente la famille d’appareils. |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>name | chaîne | Utilisé par les services mobiles. Représente le point ciblé. |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | nombre | Utilisé par les services mobiles. Représente la distance du point ciblé. |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | nombre | Collecté à partir de la variable a.loc.acc des données de contexte. Indique la précision du GPS en mètres au moment de la collecte des données. |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | chaîne | Collecté à partir de la variable a.loc.category des données de contexte. Décrit la catégorie d’un lieu en particulier. |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | chaîne | Collecté à partir de la variable a.loc.id des données de contexte. Identifiant d’un point ciblé donné. |
| video | media.mediaTimed.primaryAssetReference._id | chaîne | Nom de la vidéo. |
| videoad | advertising.adAssetReference._id | chaîne | Identifiant de la ressource publicitaire. |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | chaîne | Type de contenu vidéo. Défini automatiquement sur « Vidéo » pour toutes les consultations vidéo. |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | chaîne | Capsule dans laquelle se trouve la publicité vidéo. |
| videoadinpod | advertising.adAssetViewDetails.index | entier | Position de la publicité vidéo dans la capsule. |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | chaîne | Nom du lecteur vidéo. |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | chaîne | Canal vidéo. |
| videoadplayername | advertising.adAssetViewDetails.playerName | chaîne | Nom du lecteur de publicité vidéo. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | chaîne | Nom du chapitre vidéo. |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | chaîne | Nom de la vidéo. |
| videoadname | advertising.adAssetReference._dc.title | chaîne | Nom de la publicité vidéo. |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | chaîne | Affichage de la vidéo. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | chaîne | Saison de la vidéo. |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | chaîne | Épisode de la vidéo. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | chaîne | Réseau de la vidéo. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | chaîne | Type d’affichage de la vidéo. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | chaîne | Chargements des publicités vidéo. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | chaîne | Type de flux vidéo. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | nombre | Relais Mobile Services majeur. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | nombre | Relais Mobile Services mineur. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | chaîne | UUID du relais Mobile Services. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | chaîne | Identifiant de session vidéo. |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | tableau | Genre de la vidéo. | {title (Object), description (Object), type (Object), meta:xdmType (Object), items (string), meta:xdmField (Object)} |
| mobileinstalls | application.firstLaunches | objet | Se déclenche lors de la première exécution après l’installation ou la réinstallation. | {id (string), value (number)} |
| mobileupgrades | application.upgrades | objet | Indique le nombre de mises à niveau d’application. Se déclenche lors de la première exécution après mise à niveau ou dès que le numéro de version change. | {id (string), value (number)} |
| mobilelaunches | application.launches | objet | Nombre de fois où l’application a été lancée. | {id (string), value (number)} |
| mobilecrashes | application.crashes | objet | <!-- MISSING --> | {id (string), value (number)} |
| mobilemessageclicks | directMarketing.clicks | objet | <!-- MISSING --> | {id (string), value (number)} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | objet | <!-- MISSING --> | {id (string), value (number)} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | objet | <!-- MISSING --> | {id (string), value (number)} |
| videotime | media.mediaTimed.timePlayed | objet | <!-- MISSING --> | {id (string), value (number)} |
| videostart | media.mediaTimed.impressions | objet | <!-- MISSING --> | {id (string), value (number)} |
| videocomplete | media.mediaTimed.completes | objet | <!-- MISSING --> | {id (string), value (number)} |
| videosegmentviews | media.mediaTimed.mediaSegmentViews | objet | <!-- MISSING --> | {id (string), value (number)} |
| videoadstart | advertising.impressions | objet | <!-- MISSING --> | {id (string), value (number)} |
| videoadcomplete | advertising.completes | objet | <!-- MISSING --> | {id (string), value (number)} |
| videoadtime | advertising.timePlayed | objet | <!-- MISSING --> | {id (string), value (number)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | objet | <!-- MISSING --> | {id (string), value (number)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | objet | <!-- MISSING --> | {id (string), value (number)} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | objet | <!-- MISSING --> | {id (string), value (number)} |
| videoplay | media.mediaTimed.starts | objet | <!-- MISSING --> | {id (string), value (number)} |
| videototaltime | media.mediaTimed.totalTimePlayed | objet | <!-- MISSING --> | {id (string), value (number)} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | objet | Temps jusqu’au début de la qualité vidéo. | {id (string), value (number)} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | objet | <!-- MISSING --> | {id (string), value (number)} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | objet | Nombre de mémoires tampons de la qualité vidéo. | {id (string), value (number)} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | objet | Période tampon de la qualité vidéo. | {id (string), value (number)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | objet | Nombre de changements de la qualité vidéo. | {id (string), value (number)} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | objet | Débit moyen de la qualité vidéo. | {id (string), value (number)} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | objet | Nombre d’erreurs de la qualité vidéo. | {id (string), value (number)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | objet | <!-- MISSING --> | {id (string), value (number)} |
| videoprogress10 | media.mediaTimed.progress10 | objet | <!-- MISSING --> | {id (string), value (number)} |
| videoprogress25 | media.mediaTimed.progress25 | objet | <!-- MISSING --> | {id (string), value (number)} |
| videoprogress50 | media.mediaTimed.progress50 | objet | <!-- MISSING --> | {id (string), value (number)} |
| videoprogress75 | media.mediaTimed.progress75 | objet | <!-- MISSING --> | {id (string), value (number)} |
| videoprogress95 | media.mediaTimed.progress95 | objet | <!-- MISSING --> | {id (string), value (number)} |
| videoresume | media.mediaTimed.resumes | objet | <!-- MISSING --> | {id (string), value (number)} |
| videopausecount | media.mediaTimed.pauses | objet | <!-- MISSING --> | {id (string), value (number)} |
| videopausetime | media.mediaTimed.pauseTime | objet | <!-- MISSING --> | {id (string), value (number)} |
| videosecondssincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | entier |

{style="table-layout:auto"}

## Champs de mappage fractionné.

Ces champs ont une source unique, mais ils sont mappés à **plusieurs** emplacements XDM.

| Champ Analytics | Champ XDM | Type XDM | Description |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | entier | Identifiant numérique représentant la résolution du moniteur. |
| mobileosversion | environment.operatingSystem, environment.operatingSystemVersion | chaîne | Version du système d’exploitation mobile. |
| videoadlength | advertising.adAssetReference._xmpDM.duration | entier | Durée de la publicité vidéo. |

{style="table-layout:auto"}

## Champs de mappage générés

Il est nécessaire de transformer certains champs provenant d’ADC, ce qui nécessite une logique au-delà d’une copie directe d’Adobe Analytics pour pouvoir les générer dans XDM.

Le tableau suivant comprend des colonnes qui indiquent le nom du champ Analytics (*Champ Analytics*), le champ XDM correspondant (*Champ XDM*) et son type (*Type XDM*), ainsi qu’une description du champ (*Description*).

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Champ Analytics | Champ XDM | Type XDM | Description |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | objet | Variables de trafic personnalisées, allant de 1 à 75. | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | objet | Utilisé par les variables de hiérarchie. Contient une | liste de valeurs délimitée. | {values (array), delimiter (string)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | tableau | Liste de valeurs variables. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. | {value (string), key (string)} |
| m_color | device.colorDepth | entier | Identifiant de profondeur de la couleur, basé sur la valeur de la colonne c_color. |
| m_cookies | environment.browserDetails.cookiesEnabled | booléen | Variable utilisée dans la dimension Prise en charge des cookies. |
| m_event_list | commerce.purchases, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdds, commerce.productListRemovals, commerce.productListViews | objet | Événements de commerce standard déclenchés à l’accès. | {id (string), value (number)} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200, _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event301to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event501 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event701to800.event701 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | objet | Événements personnalisés déclenchés à l’accès. | {id (Object), value (Object)} |
| m_geo_country | placeContext.geo.countryCode | chaîne | Abréviation du pays d’où provient l’accès, selon l’adresse IP. |
| m_geo_latitude | placeContext.geo._schema.latitude | nombre | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._schema.longitude | nombre | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | booléen | Indicateur précisant si Java est activé. |
| m_latitude | placeContext.geo._schema.latitude | nombre | <!-- MISSING --> |
| m_longitude | placeContext.geo._schema.longitude | nombre | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | chaîne | Variable utilisée uniquement dans les demandes d’image de suivi de liens. Cette variable contient l’URL du lien de téléchargement, de sortie ou personnalisé sur lequel a cliqué l’utilisateur. |
| m_page_event_var2 | web.webInteraction.name | chaîne | Variable utilisée uniquement dans les demandes d’image de suivi de liens. Répertorie le nom personnalisé du lien, s’il est spécifié. |
| m_page_type | web.webPageDetails.isErrorPage | booléen | Variable utilisée pour remplir la dimension Pages introuvables. Cette variable doit être vide ou contenir « ErrorPage ». |
| m_pagename_no_url | web.webPageDetails.pageViews.value | nombre | Nom de la page (s’il est défini). Si aucune page n’est spécifiée, cette valeur n’est pas renseignée. |
| m_paid_search | search.isPaid | booléen | Indicateur défini si l’accès correspond à la détection des référencements payants. |
| m_product_list | productListItems[].items | tableau | Liste de produits, telle qu’elle est transmise par l’intermédiaire de la variable des produits. | {SKU (string), quantity (integer), priceTotal (number)} |
| m_ref_type | web.webReferrer.type | chaîne | Identifiant numérique représentant le type de référence pour l’accès. 1 signifie à l’intérieur de votre site, 2 signifie d’autres sites web, 3 signifie moteurs de recherche, 4 signifie disque dur, 5 signifie USENET, 6 signifie Tapé/Marqué (aucun référent), 7 signifie e-mail, 8 signifie Pas de JavaScript et 9 signifie Réseaux sociaux. |
| m_search_engine | search.searchEngine | chaîne | Identifiant numérique représentant le moteur de recherche qui a renvoyé le visiteur sur votre site. |
| post_currency | commerce.order.currencyCode | chaîne | Code de devise utilisé pendant la transaction. |
| post_cust_hit_time_gmt | timestamp | chaîne | Utilisé uniquement dans les jeux de données horodatés. Il s’agit de l’horodatage envoyé avec l’accès, selon l’heure Unix. |
| post_cust_visid | identityMap | objet | Identifiant visiteur du client. |
| post_cust_visid | endUserIDs._experience.aacustomid.primary | booléen | Identifiant visiteur du client. |
| post_cust_visid | endUserIDs._experience.aacustomid.namespace.code | chaîne | Identifiant visiteur du client. |
| post_visid_high + visid_low | identityMap | objet | Identifiant unique d’une visite. |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | chaîne | Identifiant unique d’une visite. |
| post_visid_high | endUserIDs._experience.aaid.primary | booléen | Utilisé conjointement avec visid_low pour identifier de manière unique une visite. |
| post_visid_high | endUserIDs._experience.aaid.namespace.code | chaîne | Utilisé conjointement avec visid_low pour identifier de manière unique une visite. |
| post_visid_low | identityMap | objet | Utilisé conjointement avec visid_high pour identifier de manière unique une visite. |
| hit_time_gmt | receivedTimestamp | chaîne | Horodatage de l’accès, selon l’heure Unix. |
| hitid_high + hitid_low | _id | chaîne | Identifiant unique permettant d’identifier un accès. |
| hitid_low | _id | chaîne | Utilisé conjointement avec hitid_high pour identifier de manière unique un accès. |
| ip | environment.ipV4 | chaîne | Adresse IP, basée sur l’en-tête HTTP de la demande d’image. |
| j_jscript | environment.browserDetails.javaScriptEnabled | booléen | Version de JavaScript utilisée. |
| mcvisid_high + mcvisid_low | identityMap | objet | Identifiant visiteur Experience Cloud. |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | chaîne | L’identifiant Experience Cloud (ECID) est également connu sous le nom de MCID et parfois utilisé dans les espaces de noms. |
| mcvisid_high | endUserIDs._experience.mcid.primary | booléen | L’identifiant Experience Cloud (ECID) est également connu sous le nom de MCID et parfois utilisé dans les espaces de noms. |
| mcvisid_high | endUserIDs._experience.mcid.namespace.code | chaîne | L’identifiant Experience Cloud (ECID) est également connu sous le nom de MCID et parfois utilisé dans les espaces de noms. |
| mcvisid_low | identityMap | objet | Identifiant visiteur Experience Cloud. |
| sdid_high + sdid_low | _experience.target.supplementalDataID | chaîne | Identifiant d’assemblage d’accès. Le champ d’analyse sdid_high et sdid_low correspond à l’identifiant de données supplémentaire utilisé pour associer deux (ou plusieurs) accès entrants. |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | chaîne | Proximité du relais Mobile Services. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | entier | Nom de chapitre vidéo. |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | entier | Durée de la vidéo. |

{style="table-layout:auto"}

## Champs de mappage avancé

Certains champs (appelés « valeurs de publication ») nécessitent des transformations plus avancées avant de pouvoir mapper les champs Adobe Analytics au modèle de données d’expérience (XDM). L’exécution de ces transformations avancées implique l’utilisation d’Adobe Experience Platform Query Service et de fonctions prédéfinies (appelées fonctions définies par Adobe) pour la transformation en sessions, l’attribution et la déduplication.

Pour en savoir plus sur l’exécution de ces transformations à l’aide de Query Service, consultez la documentation sur les [fonctions définies par Adobe](../../../../query-service/sql/adobe-defined-functions.md).

Le tableau suivant comprend des colonnes qui indiquent le nom du champ Analytics (*Champ Analytics*), le champ XDM correspondant (*Champ XDM*) et son type (*Type XDM*), ainsi qu’une description du champ (*Description*).

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Champ Analytics | Champ XDM | Type XDM | Description |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | chaîne | Variable personnalisée, qui peut être comprise entre 1 et 250. Chaque organisation peut utiliser ces eVars personnalisées différemment. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | chaîne | Variables de trafic personnalisées, qui peuvent être comprises entre 1 et 75. |
| post_browser_height | environment.browserDetails.viewportHeight | entier | Hauteur du navigateur, en pixels. |
| post_browser_width | environment.browserDetails.viewportWidth | entier | Largueur du navigateur, en pixels. |
| post_campaign | marketing.trackingCode | chaîne | Variable utilisée dans la dimension Code de suivi. |
| post_channel | web.webPageDetails.siteSection | chaîne | Variable utilisée dans la dimension Sections du site. |
| post_cust_visid | endUserIDs._experience.aacustomid.id | chaîne | Identifiant visiteur personnalisé, le cas échéant. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | chaîne | URL de la première page atteinte par le visiteur. |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | chaîne | Variable utilisée dans la dimension Page d’accès originale. Nom de page de la page d’accès du visiteur. |
| post_keywords | search.keywords | chaîne | Mots-clés collectés pour l’accès. |
| post_page_url | web.webPageDetails.URL | chaîne | URL de l’accès à la page. |
| post_pagename_no_url | web.webPageDetails.name | chaîne | Variable utilisée pour remplir la dimension Pages. |
| post_purchaseid | commerce.order.purchaseID | chaîne | Variable utilisée pour identifier de manière unique les achats. |
| post_referrer | web.webReferrer.URL | chaîne | URL de la page précédente. |
| post_state | _experience.analytics.customDimensions.stateProvince | chaîne | Variable d’état. |
| post_user_server | web.webPageDetails.server | chaîne | Variable utilisée dans la dimension Serveur. |
| post_zip | _experience.analytics.customDimensions.postalCode | chaîne | Variable utilisée pour remplir la dimension Code postal. |
| browser | _experience.analytics.environment.browserID | entier | Identifiant numérique du navigateur. |
| domain | environment.domain | chaîne | Variable utilisée dans la dimension Domaine. Dépend du fournisseur d’accès à Internet (FAI) de l’utilisateur. |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferrer.URL | chaîne | Première URL de référence du visiteur. |
| geo_city | placeContext.geo.city | chaîne | Nom de la ville de l’accès. Dépend de l’adresse IP de l’accès. |
| geo_dma | placeContext.geo.dmaID | entier | Identifiant numérique de la zone démographique pour l’accès. Dépend de l’adresse IP de l’accès. |
| geo_region | placeContext.geo.stateProvince | chaîne | Nom de l’état ou de la région de l’accès. Dépend de l’adresse IP de l’accès. |
| geo_zip | placeContext.geo.postalCode | chaîne | Code postal de l’accès. Dépend de l’adresse IP de l’accès. |
| os | _experience.analytics.environment.operatingSystemID | entier | Identifiant numérique représentant le système d’exploitation du visiteur. Dépend de la colonne user_agent. |
| search_page_num | search.pageDepth | entier | Cette variable est utilisée par la dimension Classification globale des pages de recherche et indique sur quelle page de résultats de recherche est apparu votre site | avant que l’utilisateur n’ait cliqué sur celui-ci. |
| visit_keywords | _experience.analytics.session.search.keywords | chaîne | Variable utilisée dans la dimension Mots-clés de recherche. |
| visit_num | _experience.analytics.session.num | entier | Variable utilisée dans la dimension Nombre de visites. Commence à 1 et est incrémenté chaque fois qu’une nouvelle visite est entamée (par utilisateur). |
| visit_page_num | _experience.analytics.session.depth | entier | Variable utilisée dans la dimension Détail des accès. Cette valeur augmente de 1 pour chaque accès généré par l’utilisateur et est réinitialisée après chaque visite. |
| visit_referrer | _experience.analytics.session.web.webReferrer.URL | chaîne | Premier référent de la visite. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | entier | Premier nom de page de la visite. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | objet | Variables de trafic personnalisées 1 - 75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | objet | Utilisé par les variables de hiérarchie et contient une liste délimitée de valeurs. | {values (array), delimiter (string)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | tableau | Liste de valeurs variables. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. | {value (string), key (string)} |
| post_cookies | environment.browserDetails.cookiesEnabled | booléen | Variable utilisée dans la dimension Prise en charge des cookies. |
| post_event_list | commerce.purchases, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdds, commerce.productListRemovals, commerce.productListViews | objet | Événements de commerce standard déclenchés à l’accès. | {id (string), value (number)} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200, _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event301to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event501 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event701to800.event701 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | objet | Événements personnalisés déclenchés à l’accès. | {id (Object), value (Object)} |
| post_java_enabled | environment.browserDetails.javaEnabled | booléen | Indicateur précisant si Java est activé. |
| post_latitude | placeContext.geo._schema.latitude | nombre | <!-- MISSING --> |
| post_longitude | placeContext.geo._schema.longitude | nombre | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | chaîne | Le type d’accès qui est envoyé dans la demande d’image (accès standard, lien de téléchargement, lien de sortie ou lien personnalisé sur lequel le visiteur a cliqué). |
| post_page_event | web.webInteraction.linkClicks.value | nombre | Le type d’accès qui est envoyé dans la demande d’image (accès standard, lien de téléchargement, lien de sortie ou lien personnalisé sur lequel le visiteur a cliqué). |
| post_page_event_var1 | web.webInteraction.URL | chaîne | Variable utilisée uniquement dans les demandes d’image de suivi de liens. URL du lien de téléchargement, de sortie ou personnalisé sur lequel a cliqué l’utilisateur. |
| post_page_event_var2 | web.webInteraction.name | chaîne | Variable utilisée uniquement dans les demandes d’image de suivi de liens. Il s’agira du nom personnalisé du lien. |
| post_page_type | web.webPageDetails.isErrorPage | booléen | Utilisé pour remplir la dimension Pages introuvables. Cette variable doit être vide ou contenir « ErrorPage ». |
| post_pagename_no_url | web.webPageDetails.pageViews.value | nombre | Nom de la page (s’il est défini). Si aucune page n’est spécifiée, cette valeur n’est pas renseignée. |
| post_product_list | productListItems[].items | tableau | Liste de produits, telle qu’elle est transmise par l’intermédiaire de la variable des produits. | {SKU (string), quantity (integer), priceTotal (number)} |
| post_search_engine | search.searchEngine | chaîne | Identifiant numérique représentant le moteur de recherche qui a renvoyé le visiteur sur votre site. |
| mvvar1_instances | .list.items[] | objet | Liste de valeurs variables. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. |
| mvvar2_instances | .list.items[] | objet | Liste de valeurs variables. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. |
|  | mvvar3_instances | .list.items[] | objet | Liste de valeurs variables. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. |
| color | device.colorDepth | entier | Identifiant de profondeur de la couleur, basé sur la valeur de la colonne c_color. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | chaîne | Identifiant numérique, représentant le type de référent du tout premier référent du visiteur. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | entier | Horodatage du tout premier accès du visiteur (heure Unix). |
| geo_country | placeContext.geo.countryCode | chaîne | Abréviation du pays d’où provient l’accès, selon l’adresse IP. |
| geo_latitude | placeContext.geo._schema.latitude | nombre | <!-- MISSING --> |
| geo_longitude | placeContext.geo._schema.longitude | nombre | <!-- MISSING --> |
| paid_search | search.isPaid | booléen | Indicateur défini si l’accès correspond à la détection des référencements payants. |
| ref_type | web.webReferrer.type | chaîne | Identifiant numérique représentant le type de référence pour l’accès. |
| visit_paid_search | _experience.analytics.session.search.isPaid | booléen | Indicateur (1=payant, 0=non payant) signalant si le premier accès de la visite provient d’un accès de référencement payant. |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | chaîne | Identifiant numérique, représentant le type de référent du premier référent du visiteur. |
| visit_search_engine | _experience.analytics.session.search.searchEngine | chaîne | Identifiant numérique du premier moteur de recherche de la visite. |
| visit_start_time_gmt | _experience.analytics.session.timestamp | entier | Horodatage du premier accès de la visite (heure Unix). |

{style="table-layout:auto"}