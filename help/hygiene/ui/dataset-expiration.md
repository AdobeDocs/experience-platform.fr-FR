---
title: Gérer les expirations de jeux de données
description: Découvrez comment planifier l’expiration d’un jeu de données dans l’interface utilisateur d’Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: d93036c26e9f1b86a82f4da4cce6f9e8152e3542
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 76%

---

# Gérer des expirations de jeux de données

>[!IMPORTANT]
>
>Actuellement, seules les organisations qui ont acheté l’Adobe Healthcare Shield disposent des capacités d’hygiène des données dans Adobe Experience Platform.

Le [[!UICONTROL Hygiène des données] workspace](./overview.md) dans l’interface utilisateur de Adobe Experience Platform vous permet de planifier des expirations pour les jeux de données. Lorsqu’un jeu de données atteint sa date d’expiration, le lac de données, le service d’identités et le profil client en temps réel lancent des processus distincts pour supprimer le contenu du jeu de données de leurs services respectifs. Une fois les données supprimées des trois services, l’expiration est marquée comme étant terminée.

>[!WARNING]
>
>Si un jeu de données est défini pour expirer, vous devez modifier manuellement les flux de données susceptibles d’ingérer des données dans ce jeu, afin que vos workflows en aval ne soient pas affectés négativement.

Ce document explique comment planifier et gérer des expirations de jeux de données dans l’interface utilisateur de Platform.

## Planifier l’expiration d’un jeu de données

Pour créer une requête, sélectionnez **[!UICONTROL Créer une requête]** dans la page principale de l’espace de travail.

![Image illustrant le bouton [!UICONTROL Créer une requête] sélectionné](../images/ui/ttl/create-request-button.png).

La boîte de dialogue de création de requête s’affiche. Sous , **[!UICONTROL Action requise]** , sélectionnez **[!UICONTROL Supprimer un jeu de données]** pour mettre à jour les commandes disponibles pour la planification de l’expiration du jeu de données.

![Image illustrant le bouton [!UICONTROL Créer une requête] sélectionné](../images/ui/ttl/dataset-selected.png)

### Sélectionner une date et un jeu de données

La boîte de dialogue de création de requête s’affiche. Sous , **[!UICONTROL Action requise]** , sélectionnez une date à laquelle le jeu de données doit être supprimé. Vous pouvez saisir la date manuellement (au format `mm/dd/yyyy`) ou sélectionner l’icône de calendrier (![image de l’icône de calendrier](../images/ui/ttl/calendar-icon.png)) pour sélectionner la date dans une boîte de dialogue.

![Image illustrant la définition d’une date d’expiration pour un jeu de données](../images/ui/ttl/select-date.png)

Ensuite, sous **[!UICONTROL Détails du jeu de données]**, sélectionnez l’icône de base de données (![image de l’icône de base de données](../images/ui/ttl/database-icon.png)) pour ouvrir une boîte de dialogue de sélection de jeu de données. Dans la liste, sélectionnez un jeu de données auquel appliquer l’expiration, puis cliquez sur **[!UICONTROL Terminé]**.

![Image illustrant un jeu de données sélectionné](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Seuls les jeux de données appartenant au sandbox actuel s’affichent.

### Envoyer la requête

Le [!UICONTROL Détails du jeu de données] est renseignée afin d’inclure l’identité et le schéma Principaux du jeu de données sélectionné. Sous **[!UICONTROL Paramètres de requête]**, saisissez un nom et une description facultative pour la requête, suivie de **[!UICONTROL Envoyer]**.

![Image illustrant le bouton [!UICONTROL Envoyer] sélectionné](../images/ui/ttl/submit.png)

Vous êtes invité à confirmer la date à laquelle le jeu de données sera supprimé. Sélectionnez **[!UICONTROL Envoyer]** pour continuer.

Une fois la requête soumise, un ordre de travail est créé et s’affiche dans l’onglet principal de l’espace de travail [!UICONTROL Nettoyage de données]. Ensuite, vous pouvez surveiller le statut de l’ordre de travail lors du traitement de la requête.

>[!NOTE]
>
>Consultez la section de présentation sur [calendrier et transparence](../home.md#dataset-expiration-transparency) pour plus d’informations sur le traitement des expirations de jeux de données une fois qu’elles sont exécutées.

## Modifier ou annuler l’expiration d’un jeu de données

Pour modifier ou annuler l’expiration d’un jeu de données, sélectionnez **[!UICONTROL Jeu de données]** dans la page principale de l’espace de travail, puis cliquez sur l’expiration du jeu de données dans la liste.

Dans la page des détails de l’expiration du jeu de données, le rail de droite affiche les commandes permettant de modifier ou d’annuler la suppression planifiée.

## Étapes suivantes

Ce document explique comment planifier des expirations de jeux de données dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur l’exécution d’autres tâches de nettoyage de données dans l’interface utilisateur, consultez la [Présentation de l’interface utilisateur de nettoyage de données](./overview.md).

Pour découvrir comment planifier des expirations de jeux de données à l’aide de l’API Data Hygiene, consultez le [guide de point d’entrée d’expiration de jeu de données](../api/dataset-expiration.md).
