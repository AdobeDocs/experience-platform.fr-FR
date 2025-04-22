---
title: Champs de mappage pour le connecteur Source Adobe Analytics
description: Mappez les champs Adobe Analytics aux champs XDM à l’aide du connecteur Source Analytics.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 316879afe8c94657156c768cdc14d4710da9fd35
workflow-type: tm+mt
source-wordcount: '3914'
ht-degree: 25%

---

# Mappages de champs Analytics

Adobe Experience Platform vous permet d’ingérer des données Adobe Analytics par le biais de la source Analytics. Certaines des données ingérées par l’intermédiaire d’ADC peuvent être mappées directement des champs Analytics aux champs du modèle de données d’expérience (XDM), tandis que d’autres données nécessitent des transformations et des fonctions spécifiques pour être mappées avec succès.

![Illustration du parcours de données Adobe Analytics d’Analytics vers Experience Platform.](../images/analytics-data-experience-platform.png)

## Paramètres des médias en flux continu

Lisez le tableau suivant pour plus d’informations sur les paramètres des médias en flux continu.

| Flux de données | Chemin d’accès au champ XDM | Type de données | Description |
| --- | --- | --- | --- |
| `videoname` | `mediaReporting.sessionDetails.friendlyName` | chaîne | Nom convivial (lisible par l’utilisateur) de la vidéo. |
| `videoaudioauthor` | `mediaReporting.sessionDetails.author` | Chaîne | Nom de l’auteur du média. |
| `videoaudioartist` | `mediaReporting.sessionDetails.artist` | Chaîne | Nom de l’artiste ou du groupe qui effectue l’enregistrement musical ou la vidéo. |
| `videoaudioalbum` | `mediaReporting.sessionDetails.album` | Chaîne | Nom de l’album auquel appartient la vidéo ou l’enregistrement musical. |
| `videolength` | `mediaReporting.sessionDetails.length ` | Entier | Durée d’exécution de la vidéo. |
| `videoshowtype` | `mediaReporting.sessionDetails.showType` | chaîne |
| `video` | `mediaReporting.sessionDetails.name` | chaîne | Identifiant de la vidéo. |
| `videoshow` | `mediaReporting.sessionDetails.show` | Chaîne | Nom du programme ou de la série. Le nom du programme ou de la série n’est requis que si l’émission fait partie d’une série. |
| `videostreamtype` | mediaReporting.sessionDetails.streamType | Chaîne | Type de média en flux continu tel que « vidéo » ou « audio ». |
| `videoseason` | `mediaReporting.sessionDetails.season` | Chaîne | Numéro de la saison à laquelle appartient l’émission. Cette valeur n’est nécessaire que si l’émission fait partie d’une série. |
| `videoepisode` | `mediaReporting.sessionDetails.episode` | Chaîne | Numéro de l’épisode. |
| `videogenre` | `mediaReporting.sessionDetails.genreList[]` | chaîne[] | Genre de la vidéo. |
| `videosessionid` | `mediaReporting.sessionDetails.ID` | Chaîne | Identifiant d’une instance d’un flux de contenu spécifique à une lecture. |
| `videoplayername` | `mediaReporting.sessionDetails.playerName ` | Chaîne | Nom du lecteur vidéo. |
| `videochannel` | `mediaReporting.sessionDetails.channel` | Chaîne | Canal de distribution à partir duquel le contenu a été lu. |
| `videocontenttype` | `mediaReporting.sessionDetails.contentType` | Chaîne | Type de diffusion de flux utilisé pour le contenu. Cette valeur est automatiquement définie sur « Vidéo » pour toutes les vues vidéo. Les valeurs recommandées sont les suivantes : VOD, Live, Linear, UGC, DVOD, Radio, Podcast, Audiobook et Song. |
| `videonetwork` | `mediaReporting.sessionDetails.network` | Chaîne | Nom du réseau ou du canal. |
| `videofeedtype` | `mediaReporting.sessionDetails.feed` | Chaîne | Type de flux. Cela peut représenter les données réelles liées au flux, telles que « East HD » ou « SD », ou la source du flux, telle qu’une URL. |
| `videosegment` | `mediaReporting.sessionDetails.segment` | Chaîne |
| `videostart` | `mediaReporting.sessionDetails.isViewed` | Booléen | Valeur booléenne qui indique si la vidéo a été démarrée ou non. Cela se produit une fois que l’utilisateur sélectionne le bouton de lecture et sera comptabilisé même s’il existe des publicités preroll, une mise en mémoire tampon, des erreurs, etc. |
| `videoplay` | `mediaReporting.sessionDetails.isPlayed` | Booléen | Valeur booléenne qui indique si la première image du média a commencé. Si l’utilisateur ou l’utilisatrice abandonne au cours d’une publicité ou d’une période de mise en mémoire tampon, le « début du contenu » ne sera pas admissible. |
| `videotime` | `mediaReporting.sessionDetails.timePlayed` | Entier | Durée (en secondes) de tous les événements de `type=PLAY` sur le contenu principal. |
| `videocomplete` | `mediaReporting.sessionDetails.isCompleted` | Booléen | Valeur booléenne qui indique si une ressource de média horodatée a été visionnée jusqu’à la fin. Cette valeur ne signifie pas nécessairement que le spectateur a visionné l’intégralité de la vidéo, car elle ne prend pas en compte le fait qu’il peut éventuellement avancer dans cette étape. |
| `videototaltime` | `mediaReporting.sessionDetails.totalTimePlayed` | Entier | Temps total passé par un utilisateur sur une ressource de média horodatée spécifique, y compris le temps passé à regarder des publicités. |
| `videouniquetimeplayed` | `mediaReporting.sessionDetails.uniqueTimePlayed` | Entier | Somme des intervalles uniques affichés par un utilisateur sur une ressource de média horodatée. En d’autres termes, la durée des intervalles de lecture visionnés plusieurs fois n’est comptabilisée qu’une seule fois. |
| `videoaverageminuteaudience` | `mediaReporting.sessionDetails.averageMinuteAudience` | nombre | Temps moyen passé sur le contenu pour un élément de média spécifique. En d’autres termes, le temps de contenu total divisé par la durée de toutes les sessions de lecture. |
| `videoprogress10` | `mediaReporting.sessionDetails.hasProgress10` | Booléen | Valeur booléenne qui indique si le curseur de lecture d’une vidéo donnée a dépassé le marqueur de 10 % de la durée totale de la vidéo. Le marqueur n’est comptabilisé qu’une seule fois, même si la recherche est effectuée à rebours. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés. |
| `videoprogress25` | `mediaReporting.sessionDetails.hasProgress25` | Booléen | Valeur booléenne qui indique si le curseur de lecture d’une vidéo donnée a dépassé le marqueur de 25 % de la durée totale de la vidéo. Le marqueur n’est comptabilisé qu’une seule fois, même si la recherche est effectuée à rebours. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés. |
| `videoprogress50` | `mediaReporting.sessionDetails.hasProgress50` | Booléen | Valeur booléenne qui indique si le curseur de lecture d’une vidéo donnée a dépassé le marqueur de 50 % de la durée totale de la vidéo. Le marqueur n’est comptabilisé qu’une seule fois, même si la recherche est effectuée à rebours. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés. |
| `videoprogress75` | `mediaReporting.sessionDetails.hasProgress75` | Booléen | Valeur booléenne qui indique si le curseur de lecture d’une vidéo donnée a dépassé le marqueur de 75 % de la durée totale de la vidéo. Le marqueur n’est comptabilisé qu’une seule fois, même si la recherche est effectuée à rebours. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés. |
| `videoprogress95` | `mediaReporting.sessionDetails.hasProgress95` | Booléen | Valeur booléenne qui indique si le curseur de lecture d’une vidéo donnée a dépassé le marqueur de 95 % de la durée totale de la vidéo. Le marqueur n’est comptabilisé qu’une seule fois, même si la recherche est effectuée à rebours. Si vous effectuez une recherche vers l’avant, les marqueurs ignorés ne sont pas comptabilisés. |
| `videopause` | `mediaReporting.sessionDetails.hasPauseImpactedStreams` | Booléen | Valeur booléenne qui indique si une ou plusieurs pauses se sont produites au cours de la lecture d’un seul élément de média. |
| `videopausecount` | `mediaReporting.sessionDetails.pauseCount` | Entier | Nombre de périodes de mise en pause survenues pendant la lecture. |
| `videopausetime` | `mediaReporting.sessionDetails.pauseTime` | Entier | Durée totale (en secondes) pendant laquelle la lecture a été mise en pause par un utilisateur. |
| `videomvpd` | `mediaReporting.sessionDetails.mvpd` | Chaîne | Identifiant MVPD fourni via l’authentification Adobe. |
| `videoauthorized` | `mediaReporting.sessionDetails.authorized` | Chaîne | Définit que l&#39;utilisateur a été autorisé via l&#39;authentification Adobe. |
| `videodaypart` | `mediaReporting.sessionDetails.dayPart` | Définit l’heure de diffusion ou de lecture du contenu. |
| `videoresume` | `mediaReporting.sessionDetails.hasResume` | Booléen | Valeur booléenne qui marque chaque lecture qui a été reprise après plus de 30 minutes de mise en mémoire tampon, de pause ou de période de blocage. |
| `videosegmentviews` | `mediaReporting.sessionDetails.hasSegmentView` | Booléen | Valeur booléenne qui indique qu’au moins une image a été vue. Cette image n’a pas besoin d’être la première. |
| `videoaudiolabel` | `mediaReporting.sessionDetails.label` | Chaîne | Nom de la maison de disques. |
| `videoaudiostation` | `mediaReporting.sessionDetails.station` | Chaîne | Station radio ou nom sur lequel l’audio est lu. |
| `videoaudiopublisher` | `mediaReporting.sessionDetails.publisher` | Chaîne | Nom de l’éditeur du contenu audio. |
| `videosecondssincelastcall` | `mediaReporting.sessionDetails.secondsSinceLastCall` | nombre | Indique le temps écoulé (en secondes) entre la dernière interaction connue d’un utilisateur et le moment où la session a été fermée. |
| `videoadload` | `mediaReporting.sessionDetails.adLoad` | Chaîne | Type d’annonce publicitaire chargé, tel que défini par votre propre représentation interne. |

