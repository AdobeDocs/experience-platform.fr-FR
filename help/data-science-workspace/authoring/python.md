---
keywords: Experience Platform;accueil;rubriques populaires;accès aux données;sdk python;api data access;lire python;écrire python
solution: Experience Platform
title: Accès aux données à l’aide de Python dans le Workspace de science des données
type: Tutorial
description: Le document suivant contient des exemples d’accès aux données en Python à utiliser dans le Workspace de science des données.
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
TQID: https://experienceleague.adobe.com/ZnNACjUyOdEHld7l1z8ksqitjc9oQIIuku3Tp2A8XQY
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 0%

---

# Accès aux données à l’aide de Python dans le Workspace de science des données

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

Le document suivant contient des exemples d’accès aux données à l’aide de Python pour une utilisation dans le Workspace de science des données. Pour plus d’informations sur l’accès aux données à l’aide des notebooks JupyterLab, consultez la documentation sur l’accès aux données des notebooks [JupyterLab](../jupyterlab/access-notebook-data.md) .

## Lecture d’un jeu de données

Après avoir défini les variables d’environnement et terminé l’installation, votre jeu de données peut maintenant être lu dans le cadre de données pandas.

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### SÉLECTIONNER des colonnes dans le jeu de données

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

La clause DISTINCT vous permet de récupérer toutes les valeurs distinctes au niveau de la ligne/colonne, en supprimant toutes les valeurs en double de la réponse.

Vous trouverez ci-dessous un exemple d’utilisation de la fonction `distinct()` :

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### Clause WHERE

Vous pouvez utiliser certains opérateurs en Python pour aider à filtrer votre jeu de données.

>[!NOTE]
>
>Les fonctions utilisées pour le filtrage respectent la casse.

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

La clause ORDER BY permet de trier les résultats reçus selon une colonne spécifiée dans un ordre spécifique (croissant ou décroissant). Pour ce faire, utilisez la fonction `sort()` .

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

La clause OFFSET vous permet d&#39;ignorer des lignes depuis le début pour commencer à renvoyer des lignes à partir d&#39;un point ultérieur. En combinaison avec LIMIT, cela peut être utilisé pour itérer des lignes dans des blocs.

Vous trouverez ci-dessous un exemple d’utilisation de la fonction `offset()` :

```python
df = dataset_reader.offset(100).read()
```

## Écriture d’un jeu de données

Pour écrire dans un jeu de données, vous devez fournir le cadre de données pandas à votre jeu de données.

### Écriture du Dataframe Pandas

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Répertoire de l&#39;espace utilisateur (point de contrôle)

Pour les tâches plus longues, vous devrez peut-être stocker des étapes intermédiaires. Dans des instances comme celle-ci, vous pouvez lire et écrire dans un espace utilisateur.

>[!NOTE]
>
>Les chemins d’accès aux données ne sont **pas** stockés. Vous devez stocker le chemin d’accès correspondant dans ses données respectives.

### Écrire dans l’espace utilisateur

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Lecture depuis l’espace utilisateur

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## Étapes suivantes

Le Workspace de science des données de Adobe Experience Platform fournit un exemple de recette qui utilise les exemples de code ci-dessus pour lire et écrire des données. Si vous souhaitez en savoir plus sur l’utilisation de Python pour accéder à vos données, consultez la section [Référentiel GitHub Python de Workspace de science des données](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
