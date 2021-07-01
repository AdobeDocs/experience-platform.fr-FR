---
keywords: Experience Platform;accueil;rubriques les plus consultées;jeu de données;jeu de données;temps de vie;ttl;temps de vie;
solution: Experience Platform
title: Durée de vie des jeux de données
description: Ce document fournit des instructions générales sur la durée de vie (TTL) des jeux de données dans la banque de profils pour Adobe Experience Platform.
source-git-commit: 878c04c688268f8cf1850c3e8d40f958a6d2d69b
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---


# Durée de vie du service de profil (TTL)

Le service de profil permet aux utilisateurs d’appliquer la durée de vie (TTL) aux données de la banque de profils. TTL est un mécanisme qui limite la durée de vie des données dans un jeu de données. Vous pouvez ainsi supprimer automatiquement des données de la banque de profils qui ne sont plus utiles pour vos cas d’utilisation.

Actuellement, Profile ne prend en charge que la durée de vie des événements d’expérience.

## TTL d’événement d’expérience

Experience Event TTL vous permet d’appliquer TTL sur des jeux de données activés pour Real-time Customer Profile pour supprimer des données de la banque de profils qui ne sont plus valides.

>[!NOTE]
>
>Vous devrez contacter le support pour activer le délai d’activation des événements d’expérience sur vos jeux de données.

Après avoir activé la durée de vie d’un événement d’expérience sur un jeu de données activé pour Profile, Platform appliquera automatiquement la valeur d’expiration de la durée de vie aux données de l’événement d’expérience dans un processus en deux étapes :

1. La valeur d’expiration TTL sera appliquée à toutes les nouvelles données ingérées dans le jeu de données au moment de l’ingestion.
2. La valeur d’expiration TTL sera appliquée rétroactivement à toutes les données existantes du jeu de données en tant que tâche de système de renvoi unique. Une fois que la valeur d’expiration TTL a été placée sur le jeu de données, les événements plus anciens que la valeur d’expiration TTL seront immédiatement ignorés dès que la tâche système s’exécute. Tous les autres événements seront ignorés dès qu’ils atteignent leurs valeurs d’expiration TTL à partir de l’horodatage de l’événement.

>[!NOTE]
>
>Une fois la durée de vie appliquée, toutes les données antérieures au nombre de jours de la durée de vie sont **supprimées de manière permanente** et ne peuvent pas être restaurées.
> 
>De plus, assurez-vous que l’intervalle de recherche en amont du segment se trouve dans la limite TTL. Sinon, les résultats du segment peuvent devenir incorrects après l’application de la durée de vie (TTL). Par exemple, si vous appliquez un délai d’activation de 30 jours et disposez d’un segment qui a tenté d’afficher les données il y a jusqu’à 45 jours, le segment produirait des profils incorrects.
> 
>Par conséquent, vous devez conserver le même TTL pour tous les jeux de données, si possible, afin d’éviter l’impact de différentes valeurs TTL sur différents jeux de données dans la logique de segmentation.

Par exemple, si vous appliquez une valeur TTL de 30 jours le 15 mai, les étapes suivantes se produisent :

1. Tous les nouveaux événements auront une valeur TTL de 30 jours appliquée lors de leur ingestion.
2. Tous les événements existants dont l’horodatage est antérieur au 15 avril seront immédiatement supprimés avec la tâche système.
3. Tous les événements existants dont l’horodatage est supérieur au 15 avril auront une valeur d’expiration TTL 30 jours après l’horodatage de leur événement. Ainsi, si un événement a un horodatage du 18 avril, il sera supprimé trente jours après la date de cet horodatage, qui serait le 18 mai.

