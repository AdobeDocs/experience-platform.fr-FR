---
keywords: Experience Platform;tutoriel;pipeline de fonctionnalités;Data Science Workspace;rubriques populaires
title: Création d’un pipeline de fonctionnalités à l’aide du SDK de création de modèles
type: Tutorial
description: Adobe Experience Platform vous permet de créer et de créer des pipelines de fonctionnalités personnalisés pour réaliser l’ingénierie de fonctionnalités à grande échelle via Sensei Machine Learning Framework Runtime. Ce document décrit les différentes classes trouvées dans un pipeline de fonctionnalités et fournit un tutoriel détaillé sur la création d’un pipeline de fonctionnalités personnalisé à l’aide du SDK Model Authoring dans PySpark.
exl-id: c2c821d5-7bfb-4667-ace9-9566e6754f98
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 28%

---

# Création d’un pipeline de fonctionnalités à l’aide du SDK Model Authoring

>[!IMPORTANT]
>
> Les pipelines de fonctionnalités ne sont actuellement disponibles que par le biais de l’API.

Adobe Experience Platform vous permet de créer et de créer des pipelines de fonctionnalités personnalisés pour réaliser l’ingénierie de fonctionnalités à grande échelle via Sensei Machine Learning Framework Runtime (ci-après appelée &quot;Runtime&quot;).

Ce document décrit les différentes classes trouvées dans un pipeline de fonctionnalités et fournit un tutoriel détaillé sur la création d’un pipeline de fonctionnalités personnalisé à l’aide du [SDK de création de modèles](./sdk.md) dans PySpark.

Le workflow suivant se produit lorsqu’un pipeline de fonctionnalités est exécuté :

1. La recette charge le jeu de données sur un pipeline.
2. La transformation des fonctionnalités est effectuée sur le jeu de données et réécrite dans Adobe Experience Platform.
3. Les données transformées sont chargées pour la formation.
4. Le pipeline de fonctionnalités définit les scènes avec le régresseur d’amplification en dégradé comme modèle sélectionné.
5. Le pipeline est utilisé pour correspondre aux données d’entraînement et le modèle formé est créé.
6. Le modèle est transformé avec le jeu de données de notation.
7. Les colonnes intéressantes de la sortie sont ensuite sélectionnées et réenregistrées dans [!DNL Experience Platform] avec les données associées.

## Commencer

Pour exécuter une recette dans n’importe quelle organisation, les éléments suivants sont requis :
- Jeu de données d’entrée.
- Schéma du jeu de données.
- Un schéma transformé et un jeu de données vide basé sur ce schéma.
- Un schéma de sortie et un jeu de données vide basé sur ce schéma.

Tous les jeux de données ci-dessus doivent être chargés dans l’interface utilisateur de [!DNL Platform]. Pour configurer ce paramètre, utilisez le [script de bootstrap](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap) fourni par l’Adobe.

## Classes de pipeline de fonctionnalités

Le tableau suivant décrit les principales classes abstraites que vous devez étendre pour créer un pipeline de fonctionnalités :

| Classe abstraite | Description |
| -------------- | ----------- |
| DataLoader | Une classe DataLoader fournit une implémentation pour l’extraction de données d’entrée. |
| DatasetTransformer | Une classe DatasetTransformer fournit des implémentations pour transformer le jeu de données d’entrée. Vous pouvez choisir de ne pas fournir une classe DatasetTransformer et mettre en œuvre votre logique de conception des fonctionnalités au sein de la classe FeaturePipelineFactory à la place. |
| FeaturePipelineFactory | Une classe FeaturePipelineFactory crée un pipeline Spark qui consiste en une série de Spark Transformers pour réaliser la conception des fonctionnalités. Vous pouvez choisir de ne pas fournir une classe FeaturePipelineFactory et mettre en œuvre votre logique de conception des fonctionnalités au sein de la classe DatasetTransformer à la place. |
| DataSaver | Une classe DataSaver fournit la logique de stockage d’un jeu de données de fonctionnalités. |

