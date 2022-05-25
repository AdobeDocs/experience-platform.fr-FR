---
title: Gestion des TTL de jeux de données
description: Découvrez comment planifier une heure d’activation (TTL) pour un jeu de données dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Gestion des TTL de jeux de données

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités d’hygiène des données de Adobe Experience Platform ne sont disponibles que pour les organisations qui ont acheté Adobe Shield pour les soins de santé.

Le [[!UICONTROL Hygiène des données] workspace](./overview.md) dans l’interface utilisateur de Adobe Experience Platform, vous permet de planifier une durée de vie (TTL) pour un jeu de données.

Ce document explique comment planifier et gérer des TTL de jeux de données dans l’interface utilisateur de Platform.

## Planification d’un TTL

Pour créer une requête, sélectionnez **[!UICONTROL Créer une requête]** de la page principale de l’espace de travail.

![Image montrant le [!UICONTROL Créer une requête] bouton sélectionné](../images/ui/ttl/create-request-button.png)

La boîte de dialogue de création de requête s’affiche. Sous , **[!UICONTROL Action]** , sélectionnez **[!UICONTROL Jeu de données]** pour mettre à jour les commandes disponibles pour la planification TTL.

![Image montrant le [!UICONTROL Jeu de données] option sélectionnée](../images/ui/ttl/create-request-button.png)

### Sélection d’une date et d’un jeu de données

Sous , **[!UICONTROL Action]** , sélectionnez une date à laquelle le jeu de données doit être supprimé. Vous pouvez saisir la date manuellement (au format `mm/dd/yyyy`) ou sélectionnez l’icône de calendrier (![Image de l&#39;icône du calendrier](../images/ui/ttl/calendar-icon.png)) pour sélectionner la date dans une boîte de dialogue.

![Image montrant une date d’expiration définie pour le délai d’activation](../images/ui/ttl/select-date.png)

Ensuite, sous **[!UICONTROL Détails du jeu de données]**, sélectionnez l’icône de base de données (![Image de l&#39;icône de la base de données](../images/ui/ttl/database-icon.png)) pour ouvrir une boîte de dialogue de sélection de jeux de données. Sélectionnez un jeu de données dans la liste auquel appliquer le délai d’activation, puis sélectionnez **[!UICONTROL Terminé]**.

![Image montrant un jeu de données sélectionné](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Seuls les jeux de données appartenant à l’environnement de test actif s’affichent.

### Envoyer la requête

Une fois que vous avez sélectionné un jeu de données et une date TTL, sélectionnez **[!UICONTROL Envoyer]**.

![Image montrant le [!UICONTROL Envoyer] bouton sélectionné](../images/ui/ttl/select-dataset.png)

Vous êtes invité à confirmer la date à laquelle le jeu de données sera supprimé. Sélectionner **[!UICONTROL Envoyer]** pour continuer.

Une fois la demande envoyée, un ordre de travail est créé et s’affiche sur la page [!UICONTROL Consommateur] de l’onglet [!UICONTROL Hygiène des données] workspace. À partir de là, vous pouvez surveiller l’état de l’ordre de travail lors du traitement de la requête.

## Modification ou annulation d’un TTL

Pour modifier ou annuler une durée de vie, sélectionnez **[!UICONTROL Jeu de données]** sur la page principale de l’espace de travail, puis sélectionnez TTL dans la liste.

Sur la page des détails de la durée de vie, le rail de droite affiche les commandes permettant de modifier ou d’annuler la suppression planifiée.

## Étapes suivantes

Ce document explique comment planifier des TTL de jeux de données dans l’interface utilisateur Experience Platform. Pour plus d’informations sur l’exécution d’autres tâches d’hygiène des données dans l’interface utilisateur, reportez-vous à la section [Présentation de l’interface utilisateur de l’hygiène des données](./overview.md).

Pour savoir comment planifier des TTL de jeux de données à l’aide de l’API Data Hygiene, reportez-vous à la section [guide de point d’entrée TTL du jeu de données](../api/ttl.md).
