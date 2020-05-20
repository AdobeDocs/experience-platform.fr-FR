---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Champs de mappage Analytics
topic: overview
translation-type: tm+mt
source-git-commit: 53fb7ea201ed9361584d24c8bd2ad10edd9f3975
workflow-type: tm+mt
source-wordcount: '3328'
ht-degree: 11%

---


# Champs de mappage Analytics

Adobe Experience Platform vous permet d’assimiler des données Adobe Analytics via le connecteur de données Analytics (ADC). Certaines des données ingérées par ADC peuvent être mappées directement des champs Analytics aux champs de modèle de données d’expérience (XDM), tandis que d’autres données nécessitent des transformations et des fonctions spécifiques pour être mappées avec succès.

![](../images/analytics-data-experience-platform.png)

## Champs de mappage direct

Certains champs sont directement mappés d’Adobe Analytics au modèle de données d’expérience (XDM).

Le tableau suivant comprend des colonnes qui indiquent le nom du champ Analytics (champ ** Analytics), le champ XDM correspondant (champ ** XDM) et son type (type ** XDM), ainsi qu’une description du champ (*Description).*

>[!NOTE] Veuillez faire défiler la page vers la gauche/vers la droite pour vue du contenu complet du tableau.

| Champ Analytics | Champ XDM | Type XDM | Description |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | chaîne | Variable personnalisée, qui peut être comprise entre 1 et 250. Chaque organisation utilisera ces eVars personnalisées différemment. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | chaîne | Variables de trafic personnalisées, qui peuvent varier de 1 à 75. |
| m_browser | _experience.analytics.environnement.browserID | entier | ID du numéro du navigateur. |
| m_browser_height | environment.browserDetails.viewportHeight | entier | Hauteur du navigateur, en pixels. |
| m_browser_width | environment.browserDetails.viewportWidth | entier | Largeur du navigateur, en pixels. |
| m_campaign | marketing.trackingCode | chaîne | Variable utilisée dans la dimension Code de suivi. |
| m_canal | web.webPageDetails.siteSection | chaîne | Variable utilisée dans la dimension Sections du site. |
| m_domain | environment.domain | chaîne | Variable utilisée dans la dimension Domaine. Il sera basé sur le prestataire Internet (FAI) de l&#39;utilisateur. |
| m_geo_city | placeContext.geo.city | chaîne | Nom de la ville de l’accès. Il est basé sur l’adresse IP de l’accès. |
| m_geo_dma | placeContext.geo.dmaID | entier | ID numérique de la zone démographique de l’accès. Il est basé sur l’adresse IP de l’accès. |
| m_geo_region | placeContext.geo.stateProvince | chaîne | Nom de l’état ou de la région de l’accès. Il est basé sur l’adresse IP de l’accès. |
| m_geo_zip | placeContext.geo.postalCode | chaîne | Code postal de l’accès. Il est basé sur l’adresse IP de l’accès. |
| m_keywords | search.keywords | chaîne | Variable utilisée dans la dimension Mot-clé. |
| m_os | _experience.analytics.environnement.operatingSystemID | entier | ID numérique représentant le système d’exploitation du visiteur. Il est basé sur la colonne user_agent. |
| m_page_url | web.webPageDetails.URL | chaîne | URL de l’accès à la page. |
| m_pagename_no_url | web.webPageDetails.</span>name | chaîne | Variable utilisée pour renseigner la dimension Pages. |
| m_parrain | web.webReferrer.URL | chaîne | URL de la page précédente. |
| m_search_page_num | search.pageDepth | entier | Utilisée par la dimension Classement de toutes les pages de recherche. Indique la page des résultats de recherche sur laquelle votre site s’est affiché avant que l’utilisateur n’ait cliqué sur votre site. |
| m_state | _experience.analytics.customDimensions.stateProvince | chaîne | Variable d’état. |
| m_user_server | web.webPageDetails.server | chaîne | Variable utilisée dans la dimension Serveur. |
| m_zip | _experience.analytics.customDimensions.postalCode | chaîne | Variable utilisée pour remplir la dimension Code postal. |
| accept_language | environment.browserDetails.acceptLanguage | chaîne | Liste toutes les langues acceptées, comme indiqué dans l’en-tête HTTP Accept-Language. |
| homepage | web.webPageDetails.isHomePage | booléen | N’est plus utilisé. Indique si l’URL active est la page d’accueil du navigateur. |
| ipv6 | environment.ipV6 | chaîne |
| j_jscript | environment.browserDetails.javaScriptVersion | chaîne | Version de JavaScript prise en charge par le navigateur. |
| user_agent | environment.browserDetails.userAgent | chaîne | Chaîne de l’agent utilisateur envoyée dans l’en-tête HTTP. |
| mobileappid | application.</span>name | chaîne | L’ID d’application mobile, stocké au format suivant : `[AppName][BundleVersion]`. |
| mobiledevice | device.model | chaîne | Nom du périphérique mobile. Sous iOS, il est stocké sous la forme d’une chaîne de 2 chiffres séparée par des virgules. Le premier chiffre représente la génération du périphérique et le second représente la famille du périphérique. |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>name | chaîne | Utilisé par les services mobiles. Représente le point d’intérêt. |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | nombre | Utilisé par les services mobiles. Représente la distance du point d’intérêt. |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | nombre | Collecté à partir de la variable a.loc.acc des données de contexte. Indique la précision du GPS en mètres au moment de la collecte des données. |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | chaîne | Collecté à partir de la variable a.loc.category des données de contexte. Décrit la catégorie d’un lieu en particulier. |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | chaîne | Collecté à partir de la variable de données contextuelles a.loc.id. Identifiant d’un point ciblé donné. |
| video | media.mediaTimed.primaryAssetReference._id | chaîne | Nom de la vidéo. |
| videoad | advertising.adAssetReference._id | chaîne | Identifiant de la ressource publicitaire. |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | chaîne | Type De Contenu Vidéo. Cette option est automatiquement définie sur &quot;Vidéo&quot; pour toutes les vues vidéo. |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | chaîne | Capsule dans laquelle se trouve la publicité vidéo. |
| videoadinpod | advertising.adAssetViewDetails.index | entier | Position de la publicité vidéo dans la capsule. |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | chaîne | Nom du lecteur vidéo. |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | chaîne | canal vidéo. |
| videoadplayername | advertising.adAssetViewDetails.playerName | chaîne | Nom du lecteur d’annonce vidéo. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | chaîne | Nom du chapitre Vidéo |
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
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | chaîne | ID de session vidéo. |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | tableau | Genre de la vidéo. | {title (Object), description (Object), type (Object), meta:xdmType (Object), items (string), meta:xdmField (Object)} |
| mobileinstalls | application.firstLaunches | Objet | Ceci est déclenché lors de la première exécution après l’installation ou la réinstallation. | {id (chaîne), valeur (nombre)} |
| mobileupgrades | application.upgrades | Objet | Indique le nombre de mises à niveau d’application. Déclenche à la première exécution après la mise à niveau ou à tout moment où le numéro de version change. | {id (chaîne), valeur (nombre)} |
| mobilelaunches | application.launches | Objet | Nombre de fois où l’application a été lancée. | {id (chaîne), valeur (nombre)} |
| mobilecrashes | application.crashes | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| mobilemessageclicks | directMarketing.clicks | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videotime | media.mediaTimed.timePlayed | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videostart | media.mediaTimed.impressions | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videocomplete | media.mediaTimed.completes | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videosegmentviews | media.mediaTimed.mediaSegmentViews | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videoadstart | advertising.impressions | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videoadcomplete | advertising.completes | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videoadtime | advertising.timePlayed | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videoplay | media.mediaTimed.starts | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videototaltime | media.mediaTimed.totalTimePlayed | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | Objet | Durée de qualité de la vidéo au début. | {id (chaîne), valeur (nombre)} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | Objet | Nombre de tampons de qualité vidéo | {id (chaîne), valeur (nombre)} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | Objet | Période tampon de la qualité vidéo | {id (chaîne), valeur (nombre)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | Objet | Nombre de changements de qualité vidéo | {id (chaîne), valeur (nombre)} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | Objet | Débit moyen de qualité vidéo | {id (chaîne), valeur (nombre)} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | Objet | Nombre d’erreurs de qualité vidéo | {id (chaîne), valeur (nombre)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videoprogress10 | media.mediaTimed.progress10 | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videoprogress25 | media.mediaTimed.progress25 | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videoprogress50 | media.mediaTimed.progress50 | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videoprogress75 | media.mediaTimed.progress75 | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videoprogress95 | media.mediaTimed.progress95 | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videoresume | media.mediaTimed.resumes | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videopausecount | media.mediaTimed.pauses | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videopausetime | media.mediaTimed.pauseTime | Objet | <!-- MISSING --> | {id (chaîne), valeur (nombre)} |
| videosecondssincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | entier |

## Champs de mappage fractionnés

Ces champs ont une source unique, mais sont mappés à **plusieurs** emplacements XDM.

| Champ Analytics | Champ XDM | Type XDM | Description |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | entier | Identifiant numérique représentant la résolution du moniteur. |
| mobileosversion | environnement.operatingSystem, environnement.operatingSystemVersion | chaîne | Version du système d’exploitation mobile. |
| videoadlength | advertising.adAssetReference._xmpDM.duration | entier | Longueur de la publicité vidéo. |

## Champs de mappage générés

Il est nécessaire de transformer certains champs provenant d’ADC, ce qui nécessite une logique au-delà d’une copie directe d’Adobe Analytics pour pouvoir les générer dans XDM.

Le tableau suivant comprend des colonnes qui indiquent le nom du champ Analytics (champ ** Analytics), le champ XDM correspondant (champ ** XDM) et son type (type ** XDM), ainsi qu’une description du champ (*Description).*

>[!NOTE] Veuillez faire défiler la page vers la gauche/vers la droite pour vue du contenu complet du tableau.

| Champ Analytics | Champ XDM | Type XDM | Description |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objet | Variables de trafic personnalisées, allant de 1 à 75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarchy.hier1 - _experience.analytics.customDimensions.hierarchy.hier5 | Objet | Utilisé par les variables de hiérarchie. Il contient un | liste délimitée de valeurs. | {values (array), delimiter (string)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.listes.liste1.liste[] - _experience.analytics.customDimensions.listes.liste3.liste[] | tableau | Liste des valeurs de variable. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation | {value (string), key (string)} |
| m_color | device.colorDepth | entier | ID de profondeur de couleur, qui est basé sur la valeur de la colonne c_color. |
| m_cookies | environment.browserDetails.cookiesEnabled | booléen | Variable utilisée dans la dimension Prise en charge des cookies. |
| m_événement_liste | commerce.achats, commerce.productViews, commerce.productListOuvert, commerce.checkouts, commerce.productListAdds, commerce.productListRemovals, commerce.productListViews | Objet | événements commerciaux standard déclenchés lors de l’accès. | {id (chaîne), valeur (nombre)} |
| m_événement_liste | _experience.analytics.événement1to100.événement1 - _experience.analytics.événement1to100.événement100, _experience.analytics.événement101to200.événement101 - _experience.analytics.événement101to20 0.événement200, _experience.analytics.événement201to300.événement201 - _experience.analytics.événement201to300.300, _experience.analytics.301to400.3 01 - _experience.analytics.301to400.400, _experience.analytics.401to500.401 - _experience.analytics.401to500.500, _experience .analytics.501to600.501 - _experience.analytics.501to600.600, _experience.analytics.601to700.601 - _experience.analytics. 601to700.700, _experience.analytics.701to800.701 - _experience.analytics.701to800.800, _experience.analytics.801to 900.801 - _experience.analytics.801to900.900, _experience.analytics.901to1000.901 - _experience.analytics.901to100 0.1000 | Objet | événements personnalisés déclenchés lors de l’accès. | {id (objet), value (objet)} |
| m_geo_country | placeContext.geo.countryCode | chaîne | Abréviation du pays d’où provient l’accès, qui est basée sur la période d’enquête. |
| m_geo_latitude | placeContext.geo._schéma.latitude | nombre | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._schéma.longitude | nombre | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | booléen | Indicateur précisant si Java est activé. |
| m_latitude | placeContext.geo._schéma.latitude | nombre | <!-- MISSING --> |
| m_longitude | placeContext.geo._schéma.longitude | nombre | <!-- MISSING --> |
| m_page_événement_var1 | web.webInteraction.URL | chaîne | Variable utilisée uniquement dans les demandes d’image de suivi de liens. Cette variable contient l’URL du lien de téléchargement, du lien de sortie ou du lien personnalisé sur lequel l’utilisateur a cliqué. |
| m_page_événement_var2 | web.webInteraction.name | chaîne | Variable utilisée uniquement dans les demandes d’image de suivi de liens. Cela liste le nom personnalisé du lien, s’il est spécifié. |
| m_page_type | web.webPageDetails.isErrorPage | booléen | Variable utilisée pour renseigner la dimension Pages introuvables. Cette variable doit être vide ou contenir &quot;ErrorPage&quot;. |
| m_pagename_no_url | web.webPageDetails.pageViews.value | nombre | Nom de la page (s’il est défini). Si aucune page n’est spécifiée, cette valeur reste vide. |
| m_paid_search | search.isPaid | booléen | Indicateur défini si l’accès correspond à la détection de la recherche payante. |
| m_product_liste | productListItems[].items | tableau | liste de produit, telle qu’elle est transmise par la variable products. | {SKU (chaîne), quantité (entier), prixTotal (nombre)} |
| m_ref_type | web.webReferrer.type | chaîne | Identifiant numérique représentant le type de référence pour l’accès. 1 signifie à l’intérieur de votre site, 2 signifie d’autres sites Web, 3 signifie moteurs de recherche, 4 signifie disque dur, 5 signifie USENET, 6 signifie Tapé/Marqué (pas de parrain), 7 signifie Courriel, 8 signifie Pas de JavaScript et 9 signifie Réseaux sociaux. |
| m_search_engine | search.searchEngine | chaîne | ID numérique représentant le moteur de recherche qui a renvoyé le visiteur sur votre site. |
| post_currency | commerce.order.currencyCode | chaîne | Code de devise utilisé pendant la transaction. |
| post_cust_hit_time_gmt | timestamp | chaîne | Il est utilisé uniquement dans les jeux de données horodatés. Il s’agit de l’horodatage envoyé avec l’horodatage, en fonction de l’heure Unix. |
| post_cust_visid | identityMap | objet | ID du visiteur client. |
| post_cust_visid | endUserIDs._experience.aacustomid.primary | booléen | ID du visiteur client. |
| post_cust_visid | endUserIDs._experience.aacustomid.espace de nommage.code | chaîne | ID du visiteur client. |
| post_visid_high + visid_low | identityMap | objet | Identificateur unique d’une visite. |
| post_visid_high + visid_low | endUserIDs._experience.aid.id | chaîne | Identificateur unique d’une visite. |
| post_visid_high | endUserIDs._experience.aid.primary | booléen | Utilisé conjointement avec visid_low pour identifier de manière unique une visite. |
| post_visid_high | endUserIDs._experience.aid.espace de nommage.code | chaîne | Utilisé conjointement avec visid_low pour identifier de manière unique une visite. |
| post_visid_low | identityMap | objet | Utilisé conjointement avec visid_high pour identifier de manière unique une visite. |
| hit_time_gmt | receiveTimestamp | chaîne | Horodatage de l’accès, selon l’heure Unix. |
| hitid_high + hitid_low | _id | chaîne | Identificateur unique permettant d’identifier un accès. |
| hitid_low | _id | chaîne | Utilisé conjointement avec hitid_high pour identifier de manière unique un accès. |
| ip | environment.ipV4 | chaîne | Adresse IP, basée sur l’en-tête HTTP de la demande d’image. |
| j_jscript | environment.browserDetails.javaScriptEnabled | booléen | Version de JavaScript utilisée. |
| mcvisid_high + mcvisid_low | identityMap | objet | ID de Visiteur Experience Cloud. |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | chaîne | ID de Visiteur Experience Cloud. |
| mcvisid_high | endUserIDs._experience.mcid.primary | booléen | ID de Visiteur Experience Cloud. |
| mcvisid_high | endUserIDs._experience.mcid.espace de nommage.code | chaîne | ID de Visiteur Experience Cloud. |
| mcvisid_low | identityMap | objet | ID de Visiteur Experience Cloud. |
| sdid_high + sdid_low | _experience.cible.supplementalDataID | chaîne | Identifiant d’assemblage d’accès. Le champ d’analyse sdid_high et sdid_low est l’identifiant de données supplémentaire utilisé pour associer deux (ou plusieurs) accès entrants. |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | chaîne | Proximité du relais Mobile Services. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | entier | Nom du chapitre vidéo. |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | entier | Durée de la vidéo. |

## Champs de mappage avancés

Certains champs (appelés &quot;postvaleurs&quot;) nécessitent des transformations plus avancées avant de pouvoir être mappés à partir des champs Adobe Analytics vers le modèle de données d’expérience (XDM). L’exécution de ces transformations avancées implique l’utilisation d’Adobe Experience Platfrom Requête Service et de fonctions prédéfinies (appelées fonctions définies par Adobe) pour la segmentation, l’attribution et la déduplication.

Pour en savoir plus sur l’exécution de ces transformations à l’aide de Requête Service, consultez la documentation relative aux fonctions [définies par](../../../../query-service/sql/adobe-defined-functions.md) Adobe.

Le tableau suivant comprend des colonnes qui indiquent le nom du champ Analytics (champ ** Analytics), le champ XDM correspondant (champ ** XDM) et son type (type ** XDM), ainsi qu’une description du champ (*Description).*

>[!NOTE] Veuillez faire défiler la page vers la gauche/vers la droite pour vue du contenu complet du tableau.

| Champ Analytics | Champ XDM | Type XDM | Description |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | chaîne | Variable personnalisée, qui peut être comprise entre 1 et 250. Chaque organisation utilisera ces eVars personnalisées différemment. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | chaîne | Variables de trafic personnalisées, qui peuvent varier de 1 à 75. |
| post_browser_height | environment.browserDetails.viewportHeight | entier | Hauteur du navigateur, en pixels. |
| post_browser_width | environment.browserDetails.viewportWidth | entier | Largeur du navigateur, en pixels. |
| post_campaign | marketing.trackingCode | chaîne | Variable utilisée dans la dimension Code de suivi. |
| post_canal | web.webPageDetails.siteSection | chaîne | Variable utilisée dans la dimension Sections du site. |
| post_cust_visid | endUserIDs._experience.aacustomid.id | chaîne | ID de visiteur personnalisé, s’il est défini. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | chaîne | URL de la première page atteinte par le visiteur. |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | chaîne | Variable utilisée dans la dimension Origine de la page d’entrée. Nom de la page d’entrée du visiteur. |
| post_keywords | search.keywords | chaîne | Mots-clés collectés pour l’accès. |
| post_page_url | web.webPageDetails.URL | chaîne | URL de l’accès à la page. |
| post_pagename_no_url | web.webPageDetails.name | chaîne | Variable utilisée pour renseigner la dimension Pages. |
| post_purchaseid | commerce.order.purchaseID | chaîne | Variable utilisée pour identifier de manière unique les achats. |
| post_parrain | web.webReferrer.URL | chaîne | URL de la page précédente. |
| post_state | _experience.analytics.customDimensions.stateProvince | chaîne | Variable d’état. |
| post_user_server | web.webPageDetails.server | chaîne | Variable utilisée dans la dimension Serveur. |
| post_zip | _experience.analytics.customDimensions.postalCode | chaîne | Variable utilisée pour remplir la dimension Code postal. |
| browser | _experience.analytics.environnement.browserID | entier | ID numérique du navigateur. |
| domain | environment.domain | chaîne | Variable utilisée dans la dimension Domaine. Il sera basé sur le prestataire Internet (FAI) de l&#39;utilisateur. |
| first_hit_parrain | _experience.analytics.endUser.firstWeb.webReferrer.URL | chaîne | Première URL de référence pour le visiteur. |
| geo_city | placeContext.geo.city | chaîne | Nom de la ville de l’accès. Il est basé sur l’adresse IP de l’accès. |
| geo_dma | placeContext.geo.dmaID | entier | ID numérique de la zone démographique de l’accès. Il est basé sur l’adresse IP de l’accès. |
| geo_region | placeContext.geo.stateProvince | chaîne | Nom de l’état ou de la région de l’accès. Il est basé sur l’adresse IP de l’accès. |
| geo_zip | placeContext.geo.postalCode | chaîne | Code postal de l’accès. Il est basé sur l’adresse IP de l’accès. |
| os | _experience.analytics.environnement.operatingSystemID | entier | ID numérique représentant le système d’exploitation du visiteur. Il est basé sur la colonne user_agent. |
| search_page_num | search.pageDepth | entier | Cette variable est utilisée par la dimension Classement de toutes les pages de recherche et indique la page de recherche qui génère les résultats de votre site. | s’affichait avant que l’utilisateur n’ait cliqué sur votre site. |
| visit_keywords | _experience.analytics.session.search.keywords | chaîne | Variable utilisée dans la dimension Mots-clés de recherche. |
| visit_num | _experience.analytics.session.num | entier | Variable utilisée dans la dimension Nombre de visites. Ce début est défini sur 1 et est incrémenté chaque fois qu’une nouvelle visite début (par utilisateur). |
| visit_page_num | _experience.analytics.session.depth | entier | Variable utilisée dans la dimension Profondeur d’accès. Cette valeur augmente de 1 pour chaque accès généré par l’utilisateur et est réinitialisée après chaque visite. |
| visit_parrain | _experience.analytics.session.web.webReferrer.URL | chaîne | Premier parrain de la visite. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | entier | Nom de la première page de la visite. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objet | Variables de trafic personnalisées 1 - 75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarchy.hier1 - _experience.analytics.customDimensions.hierarchy.hier5 | Objet | Utilisé par les variables de hiérarchie et contient une liste de valeurs délimitée. | {values (array), delimiter (string)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.listes.liste1.liste[] - _experience.analytics.customDimensions.listes.liste3.liste[] | tableau | liste de valeurs de variable. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. | {value (string), key (string)} |
| post_cookies | environment.browserDetails.cookiesEnabled | booléen | Variable utilisée dans la dimension Prise en charge des cookies. |
| post_événement_liste | commerce.achats, commerce.productViews, commerce.productListOuvert, commerce.checkouts, commerce.productListAdds, commerce.productListRemovals, commerce.productListViews | Objet | événements commerciaux standard déclenchés lors de l’accès. | {id (chaîne), valeur (nombre)} |
| post_événement_liste | _experience.analytics.événement1to100.événement1 - _experience.analytics.événement1to100.événement100, _experience.analytics.événement101to200.événement101 - _experience.analytics.événement101to20 0.événement200, _experience.analytics.événement201to300.événement201 - _experience.analytics.événement201to300.300, _experience.analytics.301to400.3 01 - _experience.analytics.301to400.400, _experience.analytics.401to500.401 - _experience.analytics.401to500.500, _experience .analytics.501to600.501 - _experience.analytics.501to600.600, _experience.analytics.601to700.601 - _experience.analytics. 601to700.700, _experience.analytics.701to800.701 - _experience.analytics.701to800.800, _experience.analytics.801to 900.801 - _experience.analytics.801to900.900, _experience.analytics.901to1000.901 - _experience.analytics.901to100 0.1000 | Objet | événements personnalisés déclenchés lors de l’accès. | {id (objet), value (objet)} |
| post_java_enabled | environment.browserDetails.javaEnabled | booléen | Indicateur précisant si Java est activé. |
| post_latitude | placeContext.geo._schéma.latitude | nombre | <!-- MISSING --> |
| post_longitude | placeContext.geo._schéma.longitude | nombre | <!-- MISSING --> |
| post_page_événement | web.webInteraction.type | chaîne | Type d’accès envoyé dans la demande d’image (accès standard, lien de téléchargement, lien de sortie ou lien personnalisé sur lequel l’utilisateur a cliqué). |
| post_page_événement | web.webInteraction.linkClicks.value | nombre | Type d’accès envoyé dans la demande d’image (accès standard, lien de téléchargement, lien de sortie ou lien personnalisé sur lequel l’utilisateur a cliqué). |
| post_page_événement_var1 | web.webInteraction.URL | chaîne | Cette variable n’est utilisée que dans les demandes d’image de suivi de liens. Il s’agit de l’URL du lien de téléchargement, du lien de sortie ou du lien personnalisé sur lequel l’utilisateur a cliqué. |
| post_page_événement_var2 | web.webInteraction.name | chaîne | Cette variable n’est utilisée que dans les demandes d’image de suivi de liens. Il s’agira du nom personnalisé du lien. |
| post_page_type | web.webPageDetails.isErrorPage | booléen | Elle est utilisée pour renseigner la dimension Pages introuvables. Cette variable doit être vide ou contenir &quot;ErrorPage&quot; |
| post_pagename_no_url | web.webPageDetails.pageViews.value | nombre | Nom de la page (s’il est défini). Si aucune page n’est spécifiée, cette valeur reste vide. |
| post_product_liste | productListItems[].items | tableau | liste de produit, telle qu’elle est transmise par la variable products. | {SKU (chaîne), quantité (entier), prixTotal (nombre)} |
| post_search_engine | search.searchEngine | chaîne | ID numérique représentant le moteur de recherche qui a renvoyé le visiteur sur votre site. |
| mvvar1_instances | .liste.items[] | Objet | Liste des valeurs de variable. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. |
| mvvar2_instances | .liste.items[] | Objet | Liste des valeurs de variable. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. |
|  | mvvar3_instances | .liste.items[] | Objet | Liste des valeurs de variable. Contient une liste délimitée de valeurs personnalisées, selon l’implémentation. |
| color | device.colorDepth | entier | ID de profondeur de couleur, en fonction de la valeur de la colonne c_color. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | chaîne | ID numérique représentant le type de parrain du tout premier parrain du visiteur. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | entier | Horodatage du tout premier accès du visiteur dans l’heure Unix. |
| geo_country | placeContext.geo.countryCode | chaîne | Abréviation du pays d’où provient l’accès, en fonction de l’adresse IP. |
| geo_latitude | placeContext.geo._schéma.latitude | nombre | <!-- MISSING --> |
| geo_longitude | placeContext.geo._schéma.longitude | nombre | <!-- MISSING --> |
| paid_search | search.isPaid | booléen | Indicateur défini si l’accès correspond à la détection de la recherche payante. |
| ref_type | web.webReferrer.type | chaîne | Identifiant numérique représentant le type de référence pour l’accès. |
| visit_paid_search | _experience.analytics.session.search.isPaid | booléen | Indicateur (1=payé, 0=non payé) indiquant si le premier accès de la visite provient d’un accès à la recherche payée. |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | chaîne | Identifiant numérique représentant le type de parrain du premier parrain de la visite. |
| visit_search_engine | _experience.analytics.session.search.search.searchEngine | chaîne | Identifiant numérique du premier moteur de recherche de la visite. |
| visit_début_time_gmt | _experience.analytics.session.timestamp | entier | Horodatage du premier accès de la visite à l’heure Unix. |