Lorsqu’une tâche de pipeline de fonctionnalités est lancée, le Runtime exécute d’abord le DataLoader pour charger les données d’entrée sous la forme d’un DataFrame, puis modifie le DataFrame en exécutant les fonctions DatasetTransformer, FeaturePipelineFactory ou les deux. Enfin, le jeu de données de fonctionnalités obtenu est conservé dans le DataSaver.

L’organigramme suivant montre l’ordre d’exécution du Runtime :

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Mise en œuvre de vos classes de pipeline de fonctionnalités {#implement-your-feature-pipeline-classes}

Les sections suivantes fournissent des détails et des exemples sur la mise en œuvre des classes obligatoires pour un pipeline de fonctionnalités.

### Définition de variables dans le fichier de configuration JSON {#define-variables-in-the-configuration-json-file}

Le fichier JSON de configuration se compose de paires clé-valeur et est conçu pour que vous puissiez préciser des variables à définir plus tard pendant l’exécution. Ces paires clé-valeur peuvent définir des propriétés telles que l’emplacement des jeux de données d’entrée, l’identifiant du jeu de données de sortie, l’identifiant du client, des en-têtes de colonne, etc.

L’exemple suivant illustre les paires clé-valeur trouvées dans un fichier de configuration :

**Exemple de configuration JSON**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "dataset_id",
                "value": "000"
            },
            {
                "key": "featureDatasetId",
                "value": "111"
            },
            {
                "key": "tenantId",
                "value": "_tenantid"
            }
        ]
    }
]
```

Vous pouvez accéder à la configuration JSON à l’aide de n’importe quelle méthode de classe qui définit `config_properties` comme paramètre. Par exemple :

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

Pour obtenir un exemple de configuration plus détaillé, reportez-vous au fichier [pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) fourni par Data Science Workspace.

### Préparation des données d’entrée avec DataLoader {#prepare-the-input-data-with-dataloader}

DataLoader est responsable de la récupération et du filtrage des données d’entrée. Votre mise en œuvre de DataLoader doit étendre la classe abstraite `DataLoader` et remplacer la méthode abstraite `load`.

L’exemple suivant récupère un jeu de données [!DNL Platform] par identifiant et le renvoie sous la forme d’un DataFrame, où l’identifiant du jeu de données (`dataset_id`) est une propriété définie dans le fichier de configuration.

**Exemple PySpark**

```python
# PySpark

from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
import logging

class MyDataLoader(DataLoader):
    def load_dataset(config_properties, spark, tenant_id, dataset_id):
    PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
    PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

    service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
    user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
    org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
    api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

    dataset_id = str(config_properties.get(dataset_id))

    for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
        if eval(arg) == 'None':
            raise ValueError("%s is empty" % arg)

    query_options = get_query_options(spark.sparkContext)

    pd = spark.read.format(PLATFORM_SDK_PQS_PACKAGE) \
        .option(query_options.userToken(), user_token) \
        .option(query_options.serviceToken(), service_token) \
        .option(query_options.imsOrg(), org_id) \
        .option(query_options.apiKey(), api_key) \
        .option(query_options.mode(), PLATFORM_SDK_PQS_INTERACTIVE) \
        .option(query_options.datasetId(), dataset_id) \
        .load()
    pd.show()

    # Get the distinct values of the dataframe
    pd = pd.distinct()

    # Flatten the data
    if tenant_id in pd.columns:
        pd = pd.select(col(tenant_id + ".*"))

    return pd