{style="table-layout:auto"}

## Paramètres d’Advertising

Lisez le tableau suivant pour plus d&#39;informations sur les paramètres publicitaires.

| Flux de données | Chemin d’accès au champ XDM | Type de données | Description |
| --- | --- | --- | --- |
| `videoad` | `mediaReporting.advertisingDetails.name` | chaîne | Nom de la publicité. Dans les rapports, « Nom de la publicité » est la classification et « Nom de la publicité (variable) » est l’eVar. |
| `videoadinpod` | `mediaReporting.advertisingDetails.podPosition` | Entier | Index de l’annonce publicitaire à l’intérieur du début de l’annonce publicitaire parent. Par exemple, la première publicité a l&#39;index 0 et la seconde l&#39;index 1. |
| `videoadlength` | `mediaReporting.advertisingDetails.length` | Entier | Durée de la publicité vidéo, exprimée en secondes. |
| `videoadplayername` | `mediaReporting.advertisingDetails.playerName` | Chaîne | Nom du lecteur utilisé pour effectuer le rendu de la publicité. |
| `videoadpod` | `mediaReporting.advertisingPodDetails.ID` | Chaîne | Identifiant de la coupure publicitaire. |
| `videoadname` | `mediaReporting.advertisingDetails.friendlyName` | Chaîne | Nom convivial (lisible par l’utilisateur) de la coupure publicitaire. |
| `videoadadvertiser` | `mediaReporting.advertisingDetails.advertiser` | Chaîne | Société ou marque dont le produit apparaît dans la publicité. |
| `videoadcampaign` | `mediaReporting.advertisingDetails.campaignID` | Chaîne | Identifiant de la campagne publicitaire. |
| `videoadstart` | `mediaReporting.advertisingDetails.isStarted` | Booléen | Valeur booléenne qui indique si la publicité a été lancée ou non. |
| `videoadcomplete` | `mediaReporting.advertisingDetails.isCompleted` | Booléen | Valeur booléenne qui indique si la tâche avait été terminée ou non. |
| `videoadtime` | `mediaReporting.advertisingDetails.timePlayed` | Entier | Durée totale (en secondes) passée à regarder la publicité. |

