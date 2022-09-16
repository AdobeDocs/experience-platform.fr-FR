---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;rubriques populaires;%dataset;mode interactif;mode batch;Sdk Spark;sdk python;accès aux données;accès aux données du notebook
solution: Experience Platform
title: Accès aux données dans les notebooks Jupyterlab
topic-legacy: Developer Guide
description: Ce guide porte sur l’utilisation des notebooks Jupyter, conçus dans Data Science Workspace pour accéder à vos données.
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 9e41db60580146fa90542ed00ceedd4eecb88b47
workflow-type: tm+mt
source-wordcount: '3294'
ht-degree: 24%

---

# Accès aux données dans [!DNL Jupyterlab] notebooks

Chaque noyau pris en charge fournit des fonctionnalités intégrées qui vous permettent de lire les données de Platform à partir d’un jeu de données dans un notebook. Actuellement, JupyterLab dans Adobe Experience Platform Data Science Workspace prend en charge les notebooks pour [!DNL Python], R, PySpark et Scala. Toutefois, la prise en charge de la pagination des données se limite à [!DNL Python] et les notebooks R. Ce guide se concentre sur l’utilisation des notebooks JupyterLab pour accéder à vos données.

## Prise en main

Avant de lire ce guide, veuillez consulter la section [[!DNL JupyterLab] guide de l’utilisateur](./overview.md) pour une introduction de haut niveau à [!DNL JupyterLab] et son rôle dans Data Science Workspace.

## Limites de données des notebooks {#notebook-data-limits}

