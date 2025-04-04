---
keywords: Experience Platform;accueil;rubriques les plus consultées;guide de développement des sandbox
solution: Experience Platform
title: Guide de l’API Sandbox
description: Les sandbox d’Adobe Experience Platform fournissent des environnements de développement isolés qui vous permettent de tester des fonctionnalités, d’exécuter des opérations et de créer des configurations personnalisées sans affecter votre environnement de production.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 30%

---

# Guide de l’API [!DNL Sandbox]

L’API [!DNL Sandbox] fournit plusieurs points d’entrée qui vous permettent de gérer par programmation tous les sandbox disponibles au sein de votre organisation. Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

Pour afficher tous les points d’entrée et opérations CRUD disponibles, consultez la [[!DNL Sandbox] référence de l’API](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Sandbox disponibles

Le point d’entrée des sandbox disponibles vous permet d’afficher une liste de tous les sandbox disponibles pour l’utilisateur actuel, y compris des informations sur le nom, le titre, l’état, le type et la région de chaque sandbox. Le point d’entrée des sandbox disponibles dans l’API [!DNL Sandbox] est accessible à tous les utilisateurs, y compris ceux qui ne disposent pas d’autorisations d’accès d’administration des sandbox. Consultez le [guide du point d’entrée des sandbox disponibles](./available.md) pour savoir comment afficher les sandbox disponibles dans l’API.

## Gestion des sandbox

Un sandbox est une partition virtuelle au sein d’une seule instance de Adobe Experience Platform, ce qui permet une intégration transparente au processus de développement de vos applications d’expérience digitale. Vous pouvez créer, afficher, modifier, réinitialiser et supprimer des sandbox de production et de développement à l’aide du point d’entrée `/sandboxes`. Pour savoir comment utiliser ce point d’entrée, consultez le [guide des points d’entrée des sandbox](./sandboxes.md).

## Types de sandbox

Actuellement, les types de sandbox pris en charge sur Experience Platform sont les sandbox de production et de développement. Une licence Experience Platform par défaut vous accorde un total de cinq sandbox que vous pouvez classer en tant que production ou développement. Vous pouvez ajouter des packs de 10 sandbox jusquʼà 75 sandbox maximum au total. Consultez le [guide des points d’entrée des types de sandbox](./types.md) pour savoir comment afficher les types de sandbox pris en charge pour votre organisation dans l’API.

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API [!DNL Sandbox], lisez le guide [de prise en main](./getting-started.md) puis sélectionnez l’un des guides des points d’entrée pour savoir comment utiliser des points d’entrée spécifiques.
