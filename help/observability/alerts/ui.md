---
keywords: Experience Platform;accueil;rubriques populaires;période
title: Guide de lʼinterface utilisateur des alertes
description: Découvrez comment gérer les alertes dans lʼinterface utilisateur dʼExperience Platform.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: 57261ca37bf10e394f47ea4bb3c01856a18b197d
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 37%

---

# Guide de lʼinterface utilisateur des alertes

Lʼinterface utilisateur dʼAdobe Experience Platform vous permet de consulter lʼhistorique des alertes reçues en fonction des mesures affichées par Adobe Experience Platform Observability Insights. Lʼinterface utilisateur vous permet également dʼafficher, dʼactiver, de désactiver et de vous abonner aux règles dʼalerte disponibles.

>[!NOTE]
>
>Pour démarrer avec les alertes dans Experience Platform, consultez la [Présentation des alertes](./overview.md).

Commencez par sélectionner **[!UICONTROL Alertes]** dans le volet de navigation de gauche.

![Page des alertes mettant en surbrillance [!UICONTROL Alertes] dans le volet de navigation de gauche.](../images/alerts/ui/workspace.png)

## Gestion des règles dʼalerte {#manage-rules}

Lʼonglet **[!UICONTROL Parcourir]** répertorie les règles disponibles susceptibles de déclencher une alerte.

![Une liste des alertes disponibles s’affiche dans l’onglet [!UICONTROL Parcourir].](../images/alerts/ui/rules.png)

Sélectionnez une règle dans la liste pour afficher sa description et ses paramètres de configuration dans le rail de droite, y compris le seuil et la gravité.

![Une règle d’alerte mise en surbrillance, affichant les détails dans le rail de droite.](../images/alerts/ui/rule-details.png)

Sélectionnez les points de suspension (**...**) en regard du nom dʼune règle pour afficher une liste déroulante avec les commandes suivantes : activation ou désactivation de lʼalerte (selon son statut actuel), abonnement ou désabonnement aux notifications par e-mail de lʼalerte.

![Les points de suspension sélectionnés affichent le menu déroulant.](../images/alerts/ui/disable-subscribe.png)

## Gérer les abonnés aux alertes {#manage-subscribers}

>[!NOTE]
>
> Pour attribuer une alerte à un ID utilisateur Adobe, à une adresse e-mail externe ou à une liste de groupes d’e-mails, vous devez être administrateur.

Lʼonglet **[!UICONTROL Parcourir]** répertorie les règles disponibles susceptibles de déclencher une alerte.

![Liste des règles d’alerte disponibles affichée dans l’onglet [!UICONTROL Parcourir].](../images/alerts/ui/rules.png)

Sélectionnez les points de suspension (**...**) à côté du nom d’une règle. Une liste déroulante affiche les contrôles. Sélectionnez **[!UICONTROL Gérer les abonnés aux alertes]**.

