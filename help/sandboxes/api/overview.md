---
keywords: Experience Platform;accueil;rubriques les plus consultées;guide de développement des environnements de test
solution: Experience Platform
title: Guide de l’API Sandbox
topic-legacy: developer guide
description: Les environnements de test d’Adobe Experience Platform fournissent des environnements de développement isolés qui vous permettent de tester des fonctionnalités, d’exécuter des opérations et de créer des configurations personnalisées sans affecter votre environnement de production.
source-git-commit: f00e6161d82f1fd7ba442be9f06283f3c866573f
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 29%

---

# Guide de l’API [!DNL Sandbox]

L’API [!DNL Sandbox] fournit plusieurs points de terminaison qui vous permettent de gérer par programmation tous les environnements de test disponibles pour vous au sein de votre organisation IMS. Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

Pour afficher tous les points de terminaison disponibles et les opérations CRUD, consultez la [[!DNL Sandbox] référence API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml).

## Environnements de test disponibles

Le point de terminaison des environnements de test disponibles vous permet d’afficher la liste de tous les environnements de test disponibles pour l’utilisateur actuel, y compris des informations sur le nom, le titre, l’état, le type et la région de chaque environnement de test. Tous les utilisateurs peuvent accéder au point de terminaison des environnements de test disponibles dans l’API [!DNL Sandbox], y compris ceux qui ne disposent pas des autorisations d’accès à l’administration des environnements de test. Pour savoir comment afficher les environnements de test disponibles dans l’API, consultez le [guide de point de terminaison des environnements de test disponibles](./available.md) .

## Gestion des environnements de test

Un environnement de test est une partition virtuelle au sein d’une instance unique de Adobe Experience Platform, ce qui permet une intégration transparente au processus de développement de vos applications d’expérience numérique. Vous pouvez créer, afficher, modifier, réinitialiser et supprimer des environnements de test de production et de développement à l’aide du point de terminaison `/sandboxes` . Pour savoir comment utiliser ce point de terminaison, consultez le [guide du point de terminaison des environnements de test](./sandboxes.md).

## Types de sandbox

Actuellement, les types d’environnements de test pris en charge sur Experience Platform sont les environnements de test de production et de développement. Une licence Platform par défaut vous accorde un total de cinq environnements de test que vous pouvez classer en tant que production ou développement. Vous pouvez attribuer une licence à des modules supplémentaires de 10 environnements de test, jusqu’à 75 environnements de test au total. Consultez le [guide de point de terminaison des types d’environnements de test](./types.md) pour savoir comment afficher les types d’environnements de test pris en charge pour votre organisation dans l’API.

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API [!DNL Sandbox], consultez le guide de prise en main [guide de prise en main](./getting-started.md), puis sélectionnez l’un des guides des points d’entrée pour savoir comment utiliser des points d’entrée spécifiques.