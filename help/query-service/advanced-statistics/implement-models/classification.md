---
title: Algorithmes de classification
description: Découvrez comment configurer et optimiser divers algorithmes de classification avec des paramètres, descriptions et exemples de code clés pour vous aider à mettre en oeuvre des modèles statistiques avancés.
role: Developer
exl-id: 9105ab04-b480-48a0-b8f7-cf0ed5e5399d
source-git-commit: 489063fcd003e20f233a9c9d85d8cb6c22708d88
workflow-type: tm+mt
source-wordcount: '2449'
ht-degree: 4%

---

# Algorithmes de classification {#classification-algorithms}

Ce document présente les différents algorithmes de classification, en se concentrant sur leur configuration, leurs paramètres clés et leur utilisation pratique dans les modèles statistiques avancés. Les algorithmes de classification sont utilisés pour affecter des catégories à des points de données en fonction des fonctions d’entrée. Chaque section comprend des descriptions de paramètre et des exemples de code pour vous aider à mettre en oeuvre et à optimiser ces algorithmes pour des tâches telles que les arbres de décision, la forêt aléatoire et la classification naïve de Bayes.

## [!DNL Decision Tree Classifier] {#decision-tree-classifier}

[!DNL Decision Tree Classifier] est une approche d’apprentissage supervisée utilisée dans les statistiques, l’exploration des données et l’apprentissage automatique. Dans cette approche, un arbre de décision est utilisé comme modèle prédictif pour les tâches de classification, en tirant des conclusions d’un ensemble d’observations.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances d’un [!DNL Decision Tree Classifier].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------|
| `MAX_BINS` | Le nombre maximal de classes détermine la manière dont les fonctions continues sont divisées en intervalles discrets. Cela affecte la manière dont les fonctionnalités sont fractionnées à chaque noeud de l’arborescence de décision. Plus de classes offrent une granularité plus élevée. | 32 | Doit être au moins 2 et égal au nombre de catégories dans n’importe quelle fonctionnalité catégorielle. |
| `CACHE_NODE_IDS` | Si `false`, l’algorithme transmet les arborescences aux exécuteurs pour faire correspondre les instances aux noeuds. Si `true`, l’algorithme met en cache les identifiants de noeud pour chaque instance, accélérant l’entraînement des arborescences plus profondes. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Indique la fréquence à laquelle les identifiants de noeud mis en cache doivent être vérifiés. Par exemple, `10` signifie que le cache est coché toutes les 10 itérations. | 10 | (>= 1) |
| `IMPURITY` | Le critère utilisé pour le calcul des gains d’informations (non-respect de la casse). | &quot;gini&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | Profondeur maximale de l’arborescence (non négative). Par exemple, profondeur `0` signifie 1 noeud feuille et profondeur `1` signifie 1 noeud interne et 2 noeuds feuille. | 5 | (>= 0) (plage : [0,30]) |
| `MIN_INFO_GAIN` | Gain d’informations minimal requis pour qu’un partage soit pris en compte dans un noeud d’arborescence. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | La fraction minimale de l’échantillon pondéré que chaque enfant doit avoir après un partage. Si une division entraîne une fraction du poids total de l’un des enfants à être inférieure à cette valeur, elle est ignorée. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Le nombre minimum d’instances que chaque enfant doit avoir après un partage. Si un partage entraîne un nombre d’instances inférieur à cette valeur, le partage est ignoré. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Mémoire maximale, en Mo, allouée à l’agrégation de l’histogramme. Si cette valeur est trop petite, un seul noeud est divisé par itération et ses agrégats peuvent dépasser cette taille. | 256 | (>= 0) |
| `PREDICTION_COL` | Nom de colonne pour la sortie de prédiction. | &quot;prédiction&quot; | Toute chaîne |
| `SEED` | La graine aléatoire. | S/O | Tout nombre 64 bits |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme `1.0`. | NON DÉFINI | Toute chaîne |
| `ONE_VS_REST` | Active ou désactive l’encapsulation de cet algorithme avec le paramètre One-vs-Rest, utilisé pour les problèmes de classification à plusieurs classes. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'decision_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Factorization Machine Classifier] {#factorization-machine-classifier}

