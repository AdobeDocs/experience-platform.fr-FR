---
keywords: connexion à la destination;connexion à la destination;connexion à la destination
title: Création d’une connexion de destination
type: Tutorial
description: Ce tutoriel répertorie les étapes de connexion à une destination dans Adobe Experience Platform.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 3%

---

# Création d’une connexion de destination

## Présentation {#overview}

Avant d’envoyer des données d’audience vers une destination, vous devez configurer une connexion à votre plateforme de destination. Cet article vous explique comment configurer une nouvelle destination à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Création d’une connexion de destination {#setup}

1. Accédez à **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]** .

   ![Page Catalogue](../assets/ui/connect-destinations/catalog.png)

1. Selon que vous disposez d’une connexion existante à votre destination, vous pouvez voir un bouton **[!UICONTROL Configurer]** ou **[!UICONTROL Activer les segments]** sur la carte de destination. Pour plus d’informations sur la différence entre **[!UICONTROL Activer les segments]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../ui/destinations-workspace.md#catalog) de la documentation de l’espace de travail de destination.

   Sélectionnez **[!UICONTROL Configurer]** ou **[!UICONTROL Activer les segments]**, en fonction du bouton disponible.

   ![Page Catalogue](../assets/ui/connect-destinations/set-up.png)

   ![Activation des segments](../assets/ui/connect-destinations/activate-segments.png)

1. Si vous avez sélectionné **[!UICONTROL Configurer]**, passez à l’étape suivante.

   Si vous avez sélectionné **[!UICONTROL Activer les segments]**, une liste des connexions de destination existantes s’affiche.

   Sélectionnez **[!UICONTROL Configurer une nouvelle destination]**.

   ![Configuration d’une nouvelle destination](../assets/ui/connect-destinations/configure-new-destination.png)

1. Saisissez les détails de la connexion à la plateforme de destination, puis sélectionnez **[!UICONTROL Se connecter à la destination]**.

   >[!NOTE]
   >
   >L’image ci-dessous est utilisée à titre d’illustration uniquement. Les détails de la connexion de destination varient selon les destinations. Pour plus d’informations sur les détails de connexion de votre destination, voir la section **Paramètres de connexion** de chaque page [catalogue de destination](../catalog/overview.md) (par exemple, [Correspondance client Google](..//catalog/advertising/google-customer-match.md#parameters)).

   ![Se connecter à la destination](../assets/ui/connect-destinations/connect-destination.png)

1. Sélectionnez **[!UICONTROL Suivant]**.

   ![Se connecter à la destination](../assets/ui/connect-destinations/next.png)

1. Sélectionnez les actions marketing applicables aux données que vous souhaitez exporter vers la destination. Les actions marketing indiquent l’intention pour laquelle les données seront exportées vers la destination. Vous pouvez effectuer un choix parmi des actions marketing définies par l’Adobe ou créer votre propre action marketing. Pour plus d’informations sur les actions marketing, consultez la [présentation des stratégies d’utilisation des données](../../data-governance/policies/overview.md) page.

   ![Sélection d’actions marketing](../assets/ui/connect-destinations/governance.png)

1. Sélectionnez **[!UICONTROL Enregistrer et quitter]** pour enregistrer la configuration de destination ou **[!UICONTROL Suivant]** pour accéder au [flux d’activation](activation-overview.md) des données d’audience.