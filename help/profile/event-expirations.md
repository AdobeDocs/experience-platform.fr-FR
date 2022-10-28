---
keywords: Experience Platform;accueil;rubriques populaires;jeu de données;Jeu de donnéesvdurée de vie;ttl;durée-de-vie;
solution: Experience Platform
title: Expirations des événements d’expérience
description: Ce document fournit des instructions générales sur la configuration des délais d’expiration pour des événements d’expérience individuels dans un jeu de données Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 2%

---

# Expiration des événements d’expérience

Dans Adobe Experience Platform, vous pouvez configurer des délais d’expiration pour tous les événements d’expérience ingérés dans un jeu de données activé pour [Real-time Customer Profile](./home.md). Vous pouvez ainsi supprimer automatiquement des données du lac de données et de la banque de profils qui ne sont plus valides ni utiles pour vos cas d’utilisation.

Les expirations d’événements d’expérience ne peuvent pas être configurées via l’interface utilisateur de Platform ou les API. Vous devez plutôt contacter l’assistance afin d’activer les expirations d’événements d’expérience sur vos jeux de données requis.

>[!IMPORTANT]
>
>Les expirations d’événements d’expérience ne doivent pas être confondues avec les expirations de jeux de données, qui suppriment l’ensemble du jeu de données une fois la date d’expiration atteinte. Ils sont configurés manuellement via [Hygiène des données Adobe Experience Platform](../hygiene/home.md).

## Processus d’expiration automatisé

Une fois que les expirations d’événement d’expérience ont été activées sur un jeu de données activé pour Profile, Platform applique automatiquement les valeurs d’expiration pour chaque événement capturé dans un processus en deux étapes :

1. La valeur d’expiration est appliquée à toutes les nouvelles données ingérées dans le jeu de données au moment de l’ingestion.
1. La valeur d’expiration de toutes les données existantes du jeu de données est rétroactivement appliquée en tant que tâche de système de renvoi unique. Une fois que la valeur d’expiration a été placée sur le jeu de données, les événements plus anciens que la valeur d’expiration sont immédiatement supprimés dès que la tâche système s’exécute. Tous les autres événements seront ignorés dès qu’ils atteignent leurs valeurs d’expiration à partir de l’horodatage de l’événement.

>[!WARNING]
>
>Une fois appliquée, toutes les données antérieures au nombre de jours attribué par la valeur d’expiration sont **supprimé définitivement** et ne peuvent pas être restaurés.

Par exemple, si vous appliquez une valeur d’expiration de 30 jours le 15 mai, les étapes suivantes se produisent :

1. Tous les nouveaux événements reçoivent une valeur d’expiration de 30 jours appliquée lorsqu’ils sont ingérés.
1. Tous les événements existants dont l’horodatage est antérieur au 15 avril sont immédiatement supprimés avec la tâche système.
1. Tous les événements existants dont l’horodatage est supérieur au 15 avril ont une valeur d’expiration 30 jours après leur horodatage d’événement. Ainsi, si un événement a un horodatage du 18 avril, il est supprimé 30 jours après la date de cet horodatage, qui serait le 18 mai.

## Effets sur la segmentation

Vous devez vous assurer que les intervalles de recherche en amont de vos segments se trouvent dans les limites d’expiration de leurs jeux de données dépendants afin de conserver des résultats précis. Par exemple, si vous appliquez une valeur d’expiration de 30 jours et que vous disposez d’un segment qui tente d’afficher les données d’il y a jusqu’à 45 jours, l’audience résultante sera probablement inexacte.

Vous devez donc conserver la même valeur d’expiration d’événement d’expérience pour tous les jeux de données, si possible, afin d’éviter l’impact de différentes valeurs d’expiration sur différents jeux de données dans votre logique de segmentation.
