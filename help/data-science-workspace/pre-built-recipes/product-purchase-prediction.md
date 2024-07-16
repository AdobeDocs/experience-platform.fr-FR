---
keywords: Experience Platform;recette d’achat de produit;Data Science Workspace;rubriques populaires;recettes;recette de précréation
solution: Experience Platform
title: Recette de prédiction d’achat de produit
description: La recette de prédiction d’achat de produit vous permet de prévoir la probabilité d’un certain type d’événement d’achat de client, un achat de produit, par exemple.
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 94%

---

# Recette de prédiction d’achat de produit

La recette de prédiction d’achat de produit vous permet de prévoir la probabilité d’un certain type d’événement d’achat de client, un achat de produit, par exemple.

![](../images/pre-built-recipes/ppp_bigpicture.png)

Le document suivant apporte des réponses aux questions suivantes :
* Pour qui cette recette a-t-elle été créée ?
* Comment fonctionne cette recette ?

## Pour qui cette recette a-t-elle été créée ?

Votre marque cherche à augmenter les ventes trimestrielles de votre gamme de produits grâce à des promotions ciblées et efficaces destinées à vos clients. Cependant, tous les clients ne se ressemblent pas et vous voulez en avoir pour votre argent. Qui ciblez-vous ? Quels sont vos clients les plus susceptibles de répondre sans trouver votre promotion ? Comment personnaliser vos promotions pour chaque client ? Sur quels canaux vous appuyer et à quel moment envoyer des promotions ?

## Comment fonctionne cette recette ?

La recette de prédiction d’achat de produit utilise le machine learning pour prédire le comportement d’achat des clients. Pour ce faire, elle applique une forêt aléatoire personnalisée et un modèle de données d’expérience (XDM) à deux niveaux, afin de prévoir la probabilité d’un événement d’achat. Le modèle utilise des données d’entrée incorporant des informations sur les profils clients et l’historique des achats. Il utilise par défaut des paramètres de configuration prédéterminés par nos spécialistes des données afin d’améliorer la précision des prédictions.

## Schéma des données

Cette recette utilise les [schémas XDM](../../xdm/home.md) pour modéliser les données. Le schéma utilisé pour cette recette est illustré ci-dessous :

| Nom du champ | Type |
| --- | --- |
| userId | Chaîne |
| genderRatio | Nombre |
| ageY | Nombre |
| ageM | Nombre |
| optinEmail | Booléen |
| optinMobile | Booléen |
| optinAddress | Booléen |
| created | Entier |
| totalOrders | Nombre |
| totalItems | Nombre |
| orderDate1 | Nombre |
| shippingDate1 | Nombre |
| totalPrice1 | Nombre |
| tax1 | Nombre |
| orderDate2 | Nombre |
| shippingDate2 | Nombre |
| totalPrice2 | Nombre |


## Algorithme

Tout d’abord, le jeu de données d’entraînement dans le schéma *ProductPrediction* est chargé. Ensuite, le modèle est entraîné à l’aide d’une [forêt aléatoire](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). La forêt aléatoire est un type d’algorithme intégré qui fait référence à un algorithme qui combine plusieurs algorithmes pour obtenir de meilleures performances prédictives. L’idée derrière l’algorithme est que la forêt aléatoire construit plusieurs arbres de décision et les fusionne pour créer une prédiction plus précise et plus stable.

Ce processus démarre avec la création d’un ensemble d’arbres de décision qui sélectionne de manière aléatoire des sous-ensembles de données d’apprentissage. Par la suite, une moyenne des résultats de chaque arbre de décision est calculée.
