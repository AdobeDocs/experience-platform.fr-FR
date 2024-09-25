---
title: Échantillon de jeux de données
description: Les échantillons de jeux de données Query Service vous permettent de mener des requêtes exploratoires sur le Big Data avec un temps de traitement considérablement réduit, mais au prix de la précision des requêtes. Ce guide fournit des informations sur la gestion de vos échantillons pour le traitement approximatif des requêtes.
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: 5f2b44c364183b7becf69f491b41e9d5558accc2
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 96%

---

# Échantillons de jeux de données

Adobe Experience Platform Query Service fournit des échantillons de jeux de données dans le cadre de ses fonctionnalités approximatives de traitement des requêtes. Des échantillons de jeux de données sont créés avec des échantillons aléatoires uniformes issus de jeux de données [!DNL Azure Data Lake Storage] (ADLS), utilisant uniquement un pourcentage d’enregistrements de l’original. Ce pourcentage est connu sous le nom de taux d’échantillonnage. Le réglage du taux d’échantillonnage pour contrôler l’équilibre précision/temps de traitement permet d’effectuer des requêtes exploratoires sur le Big Data avec un temps de traitement considérablement réduit, au détriment de la précision des requêtes.

Comme de nombreux utilisateurs et de nombreuses utilisatrices n’ont pas besoin d’une réponse exacte pour une opération d’agrégat sur un jeu de données, l’émission d’une requête approximative pour retourner une réponse approximative est plus efficace pour les requêtes exploratoires sur de grands jeux de données. Comme les échantillons de jeux de données ne contiennent qu’un pourcentage de données du jeu de données d’origine, ils vous permettent d’échanger la précision des requêtes contre un temps de réponse amélioré. Lors de la lecture, Query Service doit analyser moins de lignes, ce qui produit des résultats plus rapidement que si vous deviez interroger l’ensemble du jeu de données.

Pour vous aider à gérer vos échantillons pour le traitement approximatif des requêtes, Query Service prend en charge les opérations suivantes pour les échantillons de jeux de données :

- [Échantillons de jeux de données](#dataset-samples)
   - [Prise en main {#get-started}](#getting-started-get-started)
   - [Créer un exemple de jeu de données aléatoire uniforme {#create-a-sample}](#create-a-uniform-random-dataset-sample-create-a-sample)
   - [Vous pouvez éventuellement spécifier un critère de filtre {#optional-filter-criteria}](#optionally-specify-a-filter-criteria-optional-filter-criteria)
   - [Afficher la liste des exemples {#view-list-of-samples}](#view-the-list-of-samples-view-list-of-samples)
   - [Interrogation de l’exemple de jeu de données {#query-sample-datasets}](#query-the-sample-dataset-query-sample-datasets)
   - [Suppression d’exemples de jeux de données {#delete-a-sample}](#delete-dataset-samples-delete-a-sample)

## Commencer {#get-started}

Pour utiliser les fonctionnalités de création et de suppression du traitement approximatif des requêtes présentées dans ce document, vous devez définir l’indicateur de session sur `true`. Dans la ligne de commande de Query Editor ou de votre client PSQL, saisissez la commande `SET aqp=true;`.

>[!NOTE]
>
>Vous devez activer l’indicateur de session chaque fois que vous vous connectez à Platform.

![L’éditeur de requêtes avec la commande SET aqp=true mise en surbrillance.](../images/key-concepts/set-session-flag.png)

## Créer un échantillon de jeu de données aléatoire uniforme {#create-a-sample}

Utilisez la commande `ANALYZE TABLE <table_name> TABLESAMPLE SAMPLERATE x` avec un nom de jeu de données pour créer un échantillon aléatoire uniforme à partir de ce jeu de données.

Le taux d’échantillonnage est le pourcentage d’enregistrements extraits du jeu de données d’origine. Vous pouvez contrôler le taux d’échantillonnage à l’aide des mots-clés `TABLESAMPLE SAMPLERATE`. Dans cet exemple, la valeur 5,0 équivaut à un taux d’échantillonnage de 50 %. Une valeur de 2,5 équivaut à 25 %, etc.

>[!IMPORTANT]
>
>Le système autorise un maximum de cinq échantillons pour chaque jeu de données. Si vous essayez de créer un sixième échantillon de jeu de données, un message d’erreur s’affiche à l’écran pour vous informer que la limite d’échantillons a été atteinte.

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## Vous pouvez également indiquer un critère de filtre. {#optional-filter-criteria}

Vous pouvez appliquer un critère de filtre sur vos échantillons aléatoires uniformes. Vous obtiendrez alors un échantillon basé sur le sous-ensemble filtré du tableau analysé.

Lors de la création d’un échantillon, le filtre facultatif est appliqué en premier, puis l’échantillon est créé à partir de la vue filtrée du jeu de données. Un échantillon de jeu de données doté d’un filtre suit le format de requête suivant :

```sql
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND/OR <filter_condition_2>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND (<filter_condition_2> OR <filter_condition_3>)) SAMPLERATE X.Y;
```

Voici des exemples concrets de ce type d’échantillon de jeu de données filtré :

```sql
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9')) SAMPLERATE 10;
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND product.name = "product1") SAMPLERATE 10;
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND (product.name = "product1" OR product.name = "product2")) SAMPLERATE 10;
```

Dans les exemples ci-dessus, le nom du tableau est `large_table`, la condition de filtrage sur le tableau d’origine est `month(to_timestamp(timestamp)) in ('8', '9')` et le taux d’échantillonnage est (pourcentage des données filtrées), dans ce cas, `10`.

## Afficher la liste des échantillons {#view-list-of-samples}

Utilisez la fonction `sample_meta()` pour afficher la liste des échantillons associés à une table ADLS.

```sql
SELECT sample_meta('example_dataset_name')
```

La liste des échantillons de jeux de données s’affiche au format de l’échantillon ci-dessous.

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## Interroger l’échantillon de jeu de données {#query-sample-datasets}

Utilisez `{EXAMPLE_DATASET_NAME}` pour interroger directement les tables d’échantillons. Vous pouvez également ajouter le mot-clé `WITHAPPROXIMATE` à la fin d’une requête pour que Query Service utilise automatiquement l’échantillon le plus récemment créé.

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## Supprimer des échantillons de jeux de données {#delete-a-sample}

L’opération de suppression vous permet de créer de nouveaux échantillons une fois que la limite maximale de cinq échantillons de jeux de données a été atteinte.

```sql
DROP TABLESAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>Si vous disposez de plusieurs échantillons de jeux de données dérivés d’un jeu de données ADLS d’origine, lorsque l’original est supprimé, tous les échantillons associés le sont également.
