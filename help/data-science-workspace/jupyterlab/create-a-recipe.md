---
keywords: Experience Platform ; JupyterLab ; recette ; cahiers ; Espace de travail des sciences de données ; rubriques populaires ; créer une recette
solution: Experience Platform
title: Créer une recette à l'aide de portables Jupyter
topic: tutorial
type: Tutorial
description: Ce tutoriel se déroulera en deux temps. Tout d’abord, vous créerez un modèle d’apprentissage automatique à l’aide d’un modèle dans JupyterLab Notebook. Ensuite, vous utiliserez le notebook pour recevoir le workflow dans JupyterLab afin de créer une recette dans Data Science Workspace.
translation-type: tm+mt
source-git-commit: 9d84fc1eb898020ed4b154c091fcc9fc4933c7de
workflow-type: tm+mt
source-wordcount: '2366'
ht-degree: 81%

---


# Création d&#39;une recette à l&#39;aide de portables Jupyter

Ce tutoriel se déroulera en deux temps. Tout d’abord, vous créerez un modèle d’apprentissage automatique à l’aide d’un modèle dans [!DNL JupyterLab Notebook]. Ensuite, vous allez utiliser le bloc-notes pour exécuter le processus de recette dans [!DNL JupyterLab] pour créer une recette dans [!DNL Data Science Workspace].

## Concepts présentés :

- **Recettes :** une recette est le terme utilisé par Adobe pour désigner une spécification de modèle. Il s’agit d’un conteneur de niveau supérieur qui représente un apprentissage automatique spécifique, un algorithme d’intelligence artificielle ou un ensemble d’algorithmes, une logique de traitement et la configuration nécessaires pour créer et exécuter un modèle formé et ainsi aider à résoudre des problèmes d’entreprise spécifiques.
- **Modèle :** un modèle est une instance d’une recette d’apprentissage automatique formée à l’aide de données historiques et de configurations dans le but de résoudre un cas d’usage commercial.
- **Formation :** la formation est le processus de formation de modèles et de connaissances à partir de données étiquetées.
- **Notation :** la notation est le processus de génération d’informations à partir de données en utilisant un modèle formé.

## Commencez avec l&#39;environnement d&#39;ordinateur portable [!DNL JupyterLab]

