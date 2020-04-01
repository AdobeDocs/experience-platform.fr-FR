---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Recette de vente au détail
topic: overview
translation-type: tm+mt
source-git-commit: f548fb6431b7bc71c205a2b2b7ca3884e57340b1

---


# Recette de vente au détail

La recette Ventes au détail vous permet de prédire les prévisions de ventes pour tous les magasins ensemencés pour une période donnée. Avec un modèle de prévision précis, le détaillant serait en mesure de trouver la relation entre les politiques de demande et de prix et de prendre des décisions de prix optimisées pour maximiser les ventes et les recettes.

Les  suivantes répondront aux questions suivantes :
* Pour qui est construite cette recette ?
* Que fait cette recette ?
* Comment démarrer ?

## Pour qui est construite cette recette ?

Un détaillant doit faire face à de nombreux défis pour rester compétitif sur le marché actuel. Votre marque cherche à augmenter ses ventes annuelles pour votre marque de vente au détail, mais il y a de nombreuses décisions à prendre pour minimiser vos coûts d&#39;exploitation. L&#39;offre excessive augmente les coûts d&#39;inventaire, tandis que l&#39;offre insuffisante augmente le risque de perdre des clients pour d&#39;autres marques. Avez-vous besoin de commander plus d&#39;approvisionnement pour les prochains mois ? Comment décidez-vous des prix optimaux pour vos produits afin de maintenir les objectifs de ventes hebdomadaires ?

## Que fait cette recette ?

La recette Prévisions des ventes au détail utilise l&#39;apprentissage automatique pour prédire les tendances des ventes. La recette fait cela en exploitant la richesse des données historiques de vente au détail et en développant l&#39;algorithme d&#39;apprentissage automatique de régresseurs en dégradé personnalisé pour prédire les ventes une semaine à l&#39;avance. Le modèle utilise l’historique des achats et utilise par défaut des paramètres de configuration prédéterminés déterminés déterminés par nos Data Scientists pour améliorer la précision prédictive.

## Comment démarrer ?

Pour commencer, suivez ce [didacticiel](../jupyterlab/create-a-recipe.md).

Ce didacticiel décrit la création de la recette Ventes au détail dans un bloc-notes Jupyter et l’utilisation du bloc-notes pour créer la recette dans Adobe Experience Platform.

## Data schema

Cette recette utilise le [XDM](../../xdm/schema/field-dictionary.md) pour modéliser les données. Le  utilisé pour cette recette est illustré ci-dessous :

| Nom du champ | Type |
--- | ---
| date | Chaîne |
| store | Entier |
| storeType | Chaîne |
| weeklySales | Nombre |
| storeSize | Entier |
| température | Nombre |
| regionFuelPrice | Nombre |
| annotation | Nombre |
| cpi | Nombre |
| chômage | Nombre |
| isHoliday | Booléen |


## Algorithme

Tout d’abord, le jeu de données de formation dans le **DSWRetailSales** est chargé. A partir de là, le modèle est formé à l’aide d’un algorithme [de régression](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html)graduelle. L&#39;augmentation du débit utilise l&#39;idée que les apprenants faibles (qui sont au moins légèrement meilleurs que la chance aléatoire) peuvent former une succession d&#39;apprenants concentrés sur l&#39;amélioration des faiblesses de l&#39;apprenant précédent. Ensemble, ils peuvent être utilisés pour créer un modèle prédictif puissant.

Le processus comporte trois éléments : une fonction de perte, un apprenant faible et un modèle additif.

La fonction de perte fait référence à une mesure de l&#39;efficacité d&#39;un modèle de prédiction en termes de capacité à prédire le résultat attendu - la régression des moindres carrés est utilisée dans cette recette.

En cas d’augmentation du gradient, un arbre de décision est utilisé comme apprenant faible. En règle générale, les arbres avec un nombre limité de calques, de noeuds et de divisions sont utilisés pour s’assurer que l’apprenant reste faible.

Enfin, un modèle additif est utilisé. Après avoir calculé la perte avec la fonction de perte, l&#39;arbre qui réduit la perte est choisi et pondéré pour améliorer la modélisation des observations les plus difficiles. La sortie de l &#39; arbre pondéré est alors ajoutée à la séquence d &#39; arbres existante pour améliorer la sortie finale du modèle - quantité de ventes futures .