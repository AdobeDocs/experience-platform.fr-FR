---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics
solution: Experience Platform
title: Guide du développeur SDK
topic: Overview
translation-type: tm+mt
source-git-commit: 13b6c08b1038d48cdff7147dfcd7b65ea2f95599

---


# Guide du développeur SDK

Le kit SDK de création de modèles vous permet de développer des recettes d’apprentissage automatique et des pipelines de fonctionnalités personnalisés qui peuvent être utilisés dans l’espace de travail Data Science d’Adobe Experience Platform, afin de fournir des modèles applicables dans PySpark et Spark.

Ce fournit des informations sur les différentes classes trouvées dans le SDK de création de modèles :

- [DataLoader](#dataloader)
   - [Chargement de données à partir d’un jeu de données de plateforme](#load-data-from-a-platform-dataset)
- [DataSaver](#datasaver)
   - [Enregistrer les données dans un jeu de données de plateforme](#save-data-to-a-platform-dataset)
- [DatasetTransformer](#datasettransformer)
- [FeaturePipelineFactory](#featurepipelinefactory)
- [PipelineFactory](#pipelinefactory)
- [MLEvaluator](#mlevaluator)

## DataLoader

La classe DataLoader encapsule tout ce qui a trait à la récupération, au filtrage et au renvoi de données d’entrée brutes. Parmi les exemples de données d’entrée, citons la formation, la notation ou l’ingénierie des fonctionnalités. Les chargeurs de données étendent la classe abstraite `DataLoader` et doivent remplacer la méthode abstraite `load`.

**PySpark**

Le tableau suivant décrit les méthodes abstraites d’une classe PySpark Data Loader :

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
                <p>Charger et renvoyer des données de plateforme sous forme de données Pandas DataFrame</p>
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

Le tableau suivant décrit les méthodes abstraites d’une classe Spark Data Loader :

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
                <p>Chargement et renvoi des données de plateforme en tant que DataFrame</p>
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

### Chargement de données à partir d’un jeu de données de plateforme

L’exemple suivant récupère les données de la plateforme par ID et renvoie un DataFrame, où l’ID du jeu de données (`datasetId`) est une propriété définie dans le fichier de configuration.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load(self, configProperties, spark):
        """
        Load and return dataset

        :param configProperties:    Configuration properties
        :param spark:               Spark session
        :return:                    DataFrame
        """

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
        pd = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return pd
```

**Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    /**
     * @param configProperties  - Configuration properties
     * @param sparkSession      - Spark session
     * @return                  - DataFrame
     */
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

## DataSaver

La classe DataSaver encapsule tout ce qui a trait au stockage des données de sortie, y compris celles issues de l’évaluation ou de l’ingénierie des fonctionnalités. Les économiseurs de données étendent la classe abstraite `DataSaver` et doivent remplacer la méthode abstraite `save`.

**PySpark**

Le tableau suivant décrit les méthodes abstraites d’une classe PySpark Data Saver :

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
                <p>Recevoir les données de sortie sous forme de DataFrame et les stocker dans un jeu de données de plateforme</p>
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

**Spark**

Le tableau suivant décrit les méthodes abstraites d’une classe Spark Data Saver :

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
                <p><code class=" language-undefined">save(configProperties, sparkSession)</code></p>
                <p>Recevoir les données de sortie sous forme de DataFrame et les stocker dans un jeu de données de plateforme</p>
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

### Enregistrer les données dans un jeu de données de plateforme

Pour stocker des données dans un jeu de données de plateforme, les propriétés doivent être fournies ou définies dans le fichier de configuration :

- ID de jeu de données de plateforme valide auquel les données seront stockées
- ID de client appartenant à votre organisation

Les exemples suivants stockent des données (`prediction`) dans un jeu de données de plateforme, où l’ID de jeu de données (`datasetId`) et l’ID de client (`tenantId`) sont des propriétés définies dans le fichier de configuration.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, configProperties, prediction):
        """
        Store DataFrame to a Platform dataset

        :param configProperties:    Configuration properties
        :param prediction:          DataFrame to be stored to a Platform dataset
        """

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("datasetId"))
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

        # store data into dataset
        prediction.write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```




**Spark**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */
class ScoringDataSaver extends DataSaver {

    /**
     * @param configProperties  - Configuration properties
     * @param dataFrame         - DataFrame to be stored to a Platform dataset
     */
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession
        import sparkSession.implicits._

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val predictionColumn = configProperties.get(Constants.PREDICTION_COL)
            .getOrElse(Constants.DEFAULT_PREDICTION)
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("datasetId").getOrElse("")
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

        // store data into dataset
        dataFrame.write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

## DatasetTransformer

La classe DatasetTransformer modifie et transforme la structure d’un jeu de données. L’exécution Sensei Machine Learning Runtime ne nécessite pas la définition de ce composant et est implémentée en fonction de vos besoins.

En ce qui concerne un pipeline de caractéristiques, les transformateurs de jeux de données peuvent être utilisés en collaboration avec une usine de pipeline de caractéristiques pour préparer les données pour l&#39;ingénierie de caractéristiques.

**PySpark**

Le tableau suivant décrit les méthodes de classe d’une classe de transformateur de jeux de données PySpark :

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
                    <li><code class=" language-undefined">dataset</code>: Jeu de données d’entrée pour la transformation</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

Le tableau suivant décrit les méthodes abstraites d’une classe de transformateur de jeux de données Spark :

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
                    <li><code class=" language-undefined">dataset</code>: Jeu de données d’entrée pour la transformation</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory

La classe FeaturePipelineFactory contient des fonctionnalités  des algorithmes  et définit les étapes d’un tuyau de caractéristiques de l’à la fin.

**PySpark**

Le tableau suivant décrit les méthodes de classe d’une fabrique de fonctionnalités PySpark FeaturePipelineFactory :

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
                <p>Création et renvoi d’un pipeline Spark contenant une série de transformateurs Spark</p>
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
                <p>Récupérer et renvoyer la carte param des propriétés de configuration</p>
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

**Spark**

Le tableau suivant décrit les méthodes de classe d’une Spark FeaturePipelineFactory :

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
                <p>Création et renvoi d’un pipeline contenant une série de transformateurs</p>
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
                <p>Récupérer et renvoyer la carte param des propriétés de configuration</p>
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

## PipelineFactory

La classe PipelineFactory encapsule les méthodes et les définitions pour la formation et la notation des modèles, où la logique et les algorithmes de formation sont définis sous la forme d’un pipeline Spark.

**PySpark**

Le tableau suivant décrit les méthodes de classe d’une fabrique de pipelines PySpark :

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
                <p>Renvoie un pipeline personnalisé qui contient la logique et l’algorithme pour former un modèle. Cette méthode n’est pas requise si un pipeline Spark est utilisé</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">dataframe</code>: Jeu de données de fonctionnalités pour la saisie des informations de formation</li>
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
                    <li><code class=" language-undefined">model</code>: Modèle entraîné utilisé pour la notation</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrait</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Récupérer et renvoyer la carte param des propriétés de configuration</p>
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

**Spark**

Le tableau suivant décrit les méthodes de classe d’une Spark PipelineFactory :

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
                <p>Création et renvoi d’un pipeline qui contient la logique et l’algorithme de formation et de notation des modèles</p>
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
                <p>Récupérer et renvoyer la carte param des propriétés de configuration</p>
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

## MLEvaluator

La classe MLEvaluator fournit des méthodes pour définir des mesures d’évaluation et déterminer des jeux de données de formation et de test.

**PySpark**

Le tableau suivant décrit les méthodes de classe d’un MLEvaluator PySpark :

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
                <p>Divise le jeu de données d’entrée en sous-ensembles de formation et de test.</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">dataframe</code>: Jeu de données d’entrée à fractionner</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrait</i><br/><code class=" language-undefined">evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Evalue un modèle formé et renvoie les résultats de l'évaluation</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Auto-référence</li>
                    <li><code class=" language-undefined">dataframe</code>: Un DataFrame constitué de données de formation et de test</li>
                    <li><code class=" language-undefined">model</code>: Un modèle bien formé</li>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

Le tableau suivant décrit les méthodes de classe d’un MLEvaluator Spark :

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
                <p>Divise le jeu de données d’entrée en sous-ensembles de formation et de test.</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">data</code>: Jeu de données d’entrée à fractionner</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstrait</i><br/><code class=" language-undefined">evaluate(configProperties, model, data)</code></p>
                <p>Evalue un modèle formé et renvoie les résultats de l'évaluation</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Propriétés de configuration</li>
                    <li><code class=" language-undefined">model</code>: Un modèle bien formé</li>
                    <li><code class=" language-undefined">data</code>: Un DataFrame constitué de données de formation et de test</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>