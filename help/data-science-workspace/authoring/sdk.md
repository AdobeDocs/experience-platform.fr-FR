---
keywords: Experience Platform;guide de développement;SDK;Création de modèles;Workspace de science des données;rubriques populaires;test
solution: Experience Platform
title: SDK de création de modèles
description: La SDK de création de modèles vous permet de développer des pipelines de fonctionnalités et des recettes de machine learning personnalisés que vous pouvez utiliser dans Adobe Experience Platform Data Science Workspace pour fournir des modèles à mettre en œuvre dans PySpark et Spark (Scala).
exl-id: c7577f93-a64f-49b7-a76d-71f21d619052
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 62%

---

# SDK de création de modèles

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

Le SDK de création de modèles vous permet de développer des pipelines de fonctionnalités et des recettes de machine learning personnalisés que vous pouvez utiliser dans [!DNL Adobe Experience Platform] Workspace de science des données pour fournir des modèles à mettre en œuvre dans [!DNL PySpark] et [!DNL Spark (Scala)].

Ce document fournit des informations sur les différentes classes du SDK de création de modèles.

## DataLoader {#dataloader}

La classe DataLoader englobe tous les éléments en lien avec la récupération, le filtrage et le renvoi de données d’entrée brutes. Les exemples de données d’entrée incluent les exemples de formation, de notation ou de conception des fonctionnalités. Les chargeurs de données étendent la classe abstraite `DataLoader` et doivent remplacer la méthode abstraite `load`.

**PySpark**

Le tableau suivant décrit les méthodes abstraites d’une classe Data Loader PySpark :

<table>
    <thead>
        <tr>
            <th>Méthode et description</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(self, configProperties, spark)</code></p>
                <p>Charger et renvoyer des données Experience Platform en tant que DataFrame Pandas</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: auto-référence</li>
                    <li><code>configProperties</code>: map des propriétés de configuration</li>
                    <li><code>spark</code>: session Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

Le tableau suivant décrit les méthodes abstraites d’une classe [!DNL Spark] Data Loader :

<table>
    <thead>
        <tr>
            <th>Méthode et description</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(configProperties, sparkSession)</code></p>
                <p>Charger et renvoyer des données Experience Platform en tant que DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: map des propriétés de configuration</li>
                    <li><code>sparkSession</code>: session Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Charger des données à partir d’un jeu de données [!DNL Experience Platform] {#load-data-from-a-platform-dataset}

L’exemple suivant récupère les données [!DNL Experience Platform] par ID et renvoie un DataFrame, où l’ID du jeu de données (`datasetId`) est une propriété définie dans le fichier de configuration.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load_dataset(config_properties, spark, task_id):

        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
        PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

        # prepare variables
        service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        dataset_id = str(config_properties.get(task_id))

        # validate variables
        for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session

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

        # return as DataFrame
        return pd
```

**Spark (Scala)**

```scala
// Spark

package com.adobe.platform.ml

import java.time.LocalDateTime

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.ml.feature.StringIndexer
import org.apache.spark.sql.expressions.Window
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.{StructType, TimestampType}
import org.apache.spark.sql.{DataFrame, SparkSession}
import org.apache.spark.sql.Column

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
    final val PLATFORM_SDK_PQS_INTERACTIVE: String = "interactive"
    final val PLATFORM_SDK_PQS_BATCH: String = "batch"

    /**
    *
    * @param configProperties - Configuration Properties map
    * @param sparkSession     - SparkSession
    * @return                 - DataFrame which is loaded for training
    */


  def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {

    require(configProperties != null)
    require(sparkSession != null)

    // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

    val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, PLATFORM_SDK_PQS_INTERACTIVE)
      .option(QSOption.datasetId, dataSetId)
      .load()
    df.show()
    df
    }
}
```

## DataSaver {#datasaver}

La classe DataSaver englobe tous les éléments en lien avec le stockage des données de sortie, y compris les données d’évaluation ou de conception de fonctionnalités. Les Data Savers étendent la classe abstraite `DataSaver` et doivent remplacer la méthode abstraite `save`.

**PySpark**

Le tableau suivant décrit les méthodes abstraites d’une classe d’économiseur de données [!DNL PySpark] :

<table>
    <thead>
        <tr>
            <th>Méthode et description</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(self, configProperties, dataframe)</code></p>
                <p>Recevoir les données de sortie en tant que DataFrame et les stocker dans un jeu de données Experience Platform</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: auto-référence</li>
                    <li><code>configProperties</code>: map des propriétés de configuration</li>
                    <li><code>dataframe</code>: données à stocker sous la forme d’un cadre de données</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Le tableau suivant décrit les méthodes abstraites d’une classe d’économiseur de données [!DNL Spark] :

<table>
    <thead>
        <tr>
            <th>Méthode et description</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(configProperties, dataFrame)</code></p>
                <p>Recevoir les données de sortie en tant que DataFrame et les stocker dans un jeu de données Experience Platform</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: map des propriétés de configuration</li>
                    <li><code>dataFrame</code>: données à stocker sous la forme d’un cadre de données</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Enregistrer des données dans un jeu de données [!DNL Experience Platform] {#save-data-to-a-platform-dataset}

Pour stocker des données sur un jeu de données [!DNL Experience Platform], les propriétés doivent être fournies ou définies dans le fichier de configuration :

- Identifiant de jeu de données [!DNL Experience Platform] valide dans lequel les données seront stockées
- Identifiant du client appartenant à votre organisation

Les exemples suivants stockent des données (`prediction`) sur un jeu de données [!DNL Experience Platform], où l’identifiant du jeu de données (`datasetId`) et l’identifiant du client (`tenantId`) sont des propriétés définies dans le fichier de configuration .


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
from .helper import *


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to an Experience Platform dataset
    """

    def save(self, config_properties, prediction):

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if config_properties is None:
            raise ValueError("config_properties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")
        
        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"

        # prepare variables
        scored_dataset_id = str(config_properties.get("scoringResultsDataSetId"))
        tenant_id = str(config_properties.get("tenant_id"))
        timestamp = "2019-01-01 00:00:00"

        service_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
       for arg in ['service_token', 'user_token', 'org_id', 'scored_dataset_id', 'api_key', 'tenant_id']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)
        
        scored_df = prediction.withColumn("date", col("date").cast(StringType()))
        scored_df = scored_df.withColumn(tenant_id, struct(col("date"), col("store"), col("prediction")))
        scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        scored_df = scored_df.withColumn("_id", lit("empty"))
        scored_df = scored_df.withColumn("eventType", lit("empty")

        # store data into dataset

        query_options = get_query_options(sparkContext)

        scored_df.select(tenant_id, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE) \
            .option(query_options.userToken(), user_token) \
            .option(query_options.serviceToken(), service_token) \
            .option(query_options.imsOrg(), org_id) \
            .option(query_options.apiKey(), api_key) \
            .option(query_options.datasetId(), scored_dataset_id) \
            .save()
```

