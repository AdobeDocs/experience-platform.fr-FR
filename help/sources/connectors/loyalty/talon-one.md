---
title: Présentation de Talon.One Source
description: En savoir plus sur les sources Talon.One sur Adobe Experience Platform
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 558a9d6ff3222acbf77edea0a82ef50725cd6203
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 3%

---

# [!DNL Talon.One]

>[!AVAILABILITY]
>
>Les sources [!DNL Talon.One] sont en version bêta. Lisez les [termes et conditions](../../home.md#terms-and-conditions) dans la présentation des sources pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Avec [!DNL Talon.One], vous pouvez facilement créer, gérer et optimiser des campagnes marketing personnalisées et personnalisées pour vos clients. Utilisez cette plateforme puissante pour proposer des remises, distribuer des coupons, lancer des programmes de recommandation, configurer des programmes de fidélité et offrir des incentives ludiques, le tout à partir d’un seul système évolutif conçu pour vous aider à interagir avec votre audience et à la récompenser.

Vous pouvez utiliser les sources de [!DNL Talon.One] du catalogue des sources Adobe Experience Platform pour ingérer des données de fidélité par lots et par flux à partir de votre compte [!DNL Talon.One].

* [Événements de streaming Talon.One](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Connecteur Source Batch Talon.One](../../tutorials/ui/create/loyalty/talon-one-batch.md)

>[!TIP]
>
>Les données de fidélité font référence aux informations du programme de fidélité de vos utilisateurs finaux, telles que les points de fidélité, les points de fidélité dépensés, le niveau actuel, les coupons accordés, les recommandations et les succès.

## Conditions préalables {#prerequisites}

Fournissez des valeurs pour les informations d’identification suivantes afin d’authentifier et de connecter le [!DNL Talon.One Batch Source Connector].

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Domaine | URL unique associée à votre environnement d’application [!DNL Talon.One]. Assurez-vous de ne pas inclure le protocole ou le chemin d’accès lors de la saisie de votre domaine. | `acmetalonone.us-east4` |
| Clé API [!DNL Talon.One] Management | La clé API de gestion est une information d’identification utilisée pour authentifier et autoriser l’accès à l’API de gestion d’[!DNL Talon.One]. Il gère des opérations telles que : <ul><li>Importer des coupons</li><li>Récupération des données de campagne</li><li>Gestion des applications et des points d’entrée</li></ul> | `ManagementKey-v1 {YOUR_MANAGEMENT_KEY}` |

## Mappage {#mapping}

Pour vous aider à mapper chaque objet d’effet en fonction de sa valeur de `effectType` unique, vous pouvez utiliser la fonction de `array_to_map` de préparation de données. Vous pouvez ainsi convertir facilement un tableau non ordonné d’effets en paires clé-valeur correspondant à vos besoins. Consultez l’exemple ci-dessous pour obtenir des conseils.

| Source | Destination |
| ---- | --- |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsGained[0].promotionId` |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsGained[0].value` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsRedemption[0].promotionId` |
| `array_to_map(data.effects, "effectType").acceptCoupon.campaignId` | `_{TENANT_ID}.loyalty.couponRedemption[0].campaignId` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsRedemption[0].value` |
| `array_to_map(data.effects, "effectType").acceptCoupon.props.value` | `_{TENANT_ID}.loyalty.couponRedemption[0].id` |
| `array_to_map(data.effects, "effectType").setDiscount.campaignId` | `_{TENANT_ID}.loyalty.discounts[0].promotionId` |
| `array_to_map(data.effects, "effectType").setDiscount.props.value` | `_{TENANT_ID}.loyalty.discounts[0].value` |
| `data.created` | `timestamp` |
| `data.attributes.params.profileId` | `personID` |
| `data.attributes.integrationId` | `_id` |
| `data.attributes.params.cartItems[*].name` | `productListItems[*].name` |
| `data.attributes.params.cartItems[*].category` | `productListItems[*].productCategories[0].categoryID` |
| `data.attributes.params.cartItems[*].sku` | `productListItems[*].SKU` |

{style="table-layout:auto"}

## Étapes suivantes

Lisez la documentation suivante pour découvrir comment connecter votre compte [!DNL Talon.One] à Experience Platform et ingérer des données de fidélité par lots et par flux.

* [Événements de streaming Talon.One](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Connecteur Source Batch Talon.One](../../tutorials/ui/create/loyalty/talon-one-batch.md)