```

### Transformation d’un jeu de données à l’aide de DatasetTransformer {#transform-a-dataset-with-datasettransformer}

Un DatasetTransformer fournit la logique de transformation d’un DataFrame d’entrée et renvoie un nouveau DataFrame dérivé. Cette classe peut être mise en œuvre de manière à travailler soit en coopération avec une FeaturePipelineFactory, soit comme composant d d’ingénierie de fonctionnalité unique. Vous pouvez également choisir de ne pas mettre en œuvre cette classe.

L’exemple suivant étend la classe DatasetTransformer :

**Exemple PySpark**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer
from pyspark.ml.feature import StringIndexer
from pyspark.sql.types import IntegerType
from pyspark.sql.functions import unix_timestamp, from_unixtime, to_date, lit, lag, udf, date_format, lower, col, split, explode
from pyspark.sql import Window
from .helper import setupLogger

class MyDatasetTransformer(DatasetTransformer):
    logger = setupLogger(__name__)

    def transform(self, config_properties, dataset):
        tenant_id = str(config_properties.get("tenantId"))

        # Flatten the data
        if tenant_id in dataset.columns:
            self.logger.info("Flatten the data before transformation")
            dataset = dataset.select(col(tenant_id + ".*"))
            dataset.show()

        # Convert isHoliday boolean value to Int
        # Rename the column to holiday and drop isHoliday
        pd = dataset.withColumn("holiday", col("isHoliday").cast(IntegerType())).drop("isHoliday")
        pd.show()

        # Get the week and year from date
        pd = pd.withColumn("week", date_format(to_date("date", "MM/dd/yy"), "w").cast(IntegerType()))
        pd = pd.withColumn("year", date_format(to_date("date", "MM/dd/yy"), "Y").cast(IntegerType()))

        # Convert the date to TimestampType
        pd = pd.withColumn("date", to_date(unix_timestamp(pd["date"], "MM/dd/yy").cast("timestamp")))

        # Convert categorical data
        indexer = StringIndexer(inputCol="storeType", outputCol="storeTypeIndex")
        pd = indexer.fit(pd).transform(pd)

        # Get the WeeklySalesAhead and WeeklySalesLag column values
        window = Window.orderBy("date").partitionBy("store")
        pd = pd.withColumn("weeklySalesLag", lag("weeklySales", 1).over(window)).na.drop(subset=["weeklySalesLag"])
        pd = pd.withColumn("weeklySalesAhead", lag("weeklySales", -1).over(window)).na.drop(subset=["weeklySalesAhead"])
        pd = pd.withColumn("weeklySalesScaled", lag("weeklySalesAhead", -1).over(window)).na.drop(subset=["weeklySalesScaled"])
        pd = pd.withColumn("weeklySalesDiff", (pd['weeklySales'] - pd['weeklySalesLag'])/pd['weeklySalesLag'])

        pd = pd.na.drop()
        self.logger.debug("Transformed dataset count is %s " % pd.count())

        # return transformed dataframe
        return pd
```

### Conception de fonctionnalités de données avec FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

Une FeaturePipelineFactory vous permet de mettre en œuvre votre logique d’ingénierie de fonctionnalités en définissant et en associant une série de Spark Transformers à travers un pipeline Spark. Cette classe peut être mise en œuvre de manière à travailler soit en coopération avec un DatasetTransformer, soit comme composant d’ingénierie de fonctionnalité unique. Vous pouvez également choisir de ne pas mettre en œuvre cette classe.

L’exemple suivant étend la classe FeaturePipelineFactory :

**Exemple PySpark**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.regression import GBTRegressor
from pyspark.ml.feature import VectorAssembler

import numpy as np

from sdk.pipeline_factory import PipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def apply(self, config_properties):
        if config_properties is None:
            raise ValueError("config_properties parameter is null")

        tenant_id = str(config_properties.get("tenantId"))
        input_features = str(config_properties.get("ACP_DSW_INPUT_FEATURES"))

        if input_features is None:
            raise ValueError("input_features parameter is null")
        if input_features.startswith(tenant_id):
            input_features = input_features.replace(tenant_id + ".", "")

        learning_rate = float(config_properties.get("learning_rate"))
        n_estimators = int(config_properties.get("n_estimators"))
        max_depth = int(config_properties.get("max_depth"))

        feature_list = list(input_features.split(","))
        feature_list.remove("date")
        feature_list.remove("storeType")

        cols = np.array(feature_list)

        # Gradient-boosted tree estimator
        gbt = GBTRegressor(featuresCol='features', labelCol='weeklySalesAhead', predictionCol='prediction',
                       maxDepth=max_depth, maxBins=n_estimators, stepSize=learning_rate)

        # Assemble the fields to a vector
        assembler = VectorAssembler(inputCols=cols, outputCol="features")

        # Construct the pipeline
        pipeline = Pipeline(stages=[assembler, gbt])

        return pipeline

    def train(self, config_properties, dataframe):
        pass

    def score(self, config_properties, dataframe, model):
        pass

    def getParamMap(self, config_properties, sparkSession):
        return None
