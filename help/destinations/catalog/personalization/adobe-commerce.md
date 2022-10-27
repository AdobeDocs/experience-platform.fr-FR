---
title: (Version bêta) Connecteur de destination Adobe Commerce
description: Découvrez comment les marchands Adobe Commerce et Real-Time CDP peuvent personnaliser l’expérience d’achat en proposant du contenu et des promotions de site hautement pertinents, personnalisés en fonction des segments de clients créés et gérés dans Real-Time CDP.
source-git-commit: 566f26ec0f13bfaceb0ee59f3e4c72e767bc8cc9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 24%

---

# (Version bêta) Connexion Adobe Commerce {#adobe-commerce}

## Présentation {#overview}

>[!IMPORTANT]
> 
>Le **[!UICONTROL Adobe Commerce]** Le connecteur est en version bêta et n’est disponible que pour un certain nombre de clients.

Le [!DNL Adobe Commerce] Le connecteur de destination vous permet de sélectionner un ou plusieurs segments Real-Time CDP à activer dans votre [!DNL Adobe Commerce] pour offrir une expérience personnalisée dynamique à vos clients. Within [!DNL Adobe Commerce], vous pouvez ensuite sélectionner ces segments Real-Time CDP pour personnaliser les offres uniques du panier, telles que &quot;Acheter 2 et 1 gratuitement&quot;. Vous pouvez également afficher des bannières principales et modifier le prix des produits au moyen d’offres promotionnelles, toutes personnalisées dans les segments Adobe Real-Time CDP.

<!--## Use cases {#use-cases}

To help you better understand how and when you should use the *YourDestination* destination, here are sample use cases that Adobe Experience Platform customers can solve by using this destination.

### Use case #1 {#use-case-1}

*For mobile messaging platforms:*

*A home rental and sales platform wants to push mobile notifications to customers' Android and iOS devices to let them know that there are 100 updated listings in the area where they previously searched for a rental.*

### Use case #2 {#use-case-2}

*For social network platforms:*

*An athletic apparel brand wants to reach existing customers through their social media accounts. The apparel brand can ingest email addresses from their own CRM to Adobe Experience Platform, build segments from their own offline data, and send these segments to YourDestination, to display ads in their customers' social media feeds.*-->

## Conditions préalables {#prerequisites}

Cette extension est disponible dans le catalogue des destinations pour certains clients bêta ayant acheté Real-Time CDP Prime ou Ultimate et Adobe Commerce.

Les clients bêta doivent avoir accès à :

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/)
- [Adobe Commerce Cloud version 2.4.3 ou ultérieure](https://business.adobe.com/products/magento/magento-commerce.html)

Dans Experience Platform, créez les éléments suivants :

- [Schéma](../../../xdm/schema/composition.md). Le schéma que vous créez représente les données que vous prévoyez d’ingérer à partir d’Adobe Commerce. [En savoir plus](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) sur la création d’un schéma contenant des groupes de champs spécifiques à Commerce.
- [Jeu de données](../../../catalog/datasets/user-guide.md#create). Un jeu de données est une structure de stockage et de gestion pour une collecte de données. Vous devez créer ce jeu de données à partir du schéma que vous avez créé ci-dessus.
- [Flux de données](../../../edge/datastreams/overview.md#create). Identifiant qui permet aux données de passer de Adobe Experience Platform à d’autres produits DX d’Adobe. Cet identifiant doit être associé à un site web spécifique au sein de votre instance Adobe Commerce spécifique. Lorsque vous créez ce flux de données, spécifiez le schéma XDM que vous avez créé ci-dessus.

Une fois les conditions préalables remplies, connectez-vous au [!DNL Commerce] destination.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter au [!DNL Adobe Commerce] destination :

1. Dans le [Interface de Platform](https://experience.adobe.com/platform/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**.
1. Sélectionner **[!UICONTROL Personnalisation]**.
1. Sélectionnez la destination Adobe Commerce à mettre en surbrillance, puis sélectionnez **[!UICONTROL Configuration]**.
1. Suivez les étapes décrites dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

- **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
- **[!UICONTROL Description]** : saisissez une description pour votre destination. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination. Ce champ est facultatif.
- **[!UICONTROL Alias d’intégration]** : cette valeur est envoyée au SDK web Experience Platform sous forme de nom d’objet JSON.
- **[!UICONTROL Identifiant du flux de données]** : détermine dans quel flux de données de collecte de données les segments seront inclus dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Voir [Configurer un flux de données](../../../edge/datastreams/overview.md) pour plus d’informations.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur l’état du flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de fournir des détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activez les segments dans la variable [!DNL Commerce] destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation des profils et des segments vers les destinations de requête de profil](../../ui/activate-profile-request-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience dans le [!DNL Commerce] destination.

## Étapes suivantes [!DNL Adobe Commerce]

Maintenant que vous avez configuré la variable [!DNL Commerce] dans Experience Platform, vous devez configurer la variable [!DNL Commerce Admin] pour importer les segments Real-Time CDP que vous avez créés. Voir [[!DNL Commerce] documentation](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/customer-segment-rtcdp.html) pour en savoir plus.

## Validation de l’exportation des données {#exported-data}

Après avoir activé les segments Real-Time CDP dans votre [!DNL Adobe Commerce] , vous verrez ces segments disponibles dans le [!DNL Admin] lorsque vous créez une règle de prix du panier :

![Administrateur Adobe Commerce](../../assets/catalog/personalization/adobe-commerce/rtcdp-in-admin.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
