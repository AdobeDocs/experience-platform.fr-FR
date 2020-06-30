---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics
solution: Experience Platform
title: Guide du développeur SDK
topic: Overview
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 1%

---


# Guide du développeur SDK

Le kit SDK de création de modèles vous permet de développer des recettes d’apprentissage automatique personnalisées et des pipelines de fonctionnalités qui peuvent être utilisés dans [!DNL Adobe Experience Platform] Data Science Workspace, en fournissant des modèles applicables dans [!DNL PySpark] et [!DNL Spark (Scala)].

Ce document fournit des informations sur les différentes classes trouvées dans le SDK de création de modèles.

## DataLoader {#dataloader}

La classe DataLoader encapsule tout ce qui a trait à la récupération, au filtrage et au renvoi de données d’entrée brutes. Parmi les exemples de données d’entrée, citons celles destinées à la formation, à la notation ou à l’ingénierie des fonctionnalités. Les chargeurs de données étendent la classe abstraite `DataLoader` et doivent remplacer la méthode abstraite `load`.

**PySpark**

Le tableau suivant décrit les méthodes abstraites d&#39;une classe PySpark Data Loader :

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
                <p><code class=" language-undefined">load(self, configProperties, spark)</code></p>
                <p>Charger et renvoyer les données Platform en tant que DataFrame Pandas</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">configProperties</code>: Carte des propriétés de configuration</li>
                    <li><code class=" language-undefined">spark</code>: Session Spark</li>
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
                <p><code class=" language-undefined">load(configProperties, sparkSession)</code></p>
                <p>Charger et renvoyer les données Platform en tant que DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Carte des propriétés de configuration</li>
                    <li><code class=" language-undefined">sparkSession</code>: Session Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Chargement de données à partir d’un [!DNL Platform] jeu de données {#load-data-from-a-platform-dataset}

L’exemple suivant récupère [!DNL Platform] les données par ID et renvoie un DataFrame, où l’ID de jeu de données (`datasetId`) est une propriété définie dans le fichier de configuration.

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

La classe DataSaver encapsule tout ce qui a trait au stockage des données de sortie, y compris celles issues de la notation ou de l’ingénierie de fonctionnalités. Les économiseurs de données étendent la classe abstraite `DataSaver` et doivent remplacer la méthode abstraite `save`.

**PySpark**

Le tableau suivant décrit les méthodes abstraites d’une classe [!DNL PySpark] Data Saver :

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
                <p><code class=" language-undefined">save(self, configProperties, dataframe)</code></p>
                <p>Recevoir les données de sortie sous forme de DataFrame et les stocker dans un jeu de données Platform</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">configProperties</code>: Carte des propriétés de configuration</li>
                    <li><code class=" language-undefined">dataframe</code>: Données à stocker sous la forme d’un DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Le tableau suivant décrit les méthodes abstraites d’une classe [!DNL Spark] Data Saver :

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
                <p><code class=" language-undefined">save(configProperties, dataFrame)</code></p>
                <p>Recevoir les données de sortie sous forme de DataFrame et les stocker dans un jeu de données Platform</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Carte des propriétés de configuration</li>
                    <li><code class=" language-undefined">dataFrame</code>: Données à stocker sous la forme d’un DataFrame</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Enregistrer les données dans un [!DNL Platform] jeu de données {#save-data-to-a-platform-dataset}

Pour stocker des données dans un [!DNL Platform] jeu de données, les propriétés doivent être fournies ou définies dans le fichier de configuration :

- ID de [!DNL Platform] jeu de données valide auquel les données seront stockées
- ID de client appartenant à votre organisation

Les exemples suivants stockent des données (`prediction`) dans un [!DNL Platform] jeu de données, où l&#39;ID de jeu de données (`datasetId`) et l&#39;ID de client (`tenantId`) sont des propriétés définies dans le fichier de configuration.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
from .helper import *


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
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
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
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

La classe DatasetTransformer modifie et transforme la structure d&#39;un jeu de données. Le composant [!DNL Sensei Machine Learning Runtime] n’a pas besoin d’être défini et est implémenté selon vos besoins.

En ce qui concerne un pipeline de fonctionnalités, les transformateurs de jeux de données peuvent être utilisés en collaboration avec une usine de traitement de données pour préparer les données en vue de l&#39;ingénierie de fonctionnalités.

**PySpark**

Le tableau suivant décrit les méthodes de classe d&#39;une classe de transformateur de dataset PySpark :

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
                <p><i>abstrait</i><br/><code class=" language-undefined">transform(self, configProperties, dataset)</code></p>
                <p>Prend un jeu de données en entrée et en sortie un nouveau jeu de données dérivé</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">configProperties</code>: Carte des propriétés de configuration</li>
                    <li><code class=" language-undefined">dataset</code>: Jeu de données d'entrée pour la transformation</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Le tableau suivant décrit les méthodes abstraites d&#39;une classe de transformateur de [!DNL Spark] données :

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
                <p><code class=" language-undefined">transform(configProperties, dataset)</code></p>
                <p>Prend un jeu de données en entrée et en sortie un nouveau jeu de données dérivé</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Carte des propriétés de configuration</li>
                    <li><code class=" language-undefined">dataset</code>: Jeu de données d'entrée pour la transformation</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

La classe FeaturePipelineFactory contient des algorithmes d&#39;extraction de fonction et définit les étapes d&#39;un tuyau de fonction du début à la fin.

**PySpark**

Le tableau suivant décrit les méthodes de classe d&#39;une PySpark FeaturePipelineFactory :

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
                <p><i>abstrait</i><br/><code class=" language-undefined">create_pipeline(self, configProperties)</code></p>
                <p>Créer et renvoyer un tuyau Spark contenant une série de transformateurs Spark</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">configProperties</code>: Carte des propriétés de configuration</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrait</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Récupération et renvoi du mappage de paramètres à partir des propriétés de configuration</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">sparkSession</code>: Session Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Le tableau suivant décrit les méthodes de classe d&#39;une [!DNL Spark] FeaturePipelineFactory :

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
                <p><i>abstrait</i><br/><code class=" language-undefined">createPipeline(configProperties)</code></p>
                <p>Créer et renvoyer un pipeline contenant une série de transformateurs</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Carte des propriétés de configuration</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrait</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>Récupération et renvoi du mappage de paramètres à partir des propriétés de configuration</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">sparkSession</code>: Session Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

La classe PipelineFactory encapsule les méthodes et les définitions pour la formation et la notation des modèles, où la logique et les algorithmes de formation sont définis sous la forme d&#39;un [!DNL Spark] pipeline.

**PySpark**

Le tableau suivant décrit les méthodes de classe d&#39;une usine de pipelines PySpark :

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
                <p><i>abstrait</i><br/><code class=" language-undefined">apply(self, configProperties)</code></p>
                <p>Création et renvoi d’un pipeline Spark qui contient la logique et l’algorithme de formation et de notation des modèles</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrait</i><br/><code class=" language-undefined">train(self, configProperties, dataframe)</code></p>
                <p>Renvoie un pipeline personnalisé qui contient la logique et l'algorithme pour former un modèle. Cette méthode n'est pas requise si un pipeline Spark est utilisé</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">dataframe</code>: Jeu de données de fonctionnalités pour la saisie de formation</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrait</i><br/><code class=" language-undefined">score(self, configProperties, dataframe, model)</code></p>
                <p>Score à l’aide du modèle entraîné et retour des résultats</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">dataframe</code>: Jeu de données d’entrée pour le score</li>
                    <li><code class=" language-undefined">model</code>: Modèle formé utilisé pour la notation</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrait</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Récupération et renvoi du mappage de paramètres à partir des propriétés de configuration</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">sparkSession</code>: Session Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Le tableau suivant décrit les méthodes de classe d&#39;un [!DNL Spark] PipelineFactory :

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
                <p><i>abstrait</i><br/><code class=" language-undefined">apply(configProperties)</code></p>
                <p>Création et renvoi d’un pipeline contenant la logique et l’algorithme de formation et de notation des modèles</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrait</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>Récupération et renvoi du mappage de paramètres à partir des propriétés de configuration</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">sparkSession</code>: Session Spark</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

La classe MLEvaluator fournit des méthodes pour définir des mesures d&#39;évaluation et déterminer des jeux de données de formation et de test.

**PySpark**

Le tableau suivant décrit les méthodes de classe d&#39;un MLEvaluator PySpark :

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
                <p><i>abstrait</i><br/><code class=" language-undefined">split(self, configProperties, dataframe)</code></p>
                <p>Divise le jeu de données d’entrée en sous-ensembles de données de formation et de test.</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">dataframe</code>: Jeu de données d'entrée à fractionner</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrait</i><br/><code class=" language-undefined">evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Évaluer un modèle formé et renvoyer les résultats de l'évaluation</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">dataframe</code>: Un DataFrame constitué de données de formation et de test</li>
                    <li><code class=" language-undefined">model</code>: Un modèle formé</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

Le tableau suivant décrit les méthodes de classe d&#39;un [!DNL Spark] MLEvaluator :

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
                <p><i>abstrait</i><br/><code class=" language-undefined">split(configProperties, data)</code></p>
                <p>Divise le jeu de données d’entrée en sous-ensembles de données de formation et de test.</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">data</code>: Jeu de données d'entrée à fractionner</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrait</i><br/><code class=" language-undefined">evaluate(configProperties, model, data)</code></p>
                <p>Évaluer un modèle formé et renvoyer les résultats de l'évaluation</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">model</code>: Un modèle formé</li>
                    <li><code class=" language-undefined">data</code>: Un DataFrame constitué de données de formation et de test</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>