```

### Stockage du jeu de données de votre fonctionnalité avec DataSaver {#store-your-feature-dataset-with-datasaver}

DataSaver est responsable du stockage des jeux de données de fonctionnalités obtenus dans un emplacement de stockage. Votre mise en œuvre de DataSaver doit étendre la classe abstraite `DataSaver` et remplacer la méthode abstraite `save`.

L’exemple suivant étend la classe DataSaver qui stocke les données dans un jeu de données [!DNL Platform] par identifiant, où l’identifiant du jeu de données (`featureDatasetId`) et l’identifiant du client (`tenantId`) sont des propriétés définies dans la configuration.

**Exemple PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct


class MyDataSaver(DataSaver):
    def save(self, configProperties, data_feature):

        # Spark context
        sparkContext = data_features._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if data_features is None:
            raise ValueError("data_features parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("featureDatasetId"))
        tenant_id = str(
            configProperties.get("tenantId"))
        service_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['output_dataset_id', 'tenant_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # create and prepare DataFrame with valid columns
        output_df = data_features.withColumn("date", col("date").cast(StringType()))
        output_df = output_df.withColumn(tenant_id, struct(col("date"), col("store"), col("features")))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        # store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp") \
            .write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```


### Précision des noms de classe mis en œuvre dans le fichier d’application {#specify-your-implemented-class-names-in-the-application-file}

Maintenant que vos classes de pipeline de fonctionnalités sont définies et implémentées, vous devez spécifier les noms de vos classes dans le fichier YAML de l’application.

Les exemples suivants spécifient les noms de classe implémentés :

**Exemple PySpark**

```yaml
#Name of the class which contains implementation to get the input data.
feature.dataLoader: InputDataLoaderForFeaturePipeline

#Name of the class which contains implementation to get the transformed data.
feature.dataset.transformer: MyDatasetTransformer

#Name of the class which contains implementation to save the transformed data.
feature.dataSaver: DatasetSaverForTransformedData

#Name of the class which contains implementation to get the training data
training.dataLoader: TrainingDataLoader

#Name of the class which contains pipeline. It should implement PipelineFactory.scala
pipeline.class: TrainPipeline

#Name of the class which contains implementation for evaluation metrics.
evaluator: Evaluator
evaluateModel: True

#Name of the class which contains implementation to get the scoring data.
scoring.dataLoader: ScoringDataLoader

#Name of the class which contains implementation to save the scoring data.
scoring.dataSaver: MyDatasetSaver
```

## Création de votre moteur de pipeline de fonctionnalités à l’aide de l’API {#create-feature-pipeline-engine-api}

Maintenant que vous avez créé votre pipeline de fonctionnalités, vous devez créer une image Docker pour effectuer un appel aux points de terminaison du pipeline de fonctionnalités dans l’API [!DNL Sensei Machine Learning]. Vous avez besoin d’une URL d’image Docker pour effectuer un appel vers les points de terminaison du pipeline de fonctionnalités.

>[!TIP]
>
>Si vous ne disposez pas d’une URL Docker, consultez le tutoriel [Former une recette empaquetée à partir de fichiers source](../models-recipes/package-source-files-recipe.md) pour une présentation détaillée de la création d’une URL d’hôte Docker.

Vous pouvez également utiliser la collection Postman suivante pour faciliter l’exécution du processus d’API du pipeline de fonctionnalités :

https://www.postman.com/collections/c5fc0d1d5805a5ddd41a

### Création d’un moteur de pipeline de fonctionnalités {#create-engine-api}

