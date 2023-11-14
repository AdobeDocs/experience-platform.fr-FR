---
keywords: Experience Platform;accueil;rubriques populaires;jeu de données;Jeu de données;durée de vie;ttl;durée-de-vie;
solution: Experience Platform
title: Expirations des événements d’expérience
description: Ce document fournit des instructions générales sur la configuration des délais d’expiration pour des événements d’expérience individuels dans un jeu de données Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 83%

---

# Expirations des événements d’expérience

Dans Adobe Experience Platform, vous pouvez configurer des délais d’expiration pour tous les événements d’expérience ingérés dans un jeu de données activé pour [Profil client en temps réel](./home.md). Vous pouvez ainsi supprimer automatiquement des données du magasin de profils qui ne sont plus utiles pour vos cas d’utilisation.

Les expirations d’événements d’expérience ne peuvent pas être configurées via l’interface utilisateur ou les API de Platform. Vous devez plutôt contacter l’assistance afin d’activer les expirations d’événements d’expérience sur vos jeux de données requis.

>[!IMPORTANT]
>
>Les expirations d’événements d’expérience ne doivent pas être confondues avec les expirations de jeux de données, qui suppriment l’ensemble du jeu de données une fois la date d’expiration atteinte. Elles sont configurées manuellement via l’[Hygiène des données Adobe Experience Platform](../hygiene/home.md).

## Processus d’expiration automatisé

Une fois que les expirations d’événement d’expérience ont été activées sur un jeu de données activé pour un profil, Platform applique automatiquement les valeurs d’expiration pour chaque événement capturé dans un processus en deux étapes :

1. La valeur d’expiration de toutes les nouvelles données ingérées dans le jeu de données est appliquée au moment de l’ingestion en fonction de la date et de l’heure de l’événement.
1. La valeur dʼexpiration sera appliquée rétroactivement à toutes les données existantes du jeu de données en tant que traitement système unique de renvoi. Une fois que la valeur dʼexpiration a été placée sur le jeu de données, les événements plus anciens que la valeur dʼexpiration seront immédiatement ignorés dès que le traitement système s’exécutera. Tous les autres événements seront ignorés dès quʼils atteindront leurs valeurs dʼexpiration à partir de la date et de lʼheure de lʼévénement. Lorsque tous les événements d’expérience ont été supprimés, si le profil ne comporte plus d’attributs de profil, le profil n’existera plus.

>[!WARNING]
>
>Une fois la valeur d’expiration appliquée, toutes les données antérieures au nombre de jours attribué sont **supprimées définitivement** et ne peuvent pas être restaurées.

Par exemple, si vous avez appliqué une valeur d’expiration de 30 jours le 15 mai, les étapes suivantes se produisent :

1. Tous les nouveaux événements reçoivent une valeur d’expiration de 30 jours appliquée lorsqu’ils sont ingérés.
1. Tous les événements existants dont la date est antérieure au 15 avril seront immédiatement supprimés avec le traitement système.
1. Tous les événements existants dont la date est postérieure au 15 avril auront une valeur dʼexpiration de 30 jours après leur date d’exécution. Ainsi, si un événement a une date correspondant au 18 avril, il sera supprimé 30 jours après cette date, soit le 18 mai.

## Effets sur la segmentation

Vous devez vous assurer que les intervalles de recherche en amont pour vos audiences se situent dans les limites d’expiration de leurs jeux de données dépendants afin de conserver des résultats précis. Par exemple, si vous appliquez une valeur d’expiration de 30 jours et que vous disposez d’une audience qui tente d’afficher les données d’il y a jusqu’à 45 jours, l’audience obtenue sera probablement inexacte.

Si possible, vous devez essayer de conserver la même valeur d’expiration d’événement d’expérience pour tous les jeux de données, afin d’éviter l’impact de différentes valeurs d’expiration sur différents jeux de données dans votre logique de segmentation.

## Questions fréquentes {#faq}

La section suivante répertorie les questions fréquentes sur l’expiration des données d’Experience Event :

### En quoi l’expiration des données d’événement d’expérience diffère-t-elle de l’expiration des données de profil pseudonyme ?

L’expiration des données d’événement d’expérience et l’expiration des données de profil pseudonyme sont des fonctionnalités complémentaires.

#### Granularité

L’expiration des données d’événements d’expérience s’applique au **jeu de données**. Par conséquent, chaque jeu de données peut avoir un paramètre d’expiration de données différent.

L’expiration des données de profils pseudonymes s’applique à la **sandbox**. Par conséquent, l’expiration des données affecte tous les profils de la sandbox.

#### Types d’identité

L’expiration des données d’événements d’expérience supprime les événements **uniquement** sur la base de la date et de l’heure de l’enregistrement de l’événement. Les espaces de noms d’identité inclus sont **ignorés** pour les besoins de l’expiration.

L’expiration des données de profils pseudonymes prend **uniquement** en compte les profils dont les graphiques d’identités contiennent des espaces de noms d’identité sélectionnés par le client ou la cliente, tels que `ECID`, `AAID` ou d’autres types de cookies. Si le profil contient **un** espace de noms d’identité supplémentaire qui ne figurait **pas** dans la liste sélectionnée par le client ou la cliente, le profil n’est **pas** supprimé.

#### Éléments supprimés

L’expiration des données d’événements d’expérience supprime **uniquement** les événements et **non** les données de la classe de profil. Les données de classe de profil ne sont supprimées que lorsque les données de **tous** les jeux de données sont supprimées et qu’il n’existe **aucun** enregistrement de classe de profil restant pour le profil.

L’expiration des données de profils pseudonymes supprime les enregistrements d’événement **et** de profil. Les données de classe de profil sont donc également supprimées.

### Comment utiliser l’expiration des données de profils pseudonymes en parallèle avec l’expiration des données d’événements d’expérience ?

L’expiration des données de profils anonymes et l’expiration des données d’événements d’expérience sont complémentaires.

Nous vous recommandons de **toujours** appliquer l’expiration des données d’événements d’expérience à vos jeux de données, en fonction de vos besoins de conservation des données sur votre clientèle existante. Une fois la configuration de l’expiration des données d’événements d’expérience terminée, vous pouvez utiliser l’expiration des données de profils pseudonymes pour supprimer automatiquement les profils pseudonymes. En règle générale, le délai d’expiration des données des profils pseudonymes est inférieur à celui des événements d’expérience.

Dans un cas d’utilisation standard, définissez l’expiration de vos données d’événements d’expérience en fonction de vos données utilisateur existantes. Configurez ensuite l’expiration de vos données de profils pseudonymes sur un délai beaucoup plus court, afin de limiter l’impact des profils pseudonymes sur la conformité de votre licence Platform.
