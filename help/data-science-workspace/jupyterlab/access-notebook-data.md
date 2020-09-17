---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;%dataset;interactive mode;batch mode;Spark sdk;python sdk;access data;notebook data access
solution: Experience Platform
title: Accès aux données dans les portables Jupyterlab
topic: Developer Guide
description: Ce guide se concentre sur l'utilisation des blocs-notes Jupyter, conçus dans Data Science Workspace pour accéder à vos données.
translation-type: tm+mt
source-git-commit: a9d65c107d0490910239ed73ac5c19881206c189
workflow-type: tm+mt
source-wordcount: '3078'
ht-degree: 26%

---


# Accès aux données dans les [!DNL Jupyterlab] portables

Chaque noyau pris en charge fournit des fonctionnalités intégrées qui vous permettent de lire les données de Platform à partir d’un jeu de données dans un notebook. Actuellement, JupyterLab dans Adobe Experience Platform Data Science Workspace prend en charge les ordinateurs portables pour [!DNL Python], R, PySpark et Scala. However, support for paginating data is limited to [!DNL Python] and R notebooks. Ce guide se concentre sur l&#39;utilisation des portables JupyterLab pour accéder à vos données.

## Prise en main

Avant de lire ce guide, veuillez consulter le guide [[!DNL JupyterLab] ](./overview.md) d’utilisation pour découvrir [!DNL JupyterLab] et comprendre son rôle dans Data Science Workspace.

## Limites des données des ordinateurs portables {#notebook-data-limits}