**Spark (Scala)**

```scala
// Spark

package com.adobe.platform.ml

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to an Experience Platform dataset
 */

class ScoringDataSaver extends DataSaver {

  final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
  final val PLATFORM_SDK_PQS_BATCH: String = "batch"

  /**
    * Method that saves the scoring data into a dataframe
    * @param configProperties  - Configuration Properties map
    * @param dataFrame         - Dataframe with the scoring results
    */
    
  override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

    require(configProperties != null)
    require(dataFrame != null)

    val predictionColumn = configProperties.get(Constants.PREDICTION_COL).getOrElse(Constants.DEFAULT_PREDICTION)
    val sparkSession = dataFrame.sparkSession

    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val tenantId:String = configProperties.get("tenantId").getOrElse("")
    val timestamp:String = "2019-01-01 00:00:00"

    val scoringResultsDataSetId: String = configProperties.get("scoringResultsDataSetId").getOrElse("")
    import sparkSession.implicits._

    var df = dataFrame.withColumn("date", $"date".cast("String"))

    var scored_df  = df.withColumn(tenantId, struct(df("date"), df("store"), df(predictionColumn)))
    scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
    scored_df = scored_df.withColumn("_id", lit("empty"))
    scored_df = scored_df.withColumn("eventType", lit("empty"))

    scored_df.select(tenantId, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .save()
    }
}
```

## DatasetTransformer {#datasettransformer}

La classe DatasetTransformer modifie et transforme la structure d’un jeu de données. Le [!DNL Sensei Machine Learning Runtime] ne nécessite pas la définition de ce composant. Il est implémenté en fonction de vos besoins.

En ce qui concerne les pipelines de fonctionnalités, les transformateurs de jeux de données peuvent être utilisés en association avec une fabrique de pipelines de caractéristiques afin de préparer les données pour la conception des fonctionnalités.

**PySpark**

Le tableau suivant décrit les méthodes d’une classe DatasetTransformer PySpark :

<table>
    <thead>
        <tr>
            <th>Méthode et description</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>transform(self, configProperties, dataset)</code></p>
                <p>Utilise un jeu de données en entrée et émet un nouveau jeu de données dérivé en sortie</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: auto-référence</li>
                    <li><code>configProperties</code>: map des propriétés de configuration</li>
                    <li><code>dataset</code>: jeu de données d’entrée pour la transformation</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Le tableau suivant décrit les méthodes abstraites d’une classe de transformateur de jeu de données [!DNL Spark] :

<table>
    <thead>
        <tr>
            <th>Méthode et description</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>transform(configProperties, dataset)</code></p>
                <p>Utilise un jeu de données en entrée et émet un nouveau jeu de données dérivé en sortie</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: map des propriétés de configuration</li>
                    <li><code>dataset</code>: jeu de données d’entrée pour la transformation</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

La classe FeaturePipelineFactory contient des algorithmes d’extraction de fonctionnalités et définit les étapes d’un pipeline de fonctionnalités du début à la fin.