{style="table-layout:auto"}

## Paramètres du chapitre

Lisez le tableau suivant pour plus d’informations sur les paramètres de chapitre.

| Flux de données | Chemin d’accès au champ XDM | Type de données | Description |
| --- | --- | --- | --- |
| `videochapter` | `mediaReporting.chapterDetails.ID` | chaîne | Identifiant généré automatiquement pour le chapitre. |
| `videochapterstart` | `mediaReporting.chapterDetails.isStarted` | Booléen | Valeur booléenne qui indique si le chapitre a été démarré ou non. |
| `videochaptercomplete` | `mediaReporting.chapterDetails.isCompleted` | Booléen | Valeur booléenne qui indique si le chapitre est terminé ou non. |
| `videochaptertime` | `mediaReporting.chapterDetails.timePlayed` | Entier | Temps, exprimé en secondes, passé sur le chapitre. |

{style="table-layout:auto"}

## Paramètres d’état du lecteur

Lisez le tableau suivant pour plus d’informations sur les paramètres d’état du lecteur.

| Flux de données | Chemin d’accès au champ XDM | Type de données | Description |
| --- | --- | --- | --- |
| `videostatefullscreen` | `mediaReporting.states[].isSet` | Booléen | Valeur booléenne qui indique si l’état vidéo est défini ou non sur Plein écran. |
| `videostatefullscreencount` | `mediaReporting.states[].count` | Entier | Nombre de fois qu’un état vidéo a été défini sur Plein écran. |
| `videostatefullscreentime` | `mediaReporting.states[].time` | Entier | Durée totale pendant laquelle l’état vidéo a été défini sur Plein écran. |
| `videostateclosedcaptioning` | `mediaReporting.states[].isSet` | Booléen | Valeur booléenne qui indique si le sous-titrage est activé ou non. |
| `videostateclosedcaptioningcount` | `mediaReporting.states[].count` | Entier | Nombre d’activations du sous-titrage. |
| `videostateclosedcaptioningtime` | `mediaReporting.states[].time` | Entier | Durée totale pendant laquelle le sous-titrage a été activé. |
| `videostatemute` | `mediaReporting.states[].isSet` | Booléen | Valeur booléenne qui indique si l’état de la vidéo a été défini sur muet ou non. |
| `videostatemutecount` | `mediaReporting.states[].count` | Entier | Nombre de fois où une vidéo a été désactivée. |
| `videostatemutetime` | `mediaReporting.states[].time` | Entier | Durée totale de la vidéo mise en sourdine. |
| `videostatepictureinpicture` | `mediaReporting.states[].isSet` | Booléen | Valeur booléenne qui indique si le mode image dans image est activé ou non. |
| `videostatepictureinpicturecount` | `mediaReporting.states[].count` | Entier | Nombre d’activations du mode image dans image. |
| `videostatepictureinpicturetime` | `mediaReporting.states[].time` | Entier | Durée totale pendant laquelle le mode image dans image a été activé. |
| `videostateinfocus` | `mediaReporting.states[].isSet` | Booléen | Valeur booléenne qui indique si le mode actif est activé ou non |
| `videostateinfocuscount` | `mediaReporting.states[].count` | Entier | Nombre d’activations du mode Image. |
| `videostateinfocustime` | `mediaReporting.states[].time` | Entier | Durée totale pendant laquelle le mode ciblé a été activé. |

