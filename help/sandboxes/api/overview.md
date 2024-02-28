---
keywords: Experience Platform;accueil;rubriques les plus consultées;guide de développement des environnements de test
solution: Experience Platform
title: Guide de l’API Sandbox
description: Les sandbox d’Adobe Experience Platform fournissent des environnements de développement isolés qui vous permettent de tester des fonctionnalités, d’exécuter des opérations et de créer des configurations personnalisées sans affecter votre environnement de production.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 24%

---

# Guide de l’API [!DNL Sandbox]

La variable [!DNL Sandbox] L’API fournit plusieurs points de terminaison qui vous permettent de gérer par programmation tous les environnements de test disponibles pour vous au sein de votre organisation. Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

Pour afficher tous les points de terminaison disponibles et les opérations CRUD, consultez la [[!DNL Sandbox] Référence d’API](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Environnements de test disponibles

Le point de terminaison des environnements de test disponibles vous permet d’afficher la liste de tous les environnements de test disponibles pour l’utilisateur actuel, y compris des informations sur le nom, le titre, l’état, le type et la région de chaque environnement de test. Le point de terminaison des environnements de test disponibles dans la variable [!DNL Sandbox] Tous les utilisateurs peuvent accéder à l’API, y compris ceux qui ne disposent pas des autorisations d’accès à Sandbox Administration. Voir [guide de point de terminaison des environnements de test disponibles](./available.md) pour savoir comment afficher les environnements de test disponibles dans l’API.

## Gestion des environnements de test

Un environnement de test est une partition virtuelle au sein d’une instance unique de Adobe Experience Platform, ce qui permet une intégration transparente au processus de développement de vos applications d’expérience numérique. Vous pouvez créer, afficher, modifier, réinitialiser et supprimer des environnements de test de production et de développement à l’aide du `/sandboxes` point de terminaison . Pour savoir comment utiliser ce point de terminaison, voir [guide de point de terminaison des environnements de test](./sandboxes.md).

## Types de sandbox

Actuellement, les types d’environnements de test pris en charge sur Experience Platform sont les environnements de test de production et de développement. Une licence Platform par défaut vous accorde un total de cinq environnements de test que vous pouvez classer en tant que production ou développement. Vous pouvez ajouter des packs de 10 sandbox jusquʼà 75 sandbox maximum au total. Voir [guide de point de terminaison des types sandbox](./types.md) pour savoir comment afficher les types d’environnements de test pris en charge pour votre organisation dans l’API.

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de la variable [!DNL Sandbox] API, lisez la [guide de prise en main](./getting-started.md) sélectionnez ensuite l’un des guides de point de fin pour savoir comment utiliser des points de fin spécifiques.
