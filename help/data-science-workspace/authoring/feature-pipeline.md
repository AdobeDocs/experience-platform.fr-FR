---
keywords: Experience Platform;Tutorial;feature pipeline;Data Science Workspace;popular topics
solution: Adobe Experience Platform Data Science Workspace
title: Création d’un pipeline de fonctionnalités
topic: Tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 31%

---


# Création d’un pipeline de fonctionnalités

>[!IMPORTANT]
>
> Les pipelines de fonctionnalités ne sont actuellement disponibles que par API.

Adobe Experience Platform vous permet de créer et de créer des pipelines de fonctionnalités personnalisées pour effectuer l&#39;ingénierie de fonctionnalités à l&#39;échelle via le cadre d&#39;apprentissage automatique Sensei (ci-après appelé &quot;Runtime&quot;).

This document describes the various classes found in a feature pipeline, and provides a step-by-step tutorial for creating a custom feature pipeline using the [Model Authoring SDK](./sdk.md) in PySpark.

Le processus suivant se produit lorsqu’un pipeline de fonctionnalités est exécuté :

1. La recette charge le jeu de données dans un pipeline.
2. La transformation des fonctionnalités est effectuée sur le jeu de données et renvoyée à Adobe Experience Platform.
3. Les données transformées sont chargées pour la formation.
4. Le pipeline de fonctionnalités définit les étapes avec le régresseur de poussée en dégradé comme modèle choisi.
5. Le pipeline est utilisé pour adapter les données d&#39;entraînement et le modèle formé est créé.
6. Le modèle est transformé à l’aide du jeu de données de score.
7. Les colonnes intéressantes de la sortie sont ensuite sélectionnées et enregistrées à nouveau [!DNL Experience Platform] avec les données associées.

## Prise en main

Pour exécuter une recette dans n&#39;importe quelle organisation, les éléments suivants sont requis :
- Jeu de données d’entrée.
- Schéma du jeu de données.
- Un schéma transformé et un jeu de données vide basé sur ce schéma.
- Schéma de sortie et jeu de données vide basé sur ce schéma.

Tous les jeux de données ci-dessus doivent être téléchargés dans l’ [!DNL Platform] interface utilisateur. Pour configurer ce paramètre, utilisez le script [](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap)d’amorçage fourni par l’Adobe.

## Classes de pipeline de fonctionnalités

Le tableau suivant décrit les principales classes abstraites que vous devez étendre pour créer un pipeline de fonctionnalités :

| Classe abstraite | Description |
| -------------- | ----------- |
| DataLoader | Une classe DataLoader fournit une implémentation pour l’extraction de données d’entrée. |
| DatasetTransformer | Une classe DatasetTransformer fournit des implémentations pour transformer le jeu de données d’entrée. Vous pouvez choisir de ne pas fournir une classe DatasetTransformer et mettre en œuvre votre logique de conception des fonctionnalités au sein de la classe FeaturePipelineFactory à la place. |
| FeaturePipelineFactory | Une classe FeaturePipelineFactory crée un pipeline Spark qui consiste en une série de Spark Transformers pour réaliser la conception des fonctionnalités. Vous pouvez choisir de ne pas fournir une classe FeaturePipelineFactory et mettre en œuvre votre logique de conception des fonctionnalités au sein de la classe DatasetTransformer à la place. |
| DataSaver | Une classe DataSaver fournit la logique de stockage d’un jeu de données de fonctionnalités. |

Lorsqu’une tâche de pipeline de fonctionnalités est lancée, l’exécution commence par exécuter DataLoader pour charger les données d’entrée sous la forme d’un DataFrame, puis modifie le DataFrame en exécutant DatasetTransformer, FeaturePipelineFactory ou les deux. Enfin, le jeu de données de fonctionnalités obtenu est conservé dans le DataSaver.

