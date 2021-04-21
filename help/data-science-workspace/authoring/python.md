---
keywords: Experience Platform ; accueil ; sujets populaires ; accès aux données ; sdk python ; api d'accès aux données ; lire python ; écrire python
solution: Experience Platform
title: Accès aux données à l'aide de Python dans Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Le document suivant contient des exemples sur la façon d'accéder aux données en Python pour les utiliser dans Data Science Workspace.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 2%

---

# Accès aux données à l&#39;aide de Python dans Data Science Workspace

Le document suivant contient des exemples d’accès aux données à l’aide de Python pour une utilisation dans Data Science Workspace. Pour plus d&#39;informations sur l&#39;accès aux données à l&#39;aide des blocs-notes JupyterLab, consultez la [documentation relative à l&#39;accès aux données des blocs-notes JupyterLab](../jupyterlab/access-notebook-data.md).

## Lecture d’un jeu de données

Après avoir défini les variables d&#39;environnement et terminé l&#39;installation, votre jeu de données peut maintenant être lu dans la base de données pandas.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### SÉLECTIONNER les colonnes du jeu de données

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Obtenir les informations de partitionnement :

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### Clause DISTINCT

La clause DISTINCT vous permet de récupérer toutes les valeurs distinctes au niveau de la ligne/colonne, en supprimant toutes les valeurs de duplicata de la réponse.

Vous trouverez ci-dessous un exemple d&#39;utilisation de la fonction `distinct()` :

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

La clause ORDER BY permet de trier les résultats reçus selon une colonne spécifiée dans un ordre spécifique (croissant ou décroissant). Pour ce faire, utilisez la fonction `sort()`.

Vous trouverez ci-dessous un exemple d&#39;utilisation de la fonction `sort()` :

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Clause LIMIT

La clause LIMIT vous permet de limiter le nombre d&#39;enregistrements reçus du jeu de données.

Vous trouverez ci-dessous un exemple d&#39;utilisation de la fonction `limit()` :

```python
df = dataset_reader.limit(100).read()
```

### Clause OFFSET

La clause OFFSET vous permet de sauter des lignes du début au début de renvoyer des lignes d’un point ultérieur. En combinaison avec LIMIT, vous pouvez l’utiliser pour itérer des lignes dans des blocs.

Vous trouverez ci-dessous un exemple d&#39;utilisation de la fonction `offset()` :

```python
df = dataset_reader.offset(100).read()
```

## Création d’un jeu de données

Pour écrire dans un jeu de données, vous devez fournir le cadre de données pandas à votre jeu de données.

### Ecriture du cadre de données des pandas

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Répertoire Userspace (Checkpoint)

Pour les tâches à exécution plus longue, vous devrez peut-être stocker des étapes intermédiaires. Dans de tels cas, vous pouvez lire et écrire dans un espace utilisateur.

>[!NOTE]
>
>Les chemins d’accès aux données sont **non** stockés. Vous devez stocker le chemin d’accès correspondant à ses données respectives.

### Écrire dans l&#39;espace utilisateur

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

Adobe Experience Platform Data Science Workspace fournit un exemple de recette qui utilise les exemples de code ci-dessus pour lire et écrire des données. Si vous souhaitez en savoir plus sur l&#39;utilisation de Python pour accéder à vos données, consultez le [référentiel Python GitHub de Data Science Workspace](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
