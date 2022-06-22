---
keywords: Experience Platform;JupyterLab;recette;notebooks;Data Science Workspace;rubriques les plus consultées;créer une recette
solution: Experience Platform
title: Création d’un modèle à l’aide de notebooks JupyterLab
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel vous guide tout au long des étapes requises pour créer une recette à l’aide du modèle de créateur de recettes des notebooks JupyterLab.
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
source-git-commit: b4dabd36f54cc571b78a6c6c9535f9f08c403b64
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 34%

---

# Création d’un modèle à l’aide de notebooks JupyterLab

Ce tutoriel vous guide tout au long des étapes requises pour créer un modèle à l’aide du modèle de créateur de recettes de notebooks JupyterLab.

## Concepts présentés :

- **Recettes :** Une recette est le terme utilisé par l’Adobe pour désigner une spécification de modèle. Il s’agit d’un conteneur de niveau supérieur qui représente un apprentissage automatique spécifique, un algorithme d’intelligence artificielle ou un ensemble d’algorithmes, une logique de traitement et la configuration nécessaires pour créer et exécuter un modèle formé.
- **Modèle :** un modèle est une instance d’une recette d’apprentissage automatique formée à l’aide de données historiques et de configurations dans le but de résoudre un cas d’usage commercial.
- **Formation :** la formation est le processus de formation de modèles et de connaissances à partir de données étiquetées.
- **Notation :** la notation est le processus de génération d’informations à partir de données en utilisant un modèle formé.

## Téléchargement des ressources requises {#assets}

Avant de poursuivre ce tutoriel, vous devez créer les schémas et les jeux de données requis. Consultez le tutoriel pour [création de schémas et de jeux de données de modèle de propension Luma](../models-recipes/create-luma-data.md) pour télécharger les ressources requises et configurer les conditions préalables requises.

## Prise en main de la fonction [!DNL JupyterLab] environnement de notebook

