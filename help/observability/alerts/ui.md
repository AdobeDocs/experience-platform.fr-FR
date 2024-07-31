---
keywords: Experience Platform;accueil;rubriques populaires;période
title: Guide de lʼinterface utilisateur des alertes
description: Découvrez comment gérer les alertes dans lʼinterface utilisateur dʼExperience Platform.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: 9004a2203996f0fd64833a03f211232ebf14e3e4
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 40%

---

# Guide de lʼinterface utilisateur des alertes

Lʼinterface utilisateur dʼAdobe Experience Platform vous permet de consulter lʼhistorique des alertes reçues en fonction des mesures affichées par Adobe Experience Platform Observability Insights. Lʼinterface utilisateur vous permet également dʼafficher, dʼactiver, de désactiver et de vous abonner aux règles dʼalerte disponibles.

>[!NOTE]
>
>Pour démarrer avec les alertes dans Experience Platform, consultez la [Présentation des alertes](./overview.md).

Commencez par sélectionner **[!UICONTROL Alertes]** dans le volet de navigation de gauche.

![ La page Alertes surlignant les [!UICONTROL alertes] dans le volet de navigation de gauche.](../images/alerts/ui/workspace.png)

## Gestion des règles dʼalerte

Lʼonglet **[!UICONTROL Parcourir]** répertorie les règles disponibles susceptibles de déclencher une alerte.

![ Une liste des alertes disponibles s&#39;affiche dans l&#39;onglet [!UICONTROL Parcourir].](../images/alerts/ui/rules.png)

Sélectionnez une règle dans la liste pour afficher sa description et ses paramètres de configuration dans le rail de droite, y compris le seuil et la gravité.

![Une règle d’alerte mise en surbrillance pour afficher les détails dans le rail de droite.](../images/alerts/ui/rule-details.png)

Sélectionnez les points de suspension (**...**) en regard du nom dʼune règle pour afficher une liste déroulante avec les commandes suivantes : activation ou désactivation de lʼalerte (selon son statut actuel), abonnement ou désabonnement aux notifications par e-mail de lʼalerte.

![Les ellipses sélectionnées affichent le menu déroulant.](../images/alerts/ui/disable-subscribe.png)

## Gérer les abonnés aux alertes

>[!NOTE]
>
> Pour attribuer une alerte à un identifiant utilisateur Adobe, à une adresse électronique externe ou à une liste de groupes de messagerie, vous devez être un administrateur.

Lʼonglet **[!UICONTROL Parcourir]** répertorie les règles disponibles susceptibles de déclencher une alerte.

![ Liste des règles d&#39;alerte disponibles affichées dans l&#39;onglet [!UICONTROL Parcourir].](../images/alerts/ui/rules.png)

Sélectionnez les points de suspension (**...**) en regard du nom d’une règle. Une liste déroulante affiche les commandes. Sélectionnez **[!UICONTROL Gérer les abonnés aux alertes]**.

![Sélectionnez les ellipses pour afficher le menu déroulant. L&#39;option [!UICONTROL Gérer les abonnés aux alertes] est mise en surbrillance.](../images/alerts/ui/manage-alert-subscribers.png)

La page [!UICONTROL Gérer les abonnés aux alertes] s&#39;affiche. Pour attribuer des notifications à des utilisateurs spécifiques, saisissez leur identifiant utilisateur Adobe, leur adresse électronique externe ou une liste de groupes de messagerie, puis appuyez sur Entrée.

>[!NOTE]
>
>Pour envoyer cette notification à plusieurs utilisateurs à la fois, fournissez une liste d’ID utilisateur ou d’adresses électroniques séparés par des virgules.

![ La page gérer les abonnés aux alertes qui affiche les adresses électroniques saisies.](../images/alerts/ui/manage-alert-add-email.png)

Les adresses électroniques apparaissent dans la liste des abonnés actuels. Sélectionnez **[!UICONTROL Mettre à jour]**.

![ La page de gestion des abonnés aux alertes met en surbrillance les abonnés et [!UICONTROL Mettre à jour].](../images/alerts/ui/manage-alert-subscribers-added-email.png)

Vous avez correctement ajouté des utilisateurs à votre liste de notifications d’alertes. Les utilisateurs envoyés recevront désormais des notifications par courrier électronique pour cette alerte, comme illustré dans l’image ci-dessous.

![Exemple de courrier électronique de notification d’alerte reçue.](../images/alerts/ui/manage-alert-subscribers-email.png)

## Activation des alertes par email

Les notifications d&#39;alerte peuvent être diffusées directement à votre email.

Sélectionnez l’icône représentant une cloche (![icône représentant une cloche](/help/images/icons/bell.png)) située dans le ruban supérieur à droite pour afficher les notifications et les annonces. Dans la liste déroulante qui s’affiche, sélectionnez l’icône représentant un engrenage (![icône représentant un engrenage](/help/images/icons/settings.png)) pour accéder à la page des préférences de l’Experience Cloud.

![ Une liste d’alertes affichée qui met en surbrillance l’icône représentant une cloche et l’icône représentant un engrenage.](../images/alerts/ui/edit-preferences.png)

La page **Profil** s’affiche. Sélectionnez les **[!UICONTROL notifications]** dans le volet de navigation de gauche pour accéder aux préférences d’alertes par e-mail.

![ La page Profil qui surligne les [!UICONTROL notifications] dans le volet de navigation de gauche.](../images/alerts/ui/profile.png)

Accédez à la section **Emails** au bas de la page et sélectionnez **[!UICONTROL Notifications instantanées]**

![La section Emails mise en surbrillance dans la page Profil.](../images/alerts/ui/notifications.png)

Toutes les alertes auxquelles vous êtes abonné seront désormais envoyées à l’adresse électronique connectée à votre compte Adobe ID.

## Affichage de lʼhistorique des alertes

Lʼonglet **[!UICONTROL Historique]** affiche lʼhistorique des alertes reçues pour votre organisation, y compris la règle qui a déclenché lʼalerte, la date de déclenchement et la date de résolution (le cas échéant).

![Une liste des alertes reçues s&#39;affiche dans l&#39;onglet [!UICONTROL Historique].](../images/alerts/ui/history.png)

Sélectionnez une alerte répertoriée pour afficher des détails supplémentaires dans le rail de droite, y compris un bref résumé de lʼévénement qui a déclenché lʼalerte.

![Une alerte mise en surbrillance pour afficher les détails dans le rail de droite.](../images/alerts/ui/history-details.png)

## Étapes suivantes

Ce document fournit un aperçu de la manière dʼafficher et de gérer les alertes dans lʼinterface utilisateur de Platform. Pour plus dʼinformations sur les fonctionnalités du service, consultez la présentation dʼ[Observability Insights](../home.md).
