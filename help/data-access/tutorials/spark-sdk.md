---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api
solution: Experience Platform
title: SDK Secure Spark Data Access
topic: tutorial
type: Tutorial
description: Le SDK Secure Spark Data Access est un kit de développement logiciel qui permet de lire et d'écrire des jeux de données de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# SDK sécurisé [!DNL Spark Data Access]

Secure [!DNL Spark] SDK [!DNL Data Access] est un kit de développement logiciel qui permet la lecture et l&#39;écriture de jeux de données de Adobe Experience Platform.

## Prise en main

Vous devez avoir suivi le didacticiel [d’authentification](../../tutorials/authentication.md) pour pouvoir accéder aux valeurs permettant d’invoquer le [!DNL Spark] [!DNL Data Access] SDK sécurisé :

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. L’utilisation du [!DNL Spark] SDK nécessite le nom et l’ID du sandbox dans lesquels l’opération aura lieu :

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

## Configuration des Environnements

Le [!DNL Spark] SDK vous attend à fournir des informations d’identification dans les variables d’environnement ou les options de source de données.

| Variable | Valeur |
| -------- | ----- | 
| `SERVICE_TOKEN` | Jeton d’autorisation de service. |
| `SERVICE_API_KEY` | Votre clé d’API de service. En règle générale, il s’agit du même ID de client IMS. |
| `ORG_ID` | Votre `{IMS_ORG}` ID. |
| `USER_TOKEN` | Votre `{ACCESS_TOKEN}` valeur. |

Les autres paramètres de configuration sont les suivants :

| Variable | Valeur |
| -------- | ----- |
| `ENVIRONMENT_NAME` | L&#39;environnement auquel vous essayez de vous connecter. Il peut s’agir de &quot;dev&quot;, &quot;stage&quot; ou &quot;prod&quot;. |
| `SANDBOX_NAME` | Nom du sandbox auquel vous vous connectez. |

Vous pouvez également, outre `ENVIRONMENT_NAME`les variables d’environnement ci-dessus, définir l’une des variables `QSOption`ci-dessous, comme indiqué dans l’exemple ci-dessous :

```scala
val df = spark.read
    .format("com.adobe.platform.query")
    .option(QSOption.userToken, userToken) // same as env var USER_TOKEN
    .option(QSOption.imsOrg, "69A7534C5808063C0A494234@AdobeOrg") // same as env var ORG_ID
    .option(QSOption.apiKey, "acp_foundation_queryService") // same as env var SERVICE_API_KEY
    .option("mode", "interactive")
    .option("query", "SELECT * FROM csv10000row_xcm_001 LIMIT 10")
    .load()
```

## Installation

L’utilisation du [!DNL Spark] SDK nécessite des optimisations de performances qui doivent être ajoutées au `SparkSession`SDK. Vous pouvez les appliquer en utilisant l’une des méthodes suivantes :

Appliquez-la directement à la session SparkSession actuelle :

```scala
import com.adobe.platform.query.QSOptimizations
QSOptimizations.apply(spark)
```

Définissez la conf suivante avant ou lors de la création de SparkSession :

```scala
spark.sql.extensions = com.adobe.platform.query.QSSparkSessionExtensions
```

## Lecture d’un jeu de données

Le [!DNL Spark] SDK prend en charge deux modes de lecture : interactif et par lot.

Le mode interactif crée une connexion JDBC (Java Database Connectivity) [!DNL Query Service] et obtient des résultats par le biais d’un JDBC normal `ResultSet` qui est automatiquement traduit en `DataFrame`un. Ce mode fonctionne de la même manière que la [!DNL Spark] méthode intégrée `spark.read.jdbc()`. Ce mode est destiné uniquement aux petits jeux de données et nécessite uniquement un jeton utilisateur pour l’authentification.

Le mode par lot utilise [!DNL Query Service]la commande COPY pour générer des jeux de résultats Parquet dans un emplacement partagé. Ces fichiers de Parquet peuvent ensuite être traités plus en détail. Ce mode requiert à la fois un jeton utilisateur et un jeton de service avec la `acp.foundation.catalog.credentials` portée.

Vous trouverez ci-dessous un exemple de lecture d’un jeu de données en mode interactif :

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "interactive")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

De même, vous trouverez ci-dessous un exemple de lecture d’un jeu de données en mode batch :

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "batch")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
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

La clause LIMIT permet aux utilisateurs de limiter le nombre d&#39;enregistrements reçus du jeu de données.

Vous trouverez ci-dessous un exemple d’utilisation de la `limit()` fonction :

```scala
df = df.limit(100)
```

## Ecriture dans un jeu de données

Le [!DNL Spark] SDK prend en charge l’écriture de jeux de données. Les utilisateurs devront d&#39;abord récupérer un jeu de données précédent pour écrire dans un nouveau jeu de données.

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", userToken)
      .option("ims-org", "{IMS_ORG}")
      .option("api-key", "{API_KEY}")
      .option("mode", "interactive")
      .option("dataset-id", "{DATASET_ID}")
      .load()

    df.write
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", "{IMS_ORG_ID})
      .option("api-key", "{API_KEY}")
      .option("create-dataset", "{DATASET_ID}")
      .save()
```
