---
title: Exemples de jeux de données
description: Les exemples de jeux de données de Query Service vous permettent de mener des requêtes exploratoires sur les données volumineuses avec un temps de traitement considérablement réduit au prix de la précision des requêtes. Ce guide fournit des informations sur la gestion de vos exemples pour le traitement approximatif des requêtes.
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: 13779e619345c228ff2a1981efabf5b1917c4fdb
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Exemples de jeux de données

Adobe Experience Platform Query Service fournit des jeux de données d’exemple dans le cadre de ses fonctionnalités approximatives de traitement des requêtes. Des exemples de jeux de données sont créés avec des exemples aléatoires uniformes issus de [!DNL Azure Data Lake Storage] (ADLS) les jeux de données utilisant uniquement un pourcentage d’enregistrements de l’original. Ce pourcentage est connu sous le nom de taux d’échantillonnage. Le réglage du taux d’échantillonnage pour contrôler l’équilibre de précision et de temps de traitement permet d’effectuer des requêtes exploratoires sur les données volumineuses avec un temps de traitement considérablement réduit, au détriment de la précision des requêtes.

Comme de nombreux utilisateurs n’ont pas besoin d’une réponse exacte pour une opération d’agrégat sur un jeu de données, émettre une requête approximative pour renvoyer une réponse approximative est plus efficace pour les requêtes exploratoires sur les jeux de données volumineux. Comme les exemples de jeux de données ne contiennent qu’un pourcentage des données du jeu de données d’origine, ils vous permettent d’échanger la précision des requêtes pour un temps de réponse amélioré. Lors de la lecture, Query Service doit analyser moins de lignes, ce qui produit des résultats plus rapidement que si vous deviez interroger l’ensemble du jeu de données.

Pour vous aider à gérer vos exemples pour le traitement approximatif des requêtes, Query Service prend en charge les opérations suivantes pour les exemples de jeux de données :

- [Créez un exemple de jeu de données aléatoire uniforme.](#create-a-sample)
- [Vous pouvez éventuellement spécifier un critère de filtre](##optional-filter-criteria)
- [Affichez la liste des exemples pour un tableau ADLS.](#view-list-of-samples)
- [Interrogez directement les exemples de jeux de données.](#query-sample-datasets)
- [Supprimez un exemple.](#delete-a-sample)
- Supprimez les exemples associés lorsque la table ADLS d’origine est déposée.

## Prise en main {#get-started}

Pour utiliser les fonctionnalités de création et de suppression de traitement de requête approximatif présentées dans ce document, vous devez définir l’indicateur de session sur `true`. Dans la ligne de commande de l’éditeur de requêtes ou de votre client PSQL, saisissez la variable `SET aqp=true;` .

>[!NOTE]
>
>Vous devez activer l’indicateur de session chaque fois que vous vous connectez à Platform.

![L’éditeur de requêtes avec la commande &quot;SET aqp=true;&quot; mise en surbrillance.](../images/essential-concepts/set-session-flag.png)

## Créer un exemple de jeu de données aléatoire uniforme {#create-a-sample}

Utilisez la variable `ANALYZE TABLE <table_name> TABLESAMPLE SAMPLERATE x` avec un nom de jeu de données pour créer un exemple aléatoire uniforme à partir de ce jeu de données.

Le taux d’échantillonnage est le pourcentage d’enregistrements extraits du jeu de données d’origine. Vous pouvez contrôler le taux d’échantillonnage à l’aide de la variable `TABLESAMPLE SAMPLERATE` mots-clés. Dans cet exemple, la valeur de 5,0 équivaut à un taux d’échantillonnage de 50 %. Une valeur de 2,5 équivaut à 25 %, etc.

>[!IMPORTANT]
>
>Le système autorise un maximum de cinq exemples pour chaque jeu de données. Si vous essayez de créer un sixième jeu de données d’exemple, un message d’erreur s’affiche à l’écran pour vous informer que la limite de l’échantillon a été atteinte.

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## Vous pouvez éventuellement spécifier un critère de filtre {#optional-filter-criteria}

Vous pouvez choisir de spécifier un critère de filtrage pour vos échantillons aléatoires uniformes. Vous pouvez ainsi créer un exemple basé sur le sous-ensemble filtré du tableau analysé.

Lors de la création d’un exemple, le filtre facultatif est appliqué en premier, puis l’exemple est créé à partir de la vue filtrée du jeu de données. Un exemple de jeu de données avec un filtre appliqué suit le format de requête suivant :

```sql
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND/OR <filter_condition_2>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND (<filter_condition_2> OR <filter_condition_3>)) SAMPLERATE X.Y;
```

Voici des exemples pratiques de ce type de jeu de données d’exemple filtré :

```sql
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9')) SAMPLERATE 10;
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND product.name = "product1") SAMPLERATE 10;
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND (product.name = "product1" OR product.name = "product2")) SAMPLERATE 10;
```

Dans les exemples fournis, le nom de la table est `large_table`, la condition de filtrage sur la table d’origine est la suivante : `month(to_timestamp(timestamp)) in ('8', '9')`, et que le taux d’échantillonnage est (X % des données filtrées), dans ce cas, `10`.

## Afficher la liste des exemples {#view-list-of-samples}

Utilisez la variable `sample_meta()` pour afficher la liste des exemples associés à un tableau ADLS.

```sql
SELECT sample_meta('example_dataset_name')
```

La liste des exemples de jeux de données s’affiche au format de l’exemple ci-dessous.

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## Interrogation de l’exemple de jeu de données {#query-sample-datasets}

Utilisez la variable `{EXAMPLE_DATASET_NAME}` pour interroger directement des exemples de tableau. Vous pouvez également ajouter le `WITHAPPROXIMATE` à la fin d’une requête, Query Service utilise automatiquement l’exemple créé le plus récemment.

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## Suppression d’exemples de jeux de données {#delete-a-sample}

L’opération de suppression vous permet de créer de nouveaux exemples une fois que la limite maximale de cinq exemples de jeux de données a été atteinte.

```sql
DROP TABLE SAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>Si vous disposez de plusieurs exemples de jeux de données dérivés d’un jeu de données ADLS d’origine, lorsque l’original est déposé, tous les exemples associés sont également supprimés.