{style="table-layout:auto"}

## Paramètres de qualité

Lisez le tableau suivant pour plus d&#39;informations sur les paramètres de qualité.

| Flux de données | Chemin d’accès au champ XDM | Type de données | Description |
| --- | --- | --- | --- |
| `videoqoebitrateaverage` | `mediaReporting.qoeDataDetails.bitrateAverage` | nombre | Débit moyen (en Kbits/s, entier). Cette mesure est calculée sous la forme d’une moyenne pondérée de toutes les valeurs de débit liées à la durée de lecture au cours d’une session de lecture. |
| `videoqoebitratechange` | `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | Booléen | Valeur booléenne qui indique le nombre de flux dans lesquels des changements de débit se sont produits. Cette mesure n’est définie sur « true » que si au moins un événement de changement de débit s’est produit au cours d’une session de lecture. |
| `videoqoebitratechangecountevar` | `mediaReporting.qoeDataDetails.bitrateChangeCount` | Entier |
| `videoqoebitrateaverageevar` | `mediaReporting.qoeDataDetails.bitrateAverageBucket` | Chaîne | Nombre de modifications du débit. Cette valeur est calculée comme la somme de tous les événements de changement de débit qui se sont produits au cours d’une session de lecture. |
| `videoqoetimetostartevar` | `mediaReporting.qoeDataDetails.timeToStart` | Entier | Durée, exprimée en secondes, écoulée entre le chargement et le démarrage de la vidéo. |
| `videoqoedroppedframes` | `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | Booléen | Valeur booléenne qui indique le nombre de flux dans lesquels des images ont été perdues. Cette mesure n’est définie sur « true » que si au moins une image a été supprimée au cours d’une session de lecture. |
| `videoqoedroppedframecountevar` | `mediaReporting.qoeDataDetails.droppedFrames` | Entier | Nombre d’images ignorées pendant la lecture du contenu principal. |
| `videoqoebuffercountevar` | `mediaReporting.qoeDataDetails.bufferCount` | Entier | Nombre d’événements de mémoire tampon. Cette mesure est calculée comme un décompte des différents états de mémoire tampon qui se sont produits au cours d’une session de lecture. Il s’agit du nombre de fois où le lecteur entre dans un état de mémoire tampon à partir d’autres états, tels que la lecture ou la mise en pause. |
| `videoqoebuffertimeevar` | `mediaReporting.qoeDataDetails.bufferTime` | Entier | Durée totale (en secondes) passée à mettre en mémoire tampon. Cette valeur correspond à la durée totale de tous les événements de mémoire tampon qui se sont produits au cours d’une session de lecture. |
| `videoqoebuffer` | `mediaReporting.qoeDataDetails.hasBufferImpactedStreams` | Booléen | Valeur booléenne qui indique le nombre de flux impactés par la mise en mémoire tampon. Cette mesure n’est définie sur « true » que si au moins un événement de mémoire tampon s’est produit au cours d’une session de lecture. |
| `videoqoeerror` | `mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | Booléen | Valeur booléenne qui indique le nombre de flux dans lesquels un événement d’erreur s’est produit. Par exemple, si un trackError a été appelé pendant la session de lecture et qu’un appel de pulsation type=error a été généré. Cette mesure n’est définie sur « true » que si au moins une erreur s’est produite lors de la lecture. |
| `videoerrorcountevar` | `mediaReporting.qoeDataDetails.errorCount` | Entier | Nombre d’erreurs qui se sont produites. Cette valeur est calculée comme la somme de tous les événements d’erreur qui se sont produits au cours d’une session de lecture. |
| `videoqoeplayersdkerrors` | `mediaReporting.qoeDataDetails.playerSdkErrors` | tableau de chaînes | ID d’erreur uniques générés par le SDK du lecteur. Vous devez fournir les codes d’erreur ou les identifiants au moment de l’implémentation via les API d’erreur fournies. |
| `videoqoeextneralerrors` | `mediaReporting.qoeDataDetails.externalErrors` | tableau de chaînes | ID d’erreur uniques provenant de toute source externe, tels que les erreurs CDN. Vous devez fournir les codes d’erreur ou les identifiants au moment de l’implémentation via les API d’erreur fournies. |
| `videoqoedropbeforestart` | `mediaReporting.qoeDataDetails.isDroppedBeforeStart` | Booléen | ID d’erreur uniques générés par Media SDK lors de la lecture. |

{style="table-layout:auto"}

## Champs obsolètes

Lisez cette section pour plus d’informations sur les champs de mappage Analytics obsolètes.

### Champs de mappage direct

+++Sélectionner pour afficher un tableau des champs de mappage direct obsolètes

| Flux de données | Champ XDM | Type XDM | Description |
| --- | --- | --- | --- |
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
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | string | |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | nombre | Relais Mobile Services majeur. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | nombre | Relais Mobile Services mineur. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | chaîne | UUID du relais Mobile Services. |
| `mobileinstalls` | `application.firstLaunches` | Objet | Il est déclenché lors de la première exécution suivant l’installation ou la réinstallation | {id (string), value (number)} |
| `mobileupgrades` | `application.upgrades` | objet | Indique le nombre de mises à niveau d’application. Se déclenche lors de la première exécution après mise à niveau ou dès que le numéro de version change. | {id (string), value (number)} |
| `mobilelaunches` | `application.launches` | objet | Nombre de fois où l’application a été lancée. | {id (string), value (number)} |
| `mobilecrashes` | `application.crashes` | objet |  | {id (string), value (number)} |
| `mobilemessageclicks` | `directMarketing.clicks` | objet |  | {id (string), value (number)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | objet | | {id (string), value (number)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | objet | | {id (string), value (number)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | objet | Temps jusqu’au début de la qualité vidéo. | {id (string), value (number)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | objet | | {id (string), value (number)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | objet | Nombre de mémoires tampons de la qualité vidéo. | {id (string), value (number)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | objet | Période tampon de la qualité vidéo. | {id (string), value (number)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | objet | Nombre de changements de la qualité vidéo. | {id (string), value (number)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | objet | Débit moyen de la qualité vidéo. | {id (string), value (number)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | objet | Nombre d’erreurs de la qualité vidéo. | {id (string), value (number)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | objet | | {id (string), value (number)} |

{style="table-layout:auto"}

+++

## Champs de mappage générés

Certains champs provenant d’ADC doivent être transformés, ce qui nécessite la génération d’une logique au-delà d’une copie directe d’Adobe Analytics dans XDM.

+++Sélectionner pour afficher un tableau des champs de mappage générés obsolètes

| Flux de données | Champ XDM | Type XDM | Description |
| --- | --- | --- | --- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objet | Props Analytics personnalisées, configurées pour être des props de liste. Il contient une liste délimitée de valeurs. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | objet | Utilisé par les variables de hiérarchie. Il contient une liste délimitée de valeurs. | {values (array), delimiter (string)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | tableau | Variables de liste Analytics personnalisées. Contient une liste délimitée de valeurs. | {value (string), key (string)} |
| `m_color` | `device.colorDepth` | Entier | Identifiant de profondeur de couleur, qui est basé sur la valeur de la colonne c_color. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | booléen | Variable utilisée dans la dimension Prise en charge des cookies. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | objet | Événements de commerce standard déclenchés à l’accès. | {id (string), value (number)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | objet | Événements personnalisés déclenchés à l’accès. | {id (Object), value (Object)} |
| `m_geo_country` | `placeContext.geo.countryCode` | Chaîne | Abréviation du pays d’où provient l’accès, basé sur l’adresse IP. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | nombre | |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | nombre | |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | Booléen | Indicateur qui signale si Java™ est activé. |
| `m_latitude` | `placeContext.geo._schema.latitude` | nombre | |
| `m_longitude` | `placeContext.geo._schema.longitude` | nombre | |
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

{style="table-layout:auto"}

+++

## Champs de mappage partagé

Ces champs ont une source unique, mais ils sont mappés à **plusieurs** emplacements XDM.

+++Sélectionner pour afficher un tableau des champs de mappage de partage obsolètes

| Flux de données | Champ XDM | Type XDM | Description |
| --- | --- | --- | --- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | entier | Identifiant numérique représentant la résolution du moniteur. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | chaîne | Version du système d’exploitation mobile. |

{style="table-layout:auto"}

+++

## Champs de mappage avancé

Certains champs (appelés « valeurs de publication ») contiennent des données après l’ajustement de leurs valeurs par Adobe à l’aide des règles de traitement, des règles VISTA et des tables de recherche. La plupart des valeurs post ont un équivalent prétraité.

Le connecteur source Analytics envoie des données prétraitées dans un jeu de données dans Experience Platform. Vous pouvez transformer ces données en données correspondantes post-traitées à l’aide de transformations. Pour en savoir plus sur l’exécution de ces transformations à l’aide de Query Service, consultez [Fonctions définies par Adobe](/help/query-service/sql/adobe-defined-functions.md) dans le guide d’utilisation de Query Service.

Pour en savoir plus sur l’exécution de ces transformations à l’aide de Query Service, consultez [Fonctions définies par Adobe](/help/query-service/sql/adobe-defined-functions.md) dans le guide d’utilisation de Query Service.

+++Sélectionner pour afficher un tableau des champs de mappage avancés obsolètes

| Flux de données | Champ XDM | Type XDM | Description |
| — | — | — | — ||
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | chaîne | eVars d’analyse personnalisées. Chaque organisation peut utiliser des eVars différemment. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | chaîne | Props Analytics personnalisées. Chaque organisation peut utiliser des props différemment. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | nombre entier | Hauteur du navigateur, en pixels. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | nombre entier | Largeur du navigateur, en pixels. |
| `post_campaign` | `marketing.trackingCode` | chaîne | Variable utilisée dans la dimension Code de suivi . |
| `post_channel` | `web.webPageDetails.siteSection` | chaîne | Variable utilisée dans la dimension Sections du site . |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | chaîne | Identifiant visiteur personnalisé, le cas échéant. |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | chaîne | URL de la première page atteinte par le visiteur. |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | chaîne | Variable utilisée dans la dimension d’origine Page d’entrée. Nom de la page d’entrée du visiteur. |
| `post_keywords` | `search.keywords` | chaîne | Mots-clés collectés pour l’accès. |
| `post_page_url` | `web.webPageDetails.URL` | chaîne | URL de l’accès à la page. |
| `post_pagename` | `web.webPageDetails.pageViews.value` | chaîne | Est égal à 1 sur les accès ayant un nom de page. Ceci est similaire à la mesure Pages vues d’Adobe Analytics. |
| `post_purchaseid` | `commerce.order.purchaseID` | chaîne | Variable utilisée pour identifier les achats de manière unique. |
| `post_referrer` | `web.webReferrer.URL` | chaîne | URL de la page précédente. |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | chaîne |  Variable d’état. |
| `post_user_server` | `web.webPageDetails.server` | chaîne | Variable utilisée dans la dimension Serveur . |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | chaîne | Variable utilisée pour renseigner la dimension Code postal . |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | nombre entier | Identifiant numérique du navigateur. |
| `domain` | `environment.domain` | chaîne | Variable utilisée dans la dimension Domaine . Il est basé sur le fournisseur de services Internet (FAI) de l’utilisateur. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | chaîne | Première URL de référence pour le visiteur. |
| `geo_city` | `placeContext.geo.city` | chaîne | Nom de la ville de l’accès. Il est basé sur l’adresse IP de l’accès. |
| `geo_dma` | `placeContext.geo.dmaID` | nombre entier | Identifiant numérique de la zone démographique de l’accès. Il est basé sur l’adresse IP de l’accès. |
| `geo_region` | `placeContext.geo.stateProvince` | chaîne | Nom de l’état ou de la région de l’accès. Il est basé sur l’adresse IP de l’accès. |
| `geo_zip` | `placeContext.geo.postalCode` | chaîne | Code postal de l’accès. Il est basé sur l’adresse IP de l’accès. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | nombre entier | Identifiant numérique représentant le système d’exploitation du visiteur. Celui-ci est basé sur la colonne user_agent . |
| `search_page_num` | `search.pageDepth` | nombre entier | Cette variable est utilisée par la dimension Classement de toutes les pages de recherche et indique la page de résultats de recherche de votre site | est apparu sur avant que l’utilisateur ne clique sur votre site. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | chaîne | Variable utilisée dans la dimension Mots-clés de recherche . |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | nombre entier | Variable utilisée dans la dimension Nombre de visites . Cette opération commence à 1 et est incrémentée à chaque nouveau démarrage de visite (par utilisateur). |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | nombre entier | Variable utilisée dans la dimension Profondeur d’accès . Cette valeur augmente de 1 pour chaque accès généré par l’utilisateur et réinitialisé après chaque visite. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | chaîne | Premier référent de la visite. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | nombre entier | Premier nom de page de la visite. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objet | Props Analytics personnalisées, configurées pour être des props de liste. Il contient une liste délimitée de valeurs. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objet | Utilisé par des variables de hiérarchie et contenant une liste délimitée de valeurs. | {values (tableau), délimiteur (chaîne)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | tableau | Liste de valeurs de variable. Contient une liste délimitée de valeurs personnalisées, en fonction de l’implémentation. | {value (chaîne), key (chaîne)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | booléen | Variable utilisée dans la dimension Prise en charge des cookies . |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objet | Événements commerciaux standard déclenchés lors de l’accès. | {id (chaîne), valeur (nombre)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objet | Événements personnalisés déclenchés lors de l’accès.| {id (objet), value (objet)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | booléen | Indicateur qui signale si Java™ est activé. |
| `post_latitude` | `placeContext.geo._schema.latitude` | nombre |   |
| `post_longitude` | `placeContext.geo._schema.longitude` | nombre |   |
| `post_page_event` | `web.webInteraction.type` | chaîne | Type d’accès envoyé dans la demande d’image (accès standard, lien de téléchargement, lien de sortie ou lien personnalisé sur lequel l’utilisateur a cliqué). |
| `post_page_event` | `web.webInteraction.linkClicks.value` | nombre | Est égal à 1 si l’accès est un clic sur un lien. Ceci est similaire à la mesure Événements de page dans Adobe Analytics. |
| `post_page_event_var1` | `web.webInteraction.URL` | chaîne | Cette variable n’est utilisée que dans les demandes d’image de suivi de liens. Il s’agit de l’URL du lien de téléchargement, du lien de sortie ou du lien personnalisé sur lequel l’utilisateur a cliqué. |
| `post_page_event_var2` | `web.webInteraction.name` | chaîne | Cette variable n’est utilisée que dans les demandes d’image de suivi de liens. Il s’agit du nom personnalisé du lien. |
| `post_page_type` | `web.webPageDetails.isErrorPage` | booléen | Permet de renseigner la dimension Pages introuvables . Cette variable doit être vide ou contenir « ErrorPage » |
| `post_pagename_no_url` | `web.webPageDetails.name` | nombre | Nom de la page (si défini). Si aucune page n’est spécifiée, cette valeur reste vide. |
| `post_product_list` | `productListItems[].items` | tableau | La liste des produits, transmise par le biais de la variable products. | {SKU (chaîne), quantité (entier), priceTotal (nombre)} |
| `post_search_engine` | `search.searchEngine` | chaîne | Identifiant numérique représentant le moteur de recherche qui a orienté le visiteur vers votre site. |
| `mvvar1_instances` | `.list.items[]` | Objet | Liste des valeurs de variable. Contient une liste délimitée de valeurs personnalisées, en fonction de l’implémentation. |
| `mvvar2_instances` | `.list.items[]` | Objet | Liste des valeurs de variable. Contient une liste délimitée de valeurs personnalisées, en fonction de l’implémentation. |
| `mvvar3_instances` | `.list.items[]` | Objet | Liste des valeurs de variable. Contient une liste délimitée de valeurs personnalisées, en fonction de l’implémentation. |
| `color` | `device.colorDepth` | nombre entier | Identifiant de profondeur de couleur, en fonction de la valeur de la colonne c_color. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | chaîne | Identifiant numérique, représentant le type de référent du premier référent du visiteur. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | nombre entier | Horodatage du premier accès du visiteur en temps UNIX®. |
| `geo_country` | `placeContext.geo.countryCode` | chaîne | Abréviation du pays d’où provient l’accès, basé sur l’adresse IP. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | nombre |  |
| `geo_longitude` | `placeContext.geo._schema.longitude` | nombre |  |
| `paid_search` | `search.isPaid` | booléen | Indicateur défini si l’accès correspond à la détection de référencement payant. |
| `ref_type` | `web.webReferrer.type` | chaîne | Identifiant numérique représentant le type de référence de l’accès. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | booléen | Indicateur (1 = payé, 0 = non payé) indiquant si le premier accès de la visite provenait d’un accès de référencement payant. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | chaîne | Identifiant numérique représentant le type de référent du premier référent de la visite. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | chaîne | Identifiant numérique du premier moteur de recherche de la visite. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | nombre entier | Date et heure du premier accès de la visite à l’heure UNIX®. |

+++