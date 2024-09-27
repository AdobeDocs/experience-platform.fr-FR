---
title: Analyse efficace des Big Data avec des hypercubes dans Experience Query Service
description: Découvrez comment utiliser des hypercubes dans Adobe Experience Platform Query Service pour optimiser l’analyse des données volumineuses avec un comptage unique approximatif, ce qui réduit la nécessité d’un retraitement complet des données.
source-git-commit: 67d4bcbf2a055d4427218ba7d98355f09d860a8c
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 2%

---

# Analyse efficace des données volumineuses avec des hypercubes

>[!AVAILABILITY]
>
>Cette fonctionnalité n’est disponible que pour les utilisateurs qui ont acheté le [SKU de Distiller de données](../data-distiller/overview.md). Pour plus d’informations, contactez votre représentant d’Adobe.

Découvrez comment utiliser des hypercubes dans Adobe Experience Platform Experience Query Service pour effectuer une analyse avancée des données avec une efficacité accrue. Ce document explique comment utiliser les fonctions avancées de la [[!DNL Apache Datasketches] bibliothèque](https://datasketches.apache.org/) pour gérer des comptes distincts et des calculs complexes de manière incrémentielle, sans avoir à retraiter les données historiques à chaque fois.

Dans l’analyse des données volumineuses, la génération de mesures telles que des décomptes distincts, des quantiles, des éléments les plus fréquents, des jointures et des analyses graphiques implique souvent un comptage non additif (où les résultats ne peuvent pas simplement être résumés à partir de sous-groupes). Les méthodes traditionnelles nécessitent le retraitement de toutes les données historiques, ce qui peut nécessiter beaucoup de ressources et prendre du temps. Utilisez des schémas, qui sont des résumés compacts qui utilisent des probabilités pour représenter des jeux de données volumineux, et des fonctions avancées de Query Service pour rationaliser ce processus en réduisant la nécessité de recalculer.

## Fonctions clés des hypercubes {#key-functions}

Les hypercubes offrent plusieurs fonctions puissantes pour améliorer l’efficacité et la flexibilité de l’analyse des données.

1. **Compter les utilisateurs uniques ou les requêtes distinctes** : utilisez les fonctionnalités SQL pour générer des nombres uniques d’utilisateurs interagissant avec diverses dimensions de données, telles que les consultations de produits, les visites de site ou l’activité commerciale, sans réanalyser à plusieurs reprises les données brutes.
2. **Traitement incrémentiel** : effectuez des mises à jour incrémentielles pour plier et fusionner des points de données sur plusieurs dimensions et dans le temps sans recalculer tout de zéro.
3. **Analyse multidimensionnelle** : les hypercubes permettent le filtrage multidimensionnel et la réorganisation des données afin de créer des lignes récapitulatives qui représentent des combinaisons de dimensions. Ces résumés peuvent ensuite être utilisés pour générer des informations avec un temps de calcul minimal.

## Cas pratiques des hypercubes {#use-cases}

Utilisez des hypercubes pour générer efficacement des nombres distincts pour diverses interactions utilisateur sans recalculer complètement les données à chaque fois. Voici quelques scénarios pratiques d’utilisation :

- Analysez les visiteurs uniques qui affichent des produits spécifiques au cours d’une période définie.
- Identifiez les utilisateurs qui interagissent avec plusieurs produits au cours d’une période donnée afin d’améliorer l’analyse des ventes croisées.
- Distinguer les utilisateurs qui interagissent avec un produit mais pas avec un autre au fil du temps pour découvrir les modèles de préférences.
- Combinez les données d’interaction en ligne et hors ligne pour obtenir une vue d’ensemble complète du comportement des utilisateurs sur une période donnée.
- Effectuez le suivi des mouvements des utilisateurs dans différentes activités au sein d’un événement afin d’optimiser la mise en page et les services.

## Avantages des hypercubes

Dans ce cas, vous pouvez pré-calculer des informations de base pour des catégories spécifiques. Cependant, lors de l’analyse des données sur plusieurs dimensions et périodes, vous devez soit recalculer tout le contenu des données brutes, soit utiliser un hypercube Query Service. Les hypercubes rationalisent le processus en organisant efficacement les données, ce qui permet un filtrage flexible et une analyse multidimensionnelle sans retraitement. Ils utilisent des fonctions avancées pour estimer les résultats rapidement et précisément afin d’offrir des avantages clés tels qu’une meilleure efficacité de traitement, une évolutivité et une adaptabilité améliorées pour des tâches analytiques complexes.

### Efficacité de la taille des données pour le traitement des requêtes

Query Service peut compresser des millions ou des milliards de points de données (par exemple, les identifiants utilisateur) dans un formulaire compact appelé schéma. Cette esquisse a une taille de données considérablement réduite pour le traitement des requêtes, ce qui permet de maintenir l’évolutivité et de travailler beaucoup plus facilement et plus rapidement. Quelle que soit la taille des données originales, la taille du schéma reste petite, ce qui rend l&#39;analyse des données volumineuses beaucoup plus gérable et efficace.

Le diagramme ci-dessous illustre la manière dont Commerce, les Informations sur les produits et la dimension web ExperienceEvents sont traités en schémas, qui sont ensuite utilisés pour approximer des nombres uniques.

![Infographie montrant la création de schémas à l’aide de Query Service. Le diagramme illustre la manière dont les événements d’expérience avec les dimensions Commerce, Product Info et Web sont traités en schémas, qui sont ensuite utilisés pour approcher des nombres uniques.](../images/hypercubes/hypercube-overview.png)

### Fusionner des schémas pour faciliter et accélérer l’analyse des données

Pour éviter de recalculer et d’améliorer la vitesse de traitement, vous pouvez fusionner des esquisses de différentes catégories ou groupes. Query Service simplifie également la conception en organisant vos données dans un hypercube, où chaque ligne devient un résumé de sa partition (un ensemble de dimensions) à côté de la colonne de schéma. Chaque ligne de l&#39;hyper-cube contient la combinaison de dimensions, mais ne contient aucune donnée brute. Lors de l’exécution d’une requête, spécifiez les colonnes dimensionnelles que vous souhaitez utiliser pour créer des mesures additifs et fusionner les schémas de ces lignes.

![Le diagramme montre comment les schémas de différents ExperienceEvents sont fusionnés pour créer des nombres uniques approximatifs sur différentes dimensions.](../images/hypercubes/merge-sketches.png)

### Rentabilité {#cost-effectiveness}

Les données client sont souvent à grande échelle, mais vous pouvez éliminer la nécessité de retraiter les données historiques à l’aide d’un traitement incrémentiel. Les esquisses sont beaucoup plus petites et permettent des résultats plus rapides en temps réel tout en économisant sur les ressources et les coûts de calcul. Cette transformation des données rend les requêtes interactives plus réalisables et efficaces.

## Présentation des fonctions

Cette section décrit comment chaque fonction optimise le traitement des données et améliore les capacités d’analyse grâce à l’utilisation efficace de croquis et d’hypercubes. Il détaille leur objectif, la syntaxe des exemples, les paramètres et la sortie attendue.

### Création d’estimations de comptage uniques avec des schémas HLL

`hll_build_agg` est une fonction d’agrégat qui crée un schéma HLL (HyperLogLog). Cette fonction est une méthode compacte et probabiliste permettant d’estimer le nombre de valeurs uniques dans une colonne ou une expression d’un jeu de données groupé.

#### Définition de la fonction

```sql
hll_build_agg(column [, lgConfigK])
```

**Utilisation :**

L’exemple suivant montre comment la fonction peut être structurée au sein d’une requête.

```sql
SELECT
   [dim1, dim2 ... ,] hll_build_agg(coalesce(col1, col2, col3)) AS sketch_col
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Paramètres

| Paramètre | Description |
|---------------------------|---------------------------------------|
| `column` | Nom de colonne ou de colonne sur lequel créer une esquisse. |
| `lgConfigK` | *Int* (Facultatif) La base de journal-2 de K, où K est le nombre de compartiments ou d’emplacements pour l’esquisse HLL. Valeur min. : 4. Max value : 12. Valeur par défaut : 12. |

#### Sortie

| Colonne de sortie | Description |
|---------------------------|---------------------------------------|
| `sketch_res` | Une colonne de type chaîne contenant le schéma HLL stringifié. |

#### Exemple SQL

L’exemple suivant crée un schéma d’agrégat sur la colonne `customer_id` :

```sql
SELECT
  country,
  hll_build_agg(customer_id, 10) AS sketch
FROM
  EXPLODE(
    ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
      ('UA', 'customer_id_1', 'invoice_id_11'),
      ('CZ', 'customer_id_2', 'invoice_id_22'),
      ('CZ', 'customer_id_2', 'invoice_id_23'),
      ('BR', 'customer_id_3', 'invoice_id_31'),
      ('UA', 'customer_id_2', 'invoice_id_24')
    ])
