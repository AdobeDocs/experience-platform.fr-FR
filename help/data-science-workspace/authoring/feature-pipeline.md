---
keywords: Experience Platform;Tutorial;Feature Pipeline;Data Science Workspace;popular topics
solution: Experience Platform
title: Création d’un pipeline de fonctionnalités
topic: Tutorial
translation-type: tm+mt
source-git-commit: b9b0578a43182650b3cfbd71f46bcb817b3b0cda

---


# Création d’un pipeline de fonctionnalités

Adobe Experience Platform vous permet de créer et de créer des pipelines de fonctionnalités personnalisés afin d’effectuer l’ingénierie de fonctionnalités à l’échelle de l’environnement d’exécution Sensei Machine Learning Framework (ci-après dénommé &quot;Runtime&quot;).

Ce décrit les différentes classes d’un pipeline de fonctionnalités et fournit un didacticiel détaillé pour la création d’un pipeline de fonctionnalités personnalisé à l’aide du SDK [de création de](./sdk.md) modèles dans PySpark et Spark.

Ce didacticiel décrit les étapes suivantes :
- [Mise en oeuvre de vos classes Feature Pipeline](#implement-your-feature-pipeline-classes)
   - [Définition de variables dans un fichier de configuration](#define-variables-in-the-configuration-json-file)
   - [Préparation des données d’entrée avec DataLoader](#prepare-the-input-data-with-dataloader)
   - [Transformation d’un jeu de données à l’aide de DatasetTransformer](#transform-a-dataset-with-datasettransformer)
   - [Fonctionnalités de données de l&#39;ingénieur avec FeaturePipelineFactory](#engineer-data-features-with-featurepipelinefactory)
   - [Stockez votre jeu de données de fonctionnalités avec DataSaver.](#store-your-feature-dataset-with-datasaver)
   - [Spécifiez les noms de classe mis en oeuvre dans le fichier d&#39;application](#specify-your-implemented-class-names-in-the-application-file)
- [Création de l’artefact binaire](#build-the-binary-artifact)
- [Création d’un moteur de pipeline de fonctionnalités à l’aide de l’API](#create-a-feature-pipeline-engine-using-the-api)

## Classes de pipeline de fonctionnalités

Le tableau suivant décrit les principales classes abstraites que vous devez étendre pour créer un pipeline de fonctionnalités :

| Classe abstraite | Description |
| -------------- | ----------- |
| DataLoader | Une classe DataLoader fournit une implémentation pour la récupération des données d’entrée. |
| DatasetTransformer | Une classe DatasetTransformer fournit des implémentations pour transformer le jeu de données d’entrée. Vous pouvez choisir de ne pas fournir de classe DatasetTransformer et de mettre en oeuvre votre logique d&#39;ingénierie de fonctionnalités dans la classe FeaturePipelineFactory à la place. |
| FeaturePipelineFactory | Une classe FeaturePipelineFactory crée un pipeline Spark consistant en une série de transformateurs Spark pour effectuer l’ingénierie de fonctionnalités. Vous pouvez choisir de ne pas fournir une classe FeaturePipelineFactory et de mettre en oeuvre votre logique d&#39;ingénierie de fonctionnalités dans la classe DatasetTransformer à la place. |
| DataSaver | Une classe DataSaver fournit la logique pour l’  d’un jeu de données de fonctionnalités. |

Lorsqu’une tâche de pipeline de fonctionnalités est lancée, l’exécution commence par exécuter DataLoader pour charger des données d’entrée sous la forme d’un DataFrame, puis modifie le DataFrame en exécutant DataFrameTransformer ou FeaturePipelineFactory, ou les deux. Enfin, le jeu de données des fonctionnalités qui en résulte est stocké via DataSaver.

L’organigramme suivant montre l’ordre d’exécution du runtime :

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Mise en oeuvre de vos classes Feature Pipeline

Les sections suivantes fournissent des détails et des exemples sur l’implémentation des classes requises pour un pipeline de fonctionnalités.

### Définition de variables dans le fichier JSON de configuration

Le fichier JSON de configuration se compose de paires clé-valeur et vous permet de spécifier les variables à définir ultérieurement lors de l’exécution. Ces paires clé-valeur peuvent définir des propriétés telles que l’emplacement du jeu de données d’entrée, l’ID du jeu de données de sortie, l’ID du client, les en-têtes de colonne, etc.

L’exemple suivant montre les paires clé-valeur trouvées dans un fichier de configuration. Développez l’exemple pour afficher les détails :


**exemple de configuration JSON**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "datasetId",
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



Vous pouvez accéder à la configuration JSON à l’aide de n’importe quelle méthode de classe qui définit `configProperties` comme paramètre. Par exemple :

**PySpark**

```python
input_dataset_id = str(configProperties.get("datasetId"))
```

**Spark**

```scala
val input_dataset_id: String = configProperties.get("datasetId")
```


### Préparation des données d’entrée avec DataLoader

DataLoader est responsable de la récupération et du filtrage des données d’entrée. Votre implémentation de DataLoader doit étendre la classe abstraite `DataLoader` et remplacer la méthode abstraite `load`.

L’exemple suivant récupère un jeu de données Platform par ID et le renvoie sous forme de DataFrame, où l’ID du jeu de données (`datasetId`) est une propriété définie dans le fichier de configuration. Développez chaque exemple pour afficher les détails :


**Exemple PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    def load(self, configProperties, spark):

        # preliminary checks
        if configProperties is None :
            raise ValueError("configProperties parameter is null")
        if spark is None:
            raise ValueError("spark parameter is null")

        # prepare variables
        dataset_id = str(
            configProperties.get("datasetId"))
        service_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['dataset_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session
        df = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return df
```




**Exemple Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

class MyDataLoader extends DataLoader {
    override def load(configProperties: ConfigProperties, sparkSession: SparkSession): DataFrame = {

        // preliminary checks
        require(configProperties != null)
        require(sparkSession != null)

        // prepare variables
        val dataSetId: String = configProperties
            .get("datasetId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(dataSetId, serviceToken, userToken, orgId, apiKey).foreach(
            value => required(value != "")
        )

        // load dataset through Spark session
        var df = sparkSession.read.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .load(dataSetId)
        
        // return as DataFrame
        df
    }
}
```



### Transformation d’un jeu de données à l’aide de DatasetTransformer

Un DataFrameTransformer fournit la logique de transformation d’un DataFrame d’entrée et renvoie un nouveau DataFrame dérivé. Cette classe peut être implémentée pour travailler en coopération avec une FeaturePipelineFactory, pour travailler comme composant d&#39;ingénierie de fonctionnalités unique ou vous pouvez choisir de ne pas implémenter cette classe.

L’exemple suivant étend la classe DatasetTransformer. Développez chaque exemple pour afficher les détails :


**Exemple PySpark**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer

class MyDatasetTransformer(DatasetTransformer):

    def transform(self, configProperties, dataset):
        transformed = dataset

        '''
        Transformations
        '''

        # return new DataFrame
        return transformed
```




**Exemple Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DatasetTransformer

class MyDatasetTransformer extends DatasetTransformer {

    override def transform(configProperties: ConfigProperties, dataset: Dataset[_]): Dataset[_] = {
        val transformed = dataset

        /*
        transformations
        */
        
        // return new DataFrame
        transformed
    }
}
```



### Fonctionnalités de données de l&#39;ingénieur avec FeaturePipelineFactory

Une FeaturePipelineFactory vous permet de mettre en oeuvre votre logique d’ingénierie de fonctionnalités en définissant et en associant une série de transformateurs Spark à travers un pipeline Spark. Cette classe peut être implémentée pour travailler en collaboration avec un DataTransformer, pour travailler en tant que composant d’ingénierie de fonctionnalités unique ou pour ne pas implémenter cette classe.

L’exemple suivant étend la classe FeaturePipelieFactory et implémente une série de transformateurs Spark en plusieurs étapes dans un pipeline Spark. Développez chaque exemple pour afficher les détails :


**Exemple PySpark**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.feature import HashingTF, Tokenizer
from sdk.feature_pipeline_factory import FeaturePipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def create_pipeline(self, configProperties):

        # Spark Transformers
        tokenizer = Tokenizer(inputCol="lower_text", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")

        # Chain together Spark Transformers as Spark Pipeline Stages
        pipeline = Pipeline(stages=[tokenizer, hashingTF])

        # return a Spark Pipeline
        return pipeline

    def get_param_map(self, configProperties, sparkSession):
        pass
```




**Exemple Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.FeaturePipelineFactory
import org.apache.spark.ml.feature.{HashingTF, Tokenizer}
import org.apache.spark.ml.Pipeline
import org.apache.spark.ml.param.ParamMap
import org.apache.spark.sql.SparkSession

class MyFeaturePipelineFactory(uid:String) extends FeaturePipelineFactory(uid) {
    def this() = this("MyFeaturePipeline")

    override def createPipeline(configProperties: ConfigProperties): Pipeline = {
        
        // Spark Transformers
        val tokenizer = new Tokenizer()
            .setInputCol("lower_text")
            .setOutputCol("words")
        val hashingTF = new HashingTF()
            .setInputCol(tokenizer.getOutputCol())
            .setOutputCol("features")

        // Chain together Spark Transformers as Spark Pipeline Stages
        val pipeline = new Pipeline()
            .setStages(Array(tokenizer, hashingTF))
        
        // return a Spark Pipeline
        pipeline
    }

    override def getParamMap(configProperties: ConfigProperties, sparkSession: SparkSession): ParamMap = {
        val map = new ParamMap()
        map
    }
}
```



### Stockez votre jeu de données de fonctionnalités avec DataSaver.

DataSaver est chargé de stocker vos jeux de données de fonctionnalités résultants dans un emplacement  . Votre implémentation de DataSaver doit étendre la classe abstraite `DataSaver` et remplacer la méthode abstraite `save`.

L’exemple suivant étend la classe DataSaver qui stocke les données dans un jeu de données Platform par ID, où l’ID du jeu de données (`featureDatasetId`) et l’ID du client (`tenantId`) sont des propriétés définies dans le fichier de configuration. Développez chaque exemple pour afficher les détails :


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




**Exemple Spark**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

class MyDataSaver extends DataSaver {
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("featureDatasetId").getOrElse("")
        val tenant_id:String = configProperties
            .get("tenantId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(output_dataset_id, tenant_id, serviceToken, userToken, orgId, apiKey).foreach(
            value => require(value != "")
        )

        // create and prepare DataFrame with valid columns
        import sparkSession.implicits._

        var output_df  = dataFrame.withColumn("date", $"date".cast("String"))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        // store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp").write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

### Spécifiez les noms de classe mis en oeuvre dans le fichier d&#39;application

Maintenant que vos classes Feature Pipeline sont définies et implémentées, vous devez spécifier les noms de vos classes dans le fichier d’application.

Les exemples suivants indiquent les noms de classe implémentés. Développez l’exemple pour afficher les détails :


**Exemple PySpark**

```yaml
# application.yaml

# Name of the implementation of DataLoader abstract class
feature.dataLoader: MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer: MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.pipeline.class: MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver: MyDataSaver
```




**Exemple Spark**

```properties
# application.properties

# Name of the implementation of DataLoader abstract class
feature.pipeline.class=MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer=MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.dataLoader=MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver=MyDataSaver
```



## Création de l’artefact binaire

Maintenant que vos classes Feature Pipeline ont été implémentées, vous pouvez les créer et les compiler dans un artefact binaire qui peut ensuite être utilisé pour créer un pipeline de fonctionnalités via des appels d’API.

**PySpark**

Pour créer un module PySpark Feature Pipeline, exécutez le script `setup.py` Python situé dans le répertoire racine du SDK de création de modèles.

>[!NOTE] La création d&#39;un Pipeline de fonctionnalités PySpark nécessite l&#39;installation de Python 3 sur votre machine.

```shell
python3 setup.py bdist_egg
```

La création réussie de votre pipeline de caractéristiques générera un `.egg` artefact dans le `/dist` répertoire. Cet artefact est utilisé pour créer un pipeline de fonctionnalités.

**Spark**

Pour créer un pipeline de fonctionnalités Spark, exécutez la commande de console suivante dans le répertoire racine du SDK de création de modèles :

>[!NOTE] La création d’un tuyau de fonction Spark nécessite l’installation de Scala et de sbt sur votre machine.

```shell
mvn clean install
```

La création réussie de votre pipeline de caractéristiques générera un `.jar` artefact dans le `/dist` répertoire. Cet artefact est utilisé pour créer un pipeline de fonctionnalités.

## Création d’un moteur de pipeline de fonctionnalités à l’aide de l’API

Maintenant que vous avez créé votre pipeline de fonctionnalités et créé l&#39;artefact binaire, vous pouvez [créer un moteur de pipeline de fonctionnalités à l&#39;aide de l&#39;API](../api/engines.md#create-a-feature-pipeline-engine-using-binary-artifacts)d&#39;apprentissage automatique Sensei. La création réussie d’un moteur de pipeline de fonctionnalités vous fournira un ID de moteur dans le corps de la réponse. Veillez à enregistrer cette valeur avant de passer aux étapes suivantes.

## Étapes suivantes

[//]: # (Next steps section should refer to tutorials on how to score data using the Feature Pipeline Engine. Update this document once those tutorials are available)

En lisant ce , vous avez créé un pipeline de fonctionnalités à l&#39;aide du kit de développement de création de modèles, créé un artefact binaire et utilisé cet artefact pour créer un moteur de pipeline de fonctionnalités via un appel d&#39;API. Vous êtes maintenant prêt à [créer un modèle](../api/mlinstances.md#create-an-mlinstance) de pipeline de fonctionnalités à l’aide de votre nouveau moteur et de votre nouveau, qui transforment les jeux de données et extraient les fonctionnalités de données à l’échelle.