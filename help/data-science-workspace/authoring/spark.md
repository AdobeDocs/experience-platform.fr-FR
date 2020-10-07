---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api;spark recipe;read spark;write spark
solution: Experience Platform
title: Accès aux données à l’aide de Spark
topic: tutorial
type: Tutorial
description: Le document suivant contient des exemples d’accès aux données à l’aide de Spark en vue de les utiliser dans Data Science Workspace.
translation-type: tm+mt
source-git-commit: fcb4088ecac76d10b0cb69b04ad55167f5cdac3e
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Accès aux données à l’aide de Spark

Le document suivant contient des exemples d’accès aux données à l’aide de Spark en vue de les utiliser dans Data Science Workspace. Pour plus d&#39;informations sur l&#39;accès aux données à l&#39;aide des blocs-notes JupyterLab, consultez la documentation sur l&#39;accès aux [données des blocs-notes](../jupyterlab/access-notebook-data.md) JupyterLab.

## Prise en main

L’utilisation [!DNL Spark] nécessite des optimisations de performances qui doivent être ajoutées à la `SparkSession`variable. De plus, vous pouvez également configurer `configProperties` pour que les jeux de données soient lus et écrits ultérieurement.

```scala
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.{DataFrame, SparkSession}

Class Helper {

 /**
   *
   * @param configProperties - Configuration Properties map
   * @param sparkSession     - SparkSession
   * @return                 - DataFrame which is loaded for training
   */

   def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {
            // Read the configs
            val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## Lecture d’un jeu de données

Lorsque vous utilisez Spark, vous avez accès à deux modes de lecture : interactif et par lot.

Le mode interactif crée une connexion JDBC (Java Database Connectivity) [!DNL Query Service] et obtient des résultats par le biais d’un JDBC normal `ResultSet` qui est automatiquement traduit en `DataFrame`un. Ce mode fonctionne de la même manière que la [!DNL Spark] méthode intégrée `spark.read.jdbc()`. Ce mode est destiné uniquement aux petits jeux de données. Si votre jeu de données dépasse 5 millions de lignes, il est conseillé de passer en mode batch.

Le mode par lot utilise [!DNL Query Service]la commande COPY pour générer des jeux de résultats Parquet dans un emplacement partagé. Ces fichiers de Parquet peuvent ensuite être traités plus en détail.

Vous trouverez ci-dessous un exemple de lecture d’un jeu de données en mode interactif :

```scala
  // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "interactive")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
  }
```

De même, vous trouverez ci-dessous un exemple de lecture d’un jeu de données en mode batch :

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### SÉLECTIONNER les colonnes du jeu de données

```scala
df = df.select("column-a", "column-b").show()
```

### Clause DISTINCT

La clause DISTINCT vous permet de récupérer toutes les valeurs distinctes au niveau de la ligne/colonne, en supprimant toutes les valeurs de duplicata de la réponse.

Vous trouverez ci-dessous un exemple d’utilisation de la `distinct()` fonction :

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### Clause WHERE

Le [!DNL Spark] SDK permet deux méthodes de filtrage : Utilisation d&#39;une expression SQL ou filtrage des conditions.

Vous trouverez ci-dessous un exemple d’utilisation de ces fonctions de filtrage :

#### EXPRESSION SQL

```scala
df.where("age > 15")
```

#### Conditions de filtrage

```scala
df.where("age" > 15 || "name" = "Steve")
```

### Clause ORDER BY

La clause ORDER BY permet de trier les résultats reçus selon une colonne spécifiée dans un ordre spécifique (croissant ou décroissant). Dans le [!DNL Spark] SDK, cela se fait en utilisant la `sort()` fonction.

Vous trouverez ci-dessous un exemple d’utilisation de la `sort()` fonction :

```scala
df = df.sort($"column1", $"column2".desc)
```

### Clause LIMIT

La clause LIMIT vous permet de limiter le nombre d&#39;enregistrements reçus du jeu de données.

Vous trouverez ci-dessous un exemple d’utilisation de la `limit()` fonction :

```scala
df = df.limit(100)
```

## Ecriture dans un jeu de données

A l’aide de votre `configProperties` mappage, vous pouvez écrire dans un jeu de données dans l’Experience Platform à l’aide `QSOption`.

```scala
val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## Étapes suivantes

Adobe Experience Platform Data Science Workspace fournit un exemple de recette Scala (Spark) qui utilise les exemples de code ci-dessus pour lire et écrire des données. Si vous souhaitez en savoir plus sur l’utilisation de Spark pour l’accès à vos données, consultez le référentiel [Scala GitHub de](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala)Data Science Workspace.