Vous pouvez créer une recette à partir de zéro dans [!DNL Data Science Workspace]. Pour début, accédez à [Adobe Experience Platform](https://platform.adobe.com) et cliquez sur l&#39;onglet **[!UICONTROL Ordinateurs portables]** à gauche. Créez un bloc-notes en sélectionnant le modèle Créateur de recettes dans le [!DNL JupyterLab Launcher].

Le bloc-notes [!UICONTROL Recipe Builder] vous permet d&#39;exécuter des actions de formation et de notation dans le bloc-notes. Vous avez ainsi la possibilité d’apporter des modifications à leurs méthodes de `train()` et de `score()` entre deux expériences en cours d’exécution sur les données de formation et de notation. Une fois que vous êtes satisfait des résultats de la formation et du score, vous pouvez créer une recette à utiliser dans [!DNL Data Science Workspace] à l&#39;aide du bloc-notes pour la fonctionnalité de recette intégrée au bloc-notes du Générateur de recettes.

>[!NOTE]
>
>Le notebook Recipe Builder prend en charge l’utilisation de tous les formats de fichier, mais la fonctionnalité Create Recipe ne prend actuellement en charge que [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder.png)

Lorsque vous cliquez sur le bloc-notes du Générateur de recettes depuis le lanceur, le bloc-notes s&#39;ouvre dans l&#39;onglet. Le modèle utilisé dans le notebook est la recette Python de prévision des ventes au détail, qui se trouve également dans [ce référentiel public](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/).

Vous remarquerez que dans la barre d&#39;outils, il y a trois autres actions : **[!UICONTROL Train]**, **[!UICONTROL Score]** et **[!UICONTROL Créer une recette]**. Ces icônes s’affichent uniquement dans le bloc-notes [!UICONTROL Générateur de recettes]. Vous trouverez plus d’informations sur ces actions [dans la section Formation et notation](#training-and-scoring) après avoir créé votre recette dans le notebook.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Modification des fichiers de recette

Pour apporter des modifications aux fichiers de recette, accédez dans Jupyter à la cellule correspondant au chemin du fichier. Par exemple, si vous souhaitez apporter des modifications à `evaluator.py`, recherchez `%%writefile demo-recipe/evaluator.py`.

Effectuez les modifications nécessaires dans la cellule. Lorsque vous avez terminé, exécutez simplement la cellule. La commande `%%writefile filename.py` écrira le contenu de la cellule dans `filename.py`. Vous devrez exécuter manuellement la cellule pour chaque fichier avec modifications.

>[!NOTE]
>
>Vous devriez exécuter les cellules manuellement lorsque cela est nécessaire.

## Prise en main du notebook Recipe Builder

Maintenant que vous connaissez les bases de l&#39;environnement de portables [!DNL JupyterLab], vous pouvez commencer à regarder les fichiers qui constituent une recette de modèle d&#39;apprentissage automatique. Les fichiers concernés sont présentés ici :

- [Fichier des exigences](#requirements-file)
- [Fichiers de configuration](#configuration-files)
- [Chargeur de données d’apprentissage](#training-data-loader)
- [Chargeur de données de notation](#scoring-data-loader)
- [Fichier Pipeline](#pipeline-file)
- [Fichier Evaluator](#evaluator-file)
- [Fichier Data Saver](#data-saver-file)

### Fichier des exigences {#requirements-file}

Le fichier des exigences sert à définir les bibliothèques supplémentaires que vous souhaitez utiliser dans la recette. En cas de dépendance, vous pouvez spécifier le numéro de version. Pour rechercher d&#39;autres bibliothèques, visitez [anaconda.org](https://anaconda.org). Pour savoir comment formater le fichier de configuration requise, visitez [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). Voici une liste non exhaustive des principales bibliothèques déjà utilisées :

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>Les bibliothèques ou versions spécifiques que vous ajoutez peuvent être incompatibles avec les bibliothèques mentionnées ci-dessus. De plus, si vous choisissez de créer manuellement un fichier d&#39;environnement, le champ `name` n&#39;est pas autorisé à être remplacé.

### Fichiers de configuration {#configuration-files}

Les fichiers de configuration, `training.conf` et `scoring.conf`, servent à spécifier les jeux de données que vous souhaitez utiliser pour la formation et la notation, et à ajouter des hyperparamètres. Les configurations pour la formation et la notation sont distinctes.

Les utilisateurs doivent renseigner les variables suivantes avant d’exécuter la formation et la notation :
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

Pour trouver le jeu de données et les ID de schéma, accédez à l&#39;onglet de données ![Data tab](../images/jupyterlab/create-recipe/dataset-tab.png) dans les blocs-notes de la barre de navigation de gauche (sous l&#39;icône de dossier).

![](../images/jupyterlab/create-recipe/dataset_tab.png)

Vous trouverez les mêmes informations sur [Adobe Experience Platform](https://platform.adobe.com/) sous les onglets **[Schéma](https://platform.adobe.com/schema)** et **[Jeu de données](https://platform.adobe.com/dataset/overview)**.

Les paramètres de configuration suivants sont définis par défaut lorsque vous accédez aux données :

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Chargeur de données d’apprentissage  {#training-data-loader}

Le chargeur de données d’apprentissage est destiné à instancier les données utilisées pour créer le modèle d’apprentissage automatique. En règle générale, le chargeur de données d’apprentissage accomplit deux tâches :
- Charger les données de [!DNL Platform]
- Préparation des données et ingénierie des fonctionnalités

Les deux prochaines sections traiteront du chargement et de la préparation des données.

### Chargement des données  {#loading-data}

Cette étape utilise le [cadre de données pandas](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). Les données peuvent être chargées à partir de fichiers dans [!DNL Adobe Experience Platform] à l&#39;aide du SDK [!DNL Platform] (`platform_sdk`) ou à partir de sources externes utilisant les fonctions `read_csv()` ou `read_json()` de pandas.

- [[!DNL Platform SDK]](#platform-sdk)
- [Sources externes](#external-sources)

>[!NOTE]
>
> Dans le notebook Recipe Builder, les données sont chargées via le chargeur de données `platform_sdk`.

### [!DNL Platform] SDK {#platform-sdk}

Pour un tutoriel détaillé sur l’utilisation du chargeur de données `platform_sdk`, consultez le [guide SDK Platform](../authoring/platform-sdk.md). Ce tutoriel fournit des informations sur l’authentification de création, la lecture et l’écriture basiques de données.

### Sources externes  {#external-sources}

Cette section vous explique comment importer un fichier JSON ou CSV dans un objet pandas. La documentation officielle de la bibliothèque pandas se trouve ici :
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

Tout d’abord, voici un exemple d’importation d’un fichier CSV. L’argument `data` est le chemin d’accès au fichier CSV. Cette variable a été importée à partir de `configProperties` de la [section précédente](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

Vous pouvez également réaliser l’importation à partir d’un fichier JSON. L’argument `data` est le chemin d’accès au fichier CSV. Cette variable a été importée à partir de `configProperties` de la [section précédente](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

Vos données se trouvent maintenant dans l’objet « cadre de données » et peuvent être analysées et manipulées dans la [section suivante](#data-preparation-and-feature-engineering).

### A partir du SDK de plate-forme

Vous pouvez charger des données à l’aide du SDK de plate-forme. La bibliothèque peut être importée en haut de la page en incluant la ligne :

`from platform_sdk.dataset_reader import DatasetReader`

Nous utilisons ensuite la méthode `load()` pour récupérer le jeu de données d’apprentissage à partir de `trainingDataSetId` comme précisé dans notre fichier de configuration (`recipe.conf`).

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    
    dataset_reader = DatasetReader(client_context, config_properties['trainingDataSetId'])
    
    timeframe = config_properties.get("timeframe")
    tenant_id = config_properties.get("tenant_id")
```

>[!NOTE]
>
>Comme mentionné dans la section [Fichier de configuration](#configuration-files), les paramètres de configuration suivants sont définis pour vous lorsque vous accédez aux données de l&#39;Experience Platform à l&#39;aide de `client_context` :
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Maintenant que vous disposez de vos données, vous pouvez commencer leur préparation ainsi que la conception des fonctionnalités.

### Préparation des données et ingénierie des fonctionnalités  {#data-preparation-and-feature-engineering}

Une fois les données chargées, elles sont préparées puis partagées entre les jeux de données `train` et `val`. Voici un échantillon de code :

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
dataframe.date = pd.to_datetime(dataframe.date)
dataframe['week'] = dataframe.date.dt.week
dataframe['year'] = dataframe.date.dt.year

dataframe = pd.concat([dataframe, pd.get_dummies(dataframe['storeType'])], axis=1)
dataframe.drop('storeType', axis=1, inplace=True)
dataframe['isHoliday'] = dataframe['isHoliday'].astype(int)

dataframe['weeklySalesAhead'] = dataframe.shift(-45)['weeklySales']
dataframe['weeklySalesLag'] = dataframe.shift(45)['weeklySales']
dataframe['weeklySalesDiff'] = (dataframe['weeklySales'] - dataframe['weeklySalesLag']) / dataframe['weeklySalesLag']
dataframe.dropna(0, inplace=True)

dataframe = dataframe.set_index(dataframe.date)
dataframe.drop('date', axis=1, inplace=True) 
```

Dans cet exemple, le jeu de données d’origine a subi cinq opérations :
- L’ajout de colonnes `week`et `year`
- La conversion de `storeType` en variable indicatrice
- La conversion de `isHoliday` en variable numérique
- Le décalage de `weeklySales` pour obtenir la valeur des ventes futures et antérieures
- Le partage des données par date entre les jeux de données `train` et `val`

D&#39;abord, les colonnes `week` et `year` sont créées et la colonne d&#39;origine `date` est convertie en [!DNL Python] [datetime](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html). Les valeurs Semaine et Année sont extraites de l’objet de datetime.

Ensuite, `storeType` est transformé en trois colonnes représentant les trois types de magasin différents, (`A`, `B` et `C`). Chacune contient une valeur booléenne qui indique quel `storeType` est vrai. La colonne `storeType` sera supprimée.

De même, `weeklySales` change la valeur booléenne `isHoliday` en une représentation numérique (un ou zéro).

Ces données sont partagées entre les jeux de données `train` et `val`.

La fonction `load()` doit être complétée avec les jeux de données `train` et `val` en tant que sortie.

### Chargeur de données de notation  {#scoring-data-loader}

La procédure de chargement des données pour notation est similaire à celle de chargement des données d’apprentissage de la fonction `split()`. Nous utilisons le SDK Data Access pour charger les données à partir de `scoringDataSetId` dans notre fichier `recipe.conf`.

```PYTHON
def load(config_properties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    client_context = get_client_context(config_properties)

    dataset_reader = DatasetReader(client_context, config_properties['scoringDataSetId'])
    timeframe = config_properties.get("timeframe")
    tenant_id = config_properties.get("tenant_id")
```

Une fois les données chargées, la préparation des données et la conception des fonctionnalités sont effectuées.

```PYTHON
    #########################################
    # Data Preparation/Feature Engineering
    #########################################
    if '_id' in dataframe.columns:
        #Rename columns to strip tenantId
        dataframe = dataframe.rename(columns = lambda x : str(x)[str(x).find('.')+1:])
        #Drop id, eventType and timestamp
        dataframe.drop(['_id', 'eventType', 'timestamp'], axis=1, inplace=True)

    dataframe.date = pd.to_datetime(dataframe.date)
    dataframe['week'] = dataframe.date.dt.week
    dataframe['year'] = dataframe.date.dt.year

    dataframe = pd.concat([dataframe, pd.get_dummies(dataframe['storeType'])], axis=1)
    dataframe.drop('storeType', axis=1, inplace=True)
    dataframe['isHoliday'] = dataframe['isHoliday'].astype(int)

    dataframe['weeklySalesAhead'] = dataframe.shift(-45)['weeklySales']
    dataframe['weeklySalesLag'] = dataframe.shift(45)['weeklySales']
    dataframe['weeklySalesDiff'] = (dataframe['weeklySales'] - dataframe['weeklySalesLag']) / dataframe['weeklySalesLag']
    dataframe.dropna(0, inplace=True)

    dataframe = dataframe.set_index(dataframe.date)
    dataframe.drop('date', axis=1, inplace=True)

    print("Scoring Data Load Finish")

    return dataframe
```

Puisque le but de notre modèle est de prédire les futures ventes hebdomadaires, vous devrez créer un jeu de données de notation servant à évaluer les performances de prédiction du modèle.

Ce notebook Recipe Builder le fait en décalant nos ventes hebdomadaires de sept jours vers l’avant. Vous remarquerez qu’il existe des mesures pour 45 magasins par semaine : vous pouvez donc déplacer les valeurs `weeklySales` de 45 jeux de données vers l’avant dans une nouvelle colonne intitulée `weeklySalesAhead`.

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

De même, vous pouvez créer une colonne `weeklySalesLag` en reculant de 45. Grâce à cela, vous pouvez également calculer la différence entre les ventes hebdomadaires et les stocker dans la colonne `weeklySalesDiff`.

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

Puisque vous décalez les points de données `weeklySales` de 45 jeux de données vers l’avant et de 45 jeux de données vers l’arrière pour créer de nouvelles colonnes, les 45 premiers et derniers points de données auront des valeurs NaN. Vous pouvez supprimer ces points de notre jeu de données en utilisant la fonction `df.dropna()` qui supprime toutes les lignes comportant des valeurs NaN.

```PYTHON
df.dropna(0, inplace=True)
```

La fonction `load()` de votre chargeur de données de notation doit comprendre le jeu de données de notation comme sortie.

### Fichier Pipeline  {#pipeline-file}

Le fichier `pipeline.py` inclut la logique de formation et de notation.

### Formation {#training}

L’objectif de la formation est de créer un modèle à l’aide des fonctionnalités et des étiquettes présentes dans votre jeu de données d’apprentissage.

>[!NOTE]
> 
>Les Fonctionnalités font référence à la variable d’entrée utilisée par le modèle d’apprentissage automatique pour prédire les étiquettes.

La fonction `train()` doit inclure le modèle de formation et renvoyer le modèle formé. Vous trouverez quelques exemples de différents modèles dans la [documentation du guide d’utilisation de scikit-learn](https://scikit-learn.org/stable/user_guide.html).

Après avoir choisi votre modèle de formation, vous ajusterez votre jeu de données d’apprentissage x et y au modèle, et la fonction renverra le modèle formé. En voici un exemple :

```PYTHON
def train(configProperties, data):

    print("Train Start")

    #########################################
    # Extract fields from configProperties
    #########################################
    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])


    #########################################
    # Fit model
    #########################################
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values

    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)

    model.fit(X_train, y_train)

    print("Train Complete")

    return model
```

Il faut souligner que selon votre application, vous aurez des arguments dans votre fonction `GradientBoostingRegressor()`. `xTrainingDataset` devrait contenir vos fonctionnalités utilisées pour la formation, tandis que `yTrainingDataset` devrait contenir vos étiquettes.

### Notation  {#scoring}

La fonction `score()` doit contenir l’algorithme de notation et renvoyer une mesure pour indiquer le degré de réussite du modèle. La fonction `score()` utilise les étiquettes des jeux de données de notation et le modèle formé pour générer un ensemble de fonctionnalités prédites. Ces valeurs prédites sont ensuite comparées aux fonctionnalités réelles du jeu de données de notation. Dans cet exemple, la fonction `score()` utilise le modèle formé pour prédire les fonctionnalités à l’aide des étiquettes du jeu de données de notation. Les fonctionnalités prédites sont renvoyées.

```PYTHON
def score(configProperties, data, model):

    print("Score Start")

    X_test = data.drop('weeklySalesAhead', axis=1).values
    y_test = data['weeklySalesAhead'].values
    y_pred = model.predict(X_test)

    data['prediction'] = y_pred
    data = data[['store', 'prediction']].reset_index()
    data['date'] = data['date'].astype(str)

    print("Score Complete")

    return data
```

### Fichier Evaluator  {#evaluator-file}

Le fichier `evaluator.py` contient la logique de la manière dont vous souhaitez évaluer votre recette formée ainsi que la manière dont vos données d’apprentissage doivent être fractionnées. Dans l’exemple de ventes au détail, la logique de chargement et de préparation des données d’apprentissage sera incluse. Nous allons passer en revue les deux sections ci-dessous.

### Fractionnement du jeu de données  {#split-the-dataset}

La phase de préparation des données pour la formation nécessite de fractionner le jeu de données à utiliser pour la formation et les tests. Ces données `val` seront utilisées implicitement pour évaluer le modèle après sa formation. Il s’agit d’un processus distinct de celui de notation.

Cette section montre la fonction `split()` qui chargera d’abord les données dans le notebook, puis les nettoiera en supprimant les colonnes inutiles dans le jeu de données. A partir de là, vous pourrez concevoir les fonctionnalités, ce qui consiste à créer des fonctionnalités utiles supplémentaires à partir des fonctionnalités brutes existantes dans les données. Vous trouverez ci-dessous un exemple commenté de ce processus.

La fonction `split()` est illustrée ci-dessous. La base de données fournie dans l’argument sera partagée entre les variables `train` et `val` à renvoyer.

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### Évaluation du modèle formé  {#evaluate-the-trained-model}

La fonction `evaluate()` est exécutée après la formation du modèle et renvoie une mesure pour indiquer le degré de réussite du modèle. La fonction `evaluate()` utilise les étiquettes des jeux de données de test et le modèle formé pour prédire un ensemble de fonctionnalités. Ces valeurs prédites sont ensuite comparées aux fonctionnalités réelles du jeu de données de test. Voici quelques-uns des algorithmes de notation courants :
- [Pourcentage d’erreur absolue moyen (MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [Erreur absolue moyenne (MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [Racine carrée de l’erreur quadratique moyenne (RMSE)](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


La fonction `evaluate()` de l’échantillon de ventes au détail est illustrée ci-dessous :

```PYTHON
def evaluate(self, data=[], model={}, configProperties={}):
    print ("Evaluation evaluate triggered")
    val = data.drop('weeklySalesAhead', axis=1)
    y_pred = model.predict(val)
    y_actual = data['weeklySalesAhead'].values
    mape = np.mean(np.abs((y_actual - y_pred) / y_actual))
    mae = np.mean(np.abs(y_actual - y_pred))
    rmse = np.sqrt(np.mean((y_actual - y_pred) ** 2))

    metric = [{"name": "MAPE", "value": mape, "valueType": "double"},
                {"name": "MAE", "value": mae, "valueType": "double"},
                {"name": "RMSE", "value": rmse, "valueType": "double"}]

    return metric
```

Vous remarquerez que la fonction renvoie un objet `metric` contenant un tableau de mesures d’évaluation. Ces mesures serviront à évaluer les performances du modèle formé.

### Fichier Data Saver  {#data-saver-file}

Le fichier `datasaver.py` contient la fonction `save()` qui enregistre votre prédiction lors du test de notation. La fonction `save()` prend votre prédiction et utilise les API [!DNL Experience Platform Catalog], écrivez les données dans le `scoringResultsDataSetId` fichier `scoring.conf` que vous avez spécifié dans votre fichier .

L’exemple utilisé dans l’échantillon de recette des ventes au détail est illustré ici. Vous remarquez l’utilisation de la bibliothèque `DataSetWriter` pour écrire des données vers Platform :

```PYTHON
from data_access_sdk_python.writer import DataSetWriter

def save(configProperties, prediction):
    print("Datasaver Start")
    print("Setting up Writer")

    catalog_url = "https://platform.adobe.io/data/foundation/catalog"
    ingestion_url = "https://platform.adobe.io/data/foundation/import"

    writer = DataSetWriter(catalog_url=catalog_url,
                           ingestion_url=ingestion_url,
                           client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    print("Writer Configured")

    writer.write(data_set_id=configProperties['scoringResultsDataSetId'],
                 dataframe=prediction,
                 ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])

    print("Write Done")
    print("Datasaver Finish")
    print(prediction)
```

## Formation et notation  {#training-and-scoring}

Lorsque vous avez terminé de modifier votre notebook et que vous souhaitez former votre recette, vous pouvez cliquer sur les boutons associés en haut de la barre pour créer une session de formation dans la cellule. Lorsque vous cliquez sur le bouton, un journal des commandes et des sorties issues du script de formation s’affichera dans le notebook (sous la cellule `evaluator.py`). Conda installe d’abord toutes les dépendances, puis la formation commence.

Remarque : vous devez exécuter la formation au moins une fois avant de pouvoir exécuter la notation. En cliquant sur le bouton **[!UICONTROL Exécuter la notation]**, vous obtiendrez la notation du modèle formé généré pendant la formation. Le script de notation apparaîtra sous `datasaver.py`.

À des fins de débogage, si vous souhaitez afficher la sortie masquée, ajoutez `debug` à la fin de la cellule de sortie et exécutez-la de nouveau.

## Création d’une recette  {#create-recipe}

Lorsque vous avez terminé de modifier la recette et que vous êtes satisfait de la sortie formation/score, vous pouvez créer une recette à partir du bloc-notes en appuyant sur **[!UICONTROL Créer une recette]** dans la barre de navigation supérieure droite.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Après avoir appuyé sur le bouton, vous êtes invité à saisir un nom de recette. Ce nom représente la recette réelle créée sur [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Une fois que vous avez appuyé sur **[!UICONTROL OK]**, vous pourrez accéder à la nouvelle recette dans [Adobe Experience Platform](https://platform.adobe.com/). Vous pouvez cliquer sur le bouton **[!UICONTROL Voir les recettes]** pour accéder à l’onglet **[!UICONTROL Recettes]** sous **[!UICONTROL Modèles ML]**.

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

Voici l’aspect de la recette une fois le processus terminé :

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
>
> - Ne supprimer aucune cellule de fichier
> - Ne pas modifier la ligne `%%writefile` en haut des cellules de fichier
> - Ne pas créer plusieurs recettes dans différents cahiers simultanément


## Étapes suivantes  {#next-steps}

En terminant ce tutoriel, vous avez appris à créer un modèle d’apprentissage automatique dans le notebook Recipe Builder. Vous avez également appris à utiliser le notebook pour recevoir le workflow dans le notebook afin de créer une recette dans [!DNL Data Science Workspace].

Pour continuer à apprendre à utiliser les ressources dans [!DNL Data Science Workspace], veuillez visiter la liste déroulante [!DNL Data Science Workspace] recettes et modèles.

## Ressources supplémentaires {#additional-resources}

La vidéo suivante est conçue pour vous aider à comprendre comment créer et déployer des modèles.

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)