GROUP BY country;
```

**Exemple de sortie SQL :**

| Pays | Sketch |
|---------|------------------------------------------------------------|
| UA | AgEHBAMAAgCR9mUEulKCQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| CZ | AgEHBAMAACQ6UooJAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| BR | AgEHBAMAACQcmH0HAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |

### Estimation de nombres distincts avec des schémas HLL

`hll_estimate` est une fonction scalaire qui fournit une estimation du nombre distinct dans chaque ligne d’un jeu de données. Contrairement aux fonctions d’agrégat, `hll_estimate` fonctionne au niveau des lignes et est utilisé pour estimer le nombre distinct d’une esquisse au sein de lignes individuelles.

>[!NOTE]
>
>Cette fonction ne peut pas être utilisée comme fonction agrégée. Pour les comptes agrégés, utilisez `sketch_count`.

#### Définition de la fonction

```sql
hll_estimate(sketch_col)
```

**Utilisation :**

L’exemple suivant montre comment la fonction peut être structurée au sein d’une requête.

```sql
SELECT
   [col1, col2 ... ,] hll_estimate(sketch_column) AS estimate
FROM fact_sketch_table
```

#### Paramètres

| Paramètre | Description |
|---------------------------|---------------------------------------|
| `sketch_column` | Colonne contenant un schéma HLL stringifié. Il estime le nombre distinct pour l’esquisse de chaque ligne. |

#### Sortie

| Colonne de sortie | Description |
|---------------------------|---------------------------------------|
| `estimate` | Une colonne de type double qui fournit l’estimation du schéma, arrondie à deux décimales. |

#### Exemple SQL

L’exemple suivant estime le nombre distinct de clients par pays à l’aide de la fonction `hll_estimate` sur un schéma HLL :

```sql
SELECT
  country,
  hll_estimate(hll_build_agg(customer_id, 10)) AS distinct_customers_by_country
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id, 10) AS sketch
    FROM 
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
  );
