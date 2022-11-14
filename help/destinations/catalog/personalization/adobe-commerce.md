---
title: Connecteur de destination Adobe Commerce (version bêta)
description: Découvrez comment les marchands Adobe Commerce et Real-Time CDP peuvent personnaliser l’expérience d’achat en proposant du contenu et des promotions de sites hautement pertinents, personnalisés en fonction des segments des clients créés et gérés dans Real-Time CDP.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: 638a778d1d999ab6a1726333f9cde0a0b4fad57b
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 99%

---

# Connexion Adobe Commerce (version bêta) {#adobe-commerce}

## Présentation {#overview}

>[!IMPORTANT]
> 
>Le connecteur **[!UICONTROL Adobe Commerce]** est en version bêta et disponible uniquement pour un nombre restreint de clients.

Le connecteur de destination [!DNL Adobe Commerce] vous permet de sélectionner un ou plusieurs segments Real-Time CDP à activer dans votre compte [!DNL Adobe Commerce] pour offrir une expérience personnalisée dynamique à vos clients. Dans [!DNL Adobe Commerce], vous pouvez ensuite sélectionner ces segments Real-Time CDP pour personnaliser les offres exceptionnelles du panier, telles que « Pour deux produits achetés, le troisième est offert ». Vous pouvez également afficher des bannières principales et modifier le prix des produits par le biais d’offres promotionnelles, toutes personnalisées en fonction des segments Adobe Real-Time CDP.

<!--## Use cases {#use-cases}

To help you better understand how and when you should use the *YourDestination* destination, here are sample use cases that Adobe Experience Platform customers can solve by using this destination.

### Use case #1 {#use-case-1}

*For mobile messaging platforms:*

*A home rental and sales platform wants to push mobile notifications to customers' Android and iOS devices to let them know that there are 100 updated listings in the area where they previously searched for a rental.*

### Use case #2 {#use-case-2}

*For social network platforms:*

*An athletic apparel brand wants to reach existing customers through their social media accounts. The apparel brand can ingest email addresses from their own CRM to Adobe Experience Platform, build segments from their own offline data, and send these segments to YourDestination, to display ads in their customers' social media feeds.*-->

## Conditions préalables {#prerequisites}

Cette extension est disponible dans le catalogue des destinations pour certains clients de la version Beta qui ont acheté Real-Time CDP Prime ou Ultimate et Adobe Commerce.

Les clients bêta doivent avoir accès à :

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/)
- [Adobe Commerce Cloud version 2.4.4 ou ultérieure](https://business.adobe.com/fr/products/magento/magento-commerce.html)

Dans Experience Platform, créez les éléments suivants :

- [Schéma](../../../xdm/schema/composition.md). Le schéma que vous créez représente les données que vous prévoyez d’ingérer à partir d’Adobe Commerce. [En savoir plus](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html?lang=fr) sur la création d’un schéma contenant des groupes de champs spécifiques à Commerce.
- [Jeu de données](../../../catalog/datasets/user-guide.md#create). Un jeu de données est une structure de stockage et de gestion pour une collection de données. Vous devez créer ce jeu de données à partir du schéma que vous avez créé ci-dessus.
- [Flux de données](../../../edge/datastreams/overview.md#create). Identifiant qui permet aux données de passer d’Adobe Experience Platform à d’autres produits DX d’Adobe. Cet identifiant doit être associé à un site web spécifique au sein de votre instance Adobe Commerce spécifique. Lorsque vous créez ce train de données, spécifiez le schéma XDM que vous avez créé ci-dessus.

Une fois les conditions préalables remplies, connectez-vous à la destination [!DNL Commerce].

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à la destination [!DNL Adobe Commerce] :

1. Dans [l’interface de Platform](https://experience.adobe.com/platform/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**.
1. Sélectionnez **[!UICONTROL Personnalisation]**.
1. Sélectionnez la destination Adobe Commerce à mettre en surbrillance, puis **[!UICONTROL Configuration]**.
1. Suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

- **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
- **[!UICONTROL Description]** : saisissez une description pour votre destination. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination. Ce champ est facultatif.
- **[!UICONTROL Alias d’intégration]** : cette valeur est envoyée au SDK web Experience Platform sous forme de nom d’objet JSON.
- **[!UICONTROL Identifiant du flux de données]** : détermine dans quel flux de données de collecte de données les segments seront inclus dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Voir [Configurer un flux de données](../../../edge/datastreams/overview.md) pour plus d’informations.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de fournir les informations de votre connexion à la destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers la destination [!DNL Commerce] {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer des destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lisez [Activer des profils et des segments vers les destinations de requête de profil](../../ui/activate-profile-request-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers la destination [!DNL Commerce].

## Étapes suivantes dans [!DNL Adobe Commerce]

Maintenant que vous avez configuré la destination [!DNL Commerce] dans Experience Platform, vous devez configurer [!DNL Commerce Admin] pour importer les segments Real-Time CDP que vous avez créés. Consulter la [[!DNL Commerce] documentation](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/customer-segment-rtcdp.html?lang=fr) pour en savoir plus.

## Validation de l’activation de l’audience dans Commerce {#exported-data}

Une fois les segments Real-Time CDP activés dans votre compte [!DNL Adobe Commerce], ces segments sont disponibles dans le [!DNL Admin] lorsque vous créez une règle de prix de panier :

![Administrateur Adobe Commerce](../../assets/catalog/personalization/adobe-commerce/rtcdp-in-admin.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