[!DNL Factorization Machine Classifier] est un algorithme de classification qui prend en charge la descente en dégradé normal et le solveur AdamW. Le modèle de classification de la machine d’usine utilise la perte logistique, qui peut être optimisée par le biais d’une descente en dégradé, et inclut souvent des termes de régularisation tels que L2 pour empêcher le surajustement.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances de [!DNL Factorization Machine Classifier].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------|
| `TOL` | La tolérance de la convergence, en contrôlant la précision de l’optimisation. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | La dimension des facteurs. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Indique s’il convient d’adapter un terme d’ordonnée à l’origine. | `true` | `true`, `false` |
| `FIT_LINEAR` | Indique s’il convient de l’adapter au terme linéaire (également appelé terme à sens unique). | `true` | `true`, `false` |
| `INIT_STD` | Écart type pour l&#39;initialisation des coefficients. | 0,01 | (>= 0) |
| `MAX_ITER` | Nombre maximal d’itérations que l’algorithme doit exécuter. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | La fraction des données à utiliser dans les mini-lots pendant la formation. Doit se trouver dans la plage `(0, 1]`. | 1.0 | 0 &lt; valeur &lt;= 1 |
| `REG_PARAM` | Le paramètre de régularisation, qui permet de contrôler la complexité du modèle et d’éviter le surajustement. | 0,0 | (>= 0) |
| `SEED` | La source aléatoire de contrôle des processus aléatoires dans l’algorithme. | S/O | Tout nombre 64 bits |
| `SOLVER` | Algorithme de résolution utilisé pour l’optimisation. Les options prises en charge sont `gd` (descente en dégradé) et `adamW`. | &quot;adamW&quot; | `gd`, `adamW` |
| `STEP_SIZE` | Taille de l’étape initiale pour l’optimisation, souvent interprétée comme le taux d’apprentissage. | 1.0 | > 0 |
| `PROBABILITY_COL` | Nom de colonne pour les probabilités conditionnelles de classe prédites. Remarque : tous les modèles ne génèrent pas de probabilités correctement calibrées ; elles doivent être traitées comme des scores de confiance plutôt que comme des probabilités exactes. | &quot;probabilité&quot; | Toute chaîne |
| `PREDICTION_COL` | Nom de colonne des libellés de classe prédéfinis. | &quot;prédiction&quot; | Toute chaîne |
| `RAW_PREDICTION_COL` | Nom de colonne pour les valeurs de prédiction brutes (également appelées degré de confiance). | &quot;rawPrediction&quot; | Toute chaîne |
| `ONE_VS_REST` | Indique s’il faut activer One-vs-Rest pour la classification à plusieurs classes. | FALSE | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree Classifier] {#gradient-boosted-tree-classifier}

L’ [!DNL Gradient Boosted Tree Classifier] utilise un ensemble d’arbres de décision pour améliorer la précision des tâches de classification, en combinant plusieurs arbres afin d’améliorer les performances du modèle.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances de [!DNL Gradient Boosted Tree Classifier].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Le nombre maximal de classes détermine la manière dont les fonctions continues sont divisées en intervalles discrets. Cela affecte la manière dont les fonctionnalités sont fractionnées à chaque noeud de l’arborescence de décision. Plus de classes offrent une granularité plus élevée. | 32 | Doit être au moins 2 et égal ou supérieur au nombre de catégories dans une fonctionnalité catégorielle. |
| `CACHE_NODE_IDS` | Si `false`, l’algorithme transmet les arborescences aux exécuteurs pour faire correspondre les instances aux noeuds. Si `true`, l’algorithme met en cache les identifiants de noeud pour chaque instance, accélérant l’entraînement des arborescences plus profondes. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Indique la fréquence à laquelle les identifiants de noeud mis en cache doivent être vérifiés. Par exemple, `10` signifie que le cache est coché toutes les 10 itérations. | 10 | (>= 1) |
| `MAX_DEPTH` | Profondeur maximale de l’arborescence (non négative). Par exemple, profondeur `0` signifie 1 noeud feuille et profondeur `1` signifie 1 noeud interne et 2 noeuds feuille. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Gain d’informations minimal requis pour qu’un partage soit pris en compte dans un noeud d’arborescence. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | La fraction minimale de l’échantillon pondéré que chaque enfant doit avoir après un partage. Si une division entraîne une fraction du poids total de l’un des enfants à être inférieure à cette valeur, elle est ignorée. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Le nombre minimum d’instances que chaque enfant doit avoir après un partage. Si un partage entraîne un nombre d’instances inférieur à cette valeur, le partage est ignoré. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Mémoire maximale, en Mo, allouée à l’agrégation de l’histogramme. Si cette valeur est trop petite, un seul noeud est divisé par itération et ses agrégats peuvent dépasser cette taille. | 256 | (>= 0) |
| `PREDICTION_COL` | Nom de colonne pour la sortie de prédiction. | &quot;prédiction&quot; | Toute chaîne |
| `VALIDATION_INDICATOR_COL` | Le nom de la colonne indique si chaque ligne est utilisée pour la formation ou la validation. La valeur `false` indique la formation et `true` la validation. Si aucune valeur n’est définie, la valeur par défaut est `None`. | &quot;Aucun&quot; | Toute chaîne |
| `RAW_PREDICTION_COL` | Nom de colonne pour les valeurs de prédiction brutes (également appelées degré de confiance). | &quot;rawPrediction&quot; | Toute chaîne |
| `LEAF_COL` | Nom de colonne des index de feuille, qui est l’index de feuille prédit de chaque instance dans chaque arborescence, généré par la traversée de pré-ordre. | &quot;&quot; | Toute chaîne |
| `FEATURE_SUBSET_STRATEGY` | Le nombre de fonctionnalités prises en compte pour le partage sur chaque noeud de l’arborescence. Options prises en charge : `auto` (déterminées automatiquement en fonction de la tâche), `all` (utilisez toutes les fonctionnalités), `onethird` (utilisez un tiers des fonctionnalités), `sqrt` (utilisez la racine carrée du nombre de fonctionnalités), `log2` (utilisez le logarithme de base 2 du nombre de fonctionnalités) et `n` (où n représente une fraction des fonctionnalités si elles se trouvent dans la plage `(0, 1]`, ou un nombre spécifique de fonctionnalités si dans la plage `[1, total number of features]`). | &quot;auto&quot; | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme `1.0`. | NON DÉFINI | Toute chaîne |
| `LOSS_TYPE` | La fonction de perte que le modèle [!DNL Gradient Boosted Tree] tente de réduire. | &quot;logistique&quot; | `logistic` (non-respect de la casse) |
| `STEP_SIZE` | La taille de l’étape (également appelée taux d’apprentissage) dans la plage `(0, 1]`, utilisée pour réduire la contribution de chaque estimateur. | 0.1 | (>= 0.0, &lt;= 1) |
| `MAX_ITER` | Nombre maximal d’itérations pour l’algorithme. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | La fraction des données d’apprentissage utilisées pour former chaque arbre de décision. La valeur doit se trouver dans la plage 0 &lt; valeur &lt;= 1. | 1.0 | `(0, 1]` |
| `PROBABILITY_COL` | Nom de colonne pour les probabilités conditionnelles de classe prédites. Remarque : tous les modèles ne génèrent pas de probabilités correctement calibrées ; elles doivent être traitées comme des scores de confiance plutôt que comme des probabilités exactes. | &quot;probabilité&quot; | Toute chaîne |
| `ONE_VS_REST` | Active ou désactive l’encapsulation de cet algorithme avec le paramètre Un par rapport au reste pour la classification à plusieurs classes. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Linear Support Vector Classifier] (LinearSVC) {#linear-support-vector-classifier}

[!DNL Linear Support Vector Classifier] (LinearSVC) construit un hyperplan pour classer les données dans un espace multidimensionnel. Vous pouvez l’utiliser pour maximiser la marge entre les classes afin de minimiser les erreurs de classification.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances de [!DNL Linear Support Vector Classifier (LinearSVC)].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_ITER` | Nombre maximal d’itérations que l’algorithme doit exécuter. | 100 | (>= 0) |
| `AGGREGATION_DEPTH` | Profondeur de l’agrégation de l’arborescence. Ce paramètre est utilisé pour réduire la surcharge de communication réseau. | 2 | Tout entier positif |
| `FIT_INTERCEPT` | S’il convient d’adapter un terme d’ordonnée à l’origine. | `true` | `true`, `false` |
| `TOL` | Ce paramètre détermine le seuil d’arrêt des itérations. | 1E-6 | (>= 0) |
| `MAX_BLOCK_SIZE_IN_MB` | Mémoire maximale en Mo pour empiler les données d’entrée dans les blocs. Si le paramètre est défini sur `0`, la valeur optimale est automatiquement sélectionnée (généralement autour de 1 Mo). | 0,0 | (>= 0) |
| `REG_PARAM` | Le paramètre de régularisation, qui permet de contrôler la complexité du modèle et d’éviter le surajustement. | 0,0 | (>= 0) |
| `STANDARDIZATION` | Ce paramètre indique s’il faut normaliser les fonctions d’entraînement avant de s’adapter au modèle. | `true` | `true`, `false` |
| `PREDICTION_COL` | Nom de colonne pour la sortie de prédiction. | &quot;prédiction&quot; | Toute chaîne |
| `RAW_PREDICTION_COL` | Nom de colonne pour les valeurs de prédiction brutes (également appelées degré de confiance). | &quot;rawPrediction&quot; | Toute chaîne |
| `ONE_VS_REST` | Active ou désactive l’encapsulation de cet algorithme avec le paramètre Un par rapport au reste pour la classification à plusieurs classes. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'linear_svc_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Logistic Regression] {#logistic-regression}

[!DNL Logistic Regression] est un algorithme supervisé utilisé pour les tâches de classification binaire. Il modélise la probabilité qu’une instance appartienne à une classe à l’aide de la fonction logistique et affecte l’instance à la classe avec la probabilité la plus élevée. Cela permet de répondre aux problèmes dans lesquels l’objectif est de séparer les données dans l’une des deux catégories.

**Paramètres**

Le tableau ci-dessous décrit les paramètres clés de configuration et d’optimisation des performances de [!DNL Logistic Regression].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------------|
| `MAX_ITER` | Nombre maximal d’itérations exécutées par l’algorithme. | 100 | (>= 0) |
| `REGPARAM` | Le paramètre de régularisation est utilisé pour contrôler la complexité du modèle. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | Le paramètre de mixage `ElasticNet` contrôle l’équilibre entre les pénalités L1 (Lasso) et L2 (Ridge). Une valeur de 0 applique une pénalité L2 (Ridge, qui réduit la taille des coefficients), tandis qu&#39;une valeur de 1 applique une pénalité L1 (Lasso, qui encourage la dispersion en fixant certains coefficients à zéro). | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'logistic_reg'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Multilayer Perceptron Classifier] {#multilayer-perceptron-classifier}

[!DNL Multilayer Perceptron Classifier] (MLPC) est un classificateur de réseau neuronal artificiel de flux. Il se compose de plusieurs couches de noeuds entièrement connectés, où chaque noeud applique une combinaison linéaire pondérée d’entrées, suivie d’une fonction d’activation. MLPC est utilisé pour des tâches de classification complexes nécessitant des limites de décision non linéaires.

**Paramètres**

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Nombre maximal d’itérations que l’algorithme doit exécuter. | 100 | (>= 0) |
| `BLOCK_SIZE` | Taille de bloc pour l’empilement des données d’entrée dans les matrices à l’intérieur des partitions. Si la taille du bloc dépasse les données restantes dans une partition, elle est ajustée en conséquence. | 128 | (>= 0) |
| `STEP_SIZE` | Taille d’étape utilisée pour chaque itération d’optimisation (applicable uniquement pour le solveur `gd`). | 0,03 | (> 0) |
| `TOL` | Tolérance de convergence pour l’optimisation. | `1E-6` | (>= 0) |
| `PREDICTION_COL` | Nom de colonne pour la sortie de prédiction. | &quot;prédiction&quot; | Toute chaîne |
| `SEED` | La source aléatoire de contrôle des processus aléatoires dans l’algorithme. | NON DÉFINI | Tout nombre 64 bits |
| `PROBABILITY_COL` | Nom de colonne pour les probabilités conditionnelles de classe prédites. Elles doivent être traitées comme des scores de confiance plutôt que comme des probabilités exactes. | &quot;probabilité&quot; | Toute chaîne |
| `RAW_PREDICTION_COL` | Nom de colonne pour les valeurs de prédiction brutes (également appelées degré de confiance). | &quot;rawPrediction&quot; | Toute chaîne |
| `ONE_VS_REST` | Active ou désactive l’encapsulation de cet algorithme avec le paramètre Un par rapport au reste pour la classification à plusieurs classes. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'multilayer_perceptron_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Naive Bayes Classifier] {#naive-bayes-classifier}

[!DNL Naive Bayes Classifier] est un classificateur à plusieurs classes probabiliste simple basé sur le théorème de Bayes avec des hypothèses d&#39;indépendance fortes (naïves) entre les caractéristiques. Il s’entraîne efficacement en calculant les probabilités conditionnelles en un seul passage sur les données d’entraînement pour calculer la distribution des probabilités conditionnelles de chaque fonction donnée à chaque étiquette. Pour les prédictions, il utilise le théorème de Bayes pour calculer la distribution de probabilité conditionnelle de chaque étiquette à la suite d’une observation.

**Paramètres**

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MODEL_TYPE` | Spécifie le type de modèle. Les options prises en charge sont `"multinomial"`, `"complement"`, `"bernoulli"` et `"gaussian"`. Le type de modèle est sensible à la casse. | &quot;multinationale&quot; | `"multinomial"`, `"complement"`, `"bernoulli"`, `"gaussian"` |
| `SMOOTHING` | Le paramètre de lissage est utilisé pour gérer les problèmes de fréquence zéro dans les données catégoriques. | 1.0 | (>= 0) |
| `PROBABILITY_COL` | Ce paramètre spécifie le nom de colonne pour les probabilités conditionnelles de classe prédites. Remarque : tous les modèles ne fournissent pas d’estimations de probabilité bien calibrées ; traitez ces valeurs comme des configurations plutôt que comme des probabilités précises. | &quot;probabilité&quot; | Toute chaîne |
| `WEIGHT_COL` | Nom de la colonne pour les poids de l’instance. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme `1.0`. | NON DÉFINI | Toute chaîne |
| `PREDICTION_COL` | Nom de colonne pour la sortie de prédiction. | &quot;prédiction&quot; | Toute chaîne |
| `RAW_PREDICTION_COL` | Nom de colonne pour les valeurs de prédiction brutes (également appelées degré de confiance). | &quot;rawPrediction&quot; | Toute chaîne |
| `ONE_VS_REST` | Indique s’il faut activer One-vs-Rest pour la classification à plusieurs classes. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'naive_bayes_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Classifier] {#random-forest-classifier}

[!DNL Random Forest Classifier] est un algorithme d’apprentissage d’ensemble qui crée plusieurs arbres de décision lors de la formation. Il atténue le surajustement en calculant la moyenne des prédictions et en sélectionnant la classe choisie par la majorité des arborescences pour les tâches de classification.

**Paramètres**

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Le nombre maximal de classes détermine la manière dont les fonctions continues sont divisées en intervalles discrets. Cela affecte la manière dont les fonctionnalités sont fractionnées à chaque noeud de l’arborescence de décision. Plus de classes offrent une granularité plus élevée. | 32 | Doit être au moins 2 et égal ou supérieur au nombre de catégories dans une fonctionnalité catégorielle. |
| `CACHE_NODE_IDS` | Si `false`, l’algorithme transmet les arborescences aux exécuteurs pour faire correspondre les instances aux noeuds. Si `true`, l’algorithme met en cache les identifiants de noeud pour chaque instance, ce qui accélère la formation. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Indique la fréquence à laquelle les identifiants de noeud mis en cache doivent être vérifiés. Par exemple, `10` signifie que le cache est coché toutes les 10 itérations. | 10 | (>= 1) |
| `IMPURITY` | Le critère utilisé pour le calcul des gains d’informations (non-respect de la casse). | &quot;gini&quot; | `entropy`, `gini` |
| `MAX_DEPTH` | Profondeur maximale de l’arborescence (non négative). Par exemple, profondeur `0` signifie 1 noeud feuille et profondeur `1` signifie 1 noeud interne et 2 noeuds feuille. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Gain d’informations minimal requis pour qu’un partage soit pris en compte dans un noeud d’arborescence. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | La fraction minimale de l’échantillon pondéré que chaque enfant doit avoir après un partage. Si une division entraîne une fraction du poids total de l’un des enfants à être inférieure à cette valeur, elle est ignorée. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Le nombre minimum d’instances que chaque enfant doit avoir après un partage. Si un partage entraîne un nombre d’instances inférieur à cette valeur, le partage est ignoré. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Mémoire maximale, en Mo, allouée à l’agrégation de l’histogramme. Si cette valeur est trop petite, un seul noeud est divisé par itération et ses agrégats peuvent dépasser cette taille. | 256 | (>= 1) |
| `PREDICTION_COL` | Nom de colonne pour la sortie de prédiction. | &quot;prédiction&quot; | Toute chaîne |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme `1.0`. | NON DÉFINI | Tout nom de colonne valide ou vide |
| `SEED` | La valeur de départ aléatoire utilisée pour contrôler les processus aléatoires dans l’algorithme. | -1689246527 | Tout nombre 64 bits |
| `BOOTSTRAP` | Indique si des exemples de bootstrap sont utilisés lors de la construction d’arbres. | `true` | `true`, `false` |
| `NUM_TREES` | Le nombre d&#39;arbres à former. Si `1`, aucun amorçage n’est utilisé. Si la valeur est supérieure à `1`, l’amorçage est appliqué. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | La fraction des données de formation utilisées pour apprendre chaque arbre de décision. | 1.0 | (> 0, &lt;= 1) |
| `LEAF_COL` | Nom de colonne des index de feuille, qui contient l’index de feuille prédit de chaque instance dans chaque arborescence par ordre prédéfini. | &quot;&quot; | Toute chaîne |
| `PROBABILITY_COL` | Nom de colonne pour les probabilités conditionnelles de classe prédites. Elles doivent être traitées comme des scores de confiance plutôt que comme des probabilités exactes. | NON DÉFINI | Toute chaîne |
| `RAW_PREDICTION_COL` | Nom de colonne pour les valeurs de prédiction brutes (également appelées degré de confiance). | &quot;rawPrediction&quot; | Toute chaîne |
| `ONE_VS_REST` | Indique s’il faut activer One-vs-Rest pour la classification à plusieurs classes. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'random_forest_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment configurer et utiliser divers algorithmes de classification. Reportez-vous ensuite aux documents sur [régression](./regression.md) et [clustering](./clustering.md) pour en savoir plus sur d’autres types de modèles statistiques avancés.
