---
title: Groupe de champs de schéma d’extension complète Adobe Advertising Cloud ExperienceEvent
description: Découvrez le groupe de champs de schéma d’extension complète Adobe Advertising Cloud ExperienceEvent.
badgeBeta: label="Beta" type="Informative"
source-git-commit: adfd0220b8bc53c44abc76a711b148a7e03edb7a
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 11%

---

# [!UICONTROL Extension complète Adobe Advertising Cloud ExperienceEvent] groupe de champs de schéma

>[!AVAILABILITY]
>
>Le groupe de champs [!UICONTROL &#x200B; Extension complète Adobe Advertising Cloud ExperienceEvent &#x200B;] est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

[!UICONTROL &#x200B; Extension complète Adobe Advertising Cloud ExperienceEvent &#x200B;] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), qui capture les mesures courantes collectées par Adobe Advertising (anciennement appelée « [!DNL Advertising Cloud] »).

Ce document décrit la structure et le cas d’utilisation du groupe de champs de l’extension [!DNL Advertising Cloud].

>[!NOTE]
>
>Vous pouvez également rechercher ce groupe de champs [dans l’interface utilisateur d’Experience Platform](../../ui/explore.md) ou afficher le schéma complet dans le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Structure du groupe de champs

Le groupe de champs fournit un seul objet `_experience` à un schéma, qui contient lui-même un seul objet `adcloud`.

![Champs de niveau supérieur pour le groupe de champs [!DNL Advertising Cloud]](../../images/field-groups/advertising-full-extension/full-schema.png "Champs de niveau supérieur pour le groupe  [!DNL Advertising Cloud]  champs")

| Propriété | Type de données | Description |
| --- | --- | --- |
| `adDeliveryDetails` | Objet | Ajoutez les détails de diffusion. Pour plus d’informations sur le contenu de cet objet[ reportez-vous à la `adDeliveryDetails`sous-section ci-dessous de l’objet ](#adDeliveryDetails) . |
| `advertisement` | Objet | Détails de la publicité numérique. Pour plus d’informations sur le contenu de cet objet[ consultez la ](#advertisement)sous-section ci-dessous sur l’objet de publicité . |
| `campaign` | Objet | Détails de la hiérarchie de la campagne. Pour plus d’informations sur le contenu de cet objet[ reportez-vous à la ](#campaign-campaign)sous-section ci-dessous sur l’objet Campaign . |
| `conversionDetails` | Objet | Détails de conversion d’une publicité. Pour plus d’informations sur le contenu de cet objet, consultez la [sous-section ci-dessous](#conversionDetails). |
| `eventType` | Chaîne | Type d’événement Adobe Advertising. |
| `fees` | Objet | Détails des frais Advertising. Pour plus d’informations sur le contenu de cet objet[ consultez la ](#fees)sous-section ci-dessous sur l’objet des frais. |
| `inventory` | Objet | Détails de l’inventaire. Pour plus d’informations sur le contenu de cet objet, consultez la [sous-section ci-dessous](#inventory). |
| `productDetails` | Objet | Détails de l’annonce du produit. Pour plus d’informations sur le contenu de cet objet[ reportez-vous à la ](#productDetails)sous-section ci-dessous de l’objet productDetails. |
| `stitchId` | Chaîne | Identifiant des serveurs de publicités d’Adobe Advertising pour effectuer le suivi des conversions par clic sur les navigateurs qui bloquent les cookies tiers. |

## `adDeliveryDetails` {#adDeliveryDetails}

L&#39;objet adDeliveryDetails fournit des informations sur le lieu et la manière dont la publicité a été diffusée, y compris des sites web d&#39;emplacement et des identifiants d&#39;emplacement.

![Diagramme de schéma présentant l’objet `adDeliveryDetails` et ses champs.](../../images/field-groups/advertising-full-extension/adDeliveryDetails.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `placementWebsite` | Chaîne | Site web sur lequel la publicité a été affichée. |
| `siteLinkText` | Chaîne | Lien vers le site sélectionné dans la publicité. |
| `interestLocationID` | Chaîne | Emplacement déduit de la requête de recherche. Par exemple, une requête « Hôtel à Goa » renvoie l’identifiant de Goa, quel que soit l’emplacement de navigation réel de l’utilisateur. |
| `physicalLocationID` | Chaîne | Emplacement de navigation de l’utilisateur, représenté par un ID de référence provenant du réseau publicitaire. Cet identifiant n’est pas un nom d’emplacement lisible (une ville ou un pays, par exemple), mais un code attribué par le réseau publicitaire pour identifier une cible géographique. |

## `advertisement` {#advertisement}

L’objet d’annonce décrit les détails de l’annonce numérique, tels que ses identifiants, son type, son contenu créatif, son ciblage et les mots-clés associés.

![Diagramme de schéma présentant l’objet `advertisement` et ses champs.](../../images/field-groups/advertising-full-extension/advertisement.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `adId` | Chaîne | Identifiant de l’annonce publicitaire associée à cet événement. Cet ID n’est pas associé à la norme industrielle Ad-ID. |
| `runtime` | Chaîne | Le runtime de l’unité publicitaire, distinct du runtime du navigateur ou du système d’exploitation. Les valeurs possibles sont les suivantes : `unknown` et `HTML5`. |
| `adClass` | Chaîne | Classe publicitaire de l’événement déterminant : `display`, `video` ou `social`. |
| `adUnitType` | Chaîne | Identifiant du code qui effectue le rendu de la publicité dans un navigateur ou un appareil. Valeurs possibles :<ul><li>`linearVideo` : vidéo linéaire</li><li>`interactiveVideo` : vidéo interactive</li><li>`banner` : bannière,</li><li>`richMediaBanner` : bannière de média enrichi,</li><li>`newsFeedVideo` : vidéo sur les flux d’actualités,</li><li>`newsFeedDisplay` : affichage des flux d’actualités,</li><li>`HTML5` : HTML5,</li><li>`inPageVideo` : dans la vidéo de la page,</li><li>`inPageDisplay` : dans l’affichage de la page,</li><li>`facebook` : Facebook,</li><li>`twitter` : Twitter,</li><li>`linearTv` : télévision linéaire,</li><li>`vod` : Vidéo à la demande</li></ul> |
| `promotedAssetId` | Chaîne | Identifiant de la ressource promue dans la publicité associée à cet événement. |
| `creativeID` | Chaîne | Identifiant du contenu publicitaire (par exemple une bannière, une vidéo ou une publicité sur les réseaux sociaux) associé à cet événement. |
| `keywordID` | Chaîne | Identifiant du mot-clé saisi par l’utilisateur dans une requête de recherche qui a déclenché cet événement. |
| `keyword` | Chaîne | Mot-clé de liste sur lequel le client a enchéri. |
| `isDynamicSearchAd` | Booléen | Indique si l’événement provient d’une publicité de recherche dynamique. |
| `audienceID` | Chaîne | Identifiant du segment ciblé par l’annonce publicitaire. |
| `adGroupID` | Chaîne | Identifiant du groupe publicitaire associé à l’annonce publicitaire qui a déclenché cet événement. |
| `campaignID` | Chaîne | Identifiant de la campagne associée à l’annonce publicitaire qui a déclenché cet événement. |
| `networkType` | Chaîne | Type de réseau sur lequel l’événement s’est produit. Valeurs possibles : <ul><li>`search` : la publicité a été affichée sur le réseau de recherche.</li><li>`content` : la publicité s&#39;affichait sur le réseau de contenu.</li></ul> |
| `matchType` | Chaîne | Type de correspondance de mot-clé. Valeurs possibles : <ul><li>`exact` : correspondance exacte du mot-clé</li><li>`broad` : large correspondance du mot-clé</li><li>`phrase` : correspondance d’expression du mot-clé</li></ul> |

## `campaign` {#campaign}

L’objet campaign définit la hiérarchie de la campagne publicitaire, y compris les identifiants du compte, de l’annonceur, de l’emplacement et du package, ainsi que les détails de la devise.

![Diagramme de schéma présentant l’objet `campaign` et ses champs.](../../images/field-groups/advertising-full-extension/campaign.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `accountId` | Chaîne | Identifiant du compte. |
| `dspId` | Chaîne | Identifiant du Demand Side Platform (DSP) dans lequel la campagne est définie. En règle générale, cet identifiant correspond à l’identifiant d’Adobe Advertising Cloud DSP. |
| `campaignId` | Chaîne | Identifiant de la campagne. |
| `placementId` | Chaîne | Identifiant de l’emplacement. |
| `packageId` | Chaîne | Identifiant du package Advertising DSP. |
| `advertiserId` | Chaîne | Identifiant de l’annonceur. |
| `experimentId` | Chaîne | Identifiant de l’expérience. |
| `sampleGroupId` | Chaîne | Identifiant du groupe d’échantillons. |
| `currency` | Chaîne | Code de devise de facturation ISO 4217 pour le compte. Utilise le modèle d’expression régulière ^[A-Z]{3}$ (trois lettres majuscules). Par exemple : USD, EUR. |

## `conversionDetails` {#conversionDetails}

L’objet conversionDetails capture les informations de suivi pour les conversions publicitaires, y compris les codes de suivi, les identités et les propriétés de conversion.

![Diagramme de schéma présentant l’objet `conversionDetails` et ses champs.](../../images/field-groups/advertising-full-extension/conversionDetails.png " champ conversionDetails ")

| Propriété | Type de données | Description |
| --- | --- | --- |
| `trackingCode` | Chaîne | Code de suivi de conversion de l’événement. Pour obtenir la liste des formats possibles, voir [Formats d’ID AMO](https://experienceleague.adobe.com/en/docs/advertising/integrations/customer-journey-analytics/ids#amo-id-formats). |
| `trackingIdentities` | Chaîne | Identifiant d’événement (EF) ou détails d’identité de suivi pour un événement. Pour obtenir une liste des formats possibles, voir [Formats d’ID EF](https://experienceleague.adobe.com/en/docs/advertising/integrations/customer-journey-analytics/ids#ef-id-formats). |
| `conversionProperties` | Objet | Mappage des propriétés de conversion, représenté sous la forme d’un tableau de chaînes de paire clé-valeur (telles que `subscriptions=253`). |

## `fees` {#fees}

L’objet Frais capture les médias, les données et d’autres coûts publicitaires, répartis par Advertising DSP, compte et annonceur.

![Diagramme de schéma présentant l’objet `fees` et ses champs.](../../images/field-groups/advertising-full-extension/fees.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `DSPMediaFees` | Nombre | Les frais médias sont à la charge d&#39;Advertising DSP. |
| `DSPDataFees` | Nombre | Les frais de données facturables par Advertising DSP. |
| `DSPOtherFees` | Nombre | Autres frais facturables par Advertising DSP. |
| `accountMediaFees` | Nombre | Les frais de média pour le compte mais non facturables par Advertising DSP. |
| `accountDataFees` | Nombre | Frais de données pour le compte mais non facturables par Advertising DSP. |
| `accountOtherFees` | Nombre | Autres frais pour le compte, mais non facturables par Advertising DSP. |
| `advertiserMediaFees` | Nombre | Les frais facturés par l&#39;annonceur du compte à l&#39;annonceur du média. |
| `advertiserDataFees` | Nombre | Autres frais facturés à l&#39;annonceur à partir du compte. |
| `advertiserOtherFees` | Nombre | Autres frais facturés à l&#39;annonceur à partir du compte. |
| `billableMediaNetSpend` | Nombre | Dépenses nettes facturables pour la publicité dans les médias. |
| `totalMediaNetSpend` | Nombre | Total des dépenses nettes pour la publicité dans les médias. |
| `billableDataNetSpend` | Nombre | Dépenses nettes facturables pour la publicité liée aux données. |
| `billableOtherNetSpend` | Nombre | Dépenses nettes facturables pour d’autres types de publicité. |
| `totalBillableNetSpend` | Nombre | Total des dépenses nettes facturables. |
| `totalNonBillableNetSpend` | Nombre | Total des dépenses nettes non facturables. |
| `totalNetSpend` | Nombre | Total des dépenses nettes. |

## `inventory` {#inventory}

L’objet d’inventaire enregistre des détails sur l’opportunité d’inventaire publicitaire, y compris les données de session, les codes partenaire, les identifiants de site, la devise de coût et les règles de segmentation.

![Diagramme de schéma présentant l’objet `inventory` et ses champs.](../../images/field-groups/advertising-full-extension/inventory.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `sessionId` | Chaîne | Identifiant de session associé à un événement d’expérience, utilisé pour lier des événements indépendants qui se sont produits au cours de la même session. |
| `feedID` | Chaîne | Identifiant composite de l’éditeur, d’Ad Exchange et d’autres fonctionnalités. |
| `sspPartnerCode` | Chaîne | Partenaire (échange) par l’intermédiaire duquel Adobe Advertising Cloud reçoit l’opportunité d’inventaire. |
| `siteID` | Chaîne | Identifiant du site web où l’impression publicitaire a été diffusée. |
| `costCurrency` | Chaîne | Code de devise ISO 4217 utilisé pour payer un partenaire pour une opportunité publicitaire. La valeur doit suivre le modèle d’expression régulière ^[A-Z]{3}$ (trois lettres majuscules). Par exemple : USD, EUR. |
| `inventorySourceId` | Chaîne | Identifiant de la source d’inventaire Adobe Advertising Cloud sur laquelle cette opportunité a été diffusée. |
| `segment` | Objet | Détails associés aux règles de segmentation utilisateur. Ses propriétés sont les suivantes :<ul><li>`attributablePartnerId` (chaîne) : identifiant du fournisseur de segments propriétaire de l’attribut attributeSegmentId.</li><li>`attributableSegmentId` (chaîne) : segment crédité pour le ciblage utilisateur dans la règle de ciblage de l’emplacement. Il est utilisé à des fins de suivi des coûts et des partenaires payeurs.</li><li>`segments` (chaîne) : intersection des segments d’utilisateur a\) auxquels l’utilisateur appartenait et b\) que l’annonce ciblait. Il ne s’agit pas de la liste complète des segments auxquels l’utilisateur appartenait au moment de la mise aux enchères.</li></ul> |
| `optimizationTag` | Chaîne | Balise liée à l’optimisation. |
| `attributableDeviceGraphId` | Chaîne | Identifiant du graphique d’appareil attribué à un événement de conversion. |

## `productDetails` {#productDetails}

L’objet `productDetails` contient des informations sur les produits présentés dans les annonces d’achats pour [!DNL Adobe Advertising Search, Social, & Commerce], notamment les identifiants de produit, le pays, la langue, la partition, le titre et le type d’annonce.

![Diagramme de schéma présentant l’objet `productDetails` et ses champs.](../../images/field-groups/advertising-full-extension/productDetails.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `productID` | Chaîne | Identifiant du produit présenté dans la publicité associée à cet événement. |
| `country` | Chaîne | Pays de vente du produit présenté dans la publicité associée à l’événement. |
| `language` | Chaîne | Langue de vos informations sur les produits, comme indiqué dans le flux de données du centre commercial du client. |
| `partitionID` | Chaîne | Identifiant du groupe de produits associé à l’annonce publicitaire dans cet événement. |
| `title` | Chaîne | Titre du produit affiché dans la publicité. |
| `adType` | Chaîne | Type d’annonce pour le produit utilisé dans [!DNL Google] campagnes Shopping. Valeurs possibles :<ul><li>`pla_with_pog` : lorsque l’événement provient d’un achat par le biais d’une publicité d’achat</li><li>`pla` : Lorsque l&#39;événement provient d&#39;une publicité commerciale.</li><li>`pla_multichannel` : lorsque l’événement provenant d’une publicité d’achat incluait des options pour les canaux d’achat « en ligne » et « locaux ».</li><li>`pla_with_promotion` : lorsque l’événement provenant d’une publicité d’achat affichait une promotion de vendeur.</li></ul> |

## Étapes suivantes

Ce document couvrait la structure et le cas d’utilisation du groupe de champs de l’extension [!DNL Advertising Cloud]. Pour plus d’informations sur le groupe de champs lui-même, consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/adcloud/experienceevent-all.schema.json).

Si vous utilisez ce groupe de champs pour collecter des données [!DNL Advertising] à l’aide de Adobe Experience Platform Web SDK, consultez le guide sur [la configuration d’un flux de données](../../../datastreams/overview.md) pour savoir comment mapper des données à XDM côté serveur.
