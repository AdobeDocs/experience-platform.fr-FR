---
keywords: Experience Platform;accueil;rubriques les plus consultées;guide de développement des environnements de test
solution: Experience Platform
title: Guide de l’API Sandbox
topic-legacy: developer guide
description: Les environnements de test d’Adobe Experience Platform fournissent des environnements de développement isolés qui vous permettent de tester des fonctionnalités, d’exécuter des opérations et de créer des configurations personnalisées sans affecter votre environnement de production.
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 26%

---

# Guide de l’API [!DNL Sandbox]

Le [!DNL Sandbox] L’API fournit plusieurs points de terminaison qui vous permettent de gérer par programmation tous les environnements de test disponibles pour vous au sein de votre organisation IMS. Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

Pour afficher tous les points de terminaison disponibles et les opérations CRUD, rendez-vous sur la page [[!DNL Sandbox] Référence d’API](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Environnements de test disponibles

Le point de terminaison des environnements de test disponibles vous permet d’afficher la liste de tous les environnements de test disponibles pour l’utilisateur actuel, y compris des informations sur le nom, le titre, l’état, le type et la région de chaque environnement de test. Le point de terminaison des environnements de test disponibles dans la variable [!DNL Sandbox] Tous les utilisateurs peuvent accéder à l’API, y compris ceux qui ne disposent pas des autorisations d’accès à Sandbox Administration. Voir [guide de point de terminaison des environnements de test disponibles](./available.md) pour savoir comment afficher les environnements de test disponibles dans l’API.

## Gestion des environnements de test

Un environnement de test est une partition virtuelle au sein d’une instance unique de Adobe Experience Platform, ce qui permet une intégration transparente au processus de développement de vos applications d’expérience numérique. Vous pouvez créer, afficher, modifier, réinitialiser et supprimer des environnements de test de production et de développement à l’aide du `/sandboxes` point de terminaison . Pour savoir comment utiliser ce point de terminaison, voir [guide de point de terminaison des environnements de test](./sandboxes.md).

## Types de sandbox

Actuellement, les types d’environnements de test pris en charge sur Experience Platform sont les environnements de test de production et de développement. Une licence Platform par défaut vous accorde un total de cinq environnements de test que vous pouvez classer en tant que production ou développement. Vous pouvez attribuer une licence à des modules supplémentaires de 10 environnements de test, jusqu’à 75 environnements de test au total. Voir [guide de point de terminaison des types sandbox](./types.md) pour savoir comment afficher les types d’environnements de test pris en charge pour votre organisation dans l’API.

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API [!DNL Sandbox], consultez le guide de prise en main [guide de prise en main](./getting-started.md), puis sélectionnez l’un des guides des points d’entrée pour savoir comment utiliser des points d’entrée spécifiques.
