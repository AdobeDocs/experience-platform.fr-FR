---
keywords: Experience Platform;accueil;rubriques populaires;api;contrôle d’accès basé sur les attributs;contrôle d’accès basé sur les attributs
solution: Experience Platform
title: Guide de l’API de contrôle d’accès basé sur les attributs
description: L’API de contrôle d’accès basé sur les attributs vous permet de gérer par programmation les rôles et les stratégies d’accès dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 30%

---

# Guide de l’API de contrôle d’accès basé sur les attributs

Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui permet aux administrateurs de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs. Les attributs peuvent être des métadonnées ajoutées à un objet, comme un libellé ajouté à un champ ou à un segment de schéma. Un administrateur définit des politiques d’accès qui comprennent des attributs afin de gérer les autorisations d’accès des utilisateurs.

L’API de contrôle d’accès basé sur les attributs est utilisée pour accéder aux rôles, aux produits, aux catégories d’autorisations et aux jeux d’autorisations dans Adobe Experience Platform, fournissant une interface utilisateur et une API RESTful à partir desquelles toutes les ressources de bibliothèque disponibles sont accessibles.

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs ne doit pas être confondu avec les fonctionnalités de gouvernance des données des Experience Platform, qui vous permettent d’utiliser des libellés et des stratégies pour contrôler la manière dont les données sont utilisées dans Platform plutôt que les utilisateurs de votre organisation qui y ont accès. Consultez le [guide de l’API Policy Service](../../../data-governance/api/overview.md) pour savoir comment utiliser ces fonctionnalités par programmation.

Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

## Rôles

Les rôles définissent l’accès dont dispose un administrateur, un spécialiste ou un utilisateur final aux ressources de votre entreprise. Dans un environnement de contrôle d’accès basé sur les rôles, la configuration de l’accès des utilisateurs est regroupée suivant les responsabilités et les besoins communs. Un rôle possède un ensemble donné d’autorisations et les membres de votre organisation peuvent être affectés à un ou plusieurs rôles, selon la portée de l’accès en lecture ou en écriture dont ils ont besoin. Pour plus d’informations sur l’utilisation des rôles dans l’API, consultez le [guide de point de terminaison des rôles](./roles.md) .

## Politiques

Les politiques sont des déclarations qui réunissent des attributs pour établir des actions autorisées et non autorisées. Les stratégies peuvent être locales ou globales et peuvent remplacer d’autres stratégies. Le point de terminaison `/policies` vous permet de gérer par programmation les stratégies de votre entreprise. Pour plus d’informations sur l’utilisation des stratégies dans l’API, consultez le [guide de point de terminaison des stratégies](./policies.md) .

## Produits

Le point d’entrée `/products` de l’API de contrôle d’accès basé sur les attributs vous permet de gérer par programmation les produits, ainsi que les catégories d’autorisations et les jeux d’autorisations associés aux produits de votre entreprise. Pour plus d’informations sur l’utilisation des produits, leurs catégories d’autorisations correspondantes et les jeux d’autorisations correspondants dans l’API, consultez le [guide de point de terminaison de produits](./products.md) .

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API de contrôle d’accès basé sur les attributs, lisez le [guide de prise en main](./getting-started.md) , puis sélectionnez l’un des guides de point de terminaison pour savoir comment utiliser des points de terminaison spécifiques.
