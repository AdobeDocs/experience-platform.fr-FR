---
keywords: Experience Platform;recette de ventes au détail;Workspace de science des données;rubriques populaires;recettes;recette préconfigurée
solution: Experience Platform
title: Recette Ventes au détail
description: La recette Ventes au détail vous fournit des prévisions de ventes pour tous les magasins contrôlés pour une période donnée. Avec un modèle de prévision précis, le détaillant serait en mesure d’identifier la relation entre les politiques de demande et de prix, mais aussi de prendre des décisions optimisées concernant le prix afin de maximiser les ventes et le chiffre d’affaires.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 88%

---

# Recette Ventes au détail

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

La recette Ventes au détail vous fournit des prévisions de ventes pour tous les magasins contrôlés pour une période donnée. Avec un modèle de prévision précis, le détaillant serait en mesure d’identifier la relation entre les politiques de demande et de prix, mais aussi de prendre des décisions optimisées concernant le prix afin de maximiser les ventes et le chiffre d’affaires.

Le document suivant apporte des réponses aux questions suivantes :

* Pour qui cette recette a-t-elle été créée ?
* Comment fonctionne cette recette ?
* Comment démarrer ?

## Pour qui cette recette a-t-elle été créée ?

Un détaillant doit faire face à de nombreux défis pour rester compétitif sur le marché actuel. Votre marque cherche à augmenter ses ventes annuelles pour votre marque de vente au détail, mais de nombreuses décisions doivent être prises pour minimiser vos coûts d’exploitation. Une offre excessive augmente les coûts d’inventaire, tandis qu’une offre insuffisante augmente le risque de perdre des clients au profit d’autres marques. Avez-vous besoin de commander plus de produits pour les prochains mois ? De quelle manière établissez-vous les prix optimaux de vos produits afin de maintenir les objectifs de ventes hebdomadaires ?

## Comment fonctionne cette recette ?

La recette de prévision des ventes au détail se sert du machine learning pour prédire les tendances de vente. Pour ce faire, elle exploite la richesse des données historiques de vente au détail et développe l’algorithme de machine learning personnalisé de variable libre de boosting de gradient pour prédire les ventes une semaine à l’avance. Le modèle se sert de l’historique des achats et utilise par défaut des paramètres de configuration prédéterminés par nos spécialistes des données afin d’améliorer la précision des prédictions.

## Comment démarrer ?

Pour commencer, suivez ce [tutoriel](../jupyterlab/create-a-model.md).

Ce tutoriel abordera la création de la recette Ventes au détail dans un notebook Jupyter et l’utilisation du notebook pour créer la recette dans Adobe Experience Platform.

## Schéma des données

Cette recette utilise les [schémas XDM](../../xdm/schema/field-dictionary.md) pour modéliser les données. Le schéma utilisé pour cette recette est illustré ci-dessous :

| Nom du champ | Type |
| --- | --- |
| date | Chaîne |
| store | Entier |
| storeType | Chaîne |
| weeklySales | Nombre |
| storeSize | Entier |
| temperature | Nombre |
| regionalFuelPrice | Nombre |
| markdown | Nombre |
| cpi | Nombre |
| unemployment | Nombre |
| isHoliday | Booléen |


## Algorithme

Tout d’abord, le jeu de données d’entraînement dans le schéma *DSWRetailSales* est chargé. Ensuite, le modèle est entraîné à l’aide d’un [algorithme de variable libre de boosting de gradient](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). Le boosting de gradient part du principe que les apprenants faibles (ceux qui sont au moins légèrement supérieurs au hasard) peuvent former une succession d’apprenants concentrés sur l’amélioration des faiblesses de l’apprenant précédent. Ensemble, ils peuvent être utilisés pour créer un puissant modèle prédictif.

Le processus comprend trois éléments : une fonction de perte, un apprenant faible et un modèle additif.

La fonction de perte fait référence à une mesure de l’efficacité d’un modèle de prédiction en matière de capacité à prédire le résultat attendu ; la régression aux moindres carrés est utilisée dans cette recette.

Dans un boosting de gradient, l’apprenant faible est un arbre de décision. En règle générale, les arbres avec un nombre limité de calques, de nœuds et de divisions sont utilisés pour s’assurer que l’apprenant reste faible.

Pour finir, un modèle additif est utilisé. Après avoir calculé la perte avec la fonction de perte, l’arbre qui réduit la perte est choisi et pondéré pour améliorer la modélisation des observations les plus difficiles. Le résultat de l’arbre pondéré est alors ajouté à la séquence d’arbres existante pour améliorer le résultat final du modèle : le nombre de ventes futures.
