---
keywords: Experience Platform;accueil;rubriques populaires;jeu de données;Jeu de données;durée de vie;ttl;durée-de-vie;
solution: Experience Platform
title: Expirations des événements d’expérience
description: Ce document fournit des instructions générales sur la configuration des délais d’expiration pour des événements d’expérience individuels dans un jeu de données Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: faf9e72f77f04b20d2399749eaacdb9ebdf412dc
workflow-type: ht
source-wordcount: '466'
ht-degree: 100%

---

# Expirations des événements d’expérience

Dans Adobe Experience Platform, vous pouvez configurer des délais d’expiration pour tous les événements d’expérience ingérés dans un jeu de données activé pour un [profil client en temps réel](./home.md). Vous pouvez ainsi supprimer automatiquement des données du magasin de profils qui ne sont plus utiles pour vos cas d’utilisation.

Les expirations d’événements d’expérience ne peuvent pas être configurées via l’interface utilisateur ou les API de Platform. Vous devez plutôt contacter l’assistance afin d’activer les expirations d’événements d’expérience sur vos jeux de données requis.

>[!IMPORTANT]
>
>Les expirations d’événements d’expérience ne doivent pas être confondues avec les expirations de jeux de données, qui suppriment l’ensemble du jeu de données une fois la date d’expiration atteinte. Elles sont configurées manuellement via l’[Hygiène des données Adobe Experience Platform](../hygiene/home.md).

## Processus d’expiration automatisé

Une fois que les expirations d’événement d’expérience ont été activées sur un jeu de données activé pour un profil, Platform applique automatiquement les valeurs d’expiration pour chaque événement capturé dans un processus en deux étapes :

1. La valeur d’expiration de toutes les nouvelles données ingérées dans le jeu de données est appliquée au moment de l’ingestion en fonction de la date et de l’heure de l’événement.
1. La valeur dʼexpiration sera appliquée rétroactivement à toutes les données existantes du jeu de données en tant que traitement système unique de renvoi. Une fois que la valeur dʼexpiration a été placée sur le jeu de données, les événements plus anciens que la valeur dʼexpiration seront immédiatement ignorés dès que le traitement système s’exécutera. Tous les autres événements seront ignorés dès quʼils atteindront leurs valeurs dʼexpiration à partir de la date et de lʼheure de lʼévénement.

>[!WARNING]
>
>Une fois la valeur d’expiration appliquée, toutes les données antérieures au nombre de jours attribué sont **supprimées définitivement** et ne peuvent pas être restaurées.

Par exemple, si vous avez appliqué une valeur d’expiration de 30 jours le 15 mai, les étapes suivantes se produisent :

1. Tous les nouveaux événements reçoivent une valeur d’expiration de 30 jours appliquée lorsqu’ils sont ingérés.
1. Tous les événements existants dont la date est antérieure au 15 avril seront immédiatement supprimés avec le traitement système.
1. Tous les événements existants dont la date est postérieure au 15 avril auront une valeur dʼexpiration de 30 jours après leur date d’exécution. Ainsi, si un événement a une date correspondant au 18 avril, il sera supprimé 30 jours après cette date, soit le 18 mai.

## Effets sur la segmentation

Vous devez vous assurer que les intervalles de recherche en amont de vos segments se trouvent dans les limites d’expiration de leurs jeux de données dépendants afin de conserver des résultats précis. Par exemple, si vous appliquez une valeur d’expiration de 30 jours et que vous disposez d’un segment qui tente d’afficher les données jusqu’à 45 jours plus tôt, l’audience associée sera probablement inexacte.

Si possible, vous devez essayer de conserver la même valeur d’expiration d’événement d’expérience pour tous les jeux de données, afin d’éviter l’impact de différentes valeurs d’expiration sur différents jeux de données dans votre logique de segmentation.