La création d’une recette à partir de zéro peut être effectuée dans [!DNL Data Science Workspace]. Pour commencer, accédez à [Adobe Experience Platform](https://platform.adobe.com) et sélectionnez la variable **[!UICONTROL Notebooks]** de gauche. Pour créer un nouveau notebook, sélectionnez le modèle Recipe Builder dans le [!DNL JupyterLab Launcher].

Le [!UICONTROL Créateur de recettes] notebook vous permet d’exécuter des opérations de formation et de notation dans le notebook. Vous avez ainsi la possibilité d’apporter des modifications à leurs méthodes de `train()` et de `score()` entre deux expériences en cours d’exécution sur les données de formation et de notation. Une fois que vous êtes satisfait des résultats de la formation et de la notation, vous pouvez créer une recette et la publier en outre en tant que modèle à l’aide de la fonctionnalité de modèle de la recette.

>[!NOTE]
>
>Le [!UICONTROL Créateur de recettes] Le notebook prend en charge l’utilisation de tous les formats de fichier, mais la fonctionnalité de création de recette ne prend actuellement en charge que l’utilisation de [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder-new.png)

Lorsque vous sélectionnez la variable [!UICONTROL Créateur de recettes] depuis le lanceur, le notebook est ouvert dans un nouvel onglet.

Dans le nouvel onglet du notebook situé en haut, une barre d’outils se charge et contient trois actions supplémentaires : **[!UICONTROL Train]**, **[!UICONTROL Score]**, et **[!UICONTROL Créer une recette]**. Ces icônes s’affichent uniquement dans la [!UICONTROL Créateur de recettes] notebook. Des informations supplémentaires sur ces actions sont fournies [dans la section formation et notation](#training-and-scoring) après avoir créé votre recette dans le notebook.

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Prise en main de la fonction [!UICONTROL Créateur de recettes] notebook

Dans le dossier des ressources fournies, il existe un modèle de propension Luma. `propensity_model.ipynb`. À l’aide de l’option de chargement de notebook dans JupyterLab, chargez le modèle fourni et ouvrez le notebook.

![charger un notebook](../images/jupyterlab/create-recipe/upload_notebook.png)

Le reste de ce tutoriel couvre les fichiers suivants prédéfinis dans le notebook du modèle de propension :

- [Fichier des exigences](#requirements-file)
- [Fichiers de configuration](#configuration-files)
- [Chargeur de données d’apprentissage](#training-data-loader)
- [Chargeur de données de notation](#scoring-data-loader)
- [Fichier Pipeline](#pipeline-file)
- [Fichier Evaluator](#evaluator-file)
- [Fichier Data Saver](#data-saver-file)

Le tutoriel vidéo suivant explique le notebook du modèle de propension Luma :

>[!VIDEO](https://video.tv.adobe.com/v/333570)

### Fichier des exigences {#requirements-file}

Le fichier des exigences est utilisé pour déclarer les bibliothèques supplémentaires que vous souhaitez utiliser dans le modèle. En cas de dépendance, vous pouvez spécifier le numéro de version. Pour rechercher d’autres bibliothèques, rendez-vous sur la page [anaconda.org](https://anaconda.org). Pour savoir comment formater le fichier des exigences, consultez la page [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). Voici une liste non exhaustive des principales bibliothèques déjà utilisées :

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>Les bibliothèques ou versions spécifiques que vous ajoutez peuvent être incompatibles avec les bibliothèques mentionnées ci-dessus. En outre, si vous choisissez de créer manuellement un fichier d’environnement, la variable `name` n’est pas autorisé à être remplacé.

Pour le notebook de modèle de propension Luma, les exigences n’ont pas besoin d’être mises à jour.

### Fichiers de configuration {#configuration-files}

Les fichiers de configuration, `training.conf` et `scoring.conf`, servent à spécifier les jeux de données que vous souhaitez utiliser pour la formation et la notation, et à ajouter des hyperparamètres. Les configurations pour la formation et la notation sont distinctes.

Pour qu’un modèle puisse exécuter une formation, vous devez fournir la variable `trainingDataSetId`, `ACP_DSW_TRAINING_XDM_SCHEMA`, et `tenantId`. En outre, pour la notation, vous devez fournir la variable `scoringDataSetId`, `tenantId`, et `scoringResultsDataSetId `.

Pour trouver le jeu de données et les identifiants de schéma, accédez à l’onglet données . ![Onglet Données](../images/jupyterlab/create-recipe/dataset-tab.png) dans les notebooks sur la barre de navigation de gauche (sous l’icône de dossier). Trois identifiants de jeu de données différents doivent être fournis. Le `scoringResultsDataSetId` est utilisé pour stocker les résultats de notation du modèle et doit être un jeu de données vide. Ces jeux de données ont été créés précédemment dans la variable [Ressources requises](#assets) étape .

![](../images/jupyterlab/create-recipe/dataset_tab.png)

Vous trouverez les mêmes informations sur [Adobe Experience Platform](https://platform.adobe.com/) sous les onglets **[Schéma](https://platform.adobe.com/schema)** et **[Jeu de données](https://platform.adobe.com/dataset/overview)**.

Une fois que vous êtes en compétition, votre configuration de formation et de notation doit ressembler à la capture d’écran suivante :

![configuration](../images/jupyterlab/create-recipe/config.png)

Par défaut, les paramètres de configuration suivants sont définis pour vous lorsque vous entraînez et notez des données :

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## Présentation du chargeur de données d’apprentissage {#training-data-loader}

Le chargeur de données d’apprentissage est destiné à instancier les données utilisées pour créer le modèle d’apprentissage automatique. En règle générale, le chargeur de données d’apprentissage exécute deux tâches :

- Charger des données depuis [!DNL Platform]
- Préparation des données et ingénierie des fonctionnalités

Les deux prochaines sections traiteront du chargement et de la préparation des données.

### Chargement des données {#loading-data}

Cette étape utilise le [cadre de données pandas](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). Les données peuvent être chargées à partir de fichiers dans [!DNL Adobe Experience Platform] à l’aide de la fonction [!DNL Platform] SDK (`platform_sdk`), ou provenant de sources externes utilisant pandas&#39; `read_csv()` ou `read_json()` fonctions.

- [[!DNL Platform SDK]](#platform-sdk)
- [Sources externes](#external-sources)

>[!NOTE]
>
> Dans le notebook Recipe Builder, les données sont chargées via le chargeur de données `platform_sdk`.

### [!DNL Platform] SDK {#platform-sdk}

Pour un tutoriel détaillé sur l’utilisation du chargeur de données `platform_sdk`, consultez le [guide SDK Platform](../authoring/platform-sdk.md). Ce tutoriel fournit des informations sur l’authentification de création, la lecture et l’écriture basiques de données.

### Sources externes {#external-sources}

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

## Fichier de chargeur de données d’apprentissage

Dans cet exemple, les données sont chargées à l’aide du SDK Platform. La bibliothèque peut être importée en haut de la page en incluant la ligne :

`from platform_sdk.dataset_reader import DatasetReader`

Vous pouvez ensuite utiliser la variable `load()` pour récupérer le jeu de données d’apprentissage à partir de la méthode `trainingDataSetId` comme défini dans la configuration (`recipe.conf`).

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    dataset_reader = DatasetReader(client_context, dataset_id=config_properties['trainingDataSetId'])
```

>[!NOTE]
>
>Comme indiqué dans la section [Section Fichier de configuration](#configuration-files), les paramètres de configuration suivants sont définis pour vous lorsque vous accédez aux données d’Experience Platform à l’aide de `client_context = get_client_context(config_properties)`:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


Maintenant que vous disposez de vos données, vous pouvez commencer leur préparation ainsi que la conception des fonctionnalités.

### Préparation des données et ingénierie des fonctionnalités {#data-preparation-and-feature-engineering}

Une fois les données chargées, elles doivent être nettoyées et préparées. Dans cet exemple, l’objectif du modèle est de prédire si un client va commander un produit ou non. Étant donné que le modèle ne tient pas compte de produits spécifiques, vous n’avez pas besoin de `productListItems` et, par conséquent, la colonne est supprimée. Ensuite, des colonnes supplémentaires sont ignorées, qui ne contiennent qu’une ou deux valeurs dans une seule colonne. Lors de la formation d’un modèle, il est important de ne conserver que des données utiles qui aideront à prédire votre objectif.

![exemple de préparation de données](../images/jupyterlab/create-recipe/data_prep.png)

Une fois que vous avez supprimé les données inutiles, vous pouvez commencer la conception des fonctionnalités. Les données de démonstration utilisées pour cet exemple ne contiennent aucune information de session. Normalement, vous souhaitez obtenir des données sur les sessions en cours et passées pour un client particulier. En raison de l’absence d’informations sur les sessions, cet exemple reproduit les sessions en cours et passées par le biais de la démarcation des parcours.

![démarcation des parcours](../images/jupyterlab/create-recipe/journey_demarcation.png)

Une fois la démarcation terminée, les données sont étiquetées et un parcours est créé.

![étiqueter les données](../images/jupyterlab/create-recipe/label_data.png)

Ensuite, les fonctionnalités sont créées et divisées entre le passé et le présent. Ensuite, toutes les colonnes inutiles sont ignorées, ce qui vous laisse avec les parcours passés et actuels pour les clients Luma. Ces parcours contiennent des informations, telles que si un client a acheté un article et le parcours qu’il a pris avant l’achat.

![formation actuelle finale](../images/jupyterlab/create-recipe/final_journey.png)

## Chargeur de données de notation {#scoring-data-loader}

La procédure de chargement des données pour la notation est similaire au chargement des données de formation. En regardant attentivement le code, vous pouvez voir que tout est identique, à l’exception de la fonction `scoringDataSetId` dans le `dataset_reader`. En effet, la même source de données Luma est utilisée pour la formation et la notation.

Si vous souhaitez utiliser différents fichiers de données pour la formation et la notation, le chargeur de données de formation et de notation est distinct. Cela vous permet d’effectuer un pré-traitement supplémentaire, par exemple de mapper vos données de formation à vos données de notation si nécessaire.

## Fichier Pipeline {#pipeline-file}

Le fichier `pipeline.py` inclut la logique de formation et de notation.

L’objectif de la formation est de créer un modèle à l’aide des fonctionnalités et des étiquettes présentes dans votre jeu de données d’apprentissage. Après avoir choisi votre modèle de formation, vous devez adapter votre jeu de données de formation x et y au modèle, et la fonction renvoie le modèle formé.

>[!NOTE]
> 
>Les Fonctionnalités font référence à la variable d’entrée utilisée par le modèle d’apprentissage automatique pour prédire les étiquettes.

![train def](../images/jupyterlab/create-recipe/def_train.png)

La fonction `score()` doit contenir l’algorithme de notation et renvoyer une mesure pour indiquer le degré de réussite du modèle. La fonction `score()` utilise les étiquettes des jeux de données de notation et le modèle formé pour générer un ensemble de fonctionnalités prédites. Ces valeurs prédites sont ensuite comparées aux fonctionnalités réelles du jeu de données de notation. Dans cet exemple, la fonction `score()` utilise le modèle formé pour prédire les fonctionnalités à l’aide des étiquettes du jeu de données de notation. Les fonctionnalités prédites sont renvoyées.

![score def](../images/jupyterlab/create-recipe/def_score.png)

## Fichier Evaluator {#evaluator-file}

Le fichier `evaluator.py` contient la logique de la manière dont vous souhaitez évaluer votre recette formée ainsi que la manière dont vos données d’apprentissage doivent être fractionnées.

### Fractionnement du jeu de données {#split-the-dataset}

La phase de préparation des données pour la formation nécessite de fractionner le jeu de données à utiliser pour la formation et les tests. Ceci `val` Les données sont utilisées implicitement pour évaluer le modèle après sa formation. Il s’agit d’un processus distinct de celui de notation.

Cette section présente les `split()` qui charge des données dans le notebook, puis nettoie les données en supprimant les colonnes non liées dans le jeu de données. De là, vous pouvez concevoir des fonctionnalités, ce qui est le processus de création de fonctionnalités pertinentes supplémentaires à partir des fonctionnalités brutes existantes dans les données.

![Fonction de division](../images/jupyterlab/create-recipe/split.png)

### Évaluation du modèle formé {#evaluate-the-trained-model}

Le `evaluate()` est exécutée après la formation du modèle et renvoie une mesure pour indiquer le degré de réussite du modèle. Le `evaluate()` utilise les étiquettes des jeux de données de test et le modèle formé pour prédire un ensemble de fonctionnalités. Ces valeurs prédites sont ensuite comparées aux fonctionnalités réelles du jeu de données de test. Dans cet exemple, les mesures utilisées sont les suivantes : `precision`, `recall`, `f1`, et `accuracy`. Vous remarquerez que la fonction renvoie un objet `metric` contenant un tableau de mesures d’évaluation. Ces mesures sont utilisées pour évaluer les performances du modèle formé.

![evaluate](../images/jupyterlab/create-recipe/evaluate.png)

Ajouter `print(metric)` vous permet d’afficher les résultats de la mesure.

![résultats des mesures](../images/jupyterlab/create-recipe/evaluate_metric.png)

## Fichier Data Saver {#data-saver-file}

Le `datasaver.py` contient le fichier `save()` et est utilisée pour enregistrer votre prédiction lors du test de notation. Le `save()` utilise votre prédiction et [!DNL Experience Platform Catalog] Les API écrivent les données dans la variable `scoringResultsDataSetId` que vous avez spécifié dans votre `scoring.conf` fichier . Vous pouvez

![Enregistreur de données](../images/jupyterlab/create-recipe/data_saver.png)

## Formation et notation {#training-and-scoring}

Lorsque vous avez terminé d’apporter des modifications à votre notebook et que vous souhaitez entraîner votre recette, vous pouvez sélectionner les boutons associés en haut de la barre pour créer une session d’entraînement dans la cellule. Lorsque vous cliquez sur le bouton, un journal des commandes et des sorties issues du script de formation s’affiche dans le notebook (sous `evaluator.py` ). Conda installe d’abord toutes les dépendances, puis la formation commence.

Remarque : vous devez exécuter la formation au moins une fois avant de pouvoir exécuter la notation. En sélectionnant le **[!UICONTROL Exécuter la notation]** noter le modèle formé généré pendant la formation. Le script de notation apparaît sous `datasaver.py`.

À des fins de débogage, si vous souhaitez afficher la sortie masquée, ajoutez `debug` à la fin de la cellule de sortie et exécutez-la de nouveau.

![formation et score](../images/jupyterlab/create-recipe/toolbar_actions.png)

## Création d’une recette {#create-recipe}

Lorsque vous avez terminé de modifier la recette et que vous êtes satisfait du résultat de formation/notation, vous pouvez créer une recette à partir du notebook en sélectionnant **[!UICONTROL Créer une recette]** en haut à droite.

![](../images/jupyterlab/create-recipe/create-recipe.png)

Après avoir sélectionné **[!UICONTROL Créer une recette]**, vous êtes invité à saisir un nom de recette. Ce nom représente la recette réelle créée sur [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

Une fois que vous avez sélectionné **[!UICONTROL Ok]**, le processus de création de la recette commence. Cela peut prendre du temps et une barre de progression s’affiche à la place du bouton Créer une recette . Une fois l’opération terminée, vous pouvez sélectionner la variable **[!UICONTROL Afficher les recettes]** pour accéder au **[!UICONTROL Recettes]** sous **[!UICONTROL Modèles ML]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

>[!CAUTION]
>
> - Ne supprimer aucune cellule de fichier
> - Ne pas modifier la ligne `%%writefile` en haut des cellules de fichier
> - Ne pas créer plusieurs recettes dans différents cahiers simultanément


## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez appris à créer un modèle d’apprentissage automatique dans le [!UICONTROL Créateur de recettes] notebook. Vous avez également appris à utiliser le notebook pour le workflow de recette.

Pour continuer à apprendre à utiliser les ressources dans [!DNL Data Science Workspace], rendez-vous sur la page [!DNL Data Science Workspace] menu déroulant recettes et modèles.