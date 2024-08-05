---
keywords: Experience Platform;guide de développement;SDK;SDK Data Access;Data Science Workspace;rubriques les plus consultées
solution: Experience Platform
title: Création de modèles à l’aide du SDK Adobe Experience Platform Platform
description: Ce tutoriel vous fournit des informations sur la conversion de data_access_sdk_python en nouveau Python platform_sdk en Python et en R.
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 57%

---

# Création de modèles à l’aide du SDK Adobe Experience Platform [!DNL Platform]

>[!NOTE]
>
>Data Science Workspace ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs à Data Science Workspace.

Ce tutoriel vous fournit des informations sur la conversion de `data_access_sdk_python` en nouveau `platform_sdk` Python en Python et en R. Ce tutoriel fournit des informations sur les opérations suivantes :

- [Authentification de création](#build-authentication)
- [Lecture basique des données](#basic-reading-of-data)
- [Écriture basique des données](#basic-writing-of-data)

## Authentification de création {#build-authentication}

L’authentification est requise pour effectuer des appels vers [!DNL Adobe Experience Platform]. Elle comprend la clé API, l’ID d’organisation, un jeton utilisateur et un jeton de service.

### Python

Si vous utilisez Jupyter Notebook, veuillez utiliser le code ci-dessous pour créer le `client_context` :

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Si vous n’utilisez pas Jupyter Notebook ou si vous devez modifier l’organisation, utilisez l’exemple de code suivant :

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
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

Si vous n’utilisez pas Jupyter Notebook ou si vous devez changer d’organisation, utilisez l’exemple de code suivant :

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Lecture basique des données {#basic-reading-of-data}

Avec le nouveau SDK [!DNL Platform], la taille de lecture maximale est de 32 Go, avec un temps de lecture maximal de 10 minutes.

Si votre temps de lecture est trop long, vous pouvez essayer d’utiliser l’une des options de filtrage suivantes :

- [Filtrage des données par décalage et limite](#filter-by-offset-and-limit)
- [Filtrer les données par date](#filter-by-date)
- [Filtrage des données par colonne](#filter-by-selected-columns)
- [Obtention de résultats triés](#get-sorted-results)

>[!NOTE]
>
>L’organisation est définie dans le `client_context`.

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

Le nouveau SDK [!DNL Platform] prend en charge les opérations suivantes :

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
>L’organisation est définie dans le `client_context`.

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

Une fois que vous avez configuré l’outil de chargement de données `platform_sdk`, les données sont préparées puis réparties dans les jeux de données `train` et `val`. Pour en savoir plus sur la préparation des données et la conception des fonctionnalités, consultez la section sur la [préparation des données et la conception des fonctionnalités](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering) du tutoriel sur la création d’une recette à l’aide de [!DNL JupyterLab] notebooks.
