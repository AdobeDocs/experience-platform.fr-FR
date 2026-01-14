---
title: Connecteur de destination Adobe Commerce
description: Découvrez comment les commerçants Adobe Commerce et Real-Time CDP peuvent personnaliser l’expérience d’achat en proposant du contenu et des promotions de sites hautement pertinents, personnalisés en fonction des audiences de clients créées et gérées dans Real-Time CDP.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: fb8a17b8ea2ba1ddd64ceee7544f17058b43a943
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 42%

---

# Connexion Adobe Commerce {#adobe-commerce}

## Vue d’ensemble {#overview}

Le connecteur de destination [!DNL Adobe Commerce] vous permet de sélectionner une ou plusieurs audiences Real-Time CDP à activer dans votre compte [!DNL Adobe Commerce] pour offrir une expérience personnalisée dynamique à vos clientes et clients. Dans [!DNL Adobe Commerce], vous pouvez ensuite sélectionner ces audiences Real-Time CDP pour personnaliser les offres uniques du panier, telles que « Pour deux produits achetés, le troisième est offert ». Vous pouvez également afficher des bannières principales et modifier le prix des produits par le biais d’offres promotionnelles, toutes personnalisées en fonction des audiences Adobe Real-Time CDP.

## Conditions préalables {#prerequisites}

Ce connecteur est disponible dans le catalogue des destinations pour les clients qui ont acheté Real-Time CDP Prime ou Ultimate et Adobe Commerce.

Pour utiliser cette connexion de destination, vérifiez que vous avez accès aux éléments suivants :

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Grâce à l’accès à Developer Console, vous pouvez afficher le compte de service et les informations d’identification nécessaires pour [terminer la configuration](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html?lang=fr#configure-the-extension) de l’extension dans Adobe Commerce.
- [Adobe Commerce version 2.4.4 ou ultérieure](https://business.adobe.com/fr/products/commerce.html)

Dans Experience Platform, créez les éléments suivants :

- [Schéma](../../../xdm/schema/composition.md). Le schéma que vous créez représente les données que vous prévoyez d’ingérer à partir d’Adobe Commerce. [En savoir plus](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html?lang=fr) sur la création d’un schéma contenant des groupes de champs spécifiques à Commerce.
- [Jeu de données](../../../catalog/datasets/user-guide.md#create). Un jeu de données est une structure de stockage et de gestion pour une collecte de données. Vous créez ce jeu de données à partir du schéma que vous avez créé ci-dessus.
- [Flux de données](../../../datastreams/overview.md#create). Identifiant qui permet aux données de passer d’Adobe Experience Platform à d’autres produits DX d’Adobe. Cet identifiant doit être associé à un site web spécifique au sein de votre instance Adobe Commerce spécifique. Lorsque vous créez ce train de données, spécifiez le schéma XDM que vous avez créé ci-dessus.

Une fois les conditions préalables remplies, connectez-vous à la destination [!DNL Commerce].

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à la destination [!DNL Adobe Commerce] :

1. Dans l’interface d’[Experience Platform](https://experience.adobe.com/platform/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
1. Sélectionnez **[!UICONTROL Personalization]**.
1. Sélectionnez la destination Adobe Commerce à mettre en surbrillance, puis sélectionnez **[!UICONTROL Set up]**.
1. Suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

- **[!UICONTROL Name]** : renseignez le nom de votre choix pour cette destination.
- **[!UICONTROL Description]** : saisissez une description de la destination. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination. Ce champ est facultatif.
- **[!UICONTROL Integration alias]** : cette valeur est envoyée au SDK Web Experience Platform sous la forme d’un nom d’objet JSON.
- **[!UICONTROL Datastream ID]** : cela détermine le flux de données de collecte de données qui contient les audiences incluses dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Voir [Configurer un flux de données](../../../datastreams/overview.md) pour plus d’informations.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers la destination [!DNL Commerce] {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Lisez [Activer des profils et des audiences vers les destinations de requête de profil](../../ui/activate-edge-personalization-destinations.md) pour obtenir des instructions sur l’activation des audiences vers la destination [!DNL Commerce].

## Étapes suivantes dans [!DNL Adobe Commerce]

Maintenant que vous avez configuré la destination [!DNL Commerce] dans Experience Platform, vous devez installer l’extension [!DNL Audience Activation] dans [!DNL Commerce] et configurer le [!DNL Commerce Admin] pour importer les audiences Real-Time CDP que vous avez créées. Consultez la [[!DNL Commerce] documentation](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html?lang=fr) pour en savoir plus.

## Valider l’activation de l’audience dans Commerce {#exported-data}

Une fois les audiences Real-Time CDP activées sur votre compte [!DNL Adobe Commerce], elles sont disponibles lorsque vous accédez à la barre latérale _Admin_, puis à **[!UICONTROL Customers]** > **[!UICONTROL Real-Time CDP Audience]**.

![Tableau de bord des audiences Real-Time CDP](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
