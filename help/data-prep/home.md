---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;data prep;data preparation;preparing data;
solution: Experience Platform
title: Fonctions de mappage
topic: overview
description: Ce document présente l’aperçu des données dans Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: db38f0666f5c945461043ad08939ebda52c21855
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%

---


# Prép de données

La préparation des données permet aux ingénieurs de données de mapper, de transformer et de valider les données à partir du modèle de données d’expérience (XDM). L’aperçu des données s’affiche sous la forme d’une étape de &quot;mappage&quot; dans les processus d’importation de données, y compris le processus d’importation CSV. Les ingénieurs de données peuvent utiliser l’API Data Prep pour manipuler les données suivantes lors de l’assimilation :

- Définir des mappages de passes simples pour affecter des attributs d&#39;entrée à des attributs XDM
- Créez des champs calculés pour effectuer des calculs sur la ligne qui peuvent être affectés à des attributs XDM.
- Transformer les données en appliquant des fonctions de manipulation de chaînes, de chiffres ou de dates
- Création de hiérarchies XDM à l’aide de fonctions hiérarchiques
- Prévisualisation des données telles qu’elles sont manipulées dans la préparation des données

La préparation de données applique également plusieurs validations de données intrinsèques pour s’assurer que l’intégrité des données est conservée lors de l’assimilation. Dans la mesure du possible, la fonction d’aperçu des données mappe automatiquement les schémas de données entrants à XDM. Les ingénieurs de données peuvent modifier, corriger et supprimer les mappages suggérés et les remplacer par les mappages appropriés.

## Mappage

Un mappage est une association d’un attribut d’entrée ou d’un champ calculé à un attribut XDM. Un attribut unique peut être mappé à plusieurs attributs XDM en créant des mappages individuels.

Pour en savoir plus sur les différentes fonctions de mappage, veuillez lire le guide [des fonctions de](./functions.md)mappage.

## Jeu de mappages

Un ensemble de mappages qui transforment un schéma en un autre est collectivement appelé jeu de mappages. Un jeu de mappages unique est créé dans le cadre de chaque flux de données. Un jeu de mappages fait partie intégrante des flux de données et est créé, modifié et surveillé dans le cadre des flux de données.

## Étapes suivantes

Ce document couvrait les bases de la préparation des données à Adobe Experience Platform. Pour en savoir plus sur les différentes fonctions de mappage, consultez le guide [des fonctions de](./functions.md)mappage. Pour en savoir plus sur les différentes chaînes de date et heure, veuillez lire le guide [](./dates.md)chaînes de date.