---
title: Algorithmes de mise en cluster
description: Découvrez comment configurer et optimiser divers algorithmes de mise en cluster avec des paramètres clés, des descriptions et un exemple de code pour vous aider à implémenter des modèles statistiques avancés.
role: Developer
exl-id: 273853c6-85d2-43e5-b51a-aa9d20b313ae
TQID: https://experienceleague.adobe.com/YNO1UpF02pB4mb0gNL4-GJ5srMjtp6RSdNkXFU72fGQ
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1035
ht-degree: 6%

---

# Algorithmes de mise en cluster {#clustering-algorithms}

Les algorithmes de mise en grappe regroupent les points de données en grappes distinctes en fonction de leurs similitudes, ce qui permet à l&#39;apprentissage non supervisé de découvrir des modèles dans les données. Pour créer un algorithme de mise en grappe, utilisez le paramètre `type` de la clause `OPTIONS` pour spécifier l&#39;algorithme à utiliser pour l&#39;entraînement des modèles. Définissez ensuite les paramètres pertinents en tant que paires clé-valeur pour affiner le modèle.

>[!NOTE]
>
>Assurez-vous de comprendre les exigences de paramètre pour l’algorithme choisi. Si vous choisissez de ne pas personnaliser certains paramètres, le système applique les paramètres par défaut. Consultez la documentation pertinente pour comprendre la fonction et les valeurs par défaut de chaque paramètre.

## [!DNL K-Means] {#kmeans}

`K-Means` est un algorithme de regroupement qui partitionne des points de données en un nombre prédéfini de grappes (k). Il s’agit de l’un des algorithmes de mise en cluster les plus couramment utilisés en raison de sa simplicité et de son efficacité.

**Paramètres**

Lors de l’utilisation de `K-Means`, les paramètres suivants peuvent être définis dans la clause `OPTIONS` :

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|---------------------|---------------------------------------------------------------------------------------------------------------|-----------------|----------------------------------|
| `MAX_ITER` | Nombre d’itérations que l’algorithme doit exécuter. | `20` | (>= 0) |
| `TOL` | Niveau de tolérance de convergence. | `0.0001` | (>= 0) |
| `NUM_CLUSTERS` | Nombre de clusters à créer (`k`). | `2` | (>1) |
| `DISTANCE_TYPE` | Algorithme utilisé pour calculer la distance entre deux points. La valeur respecte la casse. | `euclidean` | `euclidean`, `cosine` |
| `KMEANS_INIT_METHOD` | Algorithme d’initialisation des centres de cluster. | `k-means\|\|` | `random`, `k-means\|\|` (une version parallèle de k-moyennes++) |
| `INIT_STEPS` | Nombre d’étapes pour le mode d’initialisation `k-means\|\|` (applicable uniquement lorsque `KMEANS_INIT_METHOD` est `k-means\|\|`). | `2` | (>0) |
| `PREDICTION_COL` | Nom de la colonne dans laquelle les prédictions seront stockées. | `prediction` | N’importe quelle chaîne |
| `SEED` | Adresse de contrôle aléatoire pour la reproductibilité. | `-1689246527` | N’importe quel nombre 64 bits |
| `WEIGHT_COL` | Nom de la colonne utilisée pour le poids des instances. Si elle n’est pas définie, toutes les instances sont pondérées de manière égale. | `not set` | S.O. |

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

[!DNL Bisecting K-means] est un algorithme de mise en grappe hiérarchique qui utilise une approche de division (ou « descendante »). Toutes les observations commencent dans un seul cluster et les divisions sont effectuées de manière récursive à mesure que la hiérarchie est créée. [!DNL Bisecting K-means] peut souvent être plus rapide que les moyennes K normales, mais cela produit généralement des résultats de cluster différents.

