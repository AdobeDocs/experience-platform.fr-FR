---
keywords: Experience Platform;accueil;rubriques populaires;api;contrôle d’accès basé sur les attributs;contrôle d’accès basé sur les attributs
solution: Experience Platform
title: Guide de l’API de contrôle d’accès basé sur les attributs
description: L’API de contrôle d’accès basé sur les attributs vous permet de gérer par programmation les rôles et les stratégies dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 567bfe089fd96cb08cb8ea7c90d065c804be9413
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 32%

---

# Guide de l’API de contrôle d’accès basé sur les attributs

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs est actuellement disponible pour un nombre restreint d’utilisateurs, qui sont actifs dans le secteur de la santé et basés aux États-Unis. Cette fonctionnalité sera disponible pour tous les clients Real-time Customer Data Platform dès son déploiement à grande échelle.

Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui permet aux administrateurs de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs. Les attributs peuvent être des métadonnées ajoutées à un objet, comme un libellé ajouté à un champ ou à un segment de schéma. Un administrateur définit des stratégies d’accès qui comprennent des attributs afin de gérer les autorisations d’accès des utilisateurs.

L’API de contrôle d’accès basé sur les attributs est utilisée pour accéder aux rôles, aux produits, aux catégories d’autorisations et aux jeux d’autorisations dans Adobe Experience Platform, fournissant une interface utilisateur et une API RESTful à partir desquelles toutes les ressources de bibliothèque disponibles sont accessibles.

Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

## Rôles

Les rôles définissent l’accès dont dispose un administrateur, un spécialiste ou un utilisateur final aux ressources de votre entreprise. Dans un environnement de contrôle d’accès basé sur les rôles, la configuration de l’accès des utilisateurs est regroupée par le biais de responsabilités et de besoins communs. Un rôle possède un ensemble donné d’autorisations et les membres de votre organisation peuvent être affectés à un ou plusieurs rôles, selon la portée de l’accès en lecture ou en écriture dont ils ont besoin. Voir [guide d’endpoint des rôles](./roles.md) pour plus d’informations sur l’utilisation des rôles dans l’API.

## Stratégies

Les politiques sont des déclarations qui réunissent des attributs pour établir des actions permises et non admissibles. Les stratégies peuvent être locales ou globales et peuvent remplacer d’autres stratégies. Le `/policies` endpoint vous permet de gérer par programmation les stratégies de votre entreprise. Voir [guide de point de fin des stratégies](./policies.md) pour plus d’informations sur l’utilisation des stratégies dans l’API.

## Produits

Le `/products` Le point de terminaison de l’API de contrôle d’accès basé sur les attributs vous permet de gérer par programmation les produits, ainsi que les catégories d’autorisations et les jeux d’autorisations associés aux produits de votre entreprise. Voir [guide de point de fin de produits](./products.md) pour plus d’informations sur l’utilisation des produits, de leurs catégories d’autorisations et de leurs jeux d’autorisations correspondants dans l’API.

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API de contrôle d’accès basé sur les attributs, lisez la [guide de prise en main](./getting-started.md) sélectionnez ensuite l’un des guides de point de fin pour savoir comment utiliser des points de fin spécifiques.
