---
keywords: Experience Platform;accueil;rubriques les plus consultées;accès aux données;sdk spark;api d’accès aux données;recette spark;lire spark;écrire spark
solution: Experience Platform
title: Accès aux données à l’aide de Spark dans Data Science Workspace
type: Tutorial
description: Le document suivant contient des exemples d’accès aux données à l’aide de Spark pour une utilisation dans Data Science Workspace.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Accès aux données à l’aide de Spark dans Data Science Workspace

>[!NOTE]
>
>Data Science Workspace ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs à Data Science Workspace.

Le document suivant contient des exemples d’accès aux données à l’aide de Spark pour une utilisation dans Data Science Workspace. Pour plus d’informations sur l’accès aux données à l’aide des notebooks JupyterLab, consultez la documentation [ sur l’accès aux données des notebooks JupyterLab](../jupyterlab/access-notebook-data.md).

## Prise en main

L’utilisation de [!DNL Spark] nécessite des optimisations de performances qui doivent être ajoutées à `SparkSession`. De plus, vous pouvez également configurer `configProperties` pour qu’il soit possible de lire et d’écrire ultérieurement dans des jeux de données.

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
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## Lecture d’un jeu de données

Lorsque vous utilisez Spark, vous avez accès à deux modes de lecture : interactif et par lot.

Le mode interactif crée une connexion de la base de données Java (JDBC) à [!DNL Query Service] et obtient des résultats par le biais d’une JDBC `ResultSet` standard automatiquement traduite en `DataFrame`. Ce mode fonctionne de la même manière que la méthode [!DNL Spark] intégrée `spark.read.jdbc()`. Ce mode est destiné uniquement aux petits jeux de données. Si votre jeu de données dépasse 5 millions de lignes, il est conseillé de passer en mode batch.

Le mode batch utilise la commande COPY de [!DNL Query Service] pour générer les ensembles de résultats Parquet dans un emplacement partagé. Ces fichiers Parquet peuvent ensuite être traités plus en détail.

Vous trouverez ci-dessous un exemple de lecture d’un jeu de données en mode interactif :

```scala
  // Read the configs
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
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
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### SÉLECTIONNER des colonnes du jeu de données

```scala
df = df.select("column-a", "column-b").show()
```

### Clause DISTINCT

La clause DISTINCT vous permet de récupérer toutes les valeurs distinctes au niveau d’une ligne/colonne, supprimant toutes les valeurs en double de la réponse.

Vous trouverez ci-dessous un exemple d’utilisation de la fonction `distinct()` :

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### Clause WHERE

Le SDK [!DNL Spark] permet deux méthodes de filtrage : l’utilisation d’une expression SQL ou le filtrage par conditions.

Vous trouverez ci-dessous un exemple d’utilisation de ces fonctions de filtrage :

#### Expression SQL

```scala
df.where("age > 15")
```

#### Critères de filtrage

```scala
df.where("age" > 15 || "name" = "Steve")
```

### Clause ORDER BY

La clause ORDER BY permet de trier les résultats reçus par une colonne spécifiée dans un ordre spécifique (croissant ou décroissant). Dans le SDK [!DNL Spark], cette opération est effectuée à l’aide de la fonction `sort()` .

Vous trouverez ci-dessous un exemple d’utilisation de la fonction `sort()` :

```scala
df = df.sort($"column1", $"column2".desc)
```

### Clause LIMIT

La clause LIMIT vous permet de limiter le nombre d’enregistrements reçus du jeu de données.

Vous trouverez ci-dessous un exemple d’utilisation de la fonction `limit()` :

```scala
df = df.limit(100)
```

## Écriture dans un jeu de données

En utilisant votre mappage `configProperties`, vous pouvez écrire dans un jeu de données en Experience Platform à l’aide de `QSOption`.

```scala
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## Étapes suivantes

Adobe Experience Platform Data Science Workspace fournit un exemple de recette Scala (Spark) qui utilise les exemples de code ci-dessus pour lire et écrire des données. Si vous souhaitez en savoir plus sur l’utilisation de Spark pour accéder à vos données, consultez le [référentiel Scala GitHub de Data Science Workspace](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
