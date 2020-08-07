---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: SDK Secure Python Data Access
topic: tutorial
translation-type: tm+mt
source-git-commit: 86ded28b1830d3607c8b5214c8d31dfcbf446252
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---


# SDK sécurisé [!DNL Python][!DNL Data Access]

Secure [!DNL Python] SDK [!DNL Data Access] est un kit de développement logiciel qui permet la lecture et l&#39;écriture de jeux de données de Adobe Experience Platform.

## Prise en main

Vous devez avoir suivi le didacticiel [d’authentification](../../tutorials/authentication.md) pour pouvoir accéder aux valeurs permettant d’invoquer le [!DNL Python] [!DNL Data Access] SDK sécurisé :

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. L’utilisation du [!DNL Python] SDK nécessite le nom et l’ID du sandbox dans lesquels l’opération aura lieu :

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

## Configuration des Environnements

Par défaut, les points de terminaison de service sont définis sur les points de terminaison d’environnement d’intégration. Par conséquent, pour pointer vers la production, définissez les variables d’environnement suivantes sur les valeurs suivantes :

| Variable | Point de terminaison |
| -------- | -------- |
| `ENV_CATALOG_URL` | `https://platform.adobe.io/data/foundation/catalog/` |
| `ENV_QUERY_SERVICE_URL` | `https://platform.adobe.io/data/foundation/query` |
| `ENV_BULK_INGEST_URL` | `https://platform.adobe.io/data/foundation/import/` |
| `ENV_REGISTRY_URL` | `https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas` |

De plus, vos informations d’identification peuvent être ajoutées en tant que variables d’environnement.

| Variable | Valeur |
| -------- | ----- |
| `ORG_ID` | Votre `{IMS_ORG}` identifiant. |
| `SERVICE_API_KEY` | Votre `{API_KEY}` valeur. |
| `USER_TOKEN` | Votre `{ACCESS_TOKEN}` valeur. |
| `SERVICE_TOKEN` | Votre `{SERVICE_TOKEN}`, que vous devrez peut-être autoriser à effectuer des demandes en canal arrière entre des services. |
| `SANDBOX_ID` | Valeur `{SANDBOX_ID}` de votre sandbox. |
| `SANDBOX_NAME` | Valeur `{SANDBOX_NAME}` de votre sandbox. |

## Installation

Tous les paquets sont sortis `./dist` après la création.

### Roue

```python
python3 setup.py bdist_wheel --universal
```

Dans le répertoire du projet, chargez roue dans votre [!DNL Python] environnement 3.

```python
pip3 install ./dist/<name_of_wheel_file>.whl
```

### Fichier d&#39;oeufs

```python
python3 setup.py bdist_egg
```

## Lecture d’un jeu de données

Après avoir défini les variables d&#39;environnement et terminé l&#39;installation, le jeu de données peut maintenant être lu dans la base de données pandas.

```python
from platform_sdk.client_context import ClientContext
from platform_sdk.dataset_reader import DatasetReader

client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset_reader = DatasetReader(client_context, {DATASET_ID})
df = dataset_reader.read()
```

### SÉLECTIONNER les colonnes du jeu de données

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### Obtenir les informations de partitionnement :

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### Clause DISTINCT

La clause DISTINCT vous permet de récupérer toutes les valeurs distinctes au niveau de la ligne/colonne, en supprimant toutes les valeurs de duplicata de la réponse.

Vous trouverez ci-dessous un exemple d’utilisation de la `distinct()` fonction :

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### Clause WHERE

Le [!DNL Python] SDK prend en charge certains opérateurs pour aider à filtrer le jeu de données.

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

La clause ORDER BY permet de trier les résultats reçus selon une colonne spécifiée dans un ordre spécifique (croissant ou décroissant). Dans le [!DNL Python] SDK, cela se fait en utilisant la `sort()` fonction.

Vous trouverez ci-dessous un exemple d’utilisation de la `sort()` fonction :

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### Clause LIMIT

La clause LIMIT permet aux utilisateurs de limiter le nombre d&#39;enregistrements reçus du jeu de données.

Vous trouverez ci-dessous un exemple d’utilisation de la `limit()` fonction :

```python
df = dataset_reader.limit(100).read()
```

### Clause OFFSET

La clause OFFSET permet aux utilisateurs de sauter des lignes du début au début de renvoyer des lignes d’un point ultérieur. En combinaison avec LIMIT, vous pouvez l’utiliser pour itérer des lignes dans des blocs.

Vous trouverez ci-dessous un exemple d’utilisation de la `offset()` fonction :

```python
df = dataset_reader.offset(100).read()
```

## Création d’un jeu de données

Le [!DNL Python] SDK prend en charge l’écriture de jeux de données. Les utilisateurs devront fournir le cadre de données pandas qui doit être écrit dans le jeu de données.

### Ecriture du cadre de données des pandas

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<dataFrame>, file_format='json')
```

## Répertoire Userspace (Checkpoint)

Pour les tâches plus longues, les utilisateurs peuvent avoir besoin de stocker des étapes intermédiaires. Dans des instances de ce type, le [!DNL Python] SDK permet à l’utilisateur de lire et d’écrire dans un espace utilisateur.

>!![NOTE] Les chemins d’accès aux données **ne sont pas** stockés par le SDK. Les utilisateurs devront stocker le chemin d’accès correspondant à leurs données respectives.

### Écrire dans l&#39;espace utilisateur

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### Lecture à partir de l’espace utilisateur

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```