>[!IMPORTANT]
>
>Pour les notebooks PySpark et Scala si vous recevez une erreur expliquant que &quot;Client RPC distant dissocié&quot;. Cela signifie généralement que la mémoire du pilote ou de l’exécuteur est insuffisante. Essayez de passer à [Mode &quot;batch&quot;](#mode) pour résoudre cette erreur.

Les informations suivantes définissent la quantité maximale de données pouvant être lues, le type de données utilisé et la période estimée nécessaire à la lecture des données.

Pour [!DNL Python] et R, un serveur de notebook configuré à 40 Go de RAM a été utilisé pour les références. Pour PySpark et Scala, un cluster de données configuré à 64 Go de mémoire vive, 8 coeurs, 2 DBU avec un maximum de 4 programmes de travail a été utilisé pour les références décrites ci-dessous.

Les données de schéma ExperienceEvent utilisées ont une taille variable, allant de mille (1K) lignes allant jusqu’à un milliard (1B). Notez que pour PySpark et [!DNL Spark] mesures, une période de 10 jours a été utilisée pour les données XDM.

Les données de schéma ad hoc ont été prétraitées à l’aide de [!DNL Query Service] Créer un tableau comme sélection (CTAS). La taille de ces données varie également d’un millier de lignes (1K) allant jusqu’à un milliard de lignes (1B).

### Quand utiliser le mode batch ou le mode interactif ? {#mode}

Lors de la lecture de jeux de données avec des notebooks PySpark et Scala, vous avez la possibilité d’utiliser le mode interactif ou le mode batch pour lire le jeu de données. L’option interactive est faite pour des résultats rapides, tandis que le mode batch est appliqué aux jeux de données volumineux.

- Pour les notebooks PySpark et Scala, le mode batch doit être utilisé lorsque 5 millions de lignes de données ou plus sont en cours de lecture. Pour plus d’informations sur l’efficacité de chaque mode, voir [PySpark](#pyspark-data-limits) ou [Scala](#scala-data-limits) tableau des limites de données ci-dessous.

### [!DNL Python] limites de données des notebooks

**Schéma XDM ExperienceEvent :** Vous devriez être en mesure de lire un maximum de 2 millions de lignes (~6,1 Go de données sur le disque) de données XDM en moins de 22 minutes. L’ajout de lignes supplémentaires peut entraîner des erreurs.

| Nombre de lignes | 1 000 | 10 000 | 100 000 | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Taille sur le disque (Mo) | 18,73 | 187,5 | 308 | 3000 | 6050 |
| SDK (en secondes) | 20,3 | 86,8 | 63 | 659 | 1315 |

**schéma ad hoc :** Vous devriez être en mesure de lire un maximum de 5 millions de lignes (~5,6 Go de données sur le disque) de données non XDM (ad hoc) en moins de 14 minutes. L’ajout de lignes supplémentaires peut entraîner des erreurs.

| Nombre de lignes | 1 000 | 10 000 | 100 000 | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Taille sur le disque (en Mo) | 1,21 | 11,72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (en secondes) | 7,27 | 9,04 | 27,3 | 180 | 346 | 487 | 819 |

### Limites de données des notebooks R

**Schéma XDM ExperienceEvent :** Vous devriez être en mesure de lire un maximum de 1 million de lignes de données XDM (données de 3 Go sur le disque) en moins de 13 minutes.

| Nombre de lignes | 1 000 | 10 000 | 100 000 | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Taille sur le disque (Mo) | 18,73 | 187,5 | 308 | 3 000 |
| Noyau R (en secondes) | 14,03 | 69,6 | 86,8 | 775 |

**schéma ad hoc :** Vous devriez pouvoir lire un maximum de 3 millions de lignes de données ad hoc (293 Mo de données sur le disque) en environ 10 minutes.

| Nombre de lignes | 1 000 | 10 000 | 100 000 | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Taille sur le disque (en Mo) | 0,082 | 0,612 | 9.0 | 91 | 188 | 293 |
| SDK R (en secondes) | 7,7 | 4,58 | 35,9 | 233 | 470,5 | 603 |

### PySpark ([!DNL Python] Limites des données du notebook (noyau) : {#pyspark-data-limits}

**Schéma XDM ExperienceEvent :** En mode interactif, vous devriez être en mesure de lire un maximum de 5 millions de lignes (~13,42 Go de données sur le disque) de données XDM en environ 20 minutes. Le mode interactif ne prend en charge que 5 millions de lignes au maximum. Si vous souhaitez lire des jeux de données plus volumineux, il est conseillé de passer en mode batch. En mode batch, vous devriez pouvoir lire un maximum de 500 millions de lignes (~1,31 To de données sur le disque) de données XDM en 14 heures environ.

| Nombre de lignes | 1 000 | 10 000 | 100 000 | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Taille du disque | 2,93 Mo | 4,38 Mo | 29,02 | 2.69 Go | 5.39 Go | 8.09 Go | 13.42 Go | 26.82 Go | 134.24 Go | 268.39 Go | 1,31 To |
| SDK (mode interactif) | 33s | 32,4 s | 55.1 s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK (mode batch) | 815.8s | 492.8s | 379.1s | 637,4 s | 624.5s | 869.2s | 1104.1s | 1 786 s | 5387.2s | 10624.6s | 50547s |

**schéma ad hoc :** En mode interactif, vous devriez être en mesure de lire un maximum de 5 millions de lignes (~5,36 Go de données sur le disque) de données non XDM en moins de 3 minutes. En mode Lot , vous devriez pouvoir lire un maximum de 1 milliard de lignes (~1,05 To de données sur le disque) de données non XDM en environ 18 minutes.

| Nombre de lignes | 1 000 | 10 000 | 100 000 | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Taille du disque | 1,12 Mo | 11,24 Mo | 109,48 Mo | 2.69 Go | 2.14 Go | 3.21 Go | 5.36 Go | 10.71 Go | 53.58 Go | 107.52 Go | 535.88 Go | 1,05 To |
| Mode interactif SDK (en secondes) | 28.2 s | 18.6s | 20,8 s | 20,9 s | 23,8 s | 21,7 s | 24,7 s | - | - | - | - | - |
| Mode batch du SDK (en secondes) | 428.8s | 578.8s | 641.4 s | 538.5s | 630,9 s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

### [!DNL Spark] Limites des données du notebook (noyau Scala) : {#scala-data-limits}

**Schéma XDM ExperienceEvent :** En mode interactif, vous devriez être en mesure de lire un maximum de 5 millions de lignes (~13,42 Go de données sur le disque) de données XDM en environ 18 minutes. Le mode interactif ne prend en charge que 5 millions de lignes au maximum. Si vous souhaitez lire des jeux de données plus volumineux, il est conseillé de passer en mode batch. En mode batch, vous devriez pouvoir lire un maximum de 500 millions de lignes (~1,31 To de données sur le disque) de données XDM en 14 heures environ.

| Nombre de lignes | 1 000 | 10 000 | 100 000 | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Taille du disque | 2,93 Mo | 4,38 Mo | 29,02 | 2.69 Go | 5.39 Go | 8.09 Go | 13.42 Go | 26.82 Go | 134.24 Go | 268.39 Go | 1,31 To |
| Mode interactif SDK (en secondes) | 37,9 s | 22,7 s | 45.6s | 231,7 s | 444,7 s | 660.6s | 1 100 s | - | - | - | - |
| Mode batch du SDK (en secondes) | 374.4 s | 398.5s | 527s | 487.9s | 588.9s | 829 s | 939.1s | 1 441 s | 5473.2s | 10118.8 | 49207.6 |

**schéma ad hoc :** En mode interactif, vous devriez être en mesure de lire un maximum de 5 millions de lignes (~5,36 Go de données sur le disque) de données non XDM en moins de 3 minutes. En mode batch, vous devriez pouvoir lire un maximum de 1 milliard de lignes (~1,05 To de données sur le disque) de données non XDM en environ 16 minutes.

| Nombre de lignes | 1 000 | 10 000 | 100 000 | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Taille du disque | 1,12 Mo | 11,24 Mo | 109,48 Mo | 2.69 Go | 2.14 Go | 3.21 Go | 5.36 Go | 10.71 Go | 53.58 Go | 107.52 Go | 535.88 Go | 1,05 To |
| Mode interactif SDK (en secondes) | 35,7 s | 31 s | 19.5s | 25.3 | 23 s | 33.2s | 25.5s | - | - | - | - | - |
| Mode batch du SDK (en secondes) | 448.8s | 459,7 s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397 s | 518.8s | 487.9s | 760.2s | 975.4 s |

## notebooks Python {#python-notebook}

[!DNL Python] les notebooks vous permettent de paginer les données lors de l’accès aux jeux de données. Vous trouverez ci-dessous un exemple de code pour lire des données avec et sans pagination. Pour plus d’informations sur les notebooks Python de démarrage disponibles, consultez le [[!DNL JupyterLab] Lanceur](./overview.md#launcher) dans le guide d’utilisation de JupyterLab.

La documentation Python ci-dessous décrit les concepts suivants :

- [Lecture à partir d’un jeu de données](#python-read-dataset)
- [Écriture dans un jeu de données](#write-python)
- [Données de requête](#query-data-python)
- [Filtrage des données ExperienceEvent](#python-filter)

### Lecture à partir d’un jeu de données en Python {#python-read-dataset}

**Sans pagination :**

L’exécution du code suivant lit le jeu de données complet. Si l’exécution est réussie, les données sont enregistrées sous la forme d’un cadre de données pandas référencé par la variable `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**Avec pagination :**

L’exécution du code suivant lit les données du jeu de données spécifié. La pagination est obtenue en limitant et en décalant les données à l’aide des fonctions `limit()` et `offset()` respectivement. La limitation des données fait référence au nombre maximal de points de données à lire, tandis que le décalage fait référence au nombre de points de données à ignorer avant la lecture des données. Si l’opération de lecture s’exécute correctement, les données sont enregistrées sous la forme d’un cadre de données pandas référencé par la variable `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### Écriture dans un jeu de données en Python {#write-python}

Pour écrire dans un jeu de données de votre notebook JupyterLab, sélectionnez l’onglet Icône de données (mis en évidence ci-dessous) dans le volet de navigation de gauche de JupyterLab. Le **[!UICONTROL Jeux de données]** et **[!UICONTROL Schémas]** les répertoires s’affichent. Sélectionner **[!UICONTROL Jeux de données]** puis cliquez avec le bouton droit de la souris, puis sélectionnez l’option **[!UICONTROL Écrire des données dans Notebook]** dans le menu déroulant du jeu de données que vous souhaitez utiliser. Une entrée de code exécutable s’affiche au bas de votre notebook.

![](../images/jupyterlab/data-access/write-dataset.png)

- Utilisation **[!UICONTROL Écrire des données dans Notebook]** pour générer une cellule d’écriture avec votre jeu de données sélectionné.
- Utilisation **[!UICONTROL Exploration des données dans Notebook]** pour générer une cellule de lecture avec votre jeu de données sélectionné.
- Utilisation **[!UICONTROL Données de requête dans Notebook]** pour générer une cellule de requête de base avec votre jeu de données sélectionné.

Vous pouvez également copier et coller la cellule de code suivante. Remplacez les deux `{DATASET_ID}` et `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### Requête de données à l’aide de [!DNL Query Service] in [!DNL Python] {#query-data-python}

[!DNL JupyterLab][!DNL Platform][!DNL Python] sur vous permet d’utiliser SQL dans un notebook pour accéder aux données via [Adobe Experience Platform Query Service](https://docs.adobe.com/content/help/fr-FR/experience-platform/query/home.html). Accès aux données par le biais de [!DNL Query Service] peut s’avérer utile pour traiter des jeux de données volumineux en raison de ses temps d’exécution supérieurs. Notez que l’interrogation de données à l’aide de [!DNL Query Service] a une durée de traitement de dix minutes.

Avant d’utiliser [!DNL Query Service] in [!DNL JupyterLab], assurez-vous que vous comprenez bien le [[!DNL Query Service] Syntaxe SQL](https://docs.adobe.com/content/help/fr-FR/experience-platform/query/home.html#!api-specification/markdown/narrative/technical_overview/query-service/sql/syntax.md).

Requête sur des données à l’aide de [!DNL Query Service] nécessite que vous fournissiez le nom du jeu de données cible. Vous pouvez générer les cellules de code nécessaires en recherchant le jeu de données souhaité à l’aide de l’**[!UICONTROL explorateur de données]**. Cliquez avec le bouton droit de la souris sur la liste des jeux de données, puis cliquez sur **[!UICONTROL Données de requête dans Notebook]** pour générer deux cellules de code dans votre notebook. Ces deux cellules sont décrites plus en détail ci-dessous.

![](../images/jupyterlab/data-access/python-query-dataset.png)

Pour utiliser [!DNL Query Service] in [!DNL JupyterLab], vous devez d’abord créer une connexion entre votre activité [!DNL Python] notebook et [!DNL Query Service]. Pour ce faire, exécutez la première cellule générée.

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

### Filtrer [!DNL ExperienceEvent] data {#python-filter}

Pour accéder à et filtrer une [!DNL ExperienceEvent] jeu de données dans un [!DNL Python] notebook, vous devez fournir l’identifiant du jeu de données (`{DATASET_ID}`) ainsi que les règles de filtrage qui définissent une période spécifique à l’aide d’opérateurs logiques. Lorsqu’un intervalle de temps est défini, toute pagination spécifiée est ignorée et le jeu de données complet est pris en compte.

Une liste d’opérateurs de filtrage est décrite ci-dessous :

- `eq()` : égal à
- `gt()` : supérieur à
- `ge()` : supérieur ou égal à
- `lt()` : inférieur à
- `le()` : inférieur ou égal à
- `And()` : opérateur ET logique
- `Or()` : opérateur OU logique

La cellule suivante filtre et [!DNL ExperienceEvent] jeu de données de données existant exclusivement entre le 1er janvier 2019 et la fin du 31 décembre 2019.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## notebooks R {#r-notebooks}

Les notebooks R vous permettent de paginer les données lors de l’accès aux jeux de données. Vous trouverez ci-dessous un exemple de code pour lire des données avec et sans pagination. Pour plus d’informations sur les notebooks de démarrage disponibles, consultez la page [[!DNL JupyterLab] Lanceur](./overview.md#launcher) dans le guide d’utilisation de JupyterLab.

La documentation R ci-dessous décrit les concepts suivants :

- [Lecture à partir d’un jeu de données](#r-read-dataset)
- [Écriture dans un jeu de données](#write-r)
- [Filtrage des données ExperienceEvent](#r-filter)

### Lecture à partir d’un jeu de données en R {#r-read-dataset}

**Sans pagination :**

L’exécution du code suivant lit le jeu de données complet. Si l’exécution est réussie, les données sont enregistrées sous la forme d’un cadre de données pandas référencé par la variable `df0`.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
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
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 
df0 <- dataset_reader$limit(100L)$offset(10L)$read()
```

### Écriture dans un jeu de données en R {#write-r}

Pour écrire dans un jeu de données de votre notebook JupyterLab, sélectionnez l’onglet Icône de données (mis en évidence ci-dessous) dans le volet de navigation de gauche de JupyterLab. Le **[!UICONTROL Jeux de données]** et **[!UICONTROL Schémas]** les répertoires s’affichent. Sélectionner **[!UICONTROL Jeux de données]** puis cliquez avec le bouton droit de la souris, puis sélectionnez l’option **[!UICONTROL Écrire des données dans Notebook]** dans le menu déroulant du jeu de données que vous souhaitez utiliser. Une entrée de code exécutable s’affiche au bas de votre notebook.

![](../images/jupyterlab/data-access/r-write-dataset.png)

- Utilisation **[!UICONTROL Écrire des données dans Notebook]** pour générer une cellule d’écriture avec votre jeu de données sélectionné.
- Utilisation **[!UICONTROL Exploration des données dans Notebook]** pour générer une cellule de lecture avec votre jeu de données sélectionné.

Vous pouvez également copier et coller la cellule de code suivante :

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filtrer [!DNL ExperienceEvent] data {#r-filter}

Pour accéder à et filtrer une [!DNL ExperienceEvent] jeu de données dans un notebook R, vous devez fournir l’identifiant du jeu de données (`{DATASET_ID}`) ainsi que les règles de filtrage qui définissent une période spécifique à l’aide d’opérateurs logiques. Lorsqu’un intervalle de temps est défini, toute pagination spécifiée est ignorée et le jeu de données complet est pris en compte.

Une liste d’opérateurs de filtrage est décrite ci-dessous :

- `eq()` : égal à
- `gt()` : supérieur à
- `ge()` : supérieur ou égal à
- `lt()` : inférieur à
- `le()` : inférieur ou égal à
- `And()` : opérateur ET logique
- `Or()` : opérateur OU logique

La cellule suivante filtre et [!DNL ExperienceEvent] jeu de données de données existant exclusivement entre le 1er janvier 2019 et la fin du 31 décembre 2019.

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 

df0 <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

## notebooks PySpark 3 {#pyspark-notebook}

La documentation PySpark ci-dessous décrit les concepts suivants :

- [Initialisation de sparkSession](#spark-initialize)
- [Lecture et écriture de données](#magic)
- [Création d’un cadre de données local](#pyspark-create-dataframe)
- [Filtrage des données ExperienceEvent](#pyspark-filter-experienceevent)

### Initialisation de sparkSession {#spark-initialize}

Tous [!DNL Spark] Les notebooks 2.4 requièrent l’initialisation de la session avec le code standard suivant.

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### Utilisation de %dataset pour lire et écrire avec un notebook PySpark 3 {#magic}

Avec l’introduction de [!DNL Spark] 2.4, `%dataset` la magie personnalisée est fournie pour une utilisation dans PySpark 3 ([!DNL Spark] 2.4) notebooks. Pour plus d’informations sur les commandes magiques disponibles dans le noyau IPython, consultez la page [Documentation magique IPython](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**Utilisation**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**Description**

Une [!DNL Data Science Workspace] commande magique pour lire ou écrire un jeu de données à partir d’un [!DNL PySpark] notebook ([!DNL Python] 3).

| Nom | Description | Obligatoire |
| --- | --- | --- |
| `{action}` | Type d’action à effectuer sur le jeu de données. Deux actions sont disponibles &quot;read&quot; ou &quot;write&quot;. | Oui |
| `--datasetId {id}` | Utilisé pour fournir l’identifiant du jeu de données à lire ou à écrire. | Oui |
| `--dataFrame {df}` | Le cadre de données pandas. <ul><li> Lorsque l’action est &quot;read&quot;, {df} est la variable où les résultats de l’opération de lecture du jeu de données sont disponibles (un cadre de données, par exemple). </li><li> Lorsque l’action est &quot;write&quot;, ce cadre de données {df} est écrit dans le jeu de données. </li></ul> | Oui |
| `--mode` | Paramètre supplémentaire qui modifie la manière dont les données sont lues. Les paramètres autorisés sont &quot;batch&quot; et &quot;interactive&quot;. Par défaut, le mode est défini sur &quot;batch&quot;.<br> Il est recommandé d’utiliser le mode &quot;interactif&quot; pour améliorer les performances des requêtes sur les jeux de données plus petits. | Oui |

>[!TIP]
>
>Examinez les tables PySpark dans le [limites de données des notebooks](#notebook-data-limits) pour déterminer si `mode` doit être défini sur `interactive` ou `batch`.

**Exemples**

- **Exemple de lecture**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **Exemple d’écriture**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> Mise en cache des données à l’aide de `df.cache()` avant d’écrire des données peut améliorer considérablement les performances du notebook. Cela peut vous aider si vous recevez l’une des erreurs suivantes :
> 
> - Traitement abandonné en raison d’un échec de test... Peuvent uniquement compresser les RDD avec le même nombre d&#39;éléments dans chaque partition.
> - Client RPC distant dissocié et autres erreurs de mémoire.
> - Mauvaises performances lors de la lecture et de l’écriture de jeux de données.
> 
> Voir [guide de dépannage](../troubleshooting-guide.md) pour plus d’informations.

Vous pouvez générer automatiquement les exemples ci-dessus dans JupyterLab en achetant à l’aide de la méthode suivante :

Sélectionnez l’onglet Icône de données (en surbrillance ci-dessous) dans le volet de navigation de gauche de JupyterLab. Le **[!UICONTROL Jeux de données]** et **[!UICONTROL Schémas]** les répertoires s’affichent. Sélectionner **[!UICONTROL Jeux de données]** puis cliquez avec le bouton droit de la souris, puis sélectionnez l’option **[!UICONTROL Écrire des données dans Notebook]** dans le menu déroulant du jeu de données que vous souhaitez utiliser. Une entrée de code exécutable s’affiche au bas de votre notebook.

- Utilisation **[!UICONTROL Exploration des données dans Notebook]** pour générer une cellule de lecture.
- Utilisation **[!UICONTROL Écrire des données dans Notebook]** pour générer une cellule d’écriture.

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### Création d’un cadre de données local {#pyspark-create-dataframe}

Pour créer un cadre de données local à l’aide de PySpark 3, utilisez des requêtes SQL. Par exemple :

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
>Vous pouvez également spécifier un échantillon de contrôle facultatif, tel qu’une valeur booléenne avecRemplacement, une double fraction ou une valeur de départ longue.

### Filtrer [!DNL ExperienceEvent] data {#pyspark-filter-experienceevent}

Accéder à et filtrer un [!DNL ExperienceEvent] dans un notebook PySpark, le jeu de données requiert que vous fournissiez l’identité du jeu de données (`{DATASET_ID}`), l’identité IMS de votre organisation et les règles de filtrage définissant une période spécifique. Une période de filtrage est définie à l’aide de la fonction . `spark.sql()`, où le paramètre de fonction est une chaîne de requête SQL.

Les cellules suivantes filtrent et [!DNL ExperienceEvent] jeu de données de données existant exclusivement entre le 1er janvier 2019 et la fin du 31 décembre 2019.

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df --mode batch

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## notebooks Scala {#scala-notebook}

La documentation ci-dessous contient des exemples des concepts suivants :

- [Initialisation de sparkSession](#scala-initialize)
- [Lecture d’un jeu de données](#read-scala-dataset)
- [Écriture dans un jeu de données](#scala-write-dataset)
- [Création d’un cadre de données local](#scala-create-dataframe)
- [Filtrage des données ExperienceEvent](#scala-experienceevent)

### Initialisation de SparkSession {#scala-initialize}

Tous les notebooks Scala nécessitent que vous initialisiez la session avec le code standard suivant :

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### Lecture d’un jeu de données {#read-scala-dataset}

Dans Scala, vous pouvez importer `clientContext` pour obtenir et renvoyer des valeurs Platform, cela évite d’avoir à définir des variables telles que `var userToken`. Dans l’exemple Scala ci-dessous, `clientContext` est utilisé pour obtenir et renvoyer toutes les valeurs requises pour lire un jeu de données.

>[!IMPORTANT]
>
> Mise en cache des données à l’aide de `df.cache()` avant d’écrire des données peut améliorer considérablement les performances du notebook. Cela peut vous aider si vous recevez l’une des erreurs suivantes :
> 
> - Traitement abandonné en raison d’un échec de test... Peuvent uniquement compresser les RDD avec le même nombre d&#39;éléments dans chaque partition.
> - Client RPC distant dissocié et autres erreurs de mémoire.
> - Mauvaises performances lors de la lecture et de l’écriture de jeux de données.
> 
> Voir [guide de dépannage](../troubleshooting-guide.md) pour plus d’informations.

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
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| Élément | Description |
| ------- | ----------- |
| df1 | Variable qui représente le cadre de données pandas utilisé pour lire et écrire des données. |
| user-token | Votre jeton utilisateur qui est automatiquement récupéré à l’aide de `clientContext.getUserToken()`. |
| service-token | Votre jeton de service automatiquement récupéré à l’aide de `clientContext.getServiceToken()`. |
| ims-org | Votre identifiant de l’organisation IMS qui est automatiquement récupéré à l’aide de `clientContext.getOrgId()`. |
| api-key | Votre clé API automatiquement récupérée à l’aide de `clientContext.getApiKey()`. |

>[!TIP]
>
>Examinez les tableaux Scala dans le [limites de données des notebooks](#notebook-data-limits) pour déterminer si `mode` doit être défini sur `interactive` ou `batch`.

Vous pouvez générer automatiquement l’exemple ci-dessus dans JupyterLab en achetant à l’aide de la méthode suivante :

Sélectionnez l’onglet Icône de données (en surbrillance ci-dessous) dans le volet de navigation de gauche de JupyterLab. Le **[!UICONTROL Jeux de données]** et **[!UICONTROL Schémas]** les répertoires s’affichent. Sélectionner **[!UICONTROL Jeux de données]** puis cliquez avec le bouton droit de la souris, puis sélectionnez l’option **[!UICONTROL Exploration des données dans Notebook]** dans le menu déroulant du jeu de données que vous souhaitez utiliser. Une entrée de code exécutable s’affiche au bas de votre notebook.
Et
- Utilisation **[!UICONTROL Exploration des données dans Notebook]** pour générer une cellule de lecture.
- Utilisation **[!UICONTROL Écrire des données dans Notebook]** pour générer une cellule d’écriture.

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### Écriture dans un jeu de données {#scala-write-dataset}

Dans Scala, vous pouvez importer `clientContext` pour obtenir et renvoyer des valeurs Platform, cela évite d’avoir à définir des variables telles que `var userToken`. Dans l’exemple Scala ci-dessous, `clientContext` est utilisé pour définir et renvoyer toutes les valeurs requises pour l’écriture dans un jeu de données.

>[!IMPORTANT]
>
> Mise en cache des données à l’aide de `df.cache()` avant d’écrire des données peut améliorer considérablement les performances du notebook. Cela peut vous aider si vous recevez l’une des erreurs suivantes :
> 
> - Traitement abandonné en raison d’un échec de test... Peuvent uniquement compresser les RDD avec le même nombre d&#39;éléments dans chaque partition.
> - Client RPC distant dissocié et autres erreurs de mémoire.
> - Mauvaises performances lors de la lecture et de l’écriture de jeux de données.
> 
> Voir [guide de dépannage](../troubleshooting-guide.md) pour plus d’informations.

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
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| element   | description |
| ------- | ----------- |
| df1 | Variable qui représente le cadre de données pandas utilisé pour lire et écrire des données. |
| user-token | Votre jeton utilisateur qui est automatiquement récupéré à l’aide de `clientContext.getUserToken()`. |
| service-token | Votre jeton de service automatiquement récupéré à l’aide de `clientContext.getServiceToken()`. |
| ims-org | Votre identifiant de l’organisation IMS qui est automatiquement récupéré à l’aide de `clientContext.getOrgId()`. |
| api-key | Votre clé API automatiquement récupérée à l’aide de `clientContext.getApiKey()`. |

>[!TIP]
>
>Examinez les tableaux Scala dans le [limites de données des notebooks](#notebook-data-limits) pour déterminer si `mode` doit être défini sur `interactive` ou `batch`.

### créer un cadre de données local ; {#scala-create-dataframe}

Pour créer un cadre de données local à l’aide de Scala, des requêtes SQL sont requises. Par exemple :

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filtrer [!DNL ExperienceEvent] data {#scala-experienceevent}

Accéder à et filtrer un [!DNL ExperienceEvent] dans un notebook Scala, le jeu de données requiert que vous fournissiez l’identité du jeu de données (`{DATASET_ID}`), l’identité IMS de votre organisation et les règles de filtrage définissant une période spécifique. Un intervalle de temps de filtrage est défini à l’aide de la fonction `spark.sql()`, où le paramètre de fonction est une chaîne de requête SQL.

Les cellules suivantes filtrent et [!DNL ExperienceEvent] jeu de données de données existant exclusivement entre le 1er janvier 2019 et la fin du 31 décembre 2019.

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

Ce document couvrait les instructions générales d’accès aux jeux de données à l’aide de notebooks JupyterLab. Pour obtenir des exemples plus détaillés sur l’interrogation des jeux de données, consultez la page [Query Service dans les notebooks JupyterLab](./query-service.md) documentation. Pour plus d’informations sur l’exploration et la visualisation de vos jeux de données, consultez le document sur [analyse de vos données à l’aide de notebooks](./analyze-your-data.md).

## Indicateurs SQL facultatifs pour [!DNL Query Service] {#optional-sql-flags-for-query-service}

Ce tableau décrit les indicateurs SQL facultatifs qui peuvent être utilisés pour [!DNL Query Service].

| **Indicateur** | **Description** |
| --- | --- |
| `-h`, `--help` | Affichez le message d’aide et fermez-le. |
| `-n`, `--notify` | Option d’activation et de désactivation pour la notification des résultats de la requête. |
| `-a`, `--async` | L’utilisation de cet indicateur permet d’exécuter la requête de manière asynchrone et de libérer le noyau pendant l’exécution de la requête. Soyez prudent lorsque vous attribuez les résultats de la requête à des variables, car il se peut qu’ils ne soient pas définis si la requête n’est pas terminée. |
| `-d`, `--display` | L’utilisation de cet indicateur empêche l’affichage des résultats. |
