---
keywords: Experience Platform;accueil;rubriques populaires;jeu de données;Jeu de donnéesvdurée de vie;ttl;durée-de-vie;
solution: Experience Platform
title: Durée de vie des jeux de données
description: Ce document fournit des instructions générales sur la durée de vie (TTL) des jeux de données dans le magasin de profils pour Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 100%

---

# Durée de vie dans le service de profils (TTL)

Le service de profils permet aux utilisateurs dʼappliquer une durée de vie (TTL) aux données dans le magasin de profils. Le mécanisme de durée de vie permet de limiter la durée de vie des données au sein dʼun jeu de données. Vous pouvez ainsi supprimer automatiquement des données du magasin de profils qui ne sont plus utiles pour vos cas dʼutilisation.

Actuellement, le service de profils ne prend en charge que la durée de vie des événements dʼexpérience.

## Durée de vie dʼun evénement dʼexpérience

La durée de vie dʼévénements dʼexpérience vous permet dʼappliquer la durée de vie sur les jeux de données de profil clients en temps réel afin de supprimer les données du magasin de profils qui ne sont plus valides.

>[!NOTE]
>
>Vous devez contacter lʼassistance pour activer la durée de vie dʼévénements dʼexpérience sur vos jeux de données.

Après avoir activé la durée de vie dʼévénements dʼexpérience sur un jeu de données activé pour le service de profils, Platform appliquera automatiquement la valeur dʼexpiration de la durée de vie aux données dʼévénements dʼexpérience dans un processus en deux étapes :

1. La valeur dʼexpiration de la durée de vie sera appliquée à toutes les nouvelles données ingérées dans le jeu de données au moment de lʼingestion.
2. La valeur dʼexpiration de la durée de vie sera appliquée rétroactivement à toutes les données existantes du jeu de données en tant que tâche système de renvoi unique. Une fois que la valeur dʼexpiration de la durée de vie a été placée sur le jeu de données, les événements plus anciens que la valeur dʼexpiration de la durée de vie seront immédiatement ignorés dès que la tâche système sʼexécutera. Tous les autres événements seront ignorés dès quʼils atteidront leurs valeurs dʼexpiration de durée de vie à partir de la date et lʼheure de lʼévénement.

>[!NOTE]
>
>Une fois la durée de vie appliquée, toutes les données antérieures au nombre de jours de la durée de vie sont **supprimées de manière permanente** et ne peuvent pas être restaurées.
> 
>De plus, assurez-vous que lʼintervalle de recherche pour le segment se trouve dans la limite de durée de vie. Sinon, les résultats de segment peuvent devenir incorrects après lʼapplication de la durée de vie (TTL). Par exemple, si vous appliquez une durée de vie de 30 jours et que vous disposez dʼun segment qui tente dʼafficher les données datant de 45 jours maximum, le segment produira des profils incorrects.
> 
>Par conséquent, vous devez conserver la même durée de vie pour tous les jeux de données, si possible, afin dʼéviter lʼimpact de valeurs de durée de vie différentes sur plusieurs jeux de données dans la logique de segmentation.

Par exemple, si vous appliquez une valeur de durée de vie de 30 jours le 15 mai, les étapes suivantes se produisent :

1. Tous les nouveaux événements auront une valeur de durée de vie de 30 jours appliquée lors de leur ingestion.
2. Tous les événements existants dont la date est antérieure au 15 avril seront immédiatement supprimés avec la tâche système.
3. Tous les événements existants dont la date est postérieure au 15 avril auront une valeur dʼexpiration de durée de vie de 30 jours après la date de leur événement. Ainsi, si un événement a une date correspondant au 18 avril, il sera supprimé trente jours après cette date, soit le 18 mai.
