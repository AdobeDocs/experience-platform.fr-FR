---
title: Variables mappées automatiquement en Adobe Analytics
seo-title: Variables automatiquement mises en correspondance en Adobe Analytics avec le SDK Web Adobe Experience Platform
description: Découvrez quelles variables sont automatiquement mises en correspondance en Adobe Analytics avec le SDK Web Experience Platform
seo-description: Découvrez quelles variables sont automatiquement mises en correspondance en Adobe Analytics avec le SDK Web Experience Platform
keywords: adobe analytics;variables;analytics;automatic map;automatically mapped;
translation-type: tm+mt
source-git-commit: 2e28fda40a135330054c749d73439448a55db52c
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 46%

---


# Variables automatically mapped in [!DNL Analytics]

Below is a list of variables that the Adobe Experience Platform [!DNL Edge Network] automatically maps into [!DNL Analytics].

| Chemin d’accès au champ XDM | [!DNL Analytics Query String] / En-tête HTTP | Description |
| ---------- | ------------------------- | ----------------------------------------- |
| `commerce.order.purchaseID` | `pi` | Mappage du paramètre de requête PURCHASEID AppMeasurement. |
| `commerce.order.currencyCode` | `cc` | Mappage du paramètre de requête CURRENCY AppMeasurement. |
| `commerce.purchases.value` | `events` | Mappage du paramètre de requête AppMeasurement ÉVÉNEMENT_LISTE_FULL avec conversion COMMERCE_PURCHASE, à l’aide du délimiteur `,`. |
| `commerce.productViews.value` | `events` | Mappage du paramètre de requête AppMeasurement ÉVÉNEMENT_LISTE_FULL avec conversion COMMERCE_PROD_VUE, à l’aide d’un délimiteur `,`. |
| `commerce.productListOpens.value` | `events` | Correspondance du paramètre de requête AppMeasurement ÉVÉNEMENT_LISTE_FULL avec la conversion COMMERCE_SC_OPEN, à l’aide du délimiteur `,`. |
| `commerce.productListViews.value` | `events` | Correspondance du paramètre de requête AppMeasurement ÉVÉNEMENT_LISTE_FULL avec la conversion COMMERCE_SC_VUE, à l’aide du délimiteur `,`. |
| `commerce.checkouts.value` | `events` | Correspondance du paramètre de requête AppMeasurement ÉVÉNEMENT_LISTE_FULL avec la conversion COMMERCE_SC_CHECKOUT, à l’aide du délimiteur `,`. |
| `commerce.productListAdds.value` | `events` | Correspondance du paramètre de requête AppMeasurement ÉVÉNEMENT_LISTE_FULL avec la conversion COMMERCE_SC_AJOUTE, à l’aide du délimiteur `,`. |
| `commerce.productListRemovals.value` | `events` | Correspondance du paramètre de requête AppMeasurement ÉVÉNEMENT_LISTE_FULL avec la conversion COMMERCE_SC_REMOVE, à l’aide du délimiteur `,`. |
| `commerce.productViews.id` | `events` | `prodView` Sérialisation d’événements. |
| `commerce.productListOpens.id` | `events` | `scOpen` Sérialisation d’événements. |
| `commerce.productListViews.id` | `events` | `scView` Sérialisation d’événements. |
| `commerce.productListAdds.id` | `events` | `scAdd` Sérialisation d’événements. |
| `commerce.productListRemovals.id` | `events` | `scRemove` Sérialisation d’événements. |
| `commerce.checkouts.id` | `events` | `scCheckout` Sérialisation d’événements. |
| `device.screenHeight` | `s` | Mappage de la résolution d’écran du paramètre de la requête AppMeasurement. |
| `device.screenWidth` | `s` | Mappage de la résolution d’écran du paramètre de la requête AppMeasurement. |
| `productlistitems.[N].lineitemid` | `products` | Mappage de la Catégorie Produits du paramètre de la requête AppMeasurement. |
| `productlistitems.[N].name` | `products` | Mappage du paramètre de la requête AppMeasurement pour le nom des produits. |
| `productlistitems.[N].quantity` | `products` | Mappage de quantité du paramètre de la requête AppMeasurement Produits. |
| `productlistitems.[N].pricetotal` | `products` | Paramètre de la requête AppMeasurement Mappage des prix des produits. |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.starts.value` | `c.a.media.view` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | Données contextuelles AppMeasurement. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | Données contextuelles AppMeasurement. |
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
| `web.webInteraction.type` | `pe` | Mappage du paramètre de requête AppMeasurement PAGE_ÉVÉNEMENT avec la conversion CLICK_MAP_TYPE. |
| `web.webInteraction.URL` | `pev1` | Mappage PAGE_ÉVÉNEMENT_VAR1 du paramètre de requête AppMeasurement. |
| `web.webInteraction.name` | `pev2` | Mappage PAGE_ÉVÉNEMENT_VAR2 du paramètre de requête AppMeasurement. |
| `web.webPageDetails.siteSection` | `ch` | Mappage du CANAL des paramètres de la requête AppMeasurement. |
| `web.webPageDetails.errorPage` | `pageType` | Mappage du paramètre de requête AppMeasurement PAGE_TYPE_FULL avec la conversion ERROR_PAGE_TYPE. |
| `application.id` | `c.a.appid` | Mappage des données contextuelles `c.a.appid`AppMeasurement. |
| `application.launches.value` | `c.a.launches` | Mappage des données contextuelles `c.a.launches` AppMeasurement. |
| `marketing.trackingCode` | `v0` | Mappage du paramètre de requête CAMPAIGN AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | Mappage des données contextuelles `a.media.name`AppMeasurement. |
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
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | AppMeasurement context data `c.a.media.type` mapping with conversion VIDEO_SHOW_TYPE. |
| `identityMap.ECID.[0].id` | `mid` | Mappage du paramètre de requête MID AppMeasurement. |
