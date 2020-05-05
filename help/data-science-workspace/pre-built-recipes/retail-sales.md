---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Recette de vente au détail
topic: overview
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# Recette de vente au détail

La recette Ventes au détail vous permet de prédire les prévisions de ventes pour tous les magasins prédits pour une certaine période. Grâce à un modèle de prévision précis, le détaillant serait en mesure de trouver la relation entre les politiques de demande et de tarification et de prendre des décisions de prix optimisées pour maximiser les ventes et les recettes.

Le document suivant répond à des questions telles que :
* Pour qui est construite cette recette ?
* Que fait cette recette ?
* Comment démarrer ?

## Pour qui est construite cette recette ?

Un détaillant doit faire face à de nombreux défis pour rester compétitif sur le marché actuel. Votre marque cherche à augmenter les ventes annuelles de votre marque de vente au détail, mais il y a de nombreuses décisions à prendre pour minimiser vos coûts d&#39;exploitation. L&#39;offre excessive augmente les coûts d&#39;inventaire, tandis qu&#39;une offre insuffisante augmente le risque de perdre des clients vers d&#39;autres marques. Avez-vous besoin de commander plus d&#39;approvisionnement pour les prochains mois ? Comment décidez-vous de la tarification optimale de vos produits pour maintenir les objectifs de vente hebdomadaires ?

## Que fait cette recette ?

La recette Prévision des ventes au détail utilise l&#39;apprentissage automatique pour prédire les tendances des ventes. La recette fait cela en exploitant la richesse des données historiques de vente au détail et en personnalisant l&#39;algorithme d&#39;apprentissage automatique de régresseurs pour prédire les ventes une semaine à l&#39;avance. Le modèle utilise l’historique des achats et les paramètres de configuration prédéterminés par défaut, déterminés par nos Data Scientists, pour améliorer la précision prédictive.

## Comment démarrer ?

Vous pouvez commencer en suivant ce [didacticiel](../jupyterlab/create-a-recipe.md).

Ce didacticiel porte sur la création de la recette Ventes au détail dans un bloc-notes Jupyter et sur l’utilisation du bloc-notes pour la recette afin de créer la recette dans Adobe Experience Platform.

## Data schema

Cette recette utilise des schémas [](../../xdm/schema/field-dictionary.md) XDM pour modéliser les données. Le schéma utilisé pour cette recette est illustré ci-dessous :

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

Tout d’abord, le jeu de données de formation dans le schéma *DSWRetailSales* est chargé. À partir de là, le modèle est formé à l’aide d’un algorithme [de régresseur](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html)de croissance en dégradé. Le gonflement des niveaux de gris se fonde sur l&#39;idée que les apprenants faibles (qui sont au moins légèrement meilleurs que les chances aléatoires) peuvent former une succession d&#39;apprenants concentrés sur l&#39;amélioration des faiblesses de l&#39;apprenant précédent. Ensemble, ils peuvent être utilisés pour créer un modèle prédictif puissant.

Le processus comprend trois éléments : une fonction de perte, un apprenant faible et un modèle additif.

La fonction de perte fait référence à une mesure de la qualité d&#39;un modèle de prévision en termes de capacité à prévoir le résultat attendu - la régression des moindres carrés est utilisée dans cette recette.

En augmentant le gradient, un arbre de décision est utilisé comme apprenant faible. En règle générale, les arbres avec un nombre limité de couches, de noeuds et de divisions sont utilisés pour s’assurer que l’apprenant reste faible.

Enfin, un modèle additif est utilisé. Après avoir calculé la perte avec la fonction de perte, l&#39;arbre qui réduit la perte est choisi et pondéré pour améliorer la modélisation des observations les plus difficiles. La production de l&#39;arbre pondéré est ensuite ajoutée à la séquence d&#39;arbres existante pour améliorer la production finale du modèle - quantité de ventes futures .