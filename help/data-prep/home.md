---
keywords: Experience Platform;accueil;rubriques populaires;mapper csv;mapper le fichier csv;mapper le fichier csv à xdm;mapper csv à xdm;guide de lʼui;mappeur;mappage;data prep;préparation des données;préparer des données;
solution: Experience Platform
title: Présentation de la préparation des données
description: Ce document présente Data Prep dans Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 98%

---


# Présentation de la préparation des données

La préparation des données permet aux ingénieur(e)s de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM). La préparation des données apparaît comme étape de « mappage » dans les processus dʼingestion de données, y compris le workflow dʼingestion de données CSV. Les ingénieur(e)s de données peuvent utiliser la préparation des données pour effectuer les manipulations de données suivantes lors de lʼingestion :

- définir des mappages simples pour affecter des attributs dʼentrée à des attributs XDM ;
- créer des champs calculés pour effectuer des calculs sur la ligne qui peuvent être affectés à des attributs XDM ;
- transformer les données en appliquant des fonctions de manipulation de chaînes, de chiffres ou de dates ;
- créer des hiérarchies XDM à lʼaide de fonctions hiérarchiques ;
- prévisualiser les données lors de leur manipulation lors de la préparation des données.

Data Prep applique également plusieurs validations de données intrinsèques afin de garantir le maintien de lʼintégrité des données lors de leur ingestion. Dans la mesure du possible, Data Prep mappe automatiquement les schémas de données entrants à XDM. Les ingénieur(e)s de données peuvent modifier, corriger et supprimer les mappages suggérés et les remplacer par les mappages appropriés.

>[!NOTE]
>
>À moins que le message qui en résulte ne soit un XDM non valide, toute erreur de transformation dans Data Prep entraîne la définition de ces attributs sur `null`. Toutefois, le reste de la ligne est ingéré. Si la ligne correspond à un XDM non valide, elle n’est **pas** ingérée. Dans ces deux cas, l’erreur est documentée.

## Mappage

Un mappage est l’association dʼun attribut dʼentrée ou dʼun champ calculé à un attribut XDM. Un attribut unique peut être mappé à plusieurs attributs XDM en créant des mappages individuels.

Pour en savoir plus sur les différentes fonctions de mappage, consultez le [guide des fonctions de mappage](./functions.md).

### Champs calculés

Les champs calculés permettent de créer des valeurs en fonction des attributs du schéma d’entrée. Ces valeurs peuvent ensuite être affectées à des attributs dans le schéma cible. Vous pouvez également leur fournir un nom et une description pour en faciliter la référence. La longueur maximale des champs calculés est de 4 096 caractères.

Pour en savoir plus sur les champs calculés, consultez le [guide des champs calculés](./functions.md#calculated-fields).

### Échapper les caractères spéciaux {#escape-special-characters}

Vous pouvez échapper les caractères spéciaux d’un champ à l’aide de `${...}`. Toutefois, les fichiers JSON qui contiennent des champs avec un point (`.`) ne sont pas pris en charge par ce mécanisme. Lors de l’interaction avec des hiérarchies, si un attribut enfant comporte un point (`.`), vous devez utiliser une barre oblique inverse (`\`) pour échapper les caractères spéciaux. Par exemple, `address` est un objet qui contient l’attribut `street.name`. Il peut donc être appelé `address.street\.name` au lieu de `address.street.name`.

## Jeu de mappages

Un ensemble de mappages qui transforme un schéma en un autre est collectivement appelé un jeu de mappages. Un seul jeu de mappages est créé dans le cadre de chaque flux de données. Un jeu de mappages fait partie intégrante des flux de données et est créé, modifié et surveillé dans le cadre des flux de données.

Pour en savoir plus sur les jeux de mappages, y compris sur l’utilisation des champs dans un jeu de mappages, consultez le [guide des jeux de mappages](./mapping-set.md). Pour savoir comment créer un jeu de mappages et utiliser d’autres appels d’API liés aux jeux de mappages, consultez la section sur les jeux de mappages dans le [guide de développement](./api/mapping-set.md).

## Gestion des formats de données

La préparation des données peut gérer de manière robuste différents formats de données ingérés dans Experience Platform. Pour en savoir plus sur la façon dont la préparation de données gère les différents types de données, consultez la [présentation de la gestion des formats de données](./data-handling.md).

## Envoyer des mises à jour de lignes partielles à l’aide de [!DNL Data Prep]

La diffusion en flux continu d’upserts dans [!DNL Data Prep] permet d’envoyer des mises à jour de ligne partielles aux données [!DNL Profile Service] tout en créant et en établissant de nouveaux liens d’identité avec une seule requête API. Pour en savoir plus sur la diffusion en flux continu d’upserts dans [!DNL Data Prep], reportez-vous au document sur l’[envoi de mises à jour de lignes partielles](./upserts.md).

## Contrôle d’accès basé sur les attributs dans [!DNL Data Prep]

Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui permet aux administrateurs et administratrices de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs.

Le contrôle d’accès basé sur les attributs permet de ne mapper que les attributs auxquels vous avez accès. Les attributs auxquels vous n’avez pas accès ne peuvent être utilisés dans les mappages directs et les champs calculés. Par conséquent, si vous n’avez pas accès à un champ obligatoire, vous ne pouvez pas enregistrer un mappage. De plus, vous ne pouvez pas mapper des objets ou des tableaux d’objets si vous n’avez accès à aucun des attributs enfants. Cependant, vous pouvez mapper d’autres éléments dans l’objet ou le tableau d’objets individuellement.

Pour plus d’informations, consultez la [présentation du contrôle d’accès basé sur les attributs](../access-control/abac/overview.md).

## Étapes suivantes

Ce document présentait les principes de base de Data Prep dans Adobe Experience Platform. Pour en savoir plus sur les différentes fonctions de mappage, consultez le [guide des fonctions de mappage](./functions.md). Pour en savoir plus sur la façon dont la préparation de données gère les différents types de données, consultez le [guide de la gestion des formats de données](./data-handling.md#dates). Pour savoir comment utiliser l’API Data Prep, consultez le [guide de développement de la préparation des données](api/overview.md).
