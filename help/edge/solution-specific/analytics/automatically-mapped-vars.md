---
title: Variables mappées automatiquement dans Analytics
seo-title: Variables mappées automatiquement dans Analytics avec le SDK Web de la plate-forme Adobe Experience Platform
description: Découvrez quelles variables sont automatiquement mappées dans Analytics avec le SDK Web de la plateforme d’expérience
seo-description: Découvrez quelles variables sont automatiquement mappées dans Analytics avec le SDK Web de la plateforme d’expérience
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bêta) Variables mappées automatiquement dans Analytics

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Vous trouverez ci-dessous un de variables que le réseau Edge d’Adobe Experience Platform associe automatiquement à Analytics.

| Chemin du champ XDM | Chaîne de  Analytics / En-tête HTTP | Description |
| ---------- | ------------------------- | -------- |
| `environment.browserDetails.userAgent` | `User-Agent` | Il s’agit d’un mappage d’en-tête HTTP, HEADER_USER_AGENT. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Il s’agit d’un mappage d’en-tête HTTP, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | Le paramètre AppMeasurement  le paramètre COOKIES avec la conversion BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | Mappage du paramètre  AppMeasurement pour J_JSCRIPT. |
| `environment.browserDetails.javaEnabled` | `v` | Mappage JAVA_ENABLED du paramètre du AppMeasurement avec la conversion BOOLEAN_TO_YN. |
| `environment.browserDetails.viewportHeight` | `bh` | Mappage du paramètre AppMeasurement BROWSER_HEIGHT. |
| `environment.browserDetails.viewportWidth` | `bw` | Mappage du paramètre AppMeasurement BROWSER_WIDTH. |
| `environment.connectionType` | `ct` | Mappage du paramètre de AppMeasurement CT_CONNECT_TYPE. |
| `device.colorDepth` | `c` | Mappage du paramètre C_COLOR du AppMeasurement. |
| `placeContext.geo.stateProvince` | `state` | Mappage de l’état du paramètre AppMeasurement  le paramètre AppMeasurement. |
| `placeContext.geo.postalCode` | `zip` | Mappage du paramètre ZIP du AppMeasurement. |
| `placeContext.geo.latitude` | `lat` | Mise en correspondance du paramètre de AppMeasurement avec LATITUDE. |
| `placeContext.geo.longitude` | `lon` | Mappage du paramètre de AppMeasurement pour LONGITUDE. |
| `web.webPageDetails.server` | `sv` | Mappage du paramètre AppMeasurement pour le paramètre USER_SERVER. |
| `web.webPageDetails.name` | `gn` | Mise en correspondance du paramètre de AppMeasurement avec PAGENAME. |
| `web.webPageDetails.URL` | `g` | Mappage PAGE_URL du paramètre AppMeasurement. |
| `web.webPageDetails.homePage` | `hp` | Le paramètre AppMeasurement  le mappage HOMEPAGE avec la conversion BOOLEAN_TO_YN. |
| `web.webReferrer.URL` | `r` | Mappage des paramètres de  AppMeasurement pour le . |
| `application.id` | `c.a.appid` | Mappage `c.a.appid` des données contextuelles AppMeasurement. |
| `application.launches.value` | `c.a.launches` | Mappage `c.a.launches` des données contextuelles AppMeasurement. |
| `marketing.trackingCode` | `v0` | Mappage des paramètres CAMPAIGN du AppMeasurement. |
| `commerce.purchaseID` | `pi` | Mappage du paramètre PURCHASEID  du paramètre AppMeasurement. |
| `commerce.currencyCode` | `cc` | Mappage DEVISE du paramètre AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | Mappage `a.media.name` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | Mappage `c.a.media.length` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | Mappage `c.a.contentType` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | Mappage `c.a.media.playerName` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | Mappage `c.a.media.channel` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | Mappage `c.a.media.segment` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | Mappage `c.a.media.friendlyName` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | Mappage `c.a.media.sdkVersion` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | Mappage `c.a.media.show` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | Mappage `c.a.media.format` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | Mappage `c.a.media.season` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | Mappage `c.a.media.episode` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | Mappage `c.a.media.network` des données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Mappage des données contextuelles AppMeasurement avec la conversion VEDIO_SHOW_TYPE. `c.a.media.type` |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | Mappage `c.a.media.feed` des données contextuelles AppMeasurement. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | Mappage `c.a.media.timePlayed` des données contextuelles AppMeasurement. |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | Mappage `c.a.media.totalTimePlayed` des données contextuelles AppMeasurement. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | Mappage `c.a.media.federated` des données contextuelles AppMeasurement. |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | Mappage `c.a.media.pauseCount` des données contextuelles AppMeasurement. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | Mappage `c.a.media.pauseTime` des données contextuelles AppMeasurement. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | Mappage `c.a.media.resume` des données contextuelles AppMeasurement. |
| `identitymap.ecid.[0].id` | `mid` | Mappage du MID du paramètre du AppMeasurement. |
