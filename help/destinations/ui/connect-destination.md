---
keywords: connexion à la destination;connexion à la destination;connexion à la destination
title: Créer une connexion de destination
type: Tutorial
description: Ce tutoriel répertorie les étapes de connexion à une destination dans Adobe Experience Platform.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: b275621d9c6552327e0e55c00c8fcf0397088168
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 6%

---

# Créer une connexion de destination

## Présentation {#overview}

Avant d’envoyer des données d’audience vers une destination, vous devez configurer une connexion à votre plateforme de destination. Cet article vous explique comment configurer une nouvelle destination à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Créer une connexion de destination {#setup}

1. Accédez à **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, puis sélectionnez la variable **[!UICONTROL Catalogue]** .

   ![Page Catalogue](../assets/ui/connect-destinations/catalog.png)

1. Selon que vous disposez d’une connexion existante à votre destination, vous pouvez voir une **[!UICONTROL Configuration]** ou **[!UICONTROL Activation des segments]** sur la carte de destination. Pour plus d’informations sur la différence entre **[!UICONTROL Activation des segments]** et **[!UICONTROL Configuration]**, reportez-vous à la section [Catalogue](../ui/destinations-workspace.md#catalog) de la documentation de l’espace de travail de destination.

   Sélectionnez **[!UICONTROL Configuration]** ou **[!UICONTROL Activation des segments]**, selon le bouton disponible.

   ![Page Catalogue](../assets/ui/connect-destinations/set-up.png)

   ![Activation des segments](../assets/ui/connect-destinations/activate-segments.png)

1. Si vous avez sélectionné **[!UICONTROL Configuration]**, passez à l’étape suivante.

   Si vous avez sélectionné **[!UICONTROL Activation des segments]**, vous pouvez désormais voir une liste des connexions de destination existantes.

   Sélectionner **[!UICONTROL Configuration d’une nouvelle destination]**.

   ![Configuration d’une nouvelle destination](../assets/ui/connect-destinations/configure-new-destination.png)

1. Saisissez les détails de connexion de la plateforme de destination, puis sélectionnez **[!UICONTROL Se connecter à la destination]**.

   >[!NOTE]
   >
   >L’image ci-dessous est utilisée à titre d’illustration uniquement. Les détails de la connexion de destination varient selon les destinations. Pour plus d’informations sur les détails de connexion de votre destination, voir **Paramètres de connexion** de chaque section [catalogue de destination](../catalog/overview.md) page (par exemple, [Correspondance client Google](..//catalog/advertising/google-customer-match.md#parameters)).

   ![Se connecter à la destination](../assets/ui/connect-destinations/connect-destination.png)

1. (Facultatif) Sélectionnez les alertes de flux de données de destination auxquelles vous souhaitez vous abonner. Vous pouvez vous abonner à des alertes lors de la création d’un flux de données pour recevoir des messages d’alerte concernant l’état, la réussite ou l’échec de votre exécution de flux. Voir [Abonner aux alertes de destination contextuelles](alerts.md) pour obtenir des informations détaillées sur les alertes de flux de données de destination.

   ![Image de l’interface utilisateur présentant les options d’abonnement aux alertes de destination contextuelles](../assets/ui/connect-destinations/subscribe-to-alerts.png)

1. Sélectionnez **[!UICONTROL Suivant]**.

   ![Se connecter à la destination](../assets/ui/connect-destinations/next.png)

1. Sélectionnez les actions marketing applicables aux données que vous souhaitez exporter vers la destination. Les actions marketing indiquent l’intention pour laquelle les données seront exportées vers la destination. Vous pouvez effectuer un choix parmi des actions marketing définies par l’Adobe ou créer votre propre action marketing. Pour plus d’informations sur les actions marketing, voir [présentation des stratégies d’utilisation des données](../../data-governance/policies/overview.md) page.

   ![Sélection d’actions marketing](../assets/ui/connect-destinations/governance.png)

1. Sélectionner **[!UICONTROL Enregistrer et quitter]** pour enregistrer la configuration de destination, ou sélectionnez **[!UICONTROL Suivant]** pour passer aux données d’audience [flux d’activation](activation-overview.md).