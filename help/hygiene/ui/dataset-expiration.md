---
title: Gérer des expirations de jeux de données
description: Découvrez comment planifier l’expiration d’un jeu de données dans l’interface utilisateur d’Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 6453ec6c98d90566449edaa0804ada260ae12bf6
workflow-type: ht
source-wordcount: '535'
ht-degree: 100%

---

# Gérer des expirations de jeux de données

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités d’hygiène des données d’Adobe Experience Platform sont uniquement disponibles pour les organisations qui ont acheté **Adobe Healthcare Shield** ou **Adobe Privacy &amp; Security Shield**.

L’espace de travail [[!UICONTROL Hygiène des données]](./overview.md) dans l’interface utilisateur d’Adobe Experience Platform vous permet de planifier l’expiration des jeux de données. Lorsqu’un jeu de données atteint sa date d’expiration, le lac de données, le service d’identités et le profil client en temps réel lancent des processus distincts pour supprimer le contenu du jeu de données de leurs services respectifs. Une fois les données supprimées des trois services, l’expiration est marquée comme étant terminée.

>[!WARNING]
>
>Si un jeu de données est défini pour expirer, vous devez modifier manuellement les flux de données susceptibles d’ingérer des données dans ce jeu, afin que vos workflows en aval ne soient pas affectés négativement.

Ce document explique comment planifier et gérer des expirations de jeux de données dans l’interface utilisateur de Platform.

## Planifier l’expiration d’un jeu de données

Pour créer une requête, sélectionnez **[!UICONTROL Créer une requête]** dans la page principale de l’espace de travail.

![Image illustrant le bouton [!UICONTROL Créer une requête] sélectionné](../images/ui/ttl/create-request-button.png).

La boîte de dialogue de création de requête s’affiche. Dans la section **[!UICONTROL Action demandée]**, sélectionnez **[!UICONTROL Supprimer le jeu de données]** pour mettre à jour les commandes disponibles pour la planification de l’expiration des jeux de données.

![Image illustrant le bouton [!UICONTROL Créer une requête] sélectionné](../images/ui/ttl/dataset-selected.png)

### Sélectionner une date et un jeu de données

La boîte de dialogue de création de requête s’affiche. Dans la section **[!UICONTROL Action demandée]**, sélectionnez une date à laquelle vous souhaitez que le jeu de données soit supprimé. Vous pouvez saisir la date manuellement (au format `mm/dd/yyyy`) ou sélectionner l’icône de calendrier (![image de l’icône de calendrier](../images/ui/ttl/calendar-icon.png)) pour sélectionner la date dans une boîte de dialogue.

![Image illustrant la définition d’une date d’expiration pour un jeu de données](../images/ui/ttl/select-date.png)

Ensuite, sous **[!UICONTROL Détails du jeu de données]**, sélectionnez l’icône de base de données (![image de l’icône de base de données](../images/ui/ttl/database-icon.png)) pour ouvrir une boîte de dialogue de sélection de jeu de données. Dans la liste, sélectionnez un jeu de données auquel appliquer l’expiration, puis cliquez sur **[!UICONTROL Terminé]**.

![Image illustrant un jeu de données sélectionné](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Seuls les jeux de données appartenant au sandbox actuel s’affichent.

### Envoyer la requête

La section [!UICONTROL Détails du jeu de données] est renseignée afin d’inclure l’identité principale et le schéma du jeu de données sélectionné. Dans la section **[!UICONTROL Paramètres de la requête]**, saisissez un nom et une description facultative pour la requête, suivis d’**[!UICONTROL Envoyer]**.

![Image illustrant le bouton [!UICONTROL Envoyer] sélectionné](../images/ui/ttl/submit.png)

Vous êtes invité à confirmer la date à laquelle le jeu de données sera supprimé. Sélectionnez **[!UICONTROL Envoyer]** pour continuer.

Une fois la requête soumise, un ordre de travail est créé et s’affiche dans l’onglet principal de l’espace de travail [!UICONTROL Nettoyage de données]. Ensuite, vous pouvez surveiller le statut de l’ordre de travail lors du traitement de la requête.

>[!NOTE]
>
>Consultez la section de présentation sur [la chronologie et la transparence](../home.md#dataset-expiration-transparency) pour plus d’informations sur le traitement des expirations des jeux de données une fois qu’elles sont exécutées.

## Modifier ou annuler l’expiration d’un jeu de données

Pour modifier ou annuler l’expiration d’un jeu de données, sélectionnez **[!UICONTROL Jeu de données]** dans la page principale de l’espace de travail, puis cliquez sur l’expiration du jeu de données dans la liste.

Dans la page des détails de l’expiration du jeu de données, le rail de droite affiche les commandes permettant de modifier ou d’annuler la suppression planifiée.

## Étapes suivantes

Ce document explique comment planifier des expirations de jeux de données dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur l’exécution d’autres tâches d’hygiène de données dans l’interface utilisateur, consultez la [Présentation de l’interface utilisateur de l’hygiène de données](./overview.md).

Pour découvrir comment planifier des expirations de jeux de données à l’aide de l’API Data Hygiene, consultez le [guide de point d’entrée d’expiration de jeu de données](../api/dataset-expiration.md).