**PySpark**

Le tableau suivant décrit les méthodes d’une classe FeaturePipelineFactory PySpark :

<table>
    <thead>
        <tr>
            <th>Méthode et description</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>create_pipeline(self, configProperties)</code></p>
                <p>Création et renvoi d’un pipeline Spark contenant une série de transformateurs Spark</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: auto-référence</li>
                    <li><code>configProperties</code>: map des propriétés de configuration</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Récupération et renvoi de la map param des propriétés de configuration</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: auto-référence</li>
                    <li><code>configProperties</code>: propriétés de configuration</li>
                    <li><code>sparkSession</code>: session Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Le tableau suivant décrit les méthodes de classe d’un [!DNL Spark] FeaturePipelineFactory :

<table>
    <thead>
        <tr>
            <th>Méthode et description</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>createPipeline(configProperties)</code></p>
                <p>Création et renvoi d’un pipeline contenant une série de transformateurs</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: map des propriétés de configuration</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>Récupération et renvoi de la map param des propriétés de configuration</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propriétés de configuration</li>
                    <li><code>sparkSession</code>: session Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

La classe PipelineFactory encapsule des méthodes et des définitions pour l’entraînement et la notation des modèles, où la logique d’entraînement et les algorithmes sont définis sous la forme d’un pipeline [!DNL Spark].

**PySpark**

Le tableau suivant décrit les méthodes d’une classe PipelineFactory PySpark :

<table>
    <thead>
        <tr>
            <th>Méthode et description</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>apply(self, configProperties)</code></p>
                <p>Création et renvoi d’un pipeline Spark contenant la logique et l’algorithme de formation et de notation des modèles</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: auto-référence</li>
                    <li><code>configProperties</code>: propriétés de configuration</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>train(self, configProperties, dataframe)</code></p>
                <p>Renvoie un pipeline personnalisé contenant la logique et l’algorithme de formation d’un modèle. Cette méthode n’est pas nécessaire si un pipeline Spark est utilisé</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: auto-référence</li>
                    <li><code>configProperties</code>: propriétés de configuration</li>
                    <li><code>dataframe</code>: jeu de données de fonctionnalités pour la saisie de la formation</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>score(self, configProperties, dataframe, model)</code></p>
                <p>Note à l’aide du modèle formé et renvoie les résultats</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: auto-référence</li>
                    <li><code>configProperties</code>: propriétés de configuration</li>
                    <li><code>dataframe</code>: jeu de données d’entrée pour la notation</li>
                    <li><code>model</code>: modèle formé utilisé pour la notation</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Récupération et renvoi de la map param des propriétés de configuration</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: auto-référence</li>
                    <li><code>configProperties</code>: propriétés de configuration</li>
                    <li><code>sparkSession</code>: session Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Le tableau suivant décrit les méthodes de classe d’un [!DNL Spark] PipelineFactory :

<table>
    <thead>
        <tr>
            <th>Méthode et description</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>apply(configProperties)</code></p>
                <p>Création et renvoi d’un pipeline contenant la logique et l’algorithme de formation et de notation des modèles</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propriétés de configuration</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>Récupération et renvoi de la map param des propriétés de configuration</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propriétés de configuration</li>
                    <li><code>sparkSession</code>: session Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

La classe MLEvaluator fournit des méthodes pour définir des mesures d’évaluation et déterminer des jeux de données de formation et de test.

**PySpark**

Le tableau suivant décrit les méthodes d’une classe MLEvaluator PySpark :

<table>
    <thead>
        <tr>
            <th>Méthode et description</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>split(self, configProperties, dataframe)</code></p>
                <p>Divise le jeu de données d’entrée en sous-ensembles de formation et de test</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: auto-référence</li>
                    <li><code>configProperties</code>: propriétés de configuration</li>
                    <li><code>dataframe</code>: jeu de données d’entrée à fractionner</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Évalue un modèle formé et renvoie les résultats de l’évaluation</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: auto-référence</li>
                    <li><code>dataframe</code>: un cadre de données constitué de données de formation et de test</li>
                    <li><code>model</code>: un modèle formé</li>
                    <li><code>configProperties</code>: propriétés de configuration</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Le tableau suivant décrit les méthodes de classe d&#39;un MLEvaluator [!DNL Spark] :

<table>
    <thead>
        <tr>
            <th>Méthode et description</th>
            <th>Paramètres</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>split(configProperties, data)</code></p>
                <p>Divise le jeu de données d’entrée en sous-ensembles de formation et de test</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propriétés de configuration</li>
                    <li><code>data</code>: jeu de données d’entrée à fractionner</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>evaluate(configProperties, model, data)</code></p>
                <p>Évalue un modèle formé et renvoie les résultats de l’évaluation</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: propriétés de configuration</li>
                    <li><code>model</code>: un modèle formé</li>
                    <li><code>data</code>: un cadre de données constitué de données de formation et de test</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>
