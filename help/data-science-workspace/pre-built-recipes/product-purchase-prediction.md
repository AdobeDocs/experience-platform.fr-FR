---
keywords: Experience Platform;product purchase recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Recette d'achat de produit
topic: overview
translation-type: tm+mt
source-git-commit: f548fb6431b7bc71c205a2b2b7ca3884e57340b1

---


# Recette d&#39;achat de produit

## Présentation

La recette Prédiction d’achat de produit vous permet de prévoir la probabilité d’un certain type de d’achat de client - un achat de produit, par exemple.

![](../images/pre-built-recipes/ppp_bigpicture.png)

Les  suivantes répondront aux questions suivantes :
* Pour qui est construite cette recette ?
* Que fait cette recette ?

## Pour qui est construite cette recette ?

Votre marque cherche à augmenter les ventes trimestrielles de votre gamme de produits grâce à des promotions ciblées et efficaces destinées à vos clients. Cependant, tous les clients ne se ressemblent pas et vous voulez que votre argent vaille. Qui -tu ? Quels sont vos clients les plus susceptibles de répondre sans que votre promotion soit intrusive ? Comment personnaliser vos promotions pour chaque client ? Sur quel  devriez-vous compter et quand devriez-vous envoyer des promotions ?

## Que fait cette recette ?

La recette Prédiction d’achat de produit utilise l’apprentissage automatique pour prédire le comportement d’achat des clients. Pour ce faire, il applique un classificateur de forêt aléatoire personnalisé et un modèle de données d’expérience à deux niveaux (XDM) afin de prévoir la probabilité d’un  d’achat. Le modèle utilise des données d’entrée incorporant des informations sur les  du client et l’historique des achats précédents et utilise par défaut des paramètres de configuration prédéterminés déterminés déterminés par nos chercheurs de données afin d’améliorer la précision prédictive.

## Data schema

Cette recette utilise le [XDM](../../xdm/home.md) pour modéliser les données. Le  utilisé pour cette recette est illustré ci-dessous :

| Nom du champ | Type |
--- | ---
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

Tout d’abord, le jeu de données de formation dans le  **ProductPrediction** est chargé. A partir de là, le modèle est formé à l&#39;aide d&#39;un classificateur [forestier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)aléatoire. Le classificateur de forêt aléatoire est un type d’algorithme intégré qui fait référence à un algorithme qui combine plusieurs algorithmes pour obtenir de meilleures performances prédictives. L&#39;idée derrière l&#39;algorithme est que le classificateur de forêt aléatoire construit plusieurs arbres de décision et les fusionne pour créer une prédiction plus précise et plus stable.

Ce processus  avec la création d’un ensemble d’arbres de décision qui sélectionne de manière aléatoire des sous-ensembles de données d’identification. Par la suite, les résultats de chaque arbre de décision sont calculés en moyenne.