```

**Exemple de sortie SQL :**

| Pays | distinct_customers_by_country |
|---------|-------------------------------|
| UA | 2,00 |
| CZ | 1,00 |
| BR | 1,00 |

### Fusionner plusieurs schémas HLL avec `hll_merge_agg`

`hll_merge_agg` est une fonction d’agrégat qui fusionne plusieurs schémas HLL au sein d’un groupe, produisant une nouvelle esquisse en tant que sortie. Il permet la combinaison d’esquisses sur plusieurs partitions ou dimensions, améliorant ainsi la flexibilité de l’analyse des données.

#### Définition de la fonction

```sql
hll_merge_agg(sketch_col [, allowDifferentLgConfigK])
```

**Utilisation :**

L’exemple suivant montre comment la fonction peut être structurée au sein d’une requête.

```sql
SELECT
   [dim1, dim2 ... ,] hll_merge_agg(sketch_column.sketch) AS estimate
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Paramètres

| Paramètre | Description |
|---------------------------|---------------------------------------|
| `sketch_column` | Colonne contenant le schéma HLL stringifié. |
| `allowDifferentLgConfigK` | *Boolean* (facultatif) Si la valeur est true, permet la fusion d’esquisses avec des valeurs `lgConfigK` différentes. La valeur par défaut est false. Une exception est générée si la valeur est false et que les schémas ont des valeurs `lgConfigK` différentes. |

>[!NOTE]
>
>Si `allowDifferentLgConfigK` est défini sur false, la fusion d’esquisses avec des valeurs `lgConfigK` différentes entraîne un `UnsupportedOperationException`.

#### Sortie

| Colonne de sortie | Description |
|----------------|-------------------------------------------------|
| `sketch_res` | Une colonne de type Esquisse HLL contenant l&#39;esquisse HLL fusionnée stringifiée. |

