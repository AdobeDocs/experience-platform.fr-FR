---
title: Algorithmes de régression
description: Découvrez comment configurer et optimiser divers algorithmes de régression avec des paramètres, descriptions et exemples de code clés pour vous aider à mettre en oeuvre des modèles statistiques avancés.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 4%

---

# Algorithmes de régression {#regression-algorithms}

Ce document présente les différents algorithmes de régression, en se concentrant sur leur configuration, leurs paramètres clés et leur utilisation pratique dans les modèles statistiques avancés. Les algorithmes de régression sont utilisés pour modéliser la relation entre les variables dépendantes et indépendantes, prédisant des résultats continus basés sur les données observées. Chaque section comprend des descriptions de paramètre et des exemples de code pour vous aider à mettre en oeuvre et à optimiser ces algorithmes pour des tâches telles que linéaire, forêt aléatoire et régression de survie.

## régression [!DNL Decision Tree] {#decision-tree-regression}

[!DNL Decision Tree] L’apprentissage est une méthode d’apprentissage supervisée utilisée dans les statistiques, l’exploration des données et l’apprentissage automatique. Dans cette approche, un arbre de décision de classification ou de régression est utilisé comme modèle prédictif pour tirer des conclusions sur un ensemble d’observations.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances des modèles d’arbre de décision.

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Le nombre maximal de classes détermine la manière dont les fonctions continues sont divisées en intervalles discrets. Cela affecte la manière dont les fonctionnalités sont fractionnées à chaque noeud de l’arborescence de décision. Plus de classes offrent une granularité plus élevée. | 32 | Doit comporter au moins 2 catégories et au moins le nombre de catégories dans n’importe quelle fonctionnalité catégorielle. |
| `CACHE_NODE_IDS` | Si `false`, l’algorithme transmet les arborescences aux exécuteurs pour faire correspondre les instances aux noeuds. Si `true`, l’algorithme met en cache les identifiants de noeud pour chaque instance. La mise en cache peut accélérer l’entraînement des arbres plus profonds. | False | `true` ou `false`. |
| `CHECKPOINT_INTERVAL` | Indique la fréquence à laquelle les identifiants de noeud mis en cache doivent être vérifiés. Par exemple, `10` signifie que le cache sera coché toutes les 10 itérations. | 10 | (>=1) |
| `IMPURITY` | Le critère utilisé pour le calcul des gains d’informations (non-respect de la casse). | `gini` | `entropy`, `gini` |
| `MAX_DEPTH` | Profondeur maximale de l’arborescence (non négative). Par exemple, profondeur `0` signifie 1 noeud feuille et profondeur `1` signifie 1 noeud interne et 2 noeuds feuille. | 5 | [0, 30] |
| `MIN_INFO_GAIN` | Gain d’informations minimal requis pour qu’un partage soit pris en compte dans un noeud d’arborescence. | 0,0 | (>=0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | La fraction minimale de l’échantillon pondéré que chaque enfant doit avoir après un partage. Si une division entraîne une fraction du poids total de l’un des enfants à être inférieure à cette valeur, elle est ignorée. | 0,0 | (>=0.0, 0.5) |
| `MIN_INSTANCES_PER_NODE` | Le nombre minimum d’instances que chaque enfant doit avoir après un partage. Si un partage entraîne un nombre d’instances inférieur à cette valeur, le partage est ignoré. | 1 | (>=1) |
| `MAX_MEMORY_IN_MB` | Mémoire maximale, en Mo, allouée à l’agrégation de l’histogramme. Si la mémoire est trop petite, un seul noeud est divisé par itération, ce qui peut entraîner le dépassement de la taille des agrégats. | 256 |                                                                                                        |
| `PREDICTION_COL` | Paramètre du nom de la colonne de prédiction. | &quot;prédiction&quot; | Toute chaîne |
| `SEED` | Le paramètre de la valeur de départ aléatoire. | S/O | Tout nombre 64 bits |
| `WEIGHT_COL` | Le paramètre du nom de la colonne de poids. Si cette valeur n’est pas définie ou est vide, tous les poids d’instance sont traités comme `1.0`. | non défini |                                                                                                        |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'decision_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## régression [!DNL Factorization Machines] {#factorization-machines-regression}

[!DNL Factorization Machines] est un algorithme d’apprentissage par régression qui prend en charge la descente en dégradé normal et le solveur AdamW. L’algorithme est basé sur l’article de S. Rendle (2010), &quot;[!DNL Factorization Machines]&quot;.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances de la régression [!DNL Factorization Machines].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|------------------------|--------------------------------------------------------------------------------------|---------------|----------------|
| `TOL` | La tolérance à la convergence. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | La dimension des facteurs. | 8 | (>= 0) |
| `FIT_INTERCEPT` | S’il convient d’adapter un terme d’ordonnée à l’origine. | `true` | `true`, `false` |
| `FIT_LINEAR` | S’il convient de l’adapter au terme linéaire (également appelé terme à sens unique). | `true` | `true`, `false` |
| `INIT_STD` | Écart type des coefficients initiaux. | 0,01 | (>= 0) |
| `MAX_ITER` | Nombre d’itérations que l’algorithme doit exécuter. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | La fraction mini-lot, qui doit se trouver dans la plage `(0, 1]`. | 1.0 | `(0, 1]` |
| `REG_PARAM` | Paramètre de régularisation. | 0,0 | (>= 0) |
| `SEED` | La graine aléatoire. | NON DÉFINI | Tout nombre 64 bits |
| `SOLVER` | Algorithme de résolution utilisé pour l’optimisation. | &quot;adamW&quot; | `gd`, `adamW` |
| `STEP_SIZE` | Taille de l’étape initiale de la première étape (similaire au taux d’apprentissage). | 1.0 |                   |
| `PREDICTION_COL` | Nom de la colonne de prédiction. | &quot;prédiction&quot; | Toute chaîne |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## régression [!DNL Generalized Linear] {#generalized-linear-regression}

Contrairement à la régression linéaire, qui suppose que le résultat suit une distribution normale (gaussienne), les modèles [!DNL Generalized Linear] (GLM) permettent au résultat de suivre différents types de distributions, comme [!DNL Poisson] ou binomial, selon la nature des données.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances de la régression [!DNL Generalized Linear].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------|
| `MAX_ITER` | Définit le nombre maximal d’itérations (applicable lors de l’utilisation du serveur `irls`). | 25 | (>= 0) |
| `REG_PARAM` | Paramètre de régularisation. | NON DÉFINI | (>= 0) |
| `TOL` | La tolérance à la convergence. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Profondeur suggérée pour `treeAggregate`. | 2 | (>= 2) |
| `FAMILY` | Paramètre de famille, décrivant la distribution des erreurs utilisée dans le modèle. Les options prises en charge sont `gaussian`, `binomial`, `poisson`, `gamma` et `tweedie`. | &quot;gaussian&quot; | `gaussian`, `binomial`, `poisson`, `gamma`, `tweedie` |
| `FIT_INTERCEPT` | S’il convient d’adapter un terme d’ordonnée à l’origine. | `true` | `true`, `false` |
| `LINK` | La fonction de lien, qui définit la relation entre le prédicteur linéaire et la moyenne de la fonction de distribution. Les options prises en charge sont `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog` et `sqrt`. | NON DÉFINI | `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog`, `sqrt` |
| `LINK_POWER` | Index de la fonction de liaison électrique, applicable à la famille [!DNL Tweedie]. Si elle n’est pas définie, elle prend par défaut la valeur `1 - variancePower`, en suivant le package R `statmod` . Les puissances de lien de 0, 1, -1 et 0.5 correspondent respectivement aux liens Journal, Identité, Inverse et Sqrt. | 1 |
| `SOLVER` | Algorithme de résolution utilisé pour l’optimisation. Option prise en charge : `irls` (moindres carrés itérativement pondérés). | &quot;irls&quot; | `irls` |
| `VARIANCE_POWER` | Puissance de la fonction de variance de la distribution [!DNL Tweedie], qui définit la relation entre la variance et la moyenne. Les valeurs prises en charge sont 0 et `[1, inf)`. | 0,0 | 0, `[1, inf)` |
| `LINK_PREDICTION_COL` | Nom de colonne de prédiction de lien (prédicteur linéaire). | NON DÉFINI | Toute chaîne |
| `OFFSET_COL` | Nom de la colonne de décalage. Si elle n’est pas définie, tous les décalages d’instance sont traités comme 0.0. La fonction de décalage présente un coefficient constant de 1,0. | NON DÉFINI |                                                                        |
| `WEIGHT_COL` | Nom de la colonne de poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme `1.0`. Dans la famille Binomial, les poids correspondent au nombre d’essais, et les poids non entiers sont arrondis dans le calcul AIC. | NON DÉFINI |                                                                        |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'generalized_linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## régression [!DNL Gradient Boosted Tree] {#gradient-boosted-tree-regression}

Les arbres à amplification progressive (GBT) sont une méthode efficace de classification et de régression qui combine les prédictions de plusieurs arbres de décision afin d’améliorer la précision prédictive et les performances des modèles.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances de la régression [!DNL Gradient Boosted Tree].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Nombre maximal de classes utilisées pour diviser les fonctionnalités continues en intervalles discrets, ce qui permet de déterminer la manière dont les fonctionnalités sont divisées à chaque noeud de l’arborescence de décision. Plus de classes offrent une granularité plus élevée. | 32 | Doit être au moins 2 et égal ou supérieur au nombre de catégories dans une fonctionnalité catégorielle. |
| `CACHE_NODE_IDS` | Si `false`, l’algorithme transmet les arborescences aux exécuteurs pour faire correspondre les instances aux noeuds. Si `true`, l’algorithme met en cache les identifiants de noeud pour chaque instance. La mise en cache peut accélérer l’entraînement des arbres plus profonds. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Indique la fréquence à laquelle les identifiants de noeud mis en cache doivent être vérifiés. Par exemple, `10` signifie que le cache est coché toutes les 10 itérations. | 10 | (>= 1) |
| `MAX_DEPTH` | Profondeur maximale de l’arborescence (non négative). Par exemple, profondeur `0` signifie 1 noeud feuille et profondeur `1` signifie 1 noeud interne avec 2 noeuds feuille. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Gain d’informations minimal requis pour qu’un partage soit pris en compte dans un noeud d’arborescence. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | La fraction minimale de l’échantillon pondéré que chaque enfant doit avoir après un partage. Si une division entraîne une fraction du poids total de l’un des enfants à être inférieure à cette valeur, elle est ignorée. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Le nombre minimum d’instances que chaque enfant doit avoir après un partage. Si un partage entraîne un nombre d’instances inférieur à cette valeur, le partage est ignoré. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Mémoire maximale, en Mo, allouée à l’agrégation de l’histogramme. Si cette valeur est trop petite, un seul noeud est divisé par itération et ses agrégats peuvent dépasser cette taille. | 256 |                                                                                                      |
| `PREDICTION_COL` | Nom de colonne pour la sortie de prédiction. | &quot;prédiction&quot; | Toute chaîne |
| `VALIDATION_INDICATOR_COL` | Nom de colonne indiquant si chaque ligne est utilisée pour la formation ou la validation. `false` pour la formation et `true` pour la validation. | NON DÉFINI | Toute chaîne |
| `LEAF_COL` | Nom de colonne des index de feuille. Index feuille prédit de chaque instance dans chaque arborescence, généré par la traversée préordonnée. | &quot;&quot; | Toute chaîne |
| `FEATURE_SUBSET_STRATEGY` | Le nombre de fonctionnalités prises en compte pour le partage sur chaque noeud de l’arborescence. | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` (où `n` est une fraction comprise entre 0 et 1,0) |
| `SEED` | La graine aléatoire. | NON DÉFINI | Tout nombre 64 bits |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme `1.0`. | NON DÉFINI |                                                                                                      |
| `LOSS_TYPE` | La fonction de perte que le modèle [!DNL Gradient Boosted Tree] tente de réduire. | &quot;carré&quot; | `squared` (L2) et `absolute` (L1). Remarque : Les valeurs ne sont pas sensibles à la casse. |
| `STEP_SIZE` | La taille de l’étape (également appelée taux d’apprentissage) dans la plage `(0, 1]`, utilisée pour réduire la contribution de chaque estimateur. | 0.1 | `(0, 1]` |
| `MAX_ITER` | Nombre maximal d’itérations pour l’algorithme. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | La fraction des données d’apprentissage utilisées pour apprendre chaque arbre de décision, dans la plage `(0, 1]`. | 1.0 | `(0, 1]` |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## régression [!DNL Isotonic] {#isotonic-regression}

[!DNL Isotonic Regression] est un algorithme utilisé pour ajuster les distances de manière itérative tout en préservant l’ordre relatif des dissimilarités dans les données.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances de [!DNL Isotonic Regression].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `ISOTONIC` | Indique si la séquence de sortie doit être isotonique (croissant) lorsque `true` ou antitonique (décroissant) lorsque `false`. | `true` | `true`, `false` |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme `1.0`. | NON DÉFINI | Toute chaîne |
| `PREDICTION_COL` | Nom de colonne pour la sortie de prédiction. | &quot;prédiction&quot; | Toute chaîne |
| `FEATURE_INDEX` | Index de la fonctionnalité, applicable lorsque `featuresCol` est une colonne vectorielle. Si elle n’est pas définie, la valeur par défaut est `0`. Sinon, cela n&#39;aura aucun effet. | 0 |                 |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'isotonic_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## régression [!DNL Linear] {#linear-regression}

[!DNL Linear Regression] est un algorithme d’apprentissage automatique supervisé qui correspond à une équation linéaire aux données afin de modéliser la relation entre une variable dépendante et des fonctionnalités indépendantes.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances de [!DNL Linear Regression].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Nombre maximal d’itérations. | 100 | (>= 0) |
| `REGPARAM` | Paramètre de régularisation utilisé pour contrôler la complexité du modèle. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | Le paramètre de mixage ElasticNet, qui contrôle l&#39;équilibre entre les pénalités L1 (Lasso) et L2 (Ridge). Une valeur de 0 applique une pénalité L2, tandis qu’une valeur de 1 applique une pénalité L1. | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Regression] {#random-forest-regression}

[!DNL Random Forest Regression] est un algorithme d’ensemble qui crée plusieurs arbres de décision pendant la formation et renvoie la prédiction moyenne de ces arbres pour les tâches de régression, ce qui permet d’éviter le surajustement.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances de [!DNL Random Forest Regression].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Nombre maximal de classes utilisées pour discréditer les fonctionnalités continues et déterminer la manière dont les fonctionnalités sont réparties sur chaque noeud. Plus de classes offrent une granularité plus élevée. | 32 | Doit être au moins 2 et égal au nombre de catégories dans n’importe quelle fonctionnalité catégorielle. |
| `CACHE_NODE_IDS` | Si `false`, l’algorithme transmet les arborescences aux exécuteurs pour faire correspondre les instances aux noeuds. Si `true`, l’algorithme met en cache les identifiants de noeud pour chaque instance, accélérant l’entraînement des arborescences plus profondes. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Indique la fréquence à laquelle les identifiants de noeud mis en cache doivent être vérifiés. Par exemple, `10` signifie que le cache est coché toutes les 10 itérations. | 10 | (>= 1) |
| `IMPURITY` | Le critère utilisé pour le calcul des gains d’informations (non-respect de la casse). | &quot;entropie&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | Profondeur maximale de l’arborescence (non négative). Par exemple, profondeur `0` signifie 1 noeud feuille et profondeur `1` signifie 1 noeud interne et 2 noeuds feuille. | 5 | [0, 30] |
| `MIN_INFO_GAIN` | Gain d’informations minimal requis pour qu’un partage soit pris en compte dans un noeud d’arborescence. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | La fraction minimale de l’échantillon pondéré que chaque enfant doit avoir après un partage. Si une division entraîne une fraction du poids total de l’un des enfants à être inférieure à cette valeur, elle est ignorée. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Le nombre minimum d’instances que chaque enfant doit avoir après un partage. Si un partage entraîne un nombre d’instances inférieur à cette valeur, le partage est ignoré. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Mémoire maximale, en Mo, allouée à l’agrégation de l’histogramme. Si cette valeur est trop petite, un seul noeud est divisé par itération et ses agrégats peuvent dépasser cette taille. | 256 |                                                                                                      |
| `BOOTSTRAP` | Utilisation d’exemples de bootstrap lors de la construction d’arbres. | TRUE | `true`, `false` |
| `NUM_TREES` | Nombre d’arbres à entraîner (au moins 1). Si `1`, aucun amorçage n’est utilisé. Si la valeur est supérieure à `1`, l’amorçage est appliqué. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | La fraction des données d’entraînement utilisées pour former chaque arbre de décision, dans la plage `(0, 1]`. | 1.0 | `(0, 1]` |
| `LEAF_COL` | Nom de colonne des index de feuille, qui est l’index de feuille prédit de chaque instance dans chaque arborescence, généré par la traversée de pré-ordre. | &quot;&quot; | Toute chaîne |
| `PREDICTION_COL` | Nom de colonne pour la sortie de prédiction. | &quot;prédiction&quot; | Toute chaîne |
| `SEED` | La graine aléatoire. | NON DÉFINI | Tout nombre 64 bits |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme `1.0`. | NON DÉFINI | N’importe quel nom de colonne valide ou laissez-le vide. |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'random_forest_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Survival Regression] {#survival-regression}

[!DNL Survival Regression] est utilisé pour correspondre à un modèle de régression de survie paramétrique, connu sous le nom de modèle [!DNL Accelerated Failure Time] (AFT), basé sur [!DNL Weibull distribution]. Il peut empiler des instances en blocs pour améliorer les performances.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances de [!DNL Survival Regression].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Nombre maximal d’itérations que l’algorithme doit exécuter. | 100 | (>= 0) |
| `TOL` | La tolérance à la convergence. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Profondeur suggérée pour `treeAggregate`. Si les dimensions des fonctionnalités ou le nombre de partitions sont importants, ce paramètre peut être défini sur une valeur plus grande. | 2 | (>= 2) |
| `FIT_INTERCEPT` | S’il convient d’adapter un terme d’ordonnée à l’origine. | TRUE | `true`, `false` |
| `PREDICTION_COL` | Nom de colonne pour la sortie de prédiction. | &quot;prédiction&quot; | Toute chaîne |
| `CENSOR_COL` | Nom de la colonne pour la censure. Une valeur `1` indique que l’événement s’est produit (non censuré), tandis que `0` signifie que l’événement est censuré. | &quot;censor&quot; | 0, 1 |
| `MAX_BLOCK_SIZE_IN_MB` | Mémoire maximale en Mo pour empiler les données d’entrée dans les blocs. Si la taille des données restantes dans une partition est plus petite, cette valeur est ajustée en conséquence. Une valeur `0` permet un ajustement automatique. | 0,0 | (>= 0) |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'survival_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant configurer et utiliser divers algorithmes de régression. Reportez-vous ensuite aux documents sur [classification](./classification.md) et [clustering](./clustering.md) pour en savoir plus sur d’autres types de modèles statistiques avancés.
