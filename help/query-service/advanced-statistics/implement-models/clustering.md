---
title: Clusterisation d’algorithmes
description: Découvrez comment configurer et optimiser divers algorithmes de mise en grappe avec des paramètres, descriptions et exemples de code clés pour vous aider à mettre en oeuvre des modèles statistiques avancés.
role: Developer
exl-id: 273853c6-85d2-43e5-b51a-aa9d20b313ae
source-git-commit: 69c08f688d355e689e78426dd4b0ed1f4934965c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 4%

---

# Clusterisation d’algorithmes {#clustering-algorithms}

La mise en grappe d’algorithmes regroupe les points de données dans des grappes distinctes en fonction de leurs similitudes, ce qui permet à l’apprentissage non supervisé de découvrir des modèles au sein des données. Pour créer un algorithme de mise en grappe, utilisez le paramètre `type` dans la clause `OPTIONS` pour spécifier l’algorithme que vous souhaitez utiliser pour la formation de modèle. Définissez ensuite les paramètres pertinents en tant que paires clé-valeur pour affiner le modèle.

>[!NOTE]
>
>Assurez-vous de comprendre les exigences en matière de paramètres pour l’algorithme sélectionné. Si vous choisissez de ne pas personnaliser certains paramètres, le système applique les paramètres par défaut. Consultez la documentation appropriée pour comprendre la fonction et les valeurs par défaut de chaque paramètre.

## [!DNL K-Means] {#kmeans}

`K-Means` est un algorithme de mise en grappe qui partitionne les points de données en un nombre prédéfini de grappes (k). Il s’agit de l’un des algorithmes les plus couramment utilisés pour la mise en grappe en raison de sa simplicité et de son efficacité.

**Paramètres**

Lors de l’utilisation de `K-Means`, les paramètres suivants peuvent être définis dans la clause `OPTIONS` :

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|---------------------|---------------------------------------------------------------------------------------------------------------|-----------------|----------------------------------|
| `MAX_ITER` | Nombre d’itérations que l’algorithme doit exécuter. | `20` | (>= 0) |
| `TOL` | Le niveau de tolérance de la convergence. | `0.0001` | (>= 0) |
| `NUM_CLUSTERS` | Nombre de clusters à créer (`k`). | `2` | (>1) |
| `DISTANCE_TYPE` | Algorithme utilisé pour calculer la distance entre deux points. La valeur respecte la casse. | `euclidean` | `euclidean`, `cosine` |
| `KMEANS_INIT_METHOD` | Algorithme d’initialisation pour les centres de la grappe. | `k-means\|\|` | `random`, `k-means\|\|` (Une version parallèle de k-resources++) |
| `INIT_STEPS` | Nombre d’étapes pour le mode d’initialisation `k-means\|\|` (applicable uniquement lorsque `KMEANS_INIT_METHOD` est `k-means\|\|`). | `2` | (>0) |
| `PREDICTION_COL` | Nom de la colonne dans laquelle les prédictions seront stockées. | `prediction` | Toute chaîne |
| `SEED` | Une source aléatoire de reproductibilité. | `-1689246527` | Tout nombre 64 bits |
| `WEIGHT_COL` | Nom de la colonne utilisée pour les poids de l&#39;instance. Si elle n’est pas définie, toutes les instances sont pondérées de manière égale. | `not set` | S/O |

{style="table-layout:auto"}

**Exemple**

```sql
CREATE MODEL modelname 
OPTIONS(
  type = 'kmeans',
  MAX_ITERATIONS = 30,
  NUM_CLUSTERS = 4
) 
AS SELECT col1, col2, col3 FROM training-dataset;
```

## [!DNL Bisecting K-means] {#bisecting-kmeans}

