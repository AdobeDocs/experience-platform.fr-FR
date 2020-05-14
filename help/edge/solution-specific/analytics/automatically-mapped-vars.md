---
title: Variables mappées automatiquement dans Analytics
seo-title: Variables mappées automatiquement dans Analytics avec le SDK Web d’Adobe Experience Platform
description: Découvrez quelles variables sont automatiquement mappées dans Analytics avec le SDK Web d’Adobe Experience Platform
seo-description: Découvrez quelles variables sont automatiquement mappées dans Analytics avec le SDK Web d’Adobe Experience Platform
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 100%

---


# Variables mappées automatiquement dans Analytics

Vous trouverez ci-dessous une liste de variables que le réseau Edge d’Adobe Experience Platform mappe automatiquement dans Analytics.

| Chemin d’accès au champ XDM | Chaîne de requête Analytics / En-tête HTTP | Description |
| ---------- | ------------------------- | -------- |
| `environment.browserDetails.userAgent` | `User-Agent` | Il s’agit d’un mappage d’en-tête HTTP, HEADER_USER_AGENT. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Il s’agit d’un mappage d’en-tête HTTP, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | Mappage du paramètre de requête COOKIES AppMeasurement avec conversion BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | Mappage du paramètre de requête J_JSCRIPT AppMeasurement. |
| `environment.browserDetails.javaEnabled` | `v` | Mappage du paramètre de requête JAVA_ENABLED AppMeasurement avec conversion BOOLEAN_TO_YN. |
| `environment.browserDetails.viewportHeight` | `bh` | Mappage du paramètre de requête BROWSER_HEIGHT AppMeasurement. |
| `environment.browserDetails.viewportWidth` | `bw` | Mappage du paramètre de requête BROWSER_WIDTH AppMeasurement. |
| `environment.connectionType` | `ct` | Mappage du paramètre de requête CT_CONNECT_TYPE AppMeasurement. |
| `device.colorDepth` | `c` | Mappage du paramètre de requête C_COLOR AppMeasurement. |
| `placeContext.geo.stateProvince` | `state` | Mappage du paramètre de requête STATE AppMeasurement. |
| `placeContext.geo.postalCode` | `zip` | Mappage du paramètre de requête ZIP AppMeasurement. |
| `placeContext.geo.latitude` | `lat` | Mappage du paramètre de requête LATITUDE AppMeasurement. |
| `placeContext.geo.longitude` | `lon` | Mappage du paramètre de requête LONGITUDE AppMeasurement. |
| `web.webPageDetails.server` | `sv` | Mappage du paramètre de requête USER_SERVER AppMeasurement. |
| `web.webPageDetails.name` | `gn` | Mappage du paramètre de requête PAGENAME AppMeasurement. |
| `web.webPageDetails.URL` | `g` | Mappage du paramètre de requête PAGE_URL AppMeasurement. |
| `web.webPageDetails.homePage` | `hp` | Mappage du paramètre de requête HOMEPAGE AppMeasurement avec conversion BOOLEAN_TO_YN. |
| `web.webReferrer.URL` | `r` | Mappage du paramètre de requête REFERRER AppMeasurement. |
| `application.id` | `c.a.appid` | Mappage des données contextuelles `c.a.appid`AppMeasurement. |
| `application.launches.value` | `c.a.launches` | Mappage des données contextuelles `c.a.launches` AppMeasurement. |
| `marketing.trackingCode` | `v0` | Mappage du paramètre de requête CAMPAIGN AppMeasurement. |
| `commerce.purchaseID` | `pi` | Mappage du paramètre de requête PURCHASEID AppMeasurement. |
| `commerce.currencyCode` | `cc` | Mappage du paramètre de requête CURRENCY AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | Mappage des données contextuelles `a.media.name` AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | Mappage des données contextuelles `c.a.media.length` AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | Mappage des données contextuelles `c.a.contentType` AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | Mappage des données contextuelles `c.a.media.playerName` AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | Mappage des données contextuelles `c.a.media.channel` AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | Mappage des données contextuelles `c.a.media.segment` AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | Mappage des données contextuelles `c.a.media.friendlyName` AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | Mappage des données contextuelles `c.a.media.sdkVersion` AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | Mappage des données contextuelles `c.a.media.show` AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | Mappage des données contextuelles `c.a.media.format` AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | Mappage des données contextuelles `c.a.media.season` AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | Mappage des données contextuelles `c.a.media.episode` AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | Mappage des données contextuelles `c.a.media.network` AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Mappage des données contextuelles `c.a.media.type` AppMeasurement avec conversion VEDIO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | Mappage des données contextuelles `c.a.media.feed` AppMeasurement. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | Mappage des données contextuelles `c.a.media.timePlayed` AppMeasurement. |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | Mappage des données contextuelles `c.a.media.totalTimePlayed` AppMeasurement. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | Mappage des données contextuelles `c.a.media.federated` AppMeasurement. |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | Mappage des données contextuelles `c.a.media.pauseCount` AppMeasurement. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | Mappage des données contextuelles `c.a.media.pauseTime` AppMeasurement. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | Mappage des données contextuelles `c.a.media.resume` AppMeasurement. |
| `identitymap.ecid.[0].id` | `mid` | Mappage du paramètre de requête MID AppMeasurement. |