**Paramètres**

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MAX_ITER` | Nombre maximal d’itérations exécutées par l’algorithme. | 20 | (>= 0) |
| `WEIGHT_COL` | Nom de la colonne pour le poids des instances. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme des `1.0`. | NON DÉFINI | N’importe quelle chaîne |
| `NUM_CLUSTERS` | Nombre souhaité de clusters de feuilles. Le nombre réel pourrait être inférieur s’il ne reste aucun cluster divisible. | 4 | (> 1) |
| `SEED` | Adresse de contrôle aléatoire utilisée pour contrôler les processus aléatoires dans l’algorithme. | NON DÉFINI | N’importe quel nombre 64 bits |
| `DISTANCE_MEASURE` | Mesure de distance utilisée pour calculer la similarité entre les points. | « euclidéen » | `euclidean`, `cosine` |
| `MIN_DIVISIBLE_CLUSTER_SIZE` | Nombre minimal de points (si >= 1,0) ou proportion minimale de points (si &lt; 1,0) requis pour qu’un cluster soit divisible. | 1.0 | (>= 0) |
| `PREDICTION_COL` | Nom de colonne de la sortie de prédiction. | « prédiction » | N’importe quelle chaîne |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'bisecting_kmeans',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Gaussian Mixture Model] {#gaussian-mixture-model}

[!DNL Gaussian Mixture Model] représente une distribution composite où les points de données sont tirés de l&#39;une des k sous-distributions gaussiennes, chacune avec sa propre probabilité. Il est utilisé pour modéliser des jeux de données qui sont supposés être générés à partir d’un mélange de plusieurs distributions gaussiennes.

**Paramètres**

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Nombre maximal d’itérations que l’algorithme peut exécuter. | 100 | (>= 0) |
| `WEIGHT_COL` | Le nom de la colonne, par exemple, les poids. Si elle n’est pas définie ou vide, tous les poids d’instance sont traités comme des `1.0`. | NON DÉFINI | Tout nom de colonne valide ou vide |
| `NUM_CLUSTERS` | Nombre de distributions gaussiennes indépendantes dans le modèle de mélange. | 2 | (> 1) |
| `SEED` | Adresse de contrôle aléatoire utilisée pour contrôler les processus aléatoires dans l’algorithme. | NON DÉFINI | N’importe quel nombre 64 bits |
| `AGGREGATION_DEPTH` | Ce paramètre contrôle la profondeur des arborescences d’agrégation utilisées lors du calcul. | 2 | (>= 1) |
| `PROBABILITY_COL` | Nom de colonne pour les probabilités conditionnelles de classe prédites. Ils doivent être traités comme des scores de confiance et non comme des probabilités exactes. | « probabilité » | N’importe quelle chaîne |
| `TOL` | Tolérance de convergence pour les algorithmes itératifs. | 0,01 | (>= 0) |
| `PREDICTION_COL` | Nom de colonne de la sortie de prédiction. | « prédiction » | N’importe quelle chaîne |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'gaussian_mixture',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Latent Dirichlet Allocation] (LDA) {#latent-dirichlet-allocation}

[!DNL Latent Dirichlet Allocation] (LDA) est un modèle probabiliste qui capture la structure de sujet sous-jacente à partir d’une collection de documents. Il s’agit d’un modèle bayésien hiérarchique à trois niveaux avec des calques de mots, de sujets et de documents. LDA utilise ces calques, ainsi que les documents observés, pour créer une structure de rubrique latente.

**Paramètres**

| Paramètre | Description | Valeur par défaut | Valeurs possibles |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | Nombre maximal d’itérations exécutées par l’algorithme. | 20 | (>= 0) |
| `OPTIMIZER` | Algorithme d’optimisation ou d’inférence utilisé pour estimer le modèle LDA. Les options prises en charge sont `"online"` (octets des variations en ligne) et `"em"` (optimisation des attentes). | « en ligne » | `online`, `em` (non-respect de la casse) |
| `NUM_CLUSTERS` | Nombre de clusters à créer (k). | 10 | (> 1) |
| `CHECKPOINT_INTERVAL` | Spécifie la fréquence à laquelle les ID de nœud mis en cache doivent être vérifiés. | 10 | (>= 1) |
| `DOC_CONCENTRATION` | Le paramètre de concentration (« alpha ») détermine les hypothèses préalables concernant la distribution thématique entre les documents. Le comportement par défaut est déterminé par l&#39;optimiseur. Pour l’optimiseur de `EM`, les valeurs alpha doivent être supérieures à 1,0 (par défaut : uniformément distribuées comme (50/k) + 1), en garantissant des distributions de rubrique symétriques. Pour l’optimiseur de `online`, les valeurs alpha peuvent être égales ou supérieures à 0 (par défaut : uniformément distribuées en tant que 1,0/k), ce qui permet une initialisation de rubrique plus flexible. | Automatique | Toute valeur unique ou vecteur de longueur k où les valeurs > 1 pour EM |
| `KEEP_LAST_CHECKPOINT` | Indique s’il faut conserver le dernier point de contrôle lors de l’utilisation de l’optimiseur `em`. La suppression du point de contrôle peut entraîner des échecs si une partition de données est perdue. Les points de contrôle sont automatiquement supprimés du stockage lorsqu’ils ne sont plus nécessaires, comme déterminé par le comptage des références. | `true` | `true`, `false` |
| `LEARNING_DECAY` | Taux d’apprentissage pour l’optimiseur de `online`, défini comme un taux de décroissance exponentiel entre les `(0.5, 1.0]`. | 0,51 | `(0.5, 1.0]` |
| `LEARNING_OFFSET` | Un paramètre d’apprentissage pour l’optimiseur de `online` qui réduit le poids des itérations précoces pour réduire leur nombre. | 1024 | (> 0) |
| `SEED` | Graine aléatoire pour contrôler des processus aléatoires dans l&#39;algorithme. | NON DÉFINI | N’importe quel nombre 64 bits |
| `OPTIMIZE_DOC_CONCENTRATION` | Pour l’optimiseur de `online` : s’il faut optimiser le `docConcentration` (paramètre Dirichlet pour la distribution document-topic) pendant l’apprentissage. | `false` | `true`, `false` |
| `SUBSAMPLING_RATE` | Pour l’optimiseur de `online` : la fraction du corpus échantillonnée et utilisée dans chaque itération de descente du gradient de mini-lot, dans la plage `(0, 1]`. | 0,05 | `(0, 1]` |
| `TOPIC_CONCENTRATION` | Le paramètre de concentration (« beta » ou « eta ») définit les hypothèses préalables placées sur les distributions des thèmes par rapport aux termes. La valeur par défaut est déterminée par l’optimiseur : par `EM`, valeurs > 1,0 (par défaut = 0,1 + 1). Par `online`, les valeurs ≥ 0 (par défaut = 1,0/k). | Automatique | Toute valeur unique ou vecteur de longueur k, où valeurs > 1 pour EM |
| `TOPIC_DISTRIBUTION_COL` | Ce paramètre produit la distribution estimée du mélange de sujets pour chaque document, souvent appelée « thêta » dans la littérature. Pour les documents vides, elle renvoie un vecteur de zéros. Les estimations sont calculées à l&#39;aide d&#39;une approximation variationnelle (« gamma »). | NON DÉFINI | N’importe quelle chaîne |

{style="table-layout:auto"}

**Exemple**

```sql
Create MODEL modelname OPTIONS(
  type = 'lda',
) AS
  select col1, col2, col3 from training-dataset
```

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment configurer et utiliser divers algorithmes de mise en cluster. Reportez-vous ensuite aux documents sur [classification](./classification.md) et [régression](./regression.md) pour en savoir plus sur d’autres types de modèles statistiques avancés.
