---
title: Algorithmes de classification
description: Découvrez comment configurer et optimiser divers algorithmes de classification avec des paramètres clés, des descriptions et un exemple de code pour vous aider à implémenter des modèles statistiques avancés.
role: Developer
exl-id: 9105ab04-b480-48a0-b8f7-cf0ed5e5399d
TQID: https://experienceleague.adobe.com/oHjmxfPSwGAPRqt7NhiImRwULvGRr4uY1hbJBFByBqM
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 2484
ht-degree: 5%

---

# Algorithmes de classification {#classification-algorithms}

Ce document présente un aperçu de divers algorithmes de classification, en se concentrant sur leur configuration, les paramètres clés et leur utilisation pratique dans les modèles statistiques avancés. Les algorithmes de classification sont utilisés pour attribuer des catégories aux points de données en fonction des fonctionnalités d’entrée. Chaque section comprend des descriptions des paramètres et un exemple de code pour vous aider à implémenter et à optimiser ces algorithmes pour des tâches telles que les arbres de décision, la forêt aléatoire et la classification naïve de Bayes.

## [!DNL Decision Tree Classifier] {#decision-tree-classifier}

[!DNL Decision Tree Classifier] est une approche d’apprentissage supervisée utilisée dans les domaines de la statistique, de l’exploration de données et du machine learning. Dans cette approche, un arbre de décision est utilisé comme modèle prédictif pour les tâches de classification, tirant des conclusions d’un ensemble d’observations.

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de la configuration et de l’optimisation des performances d’un [!DNL Decision Tree Classifier].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------|
| `MAX_BINS` | Le nombre maximal de classes détermine la manière dont les fonctions continues sont divisées en intervalles discrets. Cela affecte la manière dont les fonctionnalités sont fractionnées au niveau de chaque nœud de l&#39;arborescence de décision. Plus de compartiments offrent une granularité supérieure. | 32 | Doit être au moins 2 et au moins égal au nombre de catégories dans une fonctionnalité catégorielle. |
| `CACHE_NODE_IDS` | S’il est `false`, l’algorithme transmet des arborescences aux exécuteurs pour faire correspondre les instances aux nœuds. S’il est `true`, l’algorithme met en cache les ID de nœud pour chaque instance, accélérant ainsi l’entraînement des arborescences plus profondes. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Spécifie la fréquence à laquelle les ID de nœud mis en cache doivent être vérifiés. Par exemple, `10` signifie que le cache est vérifié toutes les 10 itérations. | 10 | (>= 1) |
| `IMPURITY` | Critère utilisé pour le calcul du gain d’informations (non-respect de la casse). | « gini » | `entropy`, `gini` |
| `MAX_DEPTH` | Profondeur maximale de l’arborescence (non négative). Par example, profondeur `0` signifie 1 nœud feuille, et profondeur `1` signifie 1 nœud interne et 2 nœuds feuilles. | 5 | (>= 0) (plage : [0,30]) |
| `MIN_INFO_GAIN` | Gain d’informations minimal requis pour qu’une division soit prise en compte au niveau d’un nœud d’arborescence. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Fraction minimale du nombre d’échantillons pondérés que chaque enfant doit avoir après une division. Si une division entraîne une fraction du poids total dans l&#39;un ou l&#39;autre des enfants inférieure à cette valeur, elle est ignorée. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Nombre minimum d’instances que chaque enfant doit avoir après une division. Si une division entraîne un nombre d’instances inférieur à cette valeur, la division est ignorée. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Mémoire maximale, en Mo, allouée à l’agrégation des histogrammes. Si cette valeur est trop petite, un seul nœud est divisé par itération et ses agrégats peuvent dépasser cette taille. | 256 | (>= 0) |
| `PREDICTION_COL` | Nom de colonne de la sortie de prédiction. | « prédiction » | N’importe quelle chaîne |
| `SEED` | La graine aléatoire. | S.O. | N’importe quel nombre 64 bits |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, les poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme des `1.0`. | NON DÉFINI | N’importe quelle chaîne |
| `ONE_VS_REST` | Active ou désactive l’encapsulation de cet algorithme avec One-vs-Rest, utilisé pour les problèmes de classification multiclasse. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'decision_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Factorization Machine Classifier] {#factorization-machine-classifier}

