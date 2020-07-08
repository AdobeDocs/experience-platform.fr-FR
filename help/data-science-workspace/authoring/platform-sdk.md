---
keywords: Experience Platform;developer guide;SDK;Data Access SDK;Data Science Workspace;popular topics
solution: Experience Platform
title: Guide du SDK Platform
topic: SDK authoring
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 5%

---


# [!DNL Platform] Guide SDK

Ce tutoriel vous fournit des informations sur la conversion `data_access_sdk_python` au nouveau Python `platform_sdk` en Python et en R. Ce tutoriel fournit des informations sur les opérations suivantes :

- [Créer l&#39;authentification](#build-authentication)
- [Lecture de base des données](#basic-reading-of-data)
- [Écriture de base des données](#basic-writing-of-data)

## Créer l&#39;authentification {#build-authentication}

L’authentification est requise pour effectuer des appels vers [!DNL Adobe Experience Platform]une clé d’API, un ID d’organisation IMS, un jeton d’utilisateur et un jeton de service.

### Python

Si vous utilisez Jupyter Notebook, veuillez utiliser le code ci-dessous pour créer le `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

Si vous n&#39;utilisez pas Jupyter Notebook ou que vous devez modifier l&#39;organisation IMS, veuillez utiliser l&#39;exemple de code suivant :

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### r

Si vous utilisez Jupyter Notebook, veuillez utiliser le code ci-dessous pour créer le `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

Si vous n&#39;utilisez pas Jupyter Notebook ou que vous devez modifier l&#39;organisation IMS, veuillez utiliser l&#39;exemple de code suivant :

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## Lecture de base des données {#basic-reading-of-data}

Avec le nouveau [!DNL Platform] SDK, la taille de lecture maximale est de 32 Go, avec une durée de lecture maximale de 10 minutes.

Si votre temps de lecture est trop long, vous pouvez essayer d’utiliser l’une des options de filtrage suivantes :

- [Filtrage des données par décalage et limite](#filter-by-offset-and-limit)
- [Filtrage des données par date](#filter-by-date)
- [Filtrage des données par colonne](#filter-by-selected-columns)
- [Obtention des résultats triés](#get-sorted-results)

>[!NOTE]
>
>L’organisation IMS est définie dans le `client_context`.

### Python

Pour lire les données en Python, veuillez utiliser l&#39;exemple de code ci-dessous :

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### r

Pour lire les données dans R, utilisez l&#39;exemple de code ci-dessous :

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## Filtrage par décalage et limite {#filter-by-offset-and-limit}

Comme le filtrage par ID de lot n’est plus pris en charge, pour étendre la lecture des données, vous devez utiliser `offset` et `limit`.

### Python

```python
df = dataset_reader.limit(100).offset(1).read()
df.head
```

### r

```r
df <- dataset_reader$limit(100L)$offset(1L)$read() 
df
```

## Filtrage par date {#filter-by-date}

La granularité du filtrage par date est désormais définie par l’horodatage, plutôt que par jour.

### Python

```python
df = dataset_reader.where(\
    dataset_reader['timestamp'].gt('2019-04-10 15:00:00').\
    And(dataset_reader['timestamp'].lt('2019-04-10 17:00:00'))\
).read()
df.head()
```

### r

```r
df2 <- dataset_reader$where(
    dataset_reader['timestamp']$gt('2018-12-10 15:00:00')$
    And(dataset_reader['timestamp']$lt('2019-04-10 17:00:00'))
)$read()
df2
```

Le nouveau [!DNL Platform] SDK prend en charge les opérations suivantes :

| Opération | Fonction |
| --------- | -------- |
| Est égal (`=`) | `eq()` |
| Supérieur à (`>`) | `gt()` |
| Supérieur ou égal à (`>=`) | `ge()` |
| Inférieur à (`<`) | `lt()` |
| Inférieur ou égal à (`<=`) | `le()` |
| And (`&`) | `And()` |
| Sinon (`|`) | `Or()` |

## Filtrage par colonnes sélectionnées {#filter-by-selected-columns}

Pour affiner davantage votre lecture des données, vous pouvez également filtrer par nom de colonne.

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### r

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## Obtenir les résultats triés {#get-sorted-results}

Les résultats reçus peuvent être triés selon des colonnes spécifiées du jeu de données de la cible et dans leur ordre (asc/desc) respectivement.

Dans l&#39;exemple suivant, le cadre de données est trié par &quot;colonne-a&quot; en premier dans l&#39;ordre croissant. Les lignes dont les valeurs sont identiques pour &quot;colonne-a&quot; sont ensuite triées par &quot;colonne-b&quot; dans l’ordre décroissant.

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### r

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## Écriture de base des données {#basic-writing-of-data}

>[!NOTE]
>
>L’organisation IMS est définie dans le `client_context`.

Pour écrire des données en Python et R, utilisez l&#39;un des exemples suivants :

### Python

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### r

```r
dataset <- psdk$models$Dataset(client_context)$get_by_id("{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(client_context, dataset)
write_tracker <- dataset_writer$write({PANDA_DATAFRAME}, file_format='json')
```

## Étapes suivantes

Une fois que vous avez configuré le chargeur de `platform_sdk` données, les données sont en préparation et sont ensuite fractionnées en jeux de données `train` et `val` de données. Pour en savoir plus sur la préparation des données et l&#39;ingénierie des fonctionnalités, consultez la section sur la préparation des [données et l&#39;ingénierie](../jupyterlab/create-a-recipe.md#data-preparation-and-feature-engineering) des fonctionnalités du didacticiel sur la création d&#39;une recette à l&#39;aide de [!DNL JupyterLab] cahiers.