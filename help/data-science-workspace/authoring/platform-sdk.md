---
keywords: Experience Platform;developer guide;SDK;Data Access SDK;Data Science Workspace;popular topics
solution: Experience Platform
title: Guide du SDK de Platform
topic: SDK authoring
description: Ce didacticiel vous fournit des informations sur la conversion de data_access_sdk_python en nouvelle plateforme Python_sdk dans Python et R.
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 84%

---


# [!DNL Platform] Guide SDK

Ce tutoriel vous fournit des informations sur la conversion de `data_access_sdk_python` en nouveau `platform_sdk` Python en Python et en R. Ce tutoriel fournit des informations sur les opérations suivantes :

- [Authentification de création](#build-authentication)
- [Lecture basique des données](#basic-reading-of-data)
- [Écriture basique des données](#basic-writing-of-data)

## Authentification de création {#build-authentication}

Authentication is required to make calls to [!DNL Adobe Experience Platform], and is comprised of API Key, IMS Org ID, a user token, and a service token.

### Python

Si vous utilisez Jupyter Notebook, veuillez utiliser le code ci-dessous pour créer le `client_context` :

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Si vous n’utilisez pas Jupyter Notebook ou si vous devez changer l’organisation IMS, veuillez utiliser l’exemple de code ci-dessous :

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

Si vous utilisez Jupyter Notebook, veuillez utiliser le code ci-dessous pour créer le `client_context` :

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Si vous n’utilisez pas Jupyter Notebook ou si vous devez changer l’organisation IMS, veuillez utiliser l’exemple de code ci-dessous :

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Lecture basique des données {#basic-reading-of-data}

With the new [!DNL Platform] SDK, the maximum read size is 32 GB, with a maximum read time of 10 minutes.

Si votre temps de lecture est trop long, vous pouvez essayer d’utiliser l’une des options de filtrage suivantes :

- [Filtrage des données par décalage et limite](#filter-by-offset-and-limit)
- [Filtrage des données par date](#filter-by-date)
- [Filtrage des données par colonne](#filter-by-selected-columns)
- [Obtention de résultats triés](#get-sorted-results)

>[!NOTE]
>
>L’organisation IMS est définie dans le `client_context`.

### Python

Pour lire les données en Python, veuillez utiliser l’exemple de code ci-dessous :

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

Pour lire les données en R, utilisez l’exemple de code ci-dessous :

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Filtrage par décalage et par limite {#filter-by-offset-and-limit}

Le filtrage par identifiant de lot n’étant plus pris en charge, vous devez utiliser `offset` et `limit` pour étendre la lecture des données.

### Python

```python
df = dataset_reader.limit(100).offset(1).read()
df.head
```

### R

```r
df <- dataset_reader$limit(100L)$offset(1L)$read() 
df
```

## Filtrage par date {#filter-by-date}

La granularité du filtrage par date est désormais définie par la date et l’heure, plutôt que par le jour.

### Python

```python
df = dataset_reader.where(\
    dataset_reader['timestamp'].gt('2019-04-10 15:00:00').\
    And(dataset_reader['timestamp'].lt('2019-04-10 17:00:00'))\
).read()
df.head()
```

### R

```r
df2 <- dataset_reader$where(
    dataset_reader['timestamp']$gt('2018-12-10 15:00:00')$
    And(dataset_reader['timestamp']$lt('2019-04-10 17:00:00'))
)$read()
df2
```

The new [!DNL Platform] SDK supports the following operations:

| Opération | Fonction |
| --------- | -------- |
| Est égal à (`=`) | `eq()` |
| Supérieur à (`>`) | `gt()` |
| Supérieur ou égal à (`>=`) | `ge()` |
| Inférieur à (`<`) | `lt()` |
| Inférieur ou égal à (`<=`) | `le()` |
| Et (`&`) | `And()` |
| Ou (`|`) | `Or()` |

## Filtrage par colonnes sélectionnées {#filter-by-selected-columns}

Pour affiner davantage votre lecture des données, vous pouvez également filtrer par nom de colonne.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Obtention de résultats triés {#get-sorted-results}

Les résultats obtenus peuvent être triés en fonction de colonnes spécifiques du jeu de données cible et dans leur ordre respectif (croissant/décroissant).

Dans l’exemple suivant, le cadre de données est trié par « colonne-a » en premier, dans l’ordre croissant. Les lignes ayant les mêmes valeurs pour « colonne-a » sont ensuite triées en fonction de « colonne-b » dans l’ordre décroissant.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Écriture basique des données {#basic-writing-of-data}

>[!NOTE]
>
>L’organisation IMS est définie dans le `client_context`.

Pour écrire des données en Python et en R, utilisez l’un des exemples suivants :

### Python

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### R

```r
dataset <- psdk$models$Dataset(client_context)$get_by_id("{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(client_context, dataset)
write_tracker <- dataset_writer$write({PANDA_DATAFRAME}, file_format='json')
```

## Étapes suivantes

Une fois que vous avez configuré l’outil de chargement de données `platform_sdk`, les données sont préparées puis réparties dans les jeux de données `train` et `val`. Pour en savoir plus sur la préparation des données et la conception des fonctionnalités, consultez la section sur [la préparation des données et la conception des fonctionnalités](../jupyterlab/create-a-recipe.md#data-preparation-and-feature-engineering) du tutoriel sur la création d’une recette à l’aide des notebooks [!DNL JupyterLab]