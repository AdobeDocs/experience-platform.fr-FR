---
keywords: Experience Platform;accueil;rubriques populaires;mapper csv;mapper le fichier csv;mapper le fichier csv à xdm;mapper csv à xdm;guide de lʼui;mappeur;mappage;data prep;préparation des données;préparer des données;
solution: Experience Platform
title: Présentation de Data Prep
topic-legacy: overview
description: Ce document présente Data Prep dans Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: f8ad7ce2ed5a45fa0200715a2b961d75f17d192c
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 80%

---


# Présentation de Data Prep

La préparation des données permet aux ingénieurs de données de mapper, transformer et valider les données vers et à partir du modèle de données d’expérience (XDM). Data Prep sʼaffiche en tant quʼétape de « mappage » dans les processus dʼingestion de données, y compris le processus dʼingestion de données CSV. Les ingénieurs de données peuvent utiliser Data Prep pour effectuer les manipulations de données suivantes lors de lʼingestion :

- définir des mappages simples pour affecter des attributs dʼentrée à des attributs XDM
- créer des champs calculés pour effectuer des calculs sur la ligne qui peuvent être affectés à des attributs XDM.
- transformer les données en appliquant des fonctions de manipulation de chaînes, de chiffres ou de dates
- créer des hiérarchies XDM à lʼaide de fonctions hiérarchiques
- prévisualiser les données lors de leur manipulation dans Data Prep

Data Prep applique également plusieurs validations de données intrinsèques afin de garantir le maintien de lʼintégrité des données lors de leur ingestion. Dans la mesure du possible, Data Prep mappe automatiquement les schémas de données entrants à XDM. Les ingénieurs de données peuvent modifier, corriger et supprimer les mappages suggérés et les remplacer par les mappages appropriés.

>[!NOTE]
>
>À moins que le message qui en résulte ne soit un XDM non valide, toute erreur de transformation dans Data Prep entraîne la définition de ces attributs sur `null`, tandis que le reste de la ligne sera ingéré. Si la ligne ne correspond pas à un XDM non valide, elle **et non** sera ingérée. Dans ces deux cas, l’erreur sera documentée.

## Mappage

Un mappage est l’association dʼun attribut dʼentrée ou dʼun champ calculé à un attribut XDM. Un attribut unique peut être mappé à plusieurs attributs XDM en créant des mappages individuels.

Pour en savoir plus sur les différentes fonctions de mappage, consultez le [guide des fonctions de mappage](./functions.md).

### Les champs calculés

Les champs calculés permettent de créer des valeurs en fonction des attributs du schéma d’entrée. Ces valeurs peuvent ensuite être affectées à des attributs dans le schéma cible et recevoir un nom et une description pour faciliter la référence.

Pour en savoir plus sur les champs calculés, consultez le [guide des champs calculés](./functions.md#calculated-fields).

## Jeu de mappages

Un ensemble de mappages qui transforme un schéma en un autre est collectivement appelé un jeu de mappages. Un seul jeu de mappages est créé dans le cadre de chaque flux de données. Un jeu de mappages fait partie intégrante des flux de données et est créé, modifié et surveillé dans le cadre des flux de données.

Pour en savoir plus sur les jeux de mappages, y compris sur l’utilisation des champs dans un jeu de mappages, consultez le [guide des jeux de mappages](./mapping-set.md). Pour savoir comment créer un jeu de mappages et utiliser d’autres appels d’API liés aux jeux de mappages, consultez la section sur les jeux de mappages dans le [guide de développement](./api/mapping-set.md).

## Gestion des formats de données

La préparation des données peut gérer de manière robuste différents formats de données ingérés dans Platform. Pour en savoir plus sur la façon dont la préparation de données gère les différents types de données, consultez la [présentation de la gestion des formats de données](./data-handling.md).

## Étapes suivantes

Ce document présentait les principes de base de Data Prep dans Adobe Experience Platform. Pour en savoir plus sur les différentes fonctions de mappage, consultez le [guide des fonctions de mappage](./functions.md). Pour en savoir plus sur la façon dont la préparation de données gère les différents types de données, consultez le [guide de la gestion des formats de données](./data-handling.md#dates). Pour savoir comment utiliser l’API Data Prep, consultez le [guide de développement de la préparation des données](api/overview.md).
