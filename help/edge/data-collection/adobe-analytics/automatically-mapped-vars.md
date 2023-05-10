---
title: Variables Adobe Analytics mappées automatiquement dans le SDK Web de Adobe Experience Platform
description: Découvrez les variables qui sont automatiquement mappées dans Adobe Analytics avec le SDK Web Experience Platform
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics;variables;analytics;carte automatique;mappage automatique;
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: dcbe4c1b5a085878562990ed2db8e5cb27b93e28
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 35%

---

# Variables automatiquement mappées dans [!DNL Analytics]

Vous trouverez ci-dessous une liste des variables que Adobe Experience Platform Edge Network mappe automatiquement dans Adobe Analytics. Vous trouverez des informations détaillées sur les paramètres de requête de collecte de données Adobe Analytics dans la section [Guide de mise en oeuvre Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html?lang=fr).

>[!NOTE]
>Les informations de cette page s’appliquent également au SDK Mobile Adobe.

| Chemin d’accès au champ XDM | [!DNL Analytics Query String] / En-tête HTTP | Description |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | Mappage des données contextuelles `c.a.appid`AppMeasurement. |
| application.launches.value | c.a.launches | Mappage des données contextuelles `c.a.launches`AppMeasurement. |
| commerce.checkouts.id | Événements  | `scCheckout` sérialisation des événements. Si ce champ est exclu (c’est-à-dire pour les événements non sérialisés), le système génère et affecte sa propre valeur d’identifiant à l’entité. |
| commerce.checkouts.value | Événements  | Mappage du paramètre de requête EVENT_LIST_FULL AppMeasurement avec conversion COMMERCE_SC_CHECKOUT, à l’aide d’un délimiteur `,`. |
| commerce.order.currencyCode | cc | Mappage du paramètre de requête CURRENCY AppMeasurement. |
| commerce.order.purchaseID | pi | Mappage du paramètre de requête PURCHASEID AppMeasurement. |
| commerce.productListAdds.id | Événements  | `scAdd` sérialisation des événements. Si ce champ est exclu (c’est-à-dire pour les événements non sérialisés), le système génère et affecte sa propre valeur d’identifiant à l’entité. |
| commerce.productListAdds.value | Événements  | Mappage du paramètre de requête EVENT_LIST_FULL AppMeasurement avec conversion COMMERCE_SC_ADD, à l’aide d’un délimiteur `,`. |
| commerce.productListOpens.id | Événements  | `scOpen` sérialisation des événements. Si ce champ est exclu (c’est-à-dire pour les événements non sérialisés), le système génère et affecte sa propre valeur d’identifiant à l’entité. |
| commerce.productListOpens.value | Événements  | Mappage du paramètre de requête EVENT_LIST_FULL AppMeasurement avec conversion COMMERCE_SC_OPEN à l’aide d’un délimiteur `,`. |
| commerce.productListRemovals.id | Événements  | `scRemove` sérialisation des événements. Si ce champ est exclu (c’est-à-dire pour les événements non sérialisés), le système génère et affecte sa propre valeur d’identifiant à l’entité. |
| commerce.productListRemovals.value | Événements  | Mappage du paramètre de requête EVENT_LIST_FULL AppMeasurement avec conversion COMMERCE_SC_REMOVE, à l’aide d’un délimiteur `,`. |
| commerce.productListViews.id | Événements  | `scView` sérialisation des événements. Si ce champ est exclu (c’est-à-dire pour les événements non sérialisés), le système génère et affecte sa propre valeur d’identifiant à l’entité. |
| commerce.productListViews.value | Événements  | Mappage du paramètre de requête EVENT_LIST_FULL AppMeasurement avec conversion COMMERCE_SC_VIEW, à l’aide d’un délimiteur `,`. |
| commerce.productViews.id | Événements  | `prodView` sérialisation des événements. Si ce champ est exclu (c’est-à-dire pour les événements non sérialisés), le système génère et affecte sa propre valeur d’identifiant à l’entité. |
| commerce.productViews.value | Événements  | Mappage du paramètre de requête EVENT_LIST_FULL AppMeasurement avec conversion COMMERCE_PROD_VIEW, à l’aide d’un délimiteur `,`. |
| commerce.purchases.value | Événements  | Mappage du paramètre de requête EVENT_LIST_FULL AppMeasurement avec conversion COMMERCE_PURCHASE, à l’aide d’un délimiteur `,`. |
| device.colorDepth | c | Mappage du paramètre de requête C_COLOR AppMeasurement. |
| device.screenHeight | s | Mappage du paramètre de requête Résolution d’écran AppMeasurement. |
| device.screenWidth | s | Mappage du paramètre de requête Résolution d’écran AppMeasurement. |
| environment.browserDetails.acceptLanguage | Accept-Language | Il s’agit d’un mappage d’en-tête HTTP, HEADER_ACCEPT_LANGUAGE. |
| environment.browserDetails.cookiesEnabled | k | Mappage du paramètre de requête COOKIES AppMeasurement avec conversion BOOLEAN_TO_YN. |
| environment.browserDetails.javaEnabled | v | Mappage du paramètre de requête JAVA_ENABLED AppMeasurement avec conversion BOOLEAN_TO_YN. |
| environment.browserDetails.javaScriptVersion | j | Mappage du paramètre de requête J_JSCRIPT AppMeasurement. |
| environment.browserDetails.userAgent | User-Agent | Il s’agit d’un mappage d’en-tête HTTP, HEADER_USER_AGENT. |
| environment.browserDetails.viewportHeight | bh | Mappage du paramètre de requête BROWSER_HEIGHT AppMeasurement. |
| environment.browserDetails.viewportWidth | bw | Mappage du paramètre de requête BROWSER_WIDTH AppMeasurement. |
| environment.connectionType | ct | Mappage du paramètre de requête CT_CONNECT_TYPE AppMeasurement. |
| environment.ipV4 | X-Forwarded-For | Il s’agit d’un mappage d’en-tête HTTP X-FORWARDED-FOR. |
| identityMap.ECID[0].id | mid | Mappage du paramètre de requête MID AppMeasurement. |
| marketing.trackingCode | v0 | Mappage du paramètre de requête CAMPAIGN AppMeasurement. |
| media.mediaTimed.completes.value | c.a.media.complete | Données contextuelles AppMeasurement. |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view, c.a.media.timePlayed, c.a.media.play | Données contextuelles AppMeasurement. |
| media.mediaTimed.federated.value | c.a.media.federated | Mappage des données contextuelles `c.a.media.federated`AppMeasurement. |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | Données contextuelles AppMeasurement. |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | Données contextuelles AppMeasurement. |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | Données contextuelles AppMeasurement. |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | Mappage des données contextuelles `c.a.media.pauseTime`AppMeasurement. |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | Mappage des données contextuelles `c.a.media.pauseCount`AppMeasurement. |
| media.mediaTimed.primaryAssetReference.@identifiant | c.a.media.asset | Données contextuelles AppMeasurement. |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | Mappage des données contextuelles `c.a.media.friendlyName`AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name | c.a.media.originator | Données contextuelles AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | Mappage des données contextuelles `c.a.media.episode`AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | Données contextuelles AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue | c.a.media.rating | Données contextuelles AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | Mappage des données contextuelles `c.a.media.season`AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | Mappage des données contextuelles `a.media.name`AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | Mappage des données contextuelles `c.a.media.show`AppMeasurement. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Mappage des données contextuelles `c.a.media.type` AppMeasurement avec conversion VEDIO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Données contextuelles AppMeasurement `c.a.media.type` mappage avec conversion VIDEO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | Mappage des données contextuelles `c.a.media.length`AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.@identifiant | c.a.media.vsid | Données contextuelles AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | Mappage des données contextuelles `c.a.media.channel`AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | Mappage des données contextuelles `c.a.contentType`AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | Mappage des données contextuelles `c.a.media.network`AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | Mappage des données contextuelles `c.a.media.segment`AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | Mappage des données contextuelles `c.a.media.playerName`AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | Mappage des données contextuelles `c.a.media.sdkVersion`AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | Mappage des données contextuelles `c.a.media.feed`AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | Mappage des données contextuelles `c.a.media.format`AppMeasurement. |
| media.mediaTimed.progress10.value | c.a.media.progress10 | Données contextuelles AppMeasurement. |
| media.mediaTimed.progress95.value | c.a.media.progress95 | Données contextuelles AppMeasurement. |
| media.mediaTimed.resumes.value | c.a.media.resume | Mappage des données contextuelles `c.a.media.resume`AppMeasurement. |
| media.mediaTimed.starts.value | c.a.media.view | Données contextuelles AppMeasurement. |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | Données contextuelles AppMeasurement. |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | Mappage des données contextuelles `c.a.media.timePlayed`AppMeasurement. |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | Mappage des données contextuelles `c.a.media.totalTimePlayed`AppMeasurement. |
| placeContext.geo.latitude | lat | Mappage du paramètre de requête LATITUDE AppMeasurement. |
| placeContext.geo.longitude | lon | Mappage du paramètre de requête LONGITUDE AppMeasurement. |
| placeContext.geo.postalCode | zip | Mappage du paramètre de requête ZIP AppMeasurement. |
| placeContext.geo.stateProvince | state | Mappage du paramètre de requête STATE AppMeasurement. |
| productListItems[N].lineItemId | produits | Mappage du paramètre de requête Produits AppMeasurement. |
| productlistitems[N].name | produits | Mappage du paramètre de requête Nom de produits AppMeasurement. |
| productlistitems[N].priceTotal | produits | Mappage du paramètre de requête AppMeasurement Prix des produits . |
| productlistitems[N].quantity | produits | Mappage du paramètre de requête Quantité de produits AppMeasurement. |
| web.webInteraction.URL | pev1 | Mappage du paramètre de requête PAGE_EVENT_VAR1 AppMeasurement. |
| web.webInteraction.name | pev2 | Mappage du paramètre de requête PAGE_EVENT_VAR2 AppMeasurement. |
| web.webInteraction.type | pe | `web.webInteraction.type=other` to `pe=lnk_o`; `web.webInteraction.type=download` to `pe=lnk_d`; `web.webInteraction.type=exit` to `pe=lnk_e` |
| web.webPageDetails.URL | g | Mappage du paramètre de requête PAGE_URL AppMeasurement. |
| web.webPageDetails.errorPage | pageType | Mappage du paramètre de requête PAGE_TYPE_FULL AppMeasurement avec conversion ERROR_PAGE_TYPE. |
| web.webPageDetails.homePage | hp | Mappage du paramètre de requête HOMEPAGE AppMeasurement avec conversion BOOLEAN_TO_YN. |
| web.webPageDetails.name | gn | Mappage du paramètre de requête PAGENAME AppMeasurement. |
| web.webPageDetails.server | sv | Mappage du paramètre de requête USER_SERVER AppMeasurement. |
| web.webPageDetails.siteSection | ch | Mappage du paramètre de requête CHANNEL AppMeasurement. |
| web.webReferrer.URL | r | Mappage du paramètre de requête REFERRER AppMeasurement. |

{style="table-layout:auto"}
