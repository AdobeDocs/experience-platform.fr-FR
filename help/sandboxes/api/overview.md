---
keywords: Experience Platform;accueil;rubriques les plus consultées;guide de développement des sandbox
solution: Experience Platform
title: Guide de l’API Sandbox
description: Les sandbox d’Adobe Experience Platform fournissent des environnements de développement isolés qui vous permettent de tester des fonctionnalités, d’exécuter des opérations et de créer des configurations personnalisées sans affecter votre environnement de production.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
TQID: https://experienceleague.adobe.com/hYkGh77BuGUV8IvcSj1xTTgbTcR5nkxaTqyMo301AVc
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: adf04a6a-050f-44bc-a52c-db79ccb22ebf
subfeature_v2: id: a9eb38d5-9d89-492f-af4e-b968a07f2d91id: d21bd11d-08df-4cd6-ad8f-cb59a09de5c0
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: cb424651efb1b4d71717c06a4b0d6e9354f0dcc7
workflow-type: tm+mt
source-wordcount: 334
ht-degree: 37%

---

# Guide de l’API [!DNL Sandbox]

L’API [!DNL Sandbox] fournit plusieurs points d’entrée qui vous permettent de gérer par programmation tous les sandbox disponibles au sein de votre organisation. Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

Pour afficher tous les points d’entrée et opérations CRUD disponibles, consultez la [[!DNL Sandbox] référence de l’API](https://developer.adobe.com/experience-platform-apis/references/sandbox).

## Sandbox disponibles

Le point d’entrée des sandbox disponibles vous permet d’afficher une liste de tous les sandbox disponibles pour l’utilisateur actuel, y compris des informations sur le nom, le titre, l’état, le type et la région de chaque sandbox. Le point d’entrée des sandbox disponibles dans l’API [!DNL Sandbox] est accessible à tous les utilisateurs, y compris ceux qui ne disposent pas d’autorisations d’accès d’administration des sandbox. Consultez le [guide du point d’entrée des sandbox disponibles](./available.md) pour savoir comment afficher les sandbox disponibles dans l’API.

## Gestion des sandbox

Un sandbox est une partition virtuelle au sein d’une seule instance de Adobe Experience Platform, ce qui permet une intégration transparente au processus de développement de vos applications d’expérience digitale. Vous pouvez créer, afficher, modifier, réinitialiser et supprimer des sandbox de production et de développement à l’aide du point d’entrée `/sandboxes`. Pour savoir comment utiliser ce point d’entrée, consultez le [guide des points d’entrée des sandbox](./sandboxes.md).

## Types de sandbox

Actuellement, les types de sandbox pris en charge sur Experience Platform sont les sandbox de production et de développement. Une licence Experience Platform par défaut vous accorde un total de cinq sandbox que vous pouvez classer en tant que production ou développement. Vous pouvez ajouter des packs de 10 sandbox jusquʼà 75 sandbox maximum au total. Consultez le [guide des points d’entrée des types de sandbox](./types.md) pour savoir comment afficher les types de sandbox pris en charge pour votre organisation dans l’API.

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API [!DNL Sandbox], consultez le guide de prise en main [guide de prise en main](./getting-started.md), puis sélectionnez l’un des guides des points d’entrée pour savoir comment utiliser des points d’entrée spécifiques.

