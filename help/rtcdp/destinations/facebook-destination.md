---
title: Destination Facebook
seo-title: Destination Facebook
description: Activez les  de vos campagnes Facebook pour  ciblage, personnalisation et suppression des  sur la base des courriers électroniques hachés.
seo-description: Activez les  de vos campagnes Facebook pour  ciblage, personnalisation et suppression des  sur la base des courriers électroniques hachés.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (bêta) Destination Facebook

>[!IMPORTANT]
>
>La destination Facebook du CDP en temps réel d’Adobe est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

## Présentation

Activez les  de vos campagnes Facebook pour  ciblage, personnalisation et suppression des  sur la base des courriers électroniques hachés.

## Spécifications de la destination

###  type de

Exportation de segments : vous exportez tous les membres d’un segment ( ) avec leurs identifiants (nom, numéro de téléphone, etc.). utilisé dans la destination Facebook

## Conditions préalables

Avant d’envoyer vos segments de   à [!DNL Facebook], assurez-vous de respecter les conditions suivantes :

1. L’autorisation [!DNL Facebook] Gérer les campagnes **doit être activée pour votre compte** utilisateur pour le compte publicitaire que vous prévoyez d’utiliser.
2. Ajouter le compte **Adobe Experience Cloud** en tant que partenaire publicitaire dans votre [!DNL Facebook Ad Account]entreprise. Utilisez `business ID=206617933627973`. Pour plus d’informations, consultez [Ajouter Partenaires de votre gestionnaire](https://www.facebook.com/business/help/1717412048538897) d’entreprise.
   >[!IMPORTANT]
   > Lors de la configuration des autorisations pour Adobe Experience Cloud, vous devez activer l’autorisation **Gérer les campagnes** . Ceci est nécessaire pour l’ [!DNL Adobe Real-time CDP] intégration.
3. Lisez et signez les [!DNL Facebook Custom Audiences] Conditions d&#39;utilisation. Pour ce faire, allez à `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, où `accountID` est votre [!DNL Facebook Ad Account ID].


## Se connecter à la destination

Pour connecter la destination Facebook, voir Processus [d’authentification des destinations réseau](/help/rtcdp/destinations/social-network-destinations-workflow.md)Social.


## Activer les segments sur Facebook

For instructions on how to activate segments to Facebook, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).