>[!IMPORTANT]
>
>Pour les ordinateurs portables PySpark et Scala si vous recevez une erreur indiquant la raison pour laquelle le client RPC distant a été dissocié. Cela signifie généralement que le conducteur ou un exécuteur manque de mémoire. Essayez de passer en mode [](#mode) &quot;batch&quot; pour résoudre cette erreur.

Les informations suivantes définissent la quantité maximale de données pouvant être lues, le type de données utilisé et la période estimée de lecture des données.

Pour [!DNL Python] et R, un serveur de portables configuré à 40 Go de RAM a été utilisé pour les tests. Pour PySpark et Scala, une grappe de serveurs de données configurée à 64 Go de RAM, 8 coeurs, 2 DBU avec un maximum de 4 travailleurs a été utilisée pour les bancs d’essai décrits ci-dessous.

Les données du schéma ExperienceEvent utilisées variaient en taille en commençant par un millier de lignes (1K) allant jusqu’à un milliard de lignes (1B). Notez que pour PySpark et les [!DNL Spark] mesures, une période de 10 jours a été utilisée pour les données XDM.

Les données de schéma ad hoc ont été prétraitées à l’aide de la commande [!DNL Query Service] Créer un tableau comme sélection (CTAS). Ces données varient également en taille en commençant par un millier (1K) de lignes allant jusqu&#39;à un milliard (1B) de lignes.

### Quand utiliser le mode batch ou le mode interactif {#mode}

Lors de la lecture de jeux de données avec des ordinateurs portables PySpark et Scala, vous avez la possibilité d&#39;utiliser le mode interactif ou le mode batch pour lire le jeu de données. Interactive est effectué pour des résultats rapides alors que le mode batch est utilisé pour des jeux de données volumineux.

- Pour les ordinateurs portables PySpark et Scala, le mode batch doit être utilisé lorsque 5 millions de lignes de données ou plus sont lues. Pour plus d&#39;informations sur l&#39;efficacité de chaque mode, consultez les tableaux de limite de données [PySpark](#pyspark-data-limits) ou [Scala](#scala-data-limits) ci-dessous.

### [!DNL Python] limites de données des ordinateurs portables

**Schéma XDM ExperienceEvent :** Vous devriez être en mesure de lire un maximum de 2 millions de lignes (environ 6,1 Go de données sur le disque) de données XDM en moins de 22 minutes. L’Ajoute de lignes supplémentaires peut entraîner des erreurs.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Taille sur le disque (Mo) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK (en secondes) | 20.3 | 86.8 | 63 | 659 | 1315 |

**schéma ad hoc :** Vous devriez être en mesure de lire un maximum de 5 millions de lignes (environ 5,6 Go de données sur le disque) de données non XDM (ad hoc) en moins de 14 minutes. L’Ajoute de lignes supplémentaires peut entraîner des erreurs.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Taille sur le disque (en Mo) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (en secondes) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### Limites de données des ordinateurs portables R

**Schéma XDM ExperienceEvent :** Vous devriez être en mesure de lire un maximum de 1 million de lignes de données XDM (3 Go de données sur le disque) en moins de 13 minutes.

| Nombre de lignes | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Taille sur le disque (Mo) | 18.73 | 187.5 | 308 | 3000 |
| Noyau R (en secondes) | 14.03 | 69.6 | 86.8 | 775 |

**schéma ad hoc :** Vous devriez pouvoir lire un maximum de 3 millions de lignes de données ad hoc (293 Mo de données sur le disque) en 10 minutes environ.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Taille sur le disque (en Mo) | 0.082 | 0.612 | 9,0 | 91 | 188 | 293 |
| SDK R (en s) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### Limites des données du bloc-notes PySpark ([!DNL Python] noyau) : {#pyspark-data-limits}

**Schéma XDM ExperienceEvent :** En mode interactif, vous devriez pouvoir lire un maximum de 5 millions de lignes (environ 13,42 Go de données sur disque) de données XDM en 20 minutes environ. Le mode interactif ne prend en charge que jusqu’à 5 millions de lignes. Si vous souhaitez lire des jeux de données plus volumineux, il est conseillé de passer en mode batch. En mode batch, vous devriez pouvoir lire un maximum de 500 millions de lignes (environ 1,31 To de données sur disque) de données XDM en 14 heures environ.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Taille du disque | 2.93MB | 4.38MB | 29.02 | 2.69 Go   | 5.39 Go   | 8.09 Go   | 13.42 Go   | 26.82 Go   | 134.24 Go   | 268.39 Go   | 1.31TB |
| SDK (mode interactif) | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK (mode Batch) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**schéma ad hoc :** En mode Interactif, vous devriez pouvoir lire un maximum de 5 millions de lignes (environ 5,36 Go de données sur disque) de données non-XDM en moins de 3 minutes. En mode Batch, vous devriez être en mesure de lire un maximum de 1 milliard de lignes (environ 1,05 To de données sur disque) de données non-XDM en 18 minutes environ.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Taille du disque | 1.12MB | 11.24MB | 109.48MB | 2.69 Go   | 2.14 Go   | 3.21 Go   | 5.36 Go   | 10.71 Go   | 53.58 Go   | 107.52 Go   | 535.88 Go   | 1.05TB |
| Mode interactif SDK (en secondes) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | - | - | - | - | - |
| Mode de traitement par lots du SDK (en secondes) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

### [!DNL Spark] Limites des données des blocs-notes (noyau Scala) : {#scala-data-limits}

**Schéma XDM ExperienceEvent :** En mode interactif, vous devriez pouvoir lire un maximum de 5 millions de lignes (environ 13,42 Go de données sur disque) de données XDM en 18 minutes environ. Le mode interactif ne prend en charge que jusqu’à 5 millions de lignes. Si vous souhaitez lire des jeux de données plus volumineux, il est conseillé de passer en mode batch. En mode batch, vous devriez pouvoir lire un maximum de 500 millions de lignes (environ 1,31 To de données sur disque) de données XDM en 14 heures environ.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Taille du disque | 2.93MB | 4.38MB | 29.02 | 2.69 Go   | 5.39 Go   | 8.09 Go   | 13.42 Go   | 26.82 Go   | 134.24 Go   | 268.39 Go   | 1.31TB |
| Mode interactif SDK (en secondes) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| Mode de traitement par lots du SDK (en secondes) | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**schéma ad hoc :** En mode interactif, vous devriez être en mesure de lire un maximum de 5 millions de lignes (environ 5,36 Go de données sur le disque) de données non-XDM en moins de 3 minutes. En mode batch, vous devriez être en mesure de lire un maximum de 1 milliard de lignes (~1,05 To de données sur disque) de données non-XDM en 16 minutes environ.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Taille du disque | 1.12MB | 11.24MB | 109.48MB | 2.69 Go   | 2.14 Go   | 3.21 Go   | 5.36 Go   | 10.71 Go   | 53.58 Go   | 107.52 Go   | 535.88 Go   | 1.05TB |
| Mode interactif SDK (en secondes) | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | - | - | - | - | - |
| Mode de traitement par lots du SDK (en secondes) | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

## Ordinateurs portables Python {#python-notebook}

[!DNL Python] les portables vous permettent de paginer les données lors de l&#39;accès aux jeux de données. Vous trouverez ci-dessous un exemple de code pour lire des données avec et sans pagination. Pour plus d&#39;informations sur les blocs-notes Python de démarrage disponibles, consultez la section [[!DNL JupyterLab] Launcher](./overview.md#launcher) dans le guide d&#39;utilisation de JupyterLab.

La documentation Python ci-dessous décrit les concepts suivants :

- [Lecture à partir d’un jeu de données](#python-read-dataset)
- [Écrire dans un jeu de données](#write-python)
- [Données de requête](#query-data-python)
- [Filtrage des données ExperienceEvent](#python-filter)

### Lecture à partir d’un jeu de données en Python {#python-read-dataset}

**Sans pagination :**

L’exécution du code suivant lit le jeu de données complet. Si l’exécution est réussie, les données sont enregistrées sous la forme d’un cadre de données pandas référencé par la variable `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**Avec pagination :**

L’exécution du code suivant lit les données du jeu de données spécifié. La pagination est obtenue en limitant et en décalant les données à l’aide des fonctions `limit()` et `offset()` respectivement. La limitation des données fait référence au nombre maximal de points de données à lire, tandis que le décalage fait référence au nombre de points de données à ignorer avant la lecture des données. Si l’opération de lecture s’exécute correctement, les données sont enregistrées sous la forme d’un cadre de données pandas référencé par la variable `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Écrire dans un jeu de données en Python {#write-python}

Pour écrire dans un jeu de données de votre bloc-notes JupyterLab, sélectionnez l&#39;onglet Icône de données (en surbrillance ci-dessous) dans le volet de navigation de gauche de JupyterLab. Les répertoires **[!UICONTROL Datasets]** et **[!UICONTROL Schémas]** s’affichent. Sélectionnez **[!UICONTROL Datasets]** , puis cliquez avec le bouton droit de la souris, puis sélectionnez l&#39;option **[!UICONTROL Write Data in Notebook]** dans le menu déroulant du jeu de données que vous souhaitez utiliser. Une entrée de code exécutable s&#39;affiche au bas de votre bloc-notes.

![](../images/jupyterlab/data-access/write-dataset.png)

- Utilisez **[!UICONTROL Write Data in Notebook]** pour générer une cellule d&#39;écriture avec votre jeu de données sélectionné.
- Utilisez **[!UICONTROL Explorer les données dans un bloc-notes]** pour générer une cellule de lecture avec votre jeu de données sélectionné.
- Utilisez les données de **[!UICONTROL Requête dans le bloc-notes]** pour générer une cellule de requête de base avec votre jeu de données sélectionné.

Vous pouvez également copier et coller la cellule de code suivante. Remplacez à la fois le `{DATASET_ID}` et `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Requête de données à l’aide [!DNL Query Service] de la section [!DNL Python] {#query-data-python}

[!DNL JupyterLab][!DNL Platform][!DNL Python] sur vous permet d’utiliser SQL dans un notebook pour accéder aux données via [Adobe Experience Platform Query Service](https://docs.adobe.com/content/help/fr-FR/experience-platform/query/home.html). Accessing data through [!DNL Query Service] can be useful for dealing with large datasets due to its superior running times. Be advised that querying data using [!DNL Query Service] has a processing time limit of ten minutes.

Before you use [!DNL Query Service] in [!DNL JupyterLab], ensure you have a working understanding of the [[!DNL Query Service] SQL syntax](https://docs.adobe.com/content/help/fr-FR/experience-platform/query/home.html#!api-specification/markdown/narrative/technical_overview/query-service/sql/syntax.md).

Querying data using [!DNL Query Service] requires you to provide the name of the target dataset. Vous pouvez générer les cellules de code nécessaires en recherchant le jeu de données souhaité à l’aide de l’**[!UICONTROL explorateur de données]**. Right click on the dataset listing and click **[!UICONTROL Query Data in Notebook]** to generate two code cells in your notebook. Ces deux cellules sont décrites plus en détail ci-dessous.

![](../images/jupyterlab/data-access/python-query-dataset.png)

In order to utilize [!DNL Query Service] in [!DNL JupyterLab], you must first create a connection between your working [!DNL Python] notebook and [!DNL Query Service]. Pour ce faire, exécutez la première cellule générée.

```python
qs_connect()
```

Dans la seconde cellule générée, la première ligne doit être définie avant la requête SQL. Par défaut, la cellule générée définit une variable facultative (`df0`) qui enregistre les résultats des requêtes sous la forme d’un cadre de données pandas. <br>L’argument `-c QS_CONNECTION` est obligatoire et indique au noyau d’exécuter la requête SQL sur [!DNL Query Service]. Consultez l’[annexe](#optional-sql-flags-for-query-service) pour obtenir une liste d’arguments supplémentaires.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Vous pouvez référencer les variables Python directement dans une requête SQL en utilisant une syntaxe au format chaîne et en mettant les variables entre accolades (`{}`), comme indiqué dans l’exemple suivant :

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filter [!DNL ExperienceEvent] data {#python-filter}

In order to access and filter an [!DNL ExperienceEvent] dataset in a [!DNL Python] notebook, you must provide the ID of the dataset (`{DATASET_ID}`) along with the filter rules that define a specific time range using logical operators. Lorsqu’un intervalle de temps est défini, toute pagination spécifiée est ignorée et le jeu de données complet est pris en compte.

Une liste d’opérateurs de filtrage est décrite ci-dessous :

- `eq()` : égal à
- `gt()` : supérieur à
- `ge()` : supérieur ou égal à
- `lt()` : inférieur à
- `le()` : inférieur ou égal à
- `And()` : opérateur ET logique
- `Or()` : opérateur OU logique

The following cell filters an [!DNL ExperienceEvent] dataset to data existing exclusively between January 1, 2019 and the end of December 31, 2019.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## Ordinateurs portables R {#r-notebooks}

Les portables R vous permettent de paginer les données lors de l&#39;accès aux jeux de données. Vous trouverez ci-dessous un exemple de code pour lire des données avec et sans pagination. Pour plus d&#39;informations sur les blocs-notes starter R disponibles, consultez la section [[!DNL JupyterLab] Launcher](./overview.md#launcher) du guide d&#39;utilisation de JupyterLab.

La documentation R ci-dessous décrit les concepts suivants :

- [Lecture à partir d’un jeu de données](#r-read-dataset)
- [Écrire dans un jeu de données](#write-r)
- [Filtrage des données ExperienceEvent](#r-filter)

### Read from a dataset in R {#r-read-dataset}

**Sans pagination :**

L’exécution du code suivant lit le jeu de données complet. Si l’exécution est réussie, les données sont enregistrées sous la forme d’un cadre de données pandas référencé par la variable `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df0 <- dataset_reader$read()
head(df0)
```

**Avec pagination :**

L’exécution du code suivant lit les données du jeu de données spécifié. La pagination est obtenue en limitant et en décalant les données à l’aide des fonctions `limit()` et `offset()` respectivement. La limitation des données fait référence au nombre maximal de points de données à lire, tandis que le décalage fait référence au nombre de points de données à ignorer avant la lecture des données. Si l’opération de lecture s’exécute correctement, les données sont enregistrées sous la forme d’un cadre de données pandas référencé par la variable `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 
df0 <- dataset_reader$limit(100L)$offset(10L)$read()
```

### Écrire dans un jeu de données en R {#write-r}

Pour écrire dans un jeu de données de votre bloc-notes JupyterLab, sélectionnez l&#39;onglet Icône de données (en surbrillance ci-dessous) dans le volet de navigation de gauche de JupyterLab. Les répertoires **[!UICONTROL Datasets]** et **[!UICONTROL Schémas]** s’affichent. Sélectionnez **[!UICONTROL Datasets]** , puis cliquez avec le bouton droit de la souris, puis sélectionnez l&#39;option **[!UICONTROL Write Data in Notebook]** dans le menu déroulant du jeu de données que vous souhaitez utiliser. Une entrée de code exécutable s&#39;affiche au bas de votre bloc-notes.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Utilisez **[!UICONTROL Write Data in Notebook]** pour générer une cellule d&#39;écriture avec votre jeu de données sélectionné.
- Utilisez **[!UICONTROL Explorer les données dans un bloc-notes]** pour générer une cellule de lecture avec votre jeu de données sélectionné.

Vous pouvez également copier et coller la cellule de code suivante :

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filter [!DNL ExperienceEvent] data {#r-filter}

In order to access and filter an [!DNL ExperienceEvent] dataset in a R notebook, you must provide the ID of the dataset (`{DATASET_ID}`) along with the filter rules that define a specific time range using logical operators. Lorsqu’un intervalle de temps est défini, toute pagination spécifiée est ignorée et le jeu de données complet est pris en compte.

Une liste d’opérateurs de filtrage est décrite ci-dessous :

- `eq()` : égal à
- `gt()` : supérieur à
- `ge()` : supérieur ou égal à
- `lt()` : inférieur à
- `le()` : inférieur ou égal à
- `And()` : opérateur ET logique
- `Or()` : opérateur OU logique

The following cell filters an [!DNL ExperienceEvent] dataset to data existing exclusively between January 1, 2019 and the end of December 31, 2019.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 

df0 <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

## Ordinateurs portables PySpark 3 {#pyspark-notebook}

La documentation de PySpark ci-dessous décrit les concepts suivants :

- [Initialiser sparkSession](#spark-initialize)
- [Lecture et écriture de données](#magic)
- [Création d’un cadre de données local](#pyspark-create-dataframe)
- [Filtrage des données ExperienceEvent](#pyspark-filter-experienceevent)

### Initialisation de sparkSession {#spark-initialize}

Tous les [!DNL Spark] ordinateurs portables 2.4 nécessitent que vous initialisiez la session avec le code standard suivant.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Utilisation de %dataset pour lire et écrire avec un bloc-notes PySpark 3 {#magic}

Avec l&#39;introduction de la [!DNL Spark] 2.4, la magie `%dataset` personnalisée est fournie pour les ordinateurs portables PySpark 3 ([!DNL Spark] 2.4). Pour plus d&#39;informations sur les commandes magiques disponibles dans le noyau IPython, consultez la documentation [magique](https://ipython.readthedocs.io/en/stable/interactive/magics.html)IPython.


**Utilisation**

```scala
%dataset {action} --datasetId {id} --dataFrame {df}`
```

**Description**

Commande [!DNL Data Science Workspace] magique personnalisée pour lire ou écrire un jeu de données à partir d&#39;un [!DNL PySpark] bloc-notes (noyau[!DNL Python] 3).

| Nom | Description | Obligatoire |
| --- | --- | --- |
| `{action}` | Type d’action à exécuter sur le jeu de données. Deux actions sont disponibles &quot;read&quot; ou &quot;write&quot;. | Oui |
| `--datasetId {id}` | Utilisé pour fournir l&#39;ID du jeu de données à lire ou à écrire. | Oui |
| `--dataFrame {df}` | La base de données des pandas. <ul><li> Lorsque l&#39;action est &quot;read&quot;, {df} est la variable où les résultats de l&#39;opération de lecture du jeu de données sont disponibles. </li><li> Lorsque l&#39;action est &quot;write&quot;, ce dataframe {df} est écrit dans le dataset. </li></ul> | Oui |
| `--mode` | Paramètre supplémentaire qui modifie le mode de lecture des données. Les paramètres autorisés sont &quot;batch&quot; et &quot;interactive&quot;. Par défaut, le mode est défini sur &quot;interactif&quot;. Il est recommandé d’utiliser le mode &quot;batch&quot; lors de la lecture de grandes quantités de données. | Non |

>[!TIP]
>
>Consultez les tables PySpark dans la section des limites [de données des](#notebook-data-limits) ordinateurs portables pour déterminer si `mode` vous devez définir `interactive` ou `batch`.

**Exemples**

- **Exemple** de lecture : `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
- **Exemple** d&#39;écriture : `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

Vous pouvez générer automatiquement les exemples ci-dessus dans JupyterLab buy à l’aide de la méthode suivante :

Sélectionnez l&#39;onglet Icône Données (en surbrillance ci-dessous) dans le volet de navigation de gauche de JupyterLab. Les répertoires **[!UICONTROL Datasets]** et **[!UICONTROL Schémas]** s’affichent. Sélectionnez **[!UICONTROL Datasets]** , puis cliquez avec le bouton droit de la souris, puis sélectionnez l&#39;option **[!UICONTROL Write Data in Notebook]** dans le menu déroulant du jeu de données que vous souhaitez utiliser. Une entrée de code exécutable s&#39;affiche au bas de votre bloc-notes.

- Utilisez **[!UICONTROL Explorer les données dans un bloc-notes]** pour générer une cellule lue.
- Utilisez **[!UICONTROL Write Data in Notebook]** pour générer une cellule d&#39;écriture.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Création d’un cadre de données local {#pyspark-create-dataframe}

Pour créer une base de données locale à l&#39;aide de PySpark 3, utilisez des requêtes SQL. Par exemple :

```scala
date_aggregation.createOrReplaceTempView("temp_df")

df = spark.sql('''
  SELECT *
  FROM sparkdf
''')

local_df
```

```scala
df = spark.sql('''
  SELECT *
  FROM sparkdf
  LIMIT limit
''')
```

```scala
sample_df = df.sample(fraction)
```

>[!TIP]
>
>Vous pouvez également spécifier un échantillon de semences facultatif, tel qu’un booléen avec remplacement, une fraction de doublon ou une graine longue.

### Filter [!DNL ExperienceEvent] data {#pyspark-filter-experienceevent}

Accessing and filtering an [!DNL ExperienceEvent] dataset in a PySpark notebook requires you to provide the dataset identity (`{DATASET_ID}`), your organization&#39;s IMS identity, and the filter rules defining a specific time range. A filtering time range is defined by using the function `spark.sql()`, where the function parameter is a SQL query string.

The following cells filter an [!DNL ExperienceEvent] dataset to data existing exclusively between January 1, 2019 and the end of December 31, 2019.

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## Ordinateurs portables Scala {#scala-notebook}

La documentation ci-dessous contient des exemples des concepts suivants :

- [Initialiser sparkSession](#scala-initialize)
- [Lecture d’un jeu de données](#read-scala-dataset)
- [Écrire dans un jeu de données](#scala-write-dataset)
- [Création d’un cadre de données local](#scala-create-dataframe)
- [Filtrage des données ExperienceEvent](#scala-experienceevent)

### Initialisation de SparkSession {#scala-initialize}

Tous les ordinateurs portables Scala nécessitent que vous initialisiez la session avec le code standard suivant :

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### Lecture d’un jeu de données {#read-scala-dataset}

Dans Scala, vous pouvez importer `clientContext` pour obtenir et renvoyer des valeurs de plate-forme, ce qui évite de définir des variables telles que `var userToken`. Dans l&#39;exemple Scala ci-dessous, `clientContext` est utilisé pour obtenir et renvoyer toutes les valeurs requises pour lire un jeu de données.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("service-token", clientContext.getServiceToken())
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| Élément | Description |
| ------- | ----------- |
| df1 | Variable qui représente la base de données Pandas utilisée pour lire et écrire des données. |
| user-token | Votre jeton utilisateur qui est automatiquement récupéré à l’aide de `clientContext.getUserToken()`. |
| service-token | Votre jeton de service automatiquement récupéré à l’aide de `clientContext.getServiceToken()`. |
| ims-org | Votre ID d’organisation IMS automatiquement récupéré à l’aide de `clientContext.getOrgId()`. |
| api-key | Votre clé d&#39;API automatiquement récupérée à l&#39;aide de `clientContext.getApiKey()`. |

>[!TIP]
>
>Consultez les tableaux Scala dans la section des limites [de données des](#notebook-data-limits) ordinateurs portables pour déterminer si `mode` vous devez définir `interactive` ou `batch`.

Vous pouvez générer automatiquement l’exemple ci-dessus dans JupyterLab buy à l’aide de la méthode suivante :

Sélectionnez l&#39;onglet Icône Données (en surbrillance ci-dessous) dans le volet de navigation de gauche de JupyterLab. Les répertoires **[!UICONTROL Datasets]** et **[!UICONTROL Schémas]** s’affichent. Sélectionnez **[!UICONTROL Datasets]** et cliquez avec le bouton droit de la souris, puis sélectionnez l&#39;option **[!UICONTROL Explorer les données dans le bloc-notes]** dans le menu déroulant du jeu de données que vous souhaitez utiliser. Une entrée de code exécutable s&#39;affiche au bas de votre bloc-notes.
And
- Utilisez **[!UICONTROL Explorer les données dans un bloc-notes]** pour générer une cellule lue.
- Utilisez **[!UICONTROL Write Data in Notebook]** pour générer une cellule d&#39;écriture.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Écrire dans un jeu de données {#scala-write-dataset}

Dans Scala, vous pouvez importer `clientContext` pour obtenir et renvoyer des valeurs de plate-forme, ce qui évite de définir des variables telles que `var userToken`. Dans l&#39;exemple Scala ci-dessous, `clientContext` est utilisé pour définir et renvoyer toutes les valeurs requises pour écrire dans un jeu de données.

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
df1.write.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("service-token", clientContext.getServiceToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| element   | description |
| ------- | ----------- |
| df1 | Variable qui représente la base de données Pandas utilisée pour lire et écrire des données. |
| user-token | Votre jeton utilisateur qui est automatiquement récupéré à l’aide de `clientContext.getUserToken()`. |
| service-token | Votre jeton de service automatiquement récupéré à l’aide de `clientContext.getServiceToken()`. |
| ims-org | Votre ID d’organisation IMS automatiquement récupéré à l’aide de `clientContext.getOrgId()`. |
| api-key | Votre clé d&#39;API automatiquement récupérée à l&#39;aide de `clientContext.getApiKey()`. |

>[!TIP]
>
>Consultez les tableaux Scala dans la section des limites [de données des](#notebook-data-limits) ordinateurs portables pour déterminer si `mode` vous devez définir `interactive` ou `batch`.

### créer un cadre de données local {#scala-create-dataframe}

Pour créer une base de données locale à l&#39;aide de Scala, des requêtes SQL sont requises. Par exemple :

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filter [!DNL ExperienceEvent] data {#scala-experienceevent}

Accessing and filtering an [!DNL ExperienceEvent] dataset in a Scala notebook requires you to provide the dataset identity (`{DATASET_ID}`), your organization&#39;s IMS identity, and the filter rules defining a specific time range. Un intervalle de temps de filtrage est défini à l’aide de la fonction `spark.sql()`, où le paramètre de fonction est une chaîne de requête SQL.

The following cells filter an [!DNL ExperienceEvent] dataset to data existing exclusively between January 1, 2019 and the end of December 31, 2019.

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

## Étapes suivantes

Ce document portait sur les directives générales pour l&#39;accès aux jeux de données à l&#39;aide de portables JupyterLab. Pour obtenir des exemples plus détaillés sur l&#39;interrogation de jeux de données, consultez [Requête Service dans la documentation des cahiers de travail](./query-service.md) JupyterLab. Pour plus d&#39;informations sur la manière d&#39;explorer et de visualiser vos jeux de données, consultez le document sur l&#39; [analyse de vos données à l&#39;aide de portables](./analyze-your-data.md).

## Optional SQL flags for [!DNL Query Service] {#optional-sql-flags-for-query-service}

Ce tableau décrit les indicateurs SQL facultatifs qui peuvent être utilisés pour [!DNL Query Service].

| **Indicateur** | **Description** |
| --- | --- |
| `-h`, `--help` | Affichez le message d’aide et fermez-le. |
| `-n`, `--notify` | Option d’activation et de désactivation pour la notification des résultats de la requête. |
| `-a`, `--async` | L’utilisation de cet indicateur permet d’exécuter la requête de manière asynchrone et de libérer le noyau pendant l’exécution de la requête. Soyez prudent lorsque vous attribuez les résultats de la requête à des variables, car il se peut qu’ils ne soient pas définis si la requête n’est pas terminée. |
| `-d`, `--display` | L’utilisation de cet indicateur empêche l’affichage des résultats. |