Une fois que vous disposez de l’emplacement de votre image Docker, vous pouvez [créer un moteur de pipeline de fonctionnalités](../api/engines.md#feature-pipeline-docker) à l’aide de l’API [!DNL Sensei Machine Learning] en exécutant un POST vers `/engines`. La création réussie d’un moteur de pipeline de fonctionnalités vous fournit un identifiant unique de moteur (`id`). Veillez à enregistrer cette valeur avant de continuer.

### Création d’une instance MLInstance {#create-mlinstance}

En utilisant le `engineID` que vous venez de créer, vous devez [créer une instance MLIstance](../api/mlinstances.md#create-an-mlinstance) en effectuant une requête de POST sur le point de terminaison `/mlInstance`. Une réponse réussie renvoie un payload contenant les détails de l’instance MLInstance nouvellement créée, y compris son identifiant unique (`id`) utilisé dans l’appel API suivant.

### Création d’une expérience {#create-experiment}

Ensuite, vous devez [créer une expérience](../api/experiments.md#create-an-experiment). Pour créer une expérience, vous devez disposer de votre identifiant unique MLIstance (`id`) et envoyer une requête de POST au point de terminaison `/experiment`. Une réponse réussie renvoie un payload contenant les détails de l’expérience nouvellement créée, y compris son identifiant unique (`id`) utilisé dans l’appel API suivant.

### Définition de la tâche de pipeline de fonctionnalités d’exécution d’expérience {#specify-feature-pipeline-task}

Après avoir créé une expérience, vous devez modifier le mode de l’expérience en `featurePipeline`. Pour modifier le mode, ajoutez un POST supplémentaire à [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) avec votre `EXPERIMENT_ID` et dans le corps envoyez `{ "mode":"featurePipeline"}` pour spécifier une exécution d’expérience de pipeline de fonctionnalités.

Une fois l’expérience terminée, envoyez une demande de GET à `/experiments/{EXPERIMENT_ID}` pour [récupérer l’état de l’expérience](../api/experiments.md#retrieve-specific) et attendre que l’état de l’expérience soit mis à jour pour se terminer.

### Définition de la tâche de formation d’exécution d’expérience {#training}

Ensuite, vous devez [spécifier la tâche d’exécution de formation](../api/experiments.md#experiment-training-scoring). Créez un POST sur `experiments/{EXPERIMENT_ID}/runs` et dans le corps, définissez le mode sur `train` et envoyez un tableau de tâches contenant vos paramètres de formation. Une réponse réussie renvoie un payload contenant les détails de l’expérience interrogée.

Une fois l’expérience terminée, envoyez une demande de GET à `/experiments/{EXPERIMENT_ID}` pour [récupérer l’état de l’expérience](../api/experiments.md#retrieve-specific) et attendre que l’état de l’expérience soit mis à jour pour se terminer.

### Définition de la tâche de notation d’exécution d’expérience {#scoring}

>[!NOTE]
>
> Pour terminer cette étape, vous devez avoir au moins une opération de formation réussie associée à votre expérience.

Après une opération de formation réussie, vous devez [spécifier la tâche d’exécution de notation](../api/experiments.md#experiment-training-scoring). Créez un POST sur `experiments/{EXPERIMENT_ID}/runs` et dans le corps, définissez l’attribut `mode` sur &quot;score&quot;. Cela permet de lancer l’exécution de votre expérience de notation.

Une fois l’expérience terminée, envoyez une demande de GET à `/experiments/{EXPERIMENT_ID}` pour [récupérer l’état de l’expérience](../api/experiments.md#retrieve-specific) et attendre que l’état de l’expérience soit mis à jour pour se terminer.

Une fois la notation terminée, votre pipeline de fonctionnalités doit être opérationnel.

## Étapes suivantes {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

En lisant ce document, vous avez créé un pipeline de fonctionnalités à l’aide du SDK Model Authoring, créé une image Docker et utilisé l’URL d’image Docker pour créer un modèle de pipeline de fonctionnalités à l’aide de l’API [!DNL Sensei Machine Learning]. Vous êtes maintenant prêt à continuer à transformer des jeux de données et à extraire des fonctionnalités de données à grande échelle à l’aide de [[!DNL Sensei Machine Learning API]](../api/getting-started.md).
