---
keywords: Experience Platform;accueil;rubriques populaires;accès aux données;sdk spark;api data access;recette spark;lire spark;écrire spark
solution: Experience Platform
title: Accès aux données à l’aide de Spark dans le Workspace de science des données
type: Tutorial
description: Le document suivant contient des exemples d’accès aux données à l’aide de Spark en vue de leur utilisation dans Data Science Workspace.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
TQID: https://experienceleague.adobe.com/RUes5Ao3MYLFy-O-qY7OC-iGcrQ4odGdOkkXGKHhGFM
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 478
ht-degree: 1%

---

# Accès aux données à l’aide de Spark dans Data Science Workspace

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

Le document suivant contient des exemples d’accès aux données à l’aide de Spark en vue de leur utilisation dans Data Science Workspace. Pour plus d’informations sur l’accès aux données à l’aide des notebooks JupyterLab, consultez la documentation sur l’accès aux données des notebooks [JupyterLab](../jupyterlab/access-notebook-data.md) .

## Prise en main

L’utilisation de [!DNL Spark] nécessite des optimisations de performances qui doivent être ajoutées à la `SparkSession`. En outre, vous pouvez également configurer `configProperties` pour lire et écrire ultérieurement dans les jeux de données.

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

Lorsque vous utilisez Spark, vous avez accès à deux modes de lecture : interactive et par lots.

Le mode interactif crée une connexion JDBC (Java Database Connectivity) à [!DNL Query Service] et obtient les résultats par le biais d’un `ResultSet` JDBC standard qui est automatiquement traduit en `DataFrame`. Ce mode fonctionne de la même manière que la méthode de [!DNL Spark] intégrée `spark.read.jdbc()`. Ce mode est destiné uniquement aux petits jeux de données. Si votre jeu de données dépasse 5 millions de lignes, il est suggéré de passer en mode batch.

Le mode batch utilise la commande COPY de [!DNL Query Service] pour générer des jeux de résultats Parquet dans un emplacement partagé. Ces fichiers Parquet peuvent ensuite être traités de manière plus approfondie.

Voici un exemple de lecture d’un jeu de données en mode interactif :

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

De même, un exemple de lecture d’un jeu de données en mode batch est visible ci-dessous :

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

### SÉLECTIONNER des colonnes dans le jeu de données

```scala
df = df.select("column-a", "column-b").show()
```

### Clause DISTINCT

La clause DISTINCT vous permet de récupérer toutes les valeurs distinctes au niveau de la ligne/colonne, en supprimant toutes les valeurs en double de la réponse.

Vous trouverez ci-dessous un exemple d’utilisation de la fonction `distinct()` :

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### Clause WHERE

Le SDK [!DNL Spark] permet deux méthodes de filtrage : à l’aide d’une expression SQL ou par filtrage au travers de conditions.

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

La clause ORDER BY permet de trier les résultats reçus selon une colonne spécifiée dans un ordre spécifique (croissant ou décroissant). Dans le SDK [!DNL Spark], cette opération s’effectue à l’aide de la fonction `sort()` .

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

À l’aide de votre mappage `configProperties`, vous pouvez écrire dans un jeu de données dans Experience Platform à l’aide de `QSOption`.

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

Adobe Experience Platform Data Science Workspace fournit un exemple de recette Scala (Spark) qui utilise les exemples de code ci-dessus pour lire et écrire des données. Si vous souhaitez en savoir plus sur l’utilisation de Spark pour accéder à vos données, consultez la section [Référentiel GitHub de Workspace Scala de science des données](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
