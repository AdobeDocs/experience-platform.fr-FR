---
title: Gestion des expirations de jeux de données
description: Découvrez comment planifier l’expiration d’un jeu de données dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 769c872d67141b4973b29a492e72c23491e2d1ae
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 47%

---

# Gestion des expirations de jeux de données

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités de nettoyage de données d’Adobe Experience Platform sont uniquement disponibles pour les organisations qui ont acheté Healthcare Shield.

Le [[!UICONTROL Hygiène des données] workspace](./overview.md) dans l’interface utilisateur de Adobe Experience Platform vous permet de planifier l’expiration d’un jeu de données. Lorsqu’un jeu de données atteint sa date d’expiration, le lac de données, Identity Service et Real-time Customer Profile commencent des processus distincts pour supprimer le contenu du jeu de données de leurs services respectifs. Une fois les données supprimées des trois services, l’expiration est marquée comme terminée.

Ce document explique comment planifier et gérer les expirations de jeux de données dans l’interface utilisateur de Platform.

## Planification de l’expiration d’un jeu de données

Pour créer une requête, sélectionnez **[!UICONTROL Créer une requête]** dans la page principale de l’espace de travail.

![Image illustrant le bouton [!UICONTROL Créer une requête] sélectionné](../images/ui/ttl/create-request-button.png)

<!-- The request creation dialog appears. Under the **[!UICONTROL Action]** section, select **[!UICONTROL Dataset]** to update the available controls for dataset expiration scheduling-->

### Sélectionner une date et un jeu de données

La boîte de dialogue de création de requête s’affiche. Sous la section **[!UICONTROL Action]**, sélectionnez une date à laquelle vous souhaitez que le jeu de données soit supprimé. Vous pouvez saisir la date manuellement (au format `mm/dd/yyyy`) ou sélectionner l’icône de calendrier (![image de l’icône de calendrier](../images/ui/ttl/calendar-icon.png)) pour sélectionner la date dans une boîte de dialogue.

![Image montrant une date d’expiration en cours de définition pour le jeu de données](../images/ui/ttl/select-date.png)

Ensuite, sous **[!UICONTROL Détails du jeu de données]**, sélectionnez l’icône de base de données (![image de l’icône de base de données](../images/ui/ttl/database-icon.png)) pour ouvrir une boîte de dialogue de sélection de jeu de données. Sélectionnez un jeu de données dans la liste auquel appliquer l’expiration, puis sélectionnez **[!UICONTROL Terminé]**.

![Image illustrant un jeu de données sélectionné](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Seuls les jeux de données appartenant au sandbox actuel s’affichent.

### Envoyer la requête

Une fois que vous avez sélectionné un jeu de données et une date d’expiration, sélectionnez **[!UICONTROL Envoyer]**.

![Image illustrant le bouton [!UICONTROL Envoyer] sélectionné](../images/ui/ttl/submit.png)

Vous êtes invité à confirmer la date à laquelle le jeu de données sera supprimé. Sélectionnez **[!UICONTROL Envoyer]** pour continuer.

Une fois la requête soumise, un ordre de travail est créé et s’affiche dans l’onglet principal de l’espace de travail [!UICONTROL Nettoyage de données]. Ensuite, vous pouvez surveiller le statut de l’ordre de travail lors du traitement de la requête.

## Modification ou annulation d’une expiration de jeu de données

Pour modifier ou annuler l’expiration d’un jeu de données, sélectionnez **[!UICONTROL Jeu de données]** sur la page principale de l’espace de travail, puis sélectionnez l’expiration du jeu de données dans la liste.

Sur la page des détails de l’expiration du jeu de données, le rail de droite affiche les commandes permettant de modifier ou d’annuler la suppression planifiée.

## Étapes suivantes

Ce document explique comment planifier l’expiration des jeux de données dans l’interface utilisateur de l’Experience Platform. Pour savoir comment planifier l’expiration des jeux de données à l’aide de l’API Data Hygiene, reportez-vous à la section [guide de point d’expiration du jeu de données](../api/dataset-expiration.md).