Le [!DNL Factorization Machine Classifier] est un algorithme de classification qui prend en charge la descente normale du gradient et le solveur AdamW. Le modèle de classification de la machine de factorisation utilise la perte logistique, qui peut être optimisée par descente en gradient, et inclut souvent des termes de régularisation comme L2 pour éviter le surajustement.

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de la configuration et de l’optimisation des performances de l’[!DNL Factorization Machine Classifier].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------|
| `TOL` | La tolérance de convergence, qui contrôle la précision de l’optimisation. | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | La dimensionnalité des facteurs. | 8 | (>= 0) |
| `FIT_INTERCEPT` | Spécifie s&#39;il faut adapter un terme d&#39;interception. | `true` | `true`, `false` |
| `FIT_LINEAR` | Indique s’il faut ajuster le terme linéaire (également appelé terme à une seule voie). | `true` | `true`, `false` |
| `INIT_STD` | Écart type pour l&#39;initialisation des coefficients. | 0,01 | (>= 0) |
| `MAX_ITER` | Nombre maximal d’itérations que l’algorithme peut exécuter. | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | Fraction des données à utiliser dans des mini-lots pendant l’entraînement. Doit être dans la plage `(0, 1]`. | 1.0 | 0 &lt; valeur &lt;= 1 |
| `REG_PARAM` | Le paramètre de régularisation qui permet de contrôler la complexité du modèle et d’éviter le surajustement. | 0,0 | (>= 0) |
| `SEED` | Graine aléatoire pour le contrôle des processus aléatoires dans l&#39;algorithme. | S.O. | N’importe quel nombre 64 bits |
| `SOLVER` | Algorithme du solveur utilisé pour l’optimisation. Les options prises en charge sont `gd` (descente en dégradé) et `adamW`. | « adamW » | `gd`, `adamW` |
| `STEP_SIZE` | La taille d’étape initiale de l’optimisation, souvent interprétée comme le taux d’apprentissage. | 1.0 | > 0 |
| `PROBABILITY_COL` | Nom de colonne pour les probabilités conditionnelles de classe prédites. Remarque : tous les modèles ne génèrent pas des probabilités bien calibrées ; elles doivent être traitées comme des scores de confiance plutôt que comme des probabilités exactes. | « probabilité » | N’importe quelle chaîne |
| `PREDICTION_COL` | Nom de colonne pour les libellés de classe prédits. | « prédiction » | N’importe quelle chaîne |
| `RAW_PREDICTION_COL` | Nom de colonne des valeurs de prédiction brutes (également appelé confiance). | « rawPrediction » | N’importe quelle chaîne |
| `ONE_VS_REST` | Indique s’il faut activer One-vs-Rest pour la classification multiclasse. | FALSE | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree Classifier] {#gradient-boosted-tree-classifier}

Le [!DNL Gradient Boosted Tree Classifier] utilise un ensemble d’arbres de décision pour améliorer la précision des tâches de classification, en combinant plusieurs arbres pour améliorer les performances du modèle.

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de la configuration et de l’optimisation des performances de l’[!DNL Gradient Boosted Tree Classifier].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Le nombre maximal de classes détermine la manière dont les fonctions continues sont divisées en intervalles discrets. Cela affecte la manière dont les fonctionnalités sont fractionnées au niveau de chaque nœud de l&#39;arborescence de décision. Plus de compartiments offrent une granularité supérieure. | 32 | Doit être au moins 2 et égal ou supérieur au nombre de catégories dans une fonctionnalité catégorielle. |
| `CACHE_NODE_IDS` | S’il est `false`, l’algorithme transmet des arborescences aux exécuteurs pour faire correspondre les instances aux nœuds. S’il est `true`, l’algorithme met en cache les ID de nœud pour chaque instance, accélérant ainsi l’entraînement des arborescences plus profondes. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Spécifie la fréquence à laquelle les ID de nœud mis en cache doivent être vérifiés. Par exemple, `10` signifie que le cache est vérifié toutes les 10 itérations. | 10 | (>= 1) |
| `MAX_DEPTH` | Profondeur maximale de l’arborescence (non négative). Par example, profondeur `0` signifie 1 nœud feuille, et profondeur `1` signifie 1 nœud interne et 2 nœuds feuilles. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Gain d’informations minimal requis pour qu’une division soit prise en compte au niveau d’un nœud d’arborescence. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Fraction minimale du nombre d’échantillons pondérés que chaque enfant doit avoir après une division. Si une division entraîne une fraction du poids total dans l&#39;un ou l&#39;autre des enfants inférieure à cette valeur, elle est ignorée. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Nombre minimum d’instances que chaque enfant doit avoir après une division. Si une division entraîne un nombre d’instances inférieur à cette valeur, la division est ignorée. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Mémoire maximale, en Mo, allouée à l’agrégation des histogrammes. Si cette valeur est trop petite, un seul nœud est divisé par itération et ses agrégats peuvent dépasser cette taille. | 256 | (>= 0) |
| `PREDICTION_COL` | Nom de colonne de la sortie de prédiction. | « prédiction » | N’importe quelle chaîne |
| `VALIDATION_INDICATOR_COL` | Le nom de la colonne indique si chaque ligne est utilisée pour la formation ou la validation. Une valeur `false` indique la formation et `true` indique la validation. Si aucune valeur n’est définie, la valeur par défaut est `None`. | &quot;Aucun&quot; | N’importe quelle chaîne |
| `RAW_PREDICTION_COL` | Nom de colonne des valeurs de prédiction brutes (également appelé confiance). | « rawPrediction » | N’importe quelle chaîne |
| `LEAF_COL` | Le nom de colonne pour les indices feuilles, qui est l’indice feuille prédit de chaque instance dans chaque arborescence, généré par le parcours transversal de précommande. | &quot;&quot; | N’importe quelle chaîne |
| `FEATURE_SUBSET_STRATEGY` | Nombre de fonctions prises en compte pour la division au niveau de chaque nœud de l’arborescence. Options prises en charge : `auto` (déterminée automatiquement en fonction de la tâche), `all` (utiliser toutes les fonctionnalités), `onethird` (utiliser un tiers des fonctionnalités), `sqrt` (utiliser la racine carrée du nombre de fonctionnalités), `log2` (utiliser le logarithme de base-2 du nombre de fonctionnalités) et `n` (où n est soit une fraction des fonctionnalités si elle se trouve dans la plage `(0, 1]`, soit un nombre spécifique de fonctionnalités si elle se trouve dans la plage `[1, total number of features]`). | « auto » | `auto`, `all`, `onethird`, `sqrt`, `log2`, `n` |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, les poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme des `1.0`. | NON DÉFINI | N’importe quelle chaîne |
| `LOSS_TYPE` | Fonction de perte que le modèle de [!DNL Gradient Boosted Tree] tente de minimiser. | « logistique » | `logistic` (non sensible à la casse) |
| `STEP_SIZE` | La taille du pas (également appelée taux d’apprentissage) dans la plage `(0, 1]`, utilisée pour réduire la contribution de chaque estimateur. | 0.1 | (>= 0.0, &lt;= 1) |
| `MAX_ITER` | Nombre maximal d’itérations de l’algorithme. | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | Fraction des données d’apprentissage utilisées pour entraîner chaque arborescence de décision. La valeur doit être comprise dans la plage 0 &lt; valeur &lt;= 1. | 1.0 | `(0, 1]` |
| `PROBABILITY_COL` | Nom de colonne pour les probabilités conditionnelles de classe prédites. Remarque : tous les modèles ne génèrent pas des probabilités bien calibrées ; elles doivent être traitées comme des scores de confiance plutôt que comme des probabilités exactes. | « probabilité » | N’importe quelle chaîne |
| `ONE_VS_REST` | Active ou désactive l’encapsulation de cet algorithme avec One-vs-Rest pour la classification multiclasse. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Linear Support Vector Classifier] (linéaireSVC) {#linear-support-vector-classifier}

Le [!DNL Linear Support Vector Classifier] (LinearSVC) construit un hyperplan pour classer les données dans un espace à dimensions élevées. Vous pouvez l’utiliser pour maximiser la marge entre les classes afin de minimiser les erreurs de classification.

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de la configuration et de l’optimisation des performances de l’[!DNL Linear Support Vector Classifier (LinearSVC)].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_ITER` | Nombre maximal d’itérations que l’algorithme peut exécuter. | 100 | (>= 0) |
| `AGGREGATION_DEPTH` | Profondeur de l’agrégation d’arborescences. Ce paramètre est utilisé pour réduire la surcharge de communication réseau. | 2 | N’importe quel entier positif |
| `FIT_INTERCEPT` | Permet de définir un terme d&#39;interception. | `true` | `true`, `false` |
| `TOL` | Ce paramètre détermine le seuil d’arrêt des itérations. | 1E-6 | (>= 0) |
| `MAX_BLOCK_SIZE_IN_MB` | Mémoire maximale en Mo pour l&#39;empilement des données d&#39;entrée en blocs. Si le paramètre est défini sur `0`, la valeur optimale est automatiquement choisie (généralement autour de 1 Mo). | 0,0 | (>= 0) |
| `REG_PARAM` | Le paramètre de régularisation qui permet de contrôler la complexité du modèle et d’éviter le surajustement. | 0,0 | (>= 0) |
| `STANDARDIZATION` | Ce paramètre indique s&#39;il faut normaliser les fonctions d&#39;entraînement avant d&#39;adapter le modèle. | `true` | `true`, `false` |
| `PREDICTION_COL` | Nom de colonne de la sortie de prédiction. | « prédiction » | N’importe quelle chaîne |
| `RAW_PREDICTION_COL` | Nom de colonne des valeurs de prédiction brutes (également appelé confiance). | « rawPrediction » | N’importe quelle chaîne |
| `ONE_VS_REST` | Active ou désactive l’encapsulation de cet algorithme avec One-vs-Rest pour la classification multiclasse. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'linear_svc_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Logistic Regression] {#logistic-regression}

[!DNL Logistic Regression] est un algorithme supervisé utilisé pour les tâches de classification binaire. Il modélise la probabilité qu’une instance appartient à une classe à l’aide de la fonction logistique et attribue l’instance à la classe ayant la probabilité la plus élevée. Cela le rend adapté aux problèmes où l’objectif est de séparer les données en deux catégories.

**Paramètres**

Le tableau ci-dessous présente les paramètres clés de la configuration et de l’optimisation des performances d’[!DNL Logistic Regression].

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------------|
| `MAX_ITER` | Nombre maximal d’itérations exécutées par l’algorithme. | 100 | (>= 0) |
| `REGPARAM` | Le paramètre de régularisation est utilisé pour contrôler la complexité du modèle. | 0,0 | (>= 0) |
| `ELASTICNETPARAM` | Le paramètre de mélange `ElasticNet` contrôle l&#39;équilibre entre les pénalités L1 (Lasso) et L2 (Ridge). Une valeur de 0 applique une pénalité L2 (Ridge, qui réduit la taille des coefficients), tandis qu&#39;une valeur de 1 applique une pénalité L1 (Lasso, qui encourage la parcimonie en mettant certains coefficients à zéro). | 0,0 | (>= 0, &lt;= 1) |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'logistic_reg'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Multilayer Perceptron Classifier] {#multilayer-perceptron-classifier}

Le [!DNL Multilayer Perceptron Classifier] (MLPC) est un classificateur de réseau neuronal artificiel à action directe. Il se compose de plusieurs couches de nœuds entièrement connectées, chaque nœud appliquant une combinaison linéaire pondérée d’entrées, suivie d’une fonction d’activation. Le MLPC est utilisé pour des tâches de classification complexes nécessitant des limites de décision non linéaires.

**Paramètres**

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Nombre maximal d’itérations que l’algorithme peut exécuter. | 100 | (>= 0) |
| `BLOCK_SIZE` | Taille de bloc pour l’empilement des données d’entrée dans des matrices au sein des partitions. Si la taille du bloc dépasse les données restantes dans une partition, elle est ajustée en conséquence. | 128 | (>= 0) |
| `STEP_SIZE` | Taille d’étape utilisée pour chaque itération de l’optimisation (applicable uniquement pour les `gd` du solveur). | 0,03 | (> 0) |
| `TOL` | Tolérance de convergence pour l’optimisation. | `1E-6` | (>= 0) |
| `PREDICTION_COL` | Nom de colonne de la sortie de prédiction. | « prédiction » | N’importe quelle chaîne |
| `SEED` | Graine aléatoire pour le contrôle des processus aléatoires dans l&#39;algorithme. | NON DÉFINI | N’importe quel nombre 64 bits |
| `PROBABILITY_COL` | Nom de colonne pour les probabilités conditionnelles de classe prédites. Ils doivent être traités comme des scores de confiance et non comme des probabilités exactes. | « probabilité » | N’importe quelle chaîne |
| `RAW_PREDICTION_COL` | Nom de colonne des valeurs de prédiction brutes (également appelé confiance). | « rawPrediction » | N’importe quelle chaîne |
| `ONE_VS_REST` | Active ou désactive l’encapsulation de cet algorithme avec One-vs-Rest pour la classification multiclasse. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'multilayer_perceptron_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Naive Bayes Classifier] {#naive-bayes-classifier}

[!DNL Naive Bayes Classifier] est un classificateur probabiliste simple, multiclasse basé sur le théorème de Bayes avec des hypothèses d&#39;indépendance fortes (naïves) entre les caractéristiques. Il s&#39;entraîne efficacement en calculant des probabilités conditionnelles en une seule passe sur les données d&#39;entraînement pour calculer la distribution de probabilité conditionnelle de chaque caractéristique donnée à chaque étiquette. Pour les prédictions, elle utilise le théorème de Bayes pour calculer la loi de probabilité conditionnelle de chaque étiquette donnée à une observation.

**Paramètres**

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MODEL_TYPE` | Indique le type de modèle. Les options prises en charge sont `"multinomial"`, `"complement"`, `"bernoulli"` et `"gaussian"`. Le type de modèle respecte la casse. | « multinomial » | `"multinomial"`, `"complement"`, `"bernoulli"`, `"gaussian"` |
| `SMOOTHING` | Le paramètre de lissage est utilisé pour gérer les problèmes de fréquence nulle dans les données catégorielles. | 1.0 | (>= 0) |
| `PROBABILITY_COL` | Ce paramètre spécifie le nom de colonne pour les probabilités conditionnelles de classe prédites. Remarque : tous les modèles ne fournissent pas des estimations de probabilité bien calibrées ; traitez ces valeurs comme des confidences plutôt que comme des probabilités précises. | « probabilité » | N’importe quelle chaîne |
| `WEIGHT_COL` | Nom de la colonne pour le poids des instances. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme des `1.0`. | NON DÉFINI | N’importe quelle chaîne |
| `PREDICTION_COL` | Nom de colonne de la sortie de prédiction. | « prédiction » | N’importe quelle chaîne |
| `RAW_PREDICTION_COL` | Nom de colonne des valeurs de prédiction brutes (également appelé confiance). | « rawPrediction » | N’importe quelle chaîne |
| `ONE_VS_REST` | Indique s’il faut activer One-vs-Rest pour la classification multiclasse. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'naive_bayes_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Classifier] {#random-forest-classifier}

[!DNL Random Forest Classifier] est un algorithme d’apprentissage d’ensemble qui crée plusieurs arbres de décision pendant l’apprentissage. Il atténue le surajustement en faisant la moyenne des prédictions et en sélectionnant la classe choisie par la majorité des arbres pour les tâches de classification.

**Paramètres**

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | Le nombre maximal de classes détermine la manière dont les fonctions continues sont divisées en intervalles discrets. Cela affecte la manière dont les fonctionnalités sont fractionnées au niveau de chaque nœud de l&#39;arborescence de décision. Plus de compartiments offrent une granularité supérieure. | 32 | Doit être au moins 2 et égal ou supérieur au nombre de catégories dans une fonctionnalité catégorielle. |
| `CACHE_NODE_IDS` | S’il est `false`, l’algorithme transmet des arborescences aux exécuteurs pour faire correspondre les instances aux nœuds. S’il est `true`, l’algorithme met en cache les identifiants de nœud pour chaque instance, accélérant ainsi l’entraînement. | `false` | `true`, `false` |
| `CHECKPOINT_INTERVAL` | Spécifie la fréquence à laquelle les ID de nœud mis en cache doivent être vérifiés. Par exemple, `10` signifie que le cache est vérifié toutes les 10 itérations. | 10 | (>= 1) |
| `IMPURITY` | Critère utilisé pour le calcul du gain d’informations (non-respect de la casse). | « gini » | `entropy`, `gini` |
| `MAX_DEPTH` | Profondeur maximale de l’arborescence (non négative). Par example, profondeur `0` signifie 1 nœud feuille, et profondeur `1` signifie 1 nœud interne et 2 nœuds feuilles. | 5 | (>= 0) |
| `MIN_INFO_GAIN` | Gain d’informations minimal requis pour qu’une division soit prise en compte au niveau d’un nœud d’arborescence. | 0,0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | Fraction minimale du nombre d’échantillons pondérés que chaque enfant doit avoir après une division. Si une division entraîne une fraction du poids total dans l&#39;un ou l&#39;autre des enfants inférieure à cette valeur, elle est ignorée. | 0,0 | (>= 0.0, &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | Nombre minimum d’instances que chaque enfant doit avoir après une division. Si une division entraîne un nombre d’instances inférieur à cette valeur, la division est ignorée. | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | Mémoire maximale, en Mo, allouée à l’agrégation des histogrammes. Si cette valeur est trop petite, un seul nœud est divisé par itération et ses agrégats peuvent dépasser cette taille. | 256 | (>= 1) |
| `PREDICTION_COL` | Nom de colonne de la sortie de prédiction. | « prédiction » | N’importe quelle chaîne |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, les poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme des `1.0`. | NON DÉFINI | Tout nom de colonne valide ou vide |
| `SEED` | Adresse de contrôle aléatoire utilisée pour contrôler les processus aléatoires dans l’algorithme. | -1689246527 | N’importe quel nombre 64 bits |
| `BOOTSTRAP` | Indique si les exemples de bootstrap sont utilisés lors de la création d’arborescences. | `true` | `true`, `false` |
| `NUM_TREES` | Le nombre d&#39;arbres à entraîner. Si `1`, aucun amorçage n’est utilisé. Si la valeur est supérieure à `1`, le bootstrapping est appliqué. | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | Fraction des données d’apprentissage utilisées pour apprendre chaque arborescence de décision. | 1.0 | (> 0, &lt;= 1) |
| `LEAF_COL` | Le nom de colonne des indices feuilles, qui contient l’index feuille prédit de chaque instance dans chaque arborescence par préordre. | &quot;&quot; | N’importe quelle chaîne |
| `PROBABILITY_COL` | Nom de colonne pour les probabilités conditionnelles de classe prédites. Ils doivent être traités comme des scores de confiance et non comme des probabilités exactes. | NON DÉFINI | N’importe quelle chaîne |
| `RAW_PREDICTION_COL` | Nom de colonne des valeurs de prédiction brutes (également appelé confiance). | « rawPrediction » | N’importe quelle chaîne |
| `ONE_VS_REST` | Indique s’il faut activer One-vs-Rest pour la classification multiclasse. | `false` | `true`, `false` |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'random_forest_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment configurer et utiliser divers algorithmes de classification. Reportez-vous ensuite aux documents sur [régression](./regression.md) et [mise en grappe](./clustering.md) pour en savoir plus sur d’autres types de modèles statistiques avancés.