[!DNL Bisecting K-means] est un algorithme de mise en grappe hiérarchique qui utilise une approche divisée (ou &quot;de haut en bas&quot;). Toutes les observations démarrent dans un seul cluster et les divisions sont récursivement effectuées lors de la création de la hiérarchie. [!DNL Bisecting K-means] peut souvent être plus rapide que les moyennes K ordinaires, mais il produit généralement des résultats de cluster différents.

**Paramètres**

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MAX_ITER` | Nombre maximal d’itérations exécutées par l’algorithme. | 20 | (>= 0) |
| `WEIGHT_COL` | Nom de la colonne pour les poids de l’instance. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme `1.0`. | NON DÉFINI | Toute chaîne |
| `NUM_CLUSTERS` | Nombre souhaité de grappes de feuilles. Le nombre réel peut être plus petit si aucune grappe divisible n’est conservée. | 4 | (> 1) |
| `SEED` | La valeur de départ aléatoire utilisée pour contrôler les processus aléatoires dans l’algorithme. | NON DÉFINI | Tout nombre 64 bits |
| `DISTANCE_MEASURE` | Mesure de la distance utilisée pour calculer la similarité entre les points. | &quot;euclidean&quot; | `euclidean`, `cosine` |
| `MIN_DIVISIBLE_CLUSTER_SIZE` | Nombre minimum de points (si >= 1.0) ou proportion minimale de points (si &lt; 1.0) requis pour la divisibilité d’un cluster. | 1.0 | (>= 0) |
| `PREDICTION_COL` | Nom de colonne pour la sortie de prédiction. | &quot;prédiction&quot; | Toute chaîne |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'bisecting_kmeans',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Gaussian Mixture Model] {#gaussian-mixture-model}

[!DNL Gaussian Mixture Model] représente une distribution composite où les points de données sont tirés d’une des sous-distributions gaussiennes k, chacune avec sa propre probabilité. Il est utilisé pour modéliser des jeux de données supposés être générés à partir d’un mélange de plusieurs distributions gaussiennes.

**Paramètres**

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Nombre maximal d’itérations que l’algorithme doit exécuter. | 100 | (>= 0) |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme `1.0`. | NON DÉFINI | Tout nom de colonne valide ou vide |
| `NUM_CLUSTERS` | Nombre de distributions gaussiennes indépendantes dans le modèle de mélange. | 2 | (> 1) |
| `SEED` | La valeur de départ aléatoire utilisée pour contrôler les processus aléatoires dans l’algorithme. | NON DÉFINI | Tout nombre 64 bits |
| `AGGREGATION_DEPTH` | Ce paramètre contrôle la profondeur des arbres d’agrégation utilisés lors du calcul. | 2 | (>= 1) |
| `PROBABILITY_COL` | Nom de colonne pour les probabilités conditionnelles de classe prédites. Elles doivent être traitées comme des scores de confiance plutôt que comme des probabilités exactes. | &quot;probabilité&quot; | Toute chaîne |
| `TOL` | Tolérance de convergence pour les algorithmes itératifs. | 0,01 | (>= 0) |
| `PREDICTION_COL` | Nom de colonne pour la sortie de prédiction. | &quot;prédiction&quot; | Toute chaîne |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'gaussian_mixture',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Latent Dirichlet Allocation] (LDA) {#latent-dirichlet-allocation}

[!DNL Latent Dirichlet Allocation] (LDA) est un modèle probabiliste qui capture la structure de rubrique sous-jacente à partir d’une collection de documents. Il s’agit d’un modèle bayésien hiérarchique à trois niveaux avec des couches de mots, de sujets et de documents. LDA utilise ces couches, ainsi que les documents observés, pour créer une structure de rubrique latente.

**Paramètres**

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Nombre maximal d’itérations exécutées par l’algorithme. | 20 | (>= 0) |
| `OPTIMIZER` | Opérateur ou algorithme d’inférence utilisé pour estimer le modèle LDA. Les options prises en charge sont `"online"` (Online Variational Bayes) et `"em"` (Expectation-Maximization). | &quot;online&quot; | `online`, `em` (non-respect de la casse) |
| `NUM_CLUSTERS` | Nombre de clusters à créer (k). | 10 | (> 1) |
| `CHECKPOINT_INTERVAL` | Indique la fréquence à laquelle les identifiants de noeud mis en cache doivent être vérifiés. | 10 | (>= 1) |
| `DOC_CONCENTRATION` | Le paramètre de concentration (&quot;alpha&quot;) détermine les hypothèses antérieures concernant la répartition des rubriques entre les documents. Le comportement par défaut est déterminé par l’optimiseur. Pour l’optimiseur `EM`, les valeurs alpha doivent être supérieures à 1.0 (valeur par défaut : uniformément distribuées sous la forme (50/k) + 1), ce qui garantit des distributions de rubrique symétriques. Pour l’optimiseur `online`, les valeurs alpha peuvent être 0 ou supérieures (par défaut : uniformément distribuées sous la forme 1.0/k), ce qui permet une initialisation de rubrique plus flexible. | Automatique | Toute valeur unique ou vecteur de longueur k où valeurs > 1 pour EM |
| `KEEP_LAST_CHECKPOINT` | Indique s’il faut conserver le dernier point de contrôle lors de l’utilisation de l’optimiseur `em`. La suppression du point de contrôle peut entraîner des échecs en cas de perte d’une partition de données. Les points de contrôle sont automatiquement supprimés du stockage lorsqu’ils ne sont plus nécessaires, comme déterminé par le comptage des références. | `true` | `true`, `false` |
| `LEARNING_DECAY` | Taux d’apprentissage de l’optimiseur `online`, défini comme un taux de désintégration exponentiel entre `(0.5, 1.0]`. | 0,51 | `(0.5, 1.0]` |
| `LEARNING_OFFSET` | Un paramètre d’apprentissage pour l’optimiseur `online` qui minimise les itérations précoces pour que les itérations précoces soient moins comptabilisées. | 1024 | (> 0) |
| `SEED` | Début aléatoire pour le contrôle de processus aléatoires dans l’algorithme. | NON DÉFINI | Tout nombre 64 bits |
| `OPTIMIZE_DOC_CONCENTRATION` | Pour l’optimiseur `online` : choisissez d’optimiser le `docConcentration` (paramètre Dirichlet pour la distribution de rubrique de document) pendant la formation. | `false` | `true`, `false` |
| `SUBSAMPLING_RATE` | Pour l’optimiseur `online` : fraction du corpus échantillonnée et utilisée à chaque itération de descente en dégradé mini-lot, dans la plage `(0, 1]`. | 0,05 | `(0, 1]` |
| `TOPIC_CONCENTRATION` | Le paramètre de concentration (&quot;beta&quot; ou &quot;eta&quot;) définit les hypothèses préalables placées sur la distribution des sujets par rapport aux termes. La valeur par défaut est déterminée par l’optimiseur : pour `EM`, valeurs > 1.0 (valeur par défaut = 0,1 + 1). Pour `online`, les valeurs ≥ 0 (par défaut = 1,0/k). | Automatique | N’importe quelle valeur unique ou vecteur de longueur k, où valeurs > 1 pour EM |
| `TOPIC_DISTRIBUTION_COL` | Ce paramètre génère la distribution estimée du mélange de rubriques pour chaque document, souvent appelé &quot;theta&quot; dans la littérature. Pour les documents vides, elle renvoie un vecteur de zéros. Les estimations sont dérivées à l’aide d’une approximation variable (&quot;gamma&quot;). | NON DÉFINI | Toute chaîne |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'lda',
) AS
  select col1, col2, col3 from training-dataset
```

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant configurer et utiliser divers algorithmes de mise en grappe. Reportez-vous ensuite aux documents sur [classification](./classification.md) et [régression](./regression.md) pour en savoir plus sur d’autres types de modèles statistiques avancés.