![Sélectionnez les points de suspension pour afficher le menu déroulant. L’option [!UICONTROL &#x200B; Gérer les abonnés aux alertes &#x200B;] est mise en surbrillance](../images/alerts/ui/manage-alert-subscribers.png).

La page [!UICONTROL Gérer les abonnés aux alertes] s’affiche. Pour envoyer des notifications à des utilisateurs spécifiques, saisissez leur ID utilisateur Adobe, leur adresse e-mail externe ou une liste de groupes d’e-mails, puis appuyez sur Entrée.

>[!NOTE]
>
>Pour envoyer cet avis à plusieurs utilisateurs à la fois, fournissez une liste d&#39;ID utilisateur ou d&#39;adresses électroniques séparées par des virgules.

![Page Gérer les abonnés aux alertes affichant les adresses e-mail saisies.](../images/alerts/ui/manage-alert-add-email.png)

Les adresses e-mail s’affichent dans la liste des abonnés actuels. Sélectionnez **[!UICONTROL Mettre à jour]**.

![Page Gérer les abonnés aux alertes mettant en surbrillance les abonnés et [!UICONTROL Mettre à jour].](../images/alerts/ui/manage-alert-subscribers-added-email.png)

Les utilisateurs ont été ajoutés à votre liste de notifications d’alerte. Les utilisateurs envoyés recevront désormais des notifications par e-mail pour cette alerte, comme illustré dans l’image ci-dessous.

![Exemple d’e-mail de la notification d’alerte reçue.](../images/alerts/ui/manage-alert-subscribers-email.png)

## Activer les alertes par e-mail {#enable-email}

Les notifications d’alerte peuvent être diffusées directement par e-mail.

Sélectionnez l’icône représentant une cloche (![icône représentant une cloche](/help/images/icons/bell.png)) située dans le ruban supérieur droit pour afficher les notifications et les annonces. Dans la liste déroulante qui s’affiche, sélectionnez l’icône représentant un engrenage (![icône représentant un engrenage](/help/images/icons/settings.png)) pour accéder à la page des préférences d’Experience Cloud.

![Liste des alertes affichées mettant en surbrillance l’icône représentant une cloche et l’icône représentant un engrenage.](../images/alerts/ui/edit-preferences.png)

La page **Profil** s’affiche. Sélectionnez **[!UICONTROL Notifications]** dans le volet de navigation de gauche pour accéder aux préférences des alertes par e-mail.

![Page de profil mettant en surbrillance [!UICONTROL Notifications] dans le volet de navigation de gauche.](../images/alerts/ui/profile.png)

Faites défiler la page jusqu’à la section **E-mails** en bas de la page, puis sélectionnez **[!UICONTROL Notifications instantanées]**

![la section E-mails mise en surbrillance dans la page du profil.](../images/alerts/ui/notifications.png)

Toutes les alertes auxquelles vous êtes abonné sont désormais envoyées à l’adresse e-mail connectée à votre compte Adobe ID.

## Personnaliser le seuil d’alerte {#alert-threshold}

Les seuils d’alerte peuvent être personnalisés pour les types d’alerte suivants :

| Type d’alerte | Paramètre personnalisé |
|---|---|
| Retard de la tâche relative aux segments | Seuil de retard |
| Retard d’export du segment | Seuil de retard |
| Délai d’exécution du flux de destinations | Seuil de retard |
| Retard d’exécution du flux du service d’identités | Seuil de retard |
| Retard d’exécution du flux de profils | Seuil de retard |
| Taux d’échec d’ingestion de diffusion de profil dépassé | Seuil d’erreur |
| Taux d’omission de l’ingestion en flux continu du profil dépassé | Seuil d’erreur |
| Retard dans l’exécution du flux de sources | Seuil de retard |
| Taux d’erreurs d’ingestion de sources dépassé | Seuil d’erreur |
| Retard d’exécution de requête | Seuil de retard |
| Taux d’activations ignorées dépassé | Seuil d’erreur |

Sélectionnez les points de suspension (**...**) à côté du nom d’une règle. Une liste déroulante affiche les contrôles. Sélectionnez **[!UICONTROL Modifier]**.

![L’option [!UICONTROL Modifier] est mise en surbrillance pour la règle sélectionnée.](../images/alerts/ui/threshold-edit.png)

La page **[!UICONTROL Personnaliser l’alerte]** s’affiche. Mettez à jour le seuil sur les minutes souhaitées, puis sélectionnez **[!UICONTROL Confirmer]**.

![Page Personnaliser l’alerte mettant en surbrillance les options [!UICONTROL Seuil] et [!UICONTROL Confirmer].](../images/alerts/ui/threshold-update.png)

Vous revenez alors à la page **[!UICONTROL Alertes]**. Pour afficher les paramètres de seuil de l’alerte, sélectionnez la règle dans la liste. Vous pouvez voir les paramètres de seuil de l’alerte dans le rail de droite, y compris des détails tels que le statut et la gravité.

![Alerte mise en surbrillance, affichant des détails dans le rail de droite et mettant en surbrillance [!UICONTROL Seuil].](../images/alerts/ui/threshold-view.png)

## Affichage de lʼhistorique des alertes {#alert-history}

Lʼonglet **[!UICONTROL Historique]** affiche lʼhistorique des alertes reçues pour votre organisation, y compris la règle qui a déclenché lʼalerte, la date de déclenchement et la date de résolution (le cas échéant).

![Une liste des alertes reçues s’affiche dans l’onglet [!UICONTROL Historique].](../images/alerts/ui/history.png)

Sélectionnez une alerte répertoriée pour afficher des détails supplémentaires dans le rail de droite, y compris un bref résumé de lʼévénement qui a déclenché lʼalerte.

![Une alerte mise en surbrillance, affichant des détails dans le rail de droite.](../images/alerts/ui/history-details.png)

## Étapes suivantes

Ce document présente un aperçu de l’affichage et de la gestion des alertes dans l’interface utilisateur d’Experience Platform. Pour plus dʼinformations sur les fonctionnalités du service, consultez la présentation dʼ[Observability Insights](../home.md).