L’organigramme suivant montre l’ordre d’exécution du Runtime :

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Mise en œuvre de vos classes de pipeline de fonctionnalités {#implement-your-feature-pipeline-classes}

Les sections suivantes fournissent des détails et des exemples sur la mise en œuvre des classes obligatoires pour un pipeline de fonctionnalités.

### Définition de variables dans le fichier de configuration JSON {#define-variables-in-the-configuration-json-file}

Le fichier JSON de configuration se compose de paires clé-valeur et est conçu pour que vous puissiez préciser des variables à définir plus tard pendant l’exécution. Ces paires clé-valeur peuvent définir des propriétés telles que l’emplacement des jeux de données d’entrée, l’identifiant du jeu de données de sortie, l’identifiant du client, des en-têtes de colonne, etc.

L’exemple suivant montre les paires clé-valeur trouvées au sein d’un fichier de configuration:

**exemple de configuration JSON**

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

Consultez le fichier [pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) fourni par Data Science Workspace pour un exemple de configuration plus détaillé.

### Préparation des données d’entrée avec DataLoader {#prepare-the-input-data-with-dataloader}

DataLoader est responsable de la récupération et du filtrage des données d’entrée. Votre mise en œuvre de DataLoader doit étendre la classe abstraite `DataLoader` et remplacer la méthode abstraite `load`.

The following example retrieves a [!DNL Platform] dataset by ID and returns it as a DataFrame, where the dataset ID (`dataset_id`) is a defined property in the configuration file.

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

L’exemple suivant étend la classe DatasetTransformer:


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

L&#39;exemple suivant étend la classe FeaturePipelineFactory :

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

DataSaver est responsable du stockage des jeux de données de fonctionnalités qui en résultent dans un emplacement d’enregistrement. Votre mise en œuvre de DataSaver doit étendre la classe abstraite `DataSaver` et remplacer la méthode abstraite `save`.

The following example extends the DataSaver class which stores data to a [!DNL Platform] dataset by ID, where the dataset ID (`featureDatasetId`) and tenant ID (`tenantId`) are defined properties in the configuration.

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

Maintenant que vos classes de pipeline de fonctionnalités sont définies et implémentées, vous devez spécifier les noms de vos classes dans le fichier YAML de l&#39;application.

Les exemples suivants précisent les noms des classes implémentés:

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

## Create your feature pipeline Engine using the API {#create-feature-pipeline-engine-api}

Maintenant que vous avez créé votre pipeline de fonctionnalités, vous devez créer une image Docker pour appeler les points de terminaison du pipeline de fonctionnalités dans l&#39; [!DNL Sensei Machine Learning] API. Vous avez besoin d’une URL d’image Docker pour pouvoir appeler les points de terminaison du pipeline de fonctionnalités.

>[!TIP]
>
>Si vous n&#39;avez pas d&#39;URL Docker, consultez les fichiers source du [package dans un didacticiel de recette](../models-recipes/package-source-files-recipe.md) pour découvrir comment créer une URL hôte Docker étape par étape.

Vous pouvez également utiliser la collection Postman suivante pour faciliter l’exécution du processus de l’API du pipeline de fonctionnalités :

https://www.getpostman.com/collections/c5fc0d1d5805a5ddd41a

### Création d’un moteur de pipeline de fonctionnalités {#create-engine-api}

Une fois que vous disposez de l&#39;emplacement de votre image Docker, vous pouvez [créer un moteur](../api/engines.md#feature-pipeline-docker) de pipeline de fonctionnalités à l&#39;aide de l&#39; [!DNL Sensei Machine Learning] API en exécutant un POST à `/engines`. La création réussie d&#39;un moteur de pipeline de fonctionnalités vous fournit un identifiant unique (`id`) de moteur. Veillez à enregistrer cette valeur avant de continuer.

### Création d’une instance MLInstance {#create-mlinstance}

A l’aide de votre nouvelle `engineID`instance, vous devez [créer une position](../api/mlinstances.md#create-an-mlinstance) MLI en envoyant une requête de POST au `/mlInstance` point de terminaison. A successful response returns a payload containing the details of the newly created MLInstance including its unique identifier (`id`) used in the next API call.

### Création d’une expérience {#create-experiment}

Ensuite, vous devez [créer une expérience](../api/experiments.md#create-an-experiment). Pour créer une expérience, vous devez disposer de votre identifiant unique MLIstance (`id`) et envoyer une requête de POST au `/experiment` point de terminaison. A successful response returns a payload containing the details of the newly created Experiment including its unique identifier (`id`) used in the next API call.

### Spécifier la tâche de pipeline de fonction d&#39;exécution de l&#39;expérience {#specify-feature-pipeline-task}

Après avoir créé une expérience, vous devez changer le mode de l’expérience en `featurePipeline`mode. Pour changer de mode, faites en sorte qu’un POST supplémentaire [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) avec votre `EXPERIMENT_ID` et dans le corps envoyez `{ "mode":"featurePipeline"}` pour spécifier une exécution d’expérience de pipeline de fonctionnalités.

Une fois l’expérience terminée, demandez à un GET de `/experiments/{EXPERIMENT_ID}` récupérer l’état [](../api/experiments.md#retrieve-specific) de l’expérience et d’attendre que l’état de l’expérience soit mis à jour.

### Spécifier la tâche de formation d&#39;exécution de l&#39;expérience {#training}

Ensuite, vous devez [spécifier la tâche](../api/experiments.md#experiment-training-scoring)de l&#39;exécution de la formation. Faites en sorte qu&#39;un POST `experiments/{EXPERIMENT_ID}/runs` et dans le corps définissent le mode `train` et envoyer un tableau de tâches qui contient vos paramètres d&#39;entraînement. Une réponse réussie renvoie un payload contenant les détails de l’expérience interrogée.

Une fois l’expérience terminée, demandez à un GET de `/experiments/{EXPERIMENT_ID}` récupérer l’état [](../api/experiments.md#retrieve-specific) de l’expérience et d’attendre que l’état de l’expérience soit mis à jour.

### Spécifier la tâche de notation de l&#39;exécution de l&#39;expérience {#scoring}

>[!NOTE]
>
> Pour terminer cette étape, vous devez avoir au moins une session de formation réussie associée à votre expérience.

Après une exécution de formation réussie, vous devez [spécifier la tâche](../api/experiments.md#experiment-training-scoring)d’exécution de score. Faites d’un POST `experiments/{EXPERIMENT_ID}/runs` et dans le corps définissez l’ `mode` attribut sur &quot;score&quot;. Cela début l’exécution de votre expérience de score.

Une fois l’expérience terminée, demandez à un GET de `/experiments/{EXPERIMENT_ID}` récupérer l’état [](../api/experiments.md#retrieve-specific) de l’expérience et d’attendre que l’état de l’expérience soit mis à jour.

Une fois la notation terminée, votre pipeline de fonctionnalités doit être opérationnel.

## Étapes suivantes {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

En lisant ce document, vous avez créé un pipeline de fonctionnalités à l&#39;aide du kit de développement de création de modèles, créé une image Docker et utilisé l&#39;URL d&#39;image Docker pour créer un modèle de pipeline de fonctionnalités à l&#39;aide de l&#39; [!DNL Sensei Machine Learning] API. Vous êtes maintenant prêt à continuer à transformer les jeux de données et à extraire les fonctionnalités de données à l’échelle de l’ [!DNL Sensei Machine Learning API](../api/getting-started.md)application.