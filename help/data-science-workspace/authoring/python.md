---
keywords: Experience Platform;accueil;rubriques les plus consultées;accès aux données;sdk python;api d’accès aux données;lire python;écrire python
solution: Experience Platform
title: Accès aux données à l’aide de Python dans Data Science Workspace
type: Tutorial
description: Le document suivant contient des exemples d’accès aux données en Python à utiliser dans Data Science Workspace.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Accès aux données à l’aide de Python dans Data Science Workspace

>[!NOTE]
>
>Data Science Workspace ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs à Data Science Workspace.

Le document suivant contient des exemples d’accès aux données à l’aide de Python à utiliser dans Data Science Workspace. Pour plus d’informations sur l’accès aux données à l’aide des notebooks JupyterLab, consultez la documentation [ sur l’accès aux données des notebooks JupyterLab](../jupyterlab/access-notebook-data.md).

## Lecture d’un jeu de données

Après avoir défini les variables d’environnement et terminé l’installation, votre jeu de données peut désormais être lu dans le cadre de données pandas.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### SÉLECTIONNER des colonnes du jeu de données

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Obtention des informations de partitionnement :

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### Clause DISTINCT

La clause DISTINCT vous permet de récupérer toutes les valeurs distinctes au niveau d’une ligne/colonne, supprimant toutes les valeurs en double de la réponse.

Vous trouverez ci-dessous un exemple d’utilisation de la fonction `distinct()` :

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### Clause WHERE

Vous pouvez utiliser certains opérateurs en Python pour vous aider à filtrer votre jeu de données.

>[!NOTE]
>
>Les fonctions utilisées pour le filtrage sont sensibles à la casse.

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

Vous trouverez ci-dessous un exemple d’utilisation de ces fonctions de filtrage :

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### Clause ORDER BY

La clause ORDER BY permet de trier les résultats reçus par une colonne spécifiée dans un ordre spécifique (croissant ou décroissant). Pour ce faire, utilisez la fonction `sort()` .

Vous trouverez ci-dessous un exemple d’utilisation de la fonction `sort()` :

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Clause LIMIT

La clause LIMIT vous permet de limiter le nombre d’enregistrements reçus du jeu de données.

Vous trouverez ci-dessous un exemple d’utilisation de la fonction `limit()` :

```python
df = dataset_reader.limit(100).read()
```

### Clause OFFSET

La clause OFFSET vous permet d’ignorer les lignes, dès le début, pour commencer à renvoyer des lignes à partir d’un point ultérieur. Combinée avec LIMIT, cette méthode peut être utilisée pour itérer les lignes dans des blocs.

Vous trouverez ci-dessous un exemple d’utilisation de la fonction `offset()` :

```python
df = dataset_reader.offset(100).read()
```

## Écriture d’un jeu de données

Pour écrire dans un jeu de données, vous devez fournir le cadre de données pandas à votre jeu de données.

### Écriture du cadre de données pandas

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Répertoire d’espace utilisateur (Checkpointer)

Pour les tâches plus longues, vous devrez peut-être stocker des étapes intermédiaires. Dans des cas comme celui-ci, vous pouvez lire et écrire dans un espace utilisateur.

>[!NOTE]
>
>Les chemins d’accès aux données sont **et non** stockés. Vous devez stocker le chemin d’accès correspondant à ses données respectives.

### Écriture sur l’espace utilisateur

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Lecture à partir de l’espace utilisateur

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## Étapes suivantes

Adobe Experience Platform Data Science Workspace fournit un exemple de recette qui utilise les exemples de code ci-dessus pour lire et écrire des données. Si vous souhaitez en savoir plus sur l’utilisation de Python pour accéder à vos données, consultez le [référentiel Python GitHub Python de Data Science Workspace](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
