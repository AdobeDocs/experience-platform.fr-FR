---
keywords: Experience Platform;préparation de données;api data prep;dépannage;API
title: Présentation de l’API Data Prep
description: L’API Data Prep vous permet de créer par programmation des jeux de mappages et des fonctions, pour que vous puissiez transformer vos données entre les schémas source et de destination.
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 100%

---

# Guide de l’API Mapping Service

La préparation des données permet aux ingénieurs de données de mapper, transformer et valider les données vers et à partir du modèle de données d’expérience (XDM). Data Prep sʼaffiche en tant quʼétape de « mappage » dans les processus dʼingestion de données, y compris le processus dʼingestion de données CSV.

L’API Mapping Service, également appelée API Data Prep, comprend plusieurs points d’entrée décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

## Fonctions

Les fonctions de jeux de mappages vous permettent de transformer vos données entre les schémas source et de destination. Vous pouvez utiliser le point d’entrée `/languages/el` pour valider vos expressions et obtenir une liste de toutes les fonctions et opérations de jeux de mappages disponibles.

Pour plus d’informations sur l’utilisation des fonctions de jeux de mappage, consultez le [guide des points d’entrée des fonctions](./functions.md).

## Jeu de mappages

Les jeux de mappages peuvent être utilisés pour définir la façon dont les données d’un schéma source sont mappées à celui d’un schéma de destination. Vous pouvez utiliser le point d’entrée `/mappingSets` dans l’API Data Prep pour récupérer, créer, mettre à jour et valider des jeux de mappages par programmation.

Pour plus d’informations sur l’utilisation des jeux de mappage, consultez le [guide des points d’entrée des jeux de mappage](./mapping-set.md).

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API Mapping Service, consultez le [guide de prise en main](./getting-started.md), puis sélectionnez l’un des guides des points d’entrée pour savoir comment utiliser des points d’entrée spécifiques.
