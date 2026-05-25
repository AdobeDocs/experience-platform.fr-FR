---
title: Algorithmes de régression
description: Découvrez comment configurer et optimiser divers algorithmes de régression avec des paramètres clés, des descriptions et un exemple de code pour vous aider à implémenter des modèles statistiques avancés.
role: Developer
exl-id: d38733bb-0420-40bf-a70b-19e0e0e58730
TQID: https://experienceleague.adobe.com/XHag5c1xKlcp572IXdzXoEiWS-G8EBcNDlHHS1bXfNI
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 2398
ht-degree: 5%

---

# Algorithmes de régression {#regression-algorithms}

Ce document présente un aperçu de divers algorithmes de régression, en se concentrant sur leur configuration, les paramètres clés et leur utilisation pratique dans les modèles statistiques avancés. Des algorithmes de régression sont utilisés pour modéliser la relation entre les variables dépendantes et indépendantes, prédisant des résultats continus sur la base des données observées. Chaque section comprend des descriptions des paramètres et un exemple de code pour vous aider à implémenter et à optimiser ces algorithmes pour des tâches telles que la régression linéaire, aléatoire et de survie.

## régression [!DNL Decision Tree] {#decision-tree-regression}

L’apprentissage [!DNL Decision Tree] est une méthode d’apprentissage supervisé utilisée dans les domaines de la statistique, de l’exploration de données et du machine learning. Dans cette approche, un arbre de décision de classification ou de régression est utilisé comme modèle prédictif pour tirer des conclusions sur un ensemble d&#39;observations.

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de la configuration et de l’optimisation des performances des modèles d’arborescence de décision.

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Ce paramètre spécifie le nombre maximal de classes utilisées pour discrétiser les fonctions continues et déterminer les divisions au niveau de chaque nœud. Plus de compartiments permet d’obtenir une granularité et un détail plus fins. | 32 | Doit être au moins 2 et au moins le nombre de catégories dans une fonctionnalité catégorielle. |
| `CACHE_NODE_IDS` | Ce paramètre détermine s’il faut mettre en cache les identifiants de nœud pour chaque instance. S’il est `false`, l’algorithme transmet des arborescences aux exécuteurs pour faire correspondre les instances aux nœuds. S’il est `true`, l’algorithme met en cache les identifiants de nœud pour chaque instance, ce qui peut accélérer l’entraînement des arborescences plus profondes. Les utilisateurs peuvent configurer la fréquence à laquelle le cache doit être vérifié ou le désactiver en définissant `CHECKPOINT_INTERVAL`. | False | `true` ou `false`. |
| `CHECKPOINT_INTERVAL` | Ce paramètre spécifie la fréquence à laquelle les identifiants de nœud mis en cache doivent être cochés. Par exemple, la définir sur `10` signifie que le cache sera vérifié toutes les 10 itérations. Cela ne s’applique que si `CACHE_NODE_IDS` est défini sur `true` et que le répertoire des points de contrôle est configuré dans `org.apache.spark.SparkContext`. | 10 | (>=1) |
| `IMPURITY` | Ce paramètre spécifie le critère utilisé pour calculer le gain d&#39;informations. Les valeurs prises en charge sont `entropy` et `gini`. | `gini` | `entropy`, `gini` |
| `MAX_DEPTH` | Ce paramètre spécifie la profondeur maximale de l’arborescence. Par example, une profondeur de `0` signifie 1 nœud feuille, tandis qu&#39;une profondeur de `1` signifie 1 nœud interne et 2 nœuds feuilles. La profondeur doit être comprise dans la plage `[0, 30]`. | 5 | [0, 30] |
| `MIN_INFO_GAIN` | Ce paramètre définit le gain minimal d’informations requis pour qu’une division soit considérée comme valide au niveau d’un nœud d’arborescence. | 0,0 | (>=0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Ce paramètre spécifie la fraction minimale du nombre d’échantillons pondérés que chaque nœud enfant doit avoir après une division. Si l’un des nœuds enfants a une fraction inférieure à cette valeur, la division est ignorée. | 0,0 | [0.0, 0.5] |
| `MIN_INSTANCES_PER_NODE` | Ce paramètre définit le nombre minimal d’instances que chaque nœud enfant doit avoir après une division. Si une division entraîne un nombre d’instances inférieur à cette valeur, la division est ignorée comme non valide. | 1 | (>=1) |
| `MAX_MEMORY_IN_MB` | Ce paramètre spécifie la mémoire maximale, en mégaoctets (Mo), allouée pour l’agrégation des histogrammes. Si la mémoire est trop petite, un seul nœud sera divisé par itération, et ses agrégats peuvent dépasser cette taille. | 256 | Toute valeur entière positive |
| `PREDICTION_COL` | Ce paramètre spécifie le nom de la colonne utilisée pour stocker les prédictions. | « prédiction » | N’importe quelle chaîne |
| `SEED` | Ce paramètre définit la valeur de départ aléatoire utilisée dans le modèle. | Aucune | N’importe quel nombre 64 bits |
| `WEIGHT_COL` | Ce paramètre spécifie le nom de la colonne de poids. Si ce paramètre n’est pas défini ou est vide, tous les poids d’instance sont traités comme des `1.0`. | Non défini | N’importe quelle chaîne |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'decision_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## régression [!DNL Factorization Machines] {#factorization-machines-regression}

[!DNL Factorization Machines] est un algorithme d&#39;apprentissage par régression qui prend en charge la descente normale du gradient et le solveur AdamW. L&#39;algorithme est basé sur l&#39;article de S. Rendle (2010), « [!DNL Factorization Machines] ».

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de configuration et d’optimisation des performances de la régression [!DNL Factorization Machines].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|------------------------|-------------------------------------------------------------------------------------------------|---------------|-----------------------|
| `TOL` | Ce paramètre spécifie la tolérance de convergence de l&#39;algorithme. Des valeurs plus élevées peuvent entraîner une convergence plus rapide mais une précision moindre. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | Ce paramètre définit les dimensions des facteurs. Des valeurs plus élevées augmentent la complexité du modèle. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Ce paramètre indique si le modèle doit inclure un terme d&#39;interception. | `true` | `true`, `false` |
| `FIT_LINEAR` | Ce paramètre spécifie s&#39;il faut inclure un terme linéaire (également appelé terme à sens unique) dans le modèle. | `true` | `true`, `false` |
| `INIT_STD` | Ce paramètre définit l&#39;écart type des coefficients initiaux utilisés dans le modèle. | 0,01 | (>= 0) |
| `MAX_ITER` | Ce paramètre spécifie le nombre maximal d’itérations que l’algorithme doit exécuter. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Ce paramètre définit la fraction du mini-lot, qui détermine la partie des données utilisée dans chaque lot. Il doit être dans la plage `(0, 1]`. | 1.0 | `(0, 1]` |
| `REG_PARAM` | Ce paramètre définit le paramètre de régularisation pour éviter le surajustement. | 0,0 | (>= 0) |
| `SEED` | Ce paramètre spécifie l&#39;origine aléatoire utilisée pour l&#39;initialisation du modèle. | Aucune | N’importe quel nombre 64 bits |
| `SOLVER` | Ce paramètre spécifie l’algorithme du solveur utilisé pour l’optimisation. | « adamW » | `gd` (descente en gradient), `adamW` |
| `STEP_SIZE` | Ce paramètre spécifie la taille d’étape initiale (ou taux d’apprentissage) de la première étape d’optimisation. | 1.0 | Toute valeur positive |
| `PREDICTION_COL` | Ce paramètre spécifie le nom de la colonne dans laquelle les prédictions sont stockées. | « prédiction » | N’importe quelle chaîne |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## régression [!DNL Generalized Linear] {#generalized-linear-regression}

Contrairement à la régression linéaire, qui suppose que le résultat suit une distribution normale (gaussienne), les modèles [!DNL Generalized Linear] (GLM) permettent au résultat de suivre différents types de distributions, telles que [!DNL Poisson] ou binomiales, selon la nature des données.

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de configuration et d’optimisation des performances de la régression [!DNL Generalized Linear].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------|
| `MAX_ITER` | Définit le nombre maximal d&#39;itérations (applicable lors de l&#39;utilisation du `irls` du solveur). | 25 | (>= 0) |
| `REG_PARAM` | Paramètre de régularisation. | NON DÉFINI | (>= 0) |
| `TOL` | Tolérance de convergence. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Profondeur suggérée pour `treeAggregate`. | 2 | (>= 2) |
| `FAMILY` | Paramètre de famille, décrivant la distribution d’erreur utilisée dans le modèle. Les options prises en charge sont `gaussian`, `binomial`, `poisson`, `gamma` et `tweedie`. | « gaussien » | `gaussian`, `binomial`, `poisson`, `gamma`, `tweedie` |
| `FIT_INTERCEPT` | Permet de définir un terme d&#39;interception. | `true` | `true`, `false` |
| `LINK` | La fonction de liaison, qui définit la relation entre le prédicteur linéaire et la moyenne de la fonction de distribution. Les options prises en charge sont `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog` et `sqrt`. | NON DÉFINI | `identity`, `log`, `inverse`, `logit`, `probit`, `cloglog`, `sqrt` |
| `LINK_POWER` | Ce paramètre spécifie l&#39;index dans la fonction de liaison d&#39;alimentation. Le paramètre s’applique uniquement à la famille de [!DNL Tweedie]. S’il n’est pas défini, il est défini par défaut sur `1 - variancePower`, qui s’aligne sur le package R `statmod`. Les puissances de lien spécifiques de 0, 1, -1 et 0,5 correspondent respectivement aux liens Log, Identity, Inverse et Sqrt. | 1 | Toute valeur numérique |
| `SOLVER` | Algorithme du solveur utilisé pour l’optimisation. Option prise en charge : `irls` (moindres carrés repondérés de manière itérative). | « filles » | `irls` |
| `VARIANCE_POWER` | Ce paramètre spécifie la puissance dans la fonction variance de la distribution [!DNL Tweedie], définissant la relation entre variance et moyenne. Les valeurs prises en charge sont 0 et `[1, inf)`. Les puissances de variance de 0, 1 et 2 correspondent respectivement aux familles gaussiennes, de Poisson et gamma. | 0,0 | 0, `[1, inf)` |
| `LINK_PREDICTION_COL` | Nom de la colonne de prédiction de lien (prédicteur linéaire). | NON DÉFINI | N’importe quelle chaîne |
| `OFFSET_COL` | Nom de la colonne de décalage. S&#39;il n&#39;est pas défini, tous les décalages d&#39;instance sont traités comme 0,0. La fonction de décalage a un coefficient constant de 1,0. | NON DÉFINI | N’importe quelle chaîne |
| `WEIGHT_COL` | Nom de la colonne de poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme des `1.0`. Dans la famille binomiale, les poids correspondent au nombre d&#39;essais, et les poids non entiers sont arrondis dans le calcul de l&#39;AIC. | NON DÉFINI | N’importe quelle chaîne |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'generalized_linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## régression [!DNL Gradient Boosted Tree] {#gradient-boosted-tree-regression}

Les arbres amplifiés par gradient (GBT) sont une méthode efficace de classification et de régression qui combine les prédictions de plusieurs arbres de décision pour améliorer la précision prédictive et les performances du modèle.

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de configuration et d’optimisation des performances de la régression [!DNL Gradient Boosted Tree].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Nombre maximal de classes utilisé pour diviser des fonctions continues en intervalles discrets, ce qui permet de déterminer comment les fonctions sont divisées au niveau de chaque nœud de l’arborescence de décision. Plus de compartiments offrent une granularité supérieure. | 32 | Doit être au moins 2 et égal ou supérieur au nombre de catégories dans une fonctionnalité catégorielle. |
| `CACHE_NODE_IDS` | S’il est `false`, l’algorithme transmet des arborescences aux exécuteurs pour faire correspondre les instances aux nœuds. S’il est `true`, l’algorithme met en cache les identifiants de nœud pour chaque instance. La mise en cache peut accélérer l&#39;entraînement des arbres plus profonds. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Spécifie la fréquence à laquelle les ID de nœud mis en cache doivent être vérifiés. Par exemple, `10` signifie que le cache est vérifié toutes les 10 itérations. | 10 | (>= 1) |
| `MAX_DEPTH` | Profondeur maximale de l’arborescence (non négative). Par example, profondeur `0` signifie 1 nœud feuille, et profondeur `1` signifie 1 nœud interne avec 2 nœuds feuilles. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Gain d’informations minimal requis pour qu’une division soit prise en compte au niveau d’un nœud d’arborescence. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Fraction minimale du nombre d’échantillons pondérés que chaque enfant doit avoir après une division. Si une division entraîne une fraction du poids total dans l&#39;un ou l&#39;autre des enfants inférieure à cette valeur, elle est ignorée. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Nombre minimum d’instances que chaque enfant doit avoir après une division. Si une division entraîne un nombre d’instances inférieur à cette valeur, la division est ignorée. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Mémoire maximale, en Mo, allouée à l’agrégation des histogrammes. Si cette valeur est trop petite, un seul nœud est divisé par itération et ses agrégats peuvent dépasser cette taille. | 256 | Toute valeur entière positive |
| `PREDICTION_COL` | Nom de colonne de la sortie de prédiction. | « prédiction » | N’importe quelle chaîne |
| `VALIDATION_INDICATOR_COL` | Nom de colonne indiquant si chaque ligne est utilisée à des fins d’entraînement ou de validation. `false` pour la formation et `true` pour la validation. | NON DÉFINI | N’importe quelle chaîne |
| `LEAF_COL` | Nom de colonne pour les index feuille. Index feuille prédit de chaque instance dans chaque arborescence, généré par le parcours transversal de précommande. | &quot;&quot; | N’importe quelle chaîne |
| `FEATURE_SUBSET_STRATEGY` | Ce paramètre spécifie le nombre de fonctions à prendre en compte pour les divisions au niveau de chaque nœud de l&#39;arborescence. | « auto » | `auto`, `all`, `onethird`, `sqrt`, `log2` ou une fraction comprise entre 0 et 1,0 |
| `SEED` | La graine aléatoire. | NON DÉFINI | N’importe quel nombre 64 bits |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, les poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme des `1.0`. | NON DÉFINI | N’importe quelle chaîne |
| `LOSS_TYPE` | Ce paramètre spécifie la fonction de perte que le modèle de [!DNL Gradient Boosted Tree] réduit. | « au carré » | `squared` (L2) et `absolute` (L1). Remarque : les valeurs ne respectent pas la casse. |
| `STEP_SIZE` | La taille du pas (également appelée taux d’apprentissage) dans la plage `(0, 1]`, utilisée pour réduire la contribution de chaque estimateur. | 0.1 | `(0, 1]` |
| `MAX_ITER` | Nombre maximal d’itérations de l’algorithme. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Fraction des données d’apprentissage utilisées pour apprendre chaque arbre de décision, dans la plage `(0, 1]`. | 1.0 | `(0, 1]` |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## régression [!DNL Isotonic] {#isotonic-regression}

[!DNL Isotonic Regression] est un algorithme utilisé pour ajuster les distances de manière itérative tout en conservant l&#39;ordre relatif des dissimilarités dans les données.

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de la configuration et de l’optimisation des performances d’[!DNL Isotonic Regression].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `ISOTONIC` | Indique si la séquence de sortie doit être isotonique (croissante) lorsqu’elle est `true` ou antitonique (décroissante) lorsqu’elle est `false`. | `true` | `true`, `false` |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, les poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme des `1.0`. | NON DÉFINI | N’importe quelle chaîne |
| `PREDICTION_COL` | Nom de colonne de la sortie de prédiction. | « prédiction » | N’importe quelle chaîne |
| `FEATURE_INDEX` | Index de la fonction, applicable lorsque `featuresCol` est une colonne vectorielle. Si elle n’est pas définie, la valeur par défaut est `0`. Dans le cas contraire, elle n&#39;aura aucun effet. | 0 | N’importe quel entier non négatif |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'isotonic_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## régression [!DNL Linear] {#linear-regression}

[!DNL Linear Regression] est un algorithme de machine learning supervisé qui adapte une équation linéaire aux données afin de modéliser la relation entre une variable dépendante et des caractéristiques indépendantes.

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de la configuration et de l’optimisation des performances d’[!DNL Linear Regression].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Nombre maximal d’itérations. | 100 | (>= 0) |
| `REGPARAM` | Paramètre de régularisation utilisé pour contrôler la complexité du modèle. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | Le paramètre de mélange ElasticNet, qui contrôle l&#39;équilibre entre les pénalités L1 (Lasso) et L2 (Ridge). Une valeur de 0 applique une pénalité L2, tandis qu&#39;une valeur de 1 applique une pénalité L1. | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Regression] {#random-forest-regression}

[!DNL Random Forest Regression] est un algorithme d’ensemble qui crée plusieurs arborescences de décision pendant l’entraînement et renvoie la prédiction moyenne de ces arborescences pour les tâches de régression, ce qui permet d’éviter le surajustement.

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de la configuration et de l’optimisation des performances d’[!DNL Random Forest Regression].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Nombre maximal de classes utilisées pour discrétiser les fonctions continues et déterminer comment les fonctions sont fractionnées au niveau de chaque nœud. Plus de compartiments offrent une granularité supérieure. | 32 | Doit être au moins 2 et au moins égal au nombre de catégories dans une fonctionnalité catégorielle. |
| `CACHE_NODE_IDS` | S’il est `false`, l’algorithme transmet des arborescences aux exécuteurs pour faire correspondre les instances aux nœuds. S’il est `true`, l’algorithme met en cache les ID de nœud pour chaque instance, accélérant ainsi l’entraînement des arborescences plus profondes. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Spécifie la fréquence à laquelle les ID de nœud mis en cache doivent être vérifiés. Par exemple, `10` signifie que le cache est vérifié toutes les 10 itérations. | 10 | (>= 1) |
| `IMPURITY` | Critère utilisé pour le calcul du gain d’informations (non-respect de la casse). | « entropie » | `entropy`, `gini` |
| `MAX_DEPTH` | Profondeur maximale de l’arborescence (non négative). Par example, profondeur `0` signifie 1 nœud feuille, et profondeur `1` signifie 1 nœud interne et 2 nœuds feuilles. | 5 | N’importe quel entier non négatif |
| `MIN_INFO_GAIN` | Gain d’informations minimal requis pour qu’une division soit prise en compte au niveau d’un nœud d’arborescence. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Fraction minimale du nombre d’échantillons pondérés que chaque enfant doit avoir après une division. Si une division entraîne une fraction du poids total dans l&#39;un ou l&#39;autre des enfants inférieure à cette valeur, elle est ignorée. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Nombre minimum d’instances que chaque enfant doit avoir après une division. Si une division entraîne un nombre d’instances inférieur à cette valeur, la division est ignorée. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Mémoire maximale, en Mo, allouée à l’agrégation des histogrammes. Si cette valeur est trop petite, un seul nœud est divisé par itération et ses agrégats peuvent dépasser cette taille. | 256 | (>= 1) |
| `BOOTSTRAP` | Utilisation ou non des échantillons de bootstrap lors de la création d’arborescences. | VRAI | `true`, `false` |
| `NUM_TREES` | Le nombre d&#39;arbres à entraîner (au moins 1). Si `1`, aucun amorçage n’est utilisé. Si la valeur est supérieure à `1`, le bootstrapping est appliqué. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Fraction des données d’apprentissage utilisées pour entraîner chaque arborescence de décision, dans la plage `(0, 1]`. | 1.0 | (>= 0.0, &lt;= 1) |
| `LEAF_COL` | Le nom de colonne pour les indices feuilles, qui est l’indice feuille prédit de chaque instance dans chaque arborescence, généré par le parcours transversal de précommande. | &quot;&quot; | N’importe quelle chaîne |
| `PREDICTION_COL` | Nom de colonne de la sortie de prédiction. | « prédiction » | N’importe quelle chaîne |
| `SEED` | La graine aléatoire. | NON DÉFINI | N’importe quel nombre 64 bits |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, les poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme des `1.0`. | NON DÉFINI | Tout nom de colonne valide ou laissez vide. |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'random_forest_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Survival Regression] {#survival-regression}

[!DNL Survival Regression] est utilisé pour ajuster un modèle de régression de survie paramétrique, connu sous le nom de modèle [!DNL Accelerated Failure Time] (AFT), basé sur le [!DNL Weibull distribution]. Il peut empiler les instances en blocs pour améliorer les performances.

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de la configuration et de l’optimisation des performances d’[!DNL Survival Regression].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | Nombre maximal d’itérations que l’algorithme doit exécuter. | 100 | (>= 0) |
| `TOL` | Tolérance de convergence. | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | Profondeur suggérée pour `treeAggregate`. Si les cotes de la fonction ou le nombre de partitions sont importants, ce paramètre peut être défini sur une valeur plus grande. | 2 | (>= 2) |
| `FIT_INTERCEPT` | Permet de définir un terme d&#39;interception. | VRAI | `true`, `false` |
| `PREDICTION_COL` | Nom de colonne de la sortie de prédiction. | « prédiction » | N’importe quelle chaîne |
| `CENSOR_COL` | Nom de la colonne à censurer. Une valeur `1` indique que l’événement s’est produit (non censuré), tandis que `0` signifie qu’il est censuré. | « censeur » | 0, 1 |
| `MAX_BLOCK_SIZE_IN_MB` | Mémoire maximale en Mo pour l&#39;empilement des données d&#39;entrée en blocs. Si la taille des données restantes dans une partition est inférieure, cette valeur est ajustée en conséquence. Une valeur de `0` permet l’ajustement automatique. | 0,0 | (>= 0) |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'survival_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment configurer et utiliser divers algorithmes de régression. Reportez-vous ensuite aux documents sur la [classification](./classification.md) et [mise en grappe](./clustering.md) pour en savoir plus sur d’autres types de modèles statistiques avancés.