#### Exemple SQL

L’exemple suivant fusionne plusieurs schémas HLL sur la colonne `customer_id` :

```sql
SELECT
   hll_merge_agg(hll_sketch) AS uniq_customers_with_invoice
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
    UNION
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_21'),
          ('MX', 'customer_id_3', 'invoice_id_31'),
          ('MX', 'customer_id_2', 'invoice_id_21')
        ])
    GROUP BY country
  )
GROUP BY customer_id;
```

**Exemple de sortie SQL :**

| Pays | hll_merge_agg(sketch, true) |
|---------|--------------------------------------------|
| UA | AgEHDAMAAwiR9mUEulKCQAAAAAAAAAAAAAAAAAAAA== |
| CZ | AgEHDAMAAQi6UooJAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| BR | AgEHDAMAAQicmH0HAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| MX | AgEHFQMAAgiGL/kNdAAAAAAAAAAAAAAAAAAAAAAAAAAA== |

### Estimation de la cardinalité avec `hll_merge_count_agg`

`hll_merge_count_agg` est une fonction d’agrégat qui évalue la cardinalité (nombre d’éléments uniques) à partir d’un ou de plusieurs schémas dans une colonne. Elle renvoie une estimation unique pour tous les schémas rencontrés dans le regroupement. Cette fonction est utilisée pour agréger des schémas et ne peut pas être utilisée comme transformation au niveau de la ligne. Pour les estimations par ligne, utilisez `sketch_estimate`.

#### Définition de la fonction

```sql
hll_merge_count_agg(sketch_col [, allowDifferentLgConfigK])
```

**Utilisation :**

L’exemple suivant montre comment la fonction peut être structurée au sein d’une requête.

```sql
SELECT
   [dim1, dim2 ... ,] hll_merge_count_agg(sketch_column) AS estimate
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Paramètres

| Paramètre | Description |
|-------------------------|----------------------------------------------|
| `sketch_column` | Une colonne contenant le schéma HLL simplifié. |
| `allowDifferentLgConfigK` | *Boolean* (facultatif) La valeur par défaut est false. S’il est défini sur true, il permet la fusion d’esquisses avec des valeurs `lgConfigK` différentes. Sinon, un `UnsupportedOperationException` est généré. |

#### Sortie

| Colonne de sortie | Description |
|---------------|----------------------------------------------------------|
| `estimate` | Une colonne de type Double fournissant l’estimation du schéma. |

#### Exemple SQL

L’exemple suivant évalue le nombre de clients uniques avec des factures à l’aide de la fonction `hll_merge_count_agg` :

```sql
SELECT
   hll_merge_count_agg(hll_sketch) AS uniq_customers_with_invoice
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
    UNION
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_21'),
          ('MX', 'customer_id_3', 'invoice_id_31'),
          ('MX', 'customer_id_2', 'invoice_id_21')
        ])
    GROUP BY country
  )
GROUP BY customer_id;
```

**Exemple de sortie SQL :**

| Pays | hll_merge_count_agg(sketch, true) |
|---------|----------------------------------|
| UA | 2.0 |
| CZ | 1.0 |
| BR | 1.0 |
| MX | 2.0 |

## Limites

Actuellement, les schémas ne peuvent pas être mis à jour une fois créés. Les futures mises à jour permettront de mettre à jour les schémas. Grâce à cette fonctionnalité, vous pouvez gérer plus efficacement les exécutions ratées et les données arrivées tardivement.

## Étapes suivantes

En lisant ce document, vous savez désormais utiliser des hypercubes et les fonctions de schéma associées pour effectuer un traitement efficace des données pour des analyses complexes et multidimensionnelles sans avoir à retraiter les données historiques. Cette approche permet de gagner du temps, de réduire les coûts et offre la flexibilité requise pour les requêtes interactives en temps réel, ce qui en fait un outil précieux pour l’analyse de données volumineuses dans Adobe Experience Platform.

Ensuite, explorez d’autres concepts clés tels que le [chargement incrémentiel](../key-concepts/incremental-load.md) et la [déduplication des données](../key-concepts/deduplication.md) pour mieux comprendre comment utiliser ces fonctions efficacement en fonction de vos besoins de données spécifiques.


