---
keywords: Experience Platform ; accueil ; rubriques populaires ; mapper csv ; mapper le fichier csv ; mapper le fichier csv à xdm ; mapper csv à xdm ; ui guide ; mapper ; mapper ; prép de données ; préparation des données ; préparation des données ; préparation des données ;
solution: Experience Platform
title: Aperçu de l’aperçu de l’aperçu des données d’aperçu
topic-legacy: overview
description: Ce document présente l’aperçu des données dans Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
translation-type: tm+mt
source-git-commit: daefd977cd09bd9cd7f8d6101b45be98f30d24ae
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Présentation de l’Aperçu de l’Aperçu des données

La préparation des données permet aux ingénieurs de données de mapper, de transformer et de valider les données à partir du modèle de données d’expérience (XDM). L’aperçu des données s’affiche sous la forme d’une étape de &quot;mappage&quot; dans les processus d’importation de données, y compris le processus d’importation CSV. Les ingénieurs de données peuvent utiliser l’API Data Prep pour manipuler les données suivantes lors de l’assimilation :

- Définir des mappages de passes simples pour affecter des attributs d&#39;entrée à des attributs XDM
- Créez des champs calculés pour effectuer des calculs sur la ligne qui peuvent être affectés à des attributs XDM.
- Transformer les données en appliquant des fonctions de manipulation de chaînes, de chiffres ou de dates
- Création de hiérarchies XDM à l’aide de fonctions hiérarchiques
- Prévisualisation des données telles qu’elles sont manipulées dans la préparation des données

La préparation de données applique également plusieurs validations de données intrinsèques pour s’assurer que l’intégrité des données est conservée lors de l’assimilation. Dans la mesure du possible, la fonction d’aperçu des données mappe automatiquement les schémas de données entrants à XDM. Les ingénieurs de données peuvent modifier, corriger et supprimer les mappages suggérés et les remplacer par les mappages appropriés.

## Mappage

Un mappage est une association d’un attribut d’entrée ou d’un champ calculé à un attribut XDM. Un attribut unique peut être mappé à plusieurs attributs XDM en créant des mappages individuels.

Pour en savoir plus sur les différentes fonctions de mappage, consultez le [guide des fonctions de mappage](./functions.md).

## Jeu de mappages

Un ensemble de mappages qui transforment un schéma en un autre est collectivement appelé jeu de mappages. Un jeu de mappages unique est créé dans le cadre de chaque flux de données. Un jeu de mappages fait partie intégrante des flux de données et est créé, modifié et surveillé dans le cadre des flux de données.

Pour en savoir plus sur les jeux de mappages, y compris sur l&#39;utilisation des champs dans un jeu de mappages, consultez le [guide des jeux de mappages](./mapping-set.md). Pour savoir comment créer une visionneuse de mappages et utiliser d&#39;autres appels d&#39;API liés aux visionneuses de mappages, consultez la section jeu de mappages du [guide du développeur](./api/mapping-set.md).

## Gestion du format de données

La fonction d’élaboration des données peut gérer de manière robuste différents formats de données ingérées dans la plate-forme. Pour en savoir plus sur la façon dont l’API traite les différents types de données, consultez la [présentation de la gestion du format de données](./data-handling.md).

## Étapes suivantes

Ce document couvrait les bases de la préparation des données à Adobe Experience Platform. Pour en savoir plus sur les différentes fonctions de mappage, consultez le [guide des fonctions de mappage](./functions.md). Pour en savoir plus sur la façon dont l’API traite les différents types de données, consultez le [guide de gestion du format de données](./data-handling.md#dates). Pour savoir comment utiliser l’API d’aperçu des données, consultez le [Guide du développeur d’API d’aperçu des données](api/overview.md).
