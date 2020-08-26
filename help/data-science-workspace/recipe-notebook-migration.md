---
keywords: Experience Platform;Data Science Workspace;popular topics
solution: Experience Platform
title: Guides de migration des recettes et des blocs-notes
topic: Tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '3311'
ht-degree: 1%

---


# Guides de migration des recettes et des blocs-notes

>[!NOTE]
>Les ordinateurs portables et les recettes utilisant [!DNL Python]/R ne sont pas concernés. La migration ne s&#39;applique qu&#39;aux recettes et cahiers PySpark/[!DNL Spark] (2.3).

Les guides suivants décrivent les étapes et les informations requises pour migrer des recettes et des cahiers de notes existants.

- [Guides de migration des recettes](#recipe-migration)
- [Guides de migration vers les ordinateurs portables](#notebook-migration)

## Guides de migration des recettes {#recipe-migration}

Des modifications récentes pour [!DNL Data Science Workspace] exiger la mise à jour des recettes existantes [!DNL Spark] et PySpark. Utilisez les workflows suivants pour faciliter la transition de vos recettes.

- [Guide de migration Spark](#spark-migration-guide)
   - [Modifier la manière dont vous lisez et écrivez des jeux de données](#read-write-recipe-spark)
   - [Télécharger l&#39;exemple de recette](#download-sample-spark)
   - [ajouter le fichier d&#39;ancrage](#add-dockerfile-spark)
   - [Vérifier les dépendances](#change-dependencies-spark)
   - [Préparation des scripts d’ancrage](#prepare-docker-spark)
   - [créer la recette avec un docker](#create-recipe-spark)
- [Guide de migration PySpark](#pyspark-migration-guide)
   - [Modifier la manière dont vous lisez et écrivez des jeux de données](#pyspark-read-write)
   - [Télécharger l&#39;exemple de recette](#pyspark-download-sample)
   - [ajouter le fichier d&#39;ancrage](#pyspark-add-dockerfile)
   - [Préparation des scripts d’ancrage](#pyspark-prepare-docker)
   - [créer la recette avec un docker](#pyspark-create-recipe)

## [!DNL Spark] guide de migration {#spark-migration-guide}

L&#39;artefact de recette généré par les étapes de création est désormais une image Docker qui contient votre fichier binaire .jar. De plus, la syntaxe utilisée pour lire et écrire des jeux de données à l&#39;aide du [!DNL Platform] SDK a été modifiée et nécessite la modification du code de la recette.

La vidéo suivante est conçue pour aider à mieux comprendre les changements nécessaires pour [!DNL Spark] les recettes :

>[!VIDEO](https://video.tv.adobe.com/v/33243)

### Lecture et écriture de jeux de données ([!DNL Spark]) {#read-write-recipe-spark}

Avant de créer l&#39;image Docker, consultez les exemples de lecture et d&#39;écriture de jeux de données dans le [!DNL Platform] SDK, fournis dans les sections ci-dessous. Si vous convertissez des recettes existantes, votre code [!DNL Platform] SDK doit être mis à jour.

#### Lecture d’un jeu de données

Cette section décrit les modifications nécessaires à la lecture d&#39;un jeu de données et utilise l&#39;exemple [helper.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/helper/Helper.scala) , fourni par Adobe.

**Ancienne manière de lire un jeu de données**

```scala
 var df = sparkSession.read.format("com.adobe.platform.dataset")
    .option(DataSetOptions.orgId, orgId)
    .option(DataSetOptions.serviceToken, serviceToken)
    .option(DataSetOptions.userToken, userToken)
    .option(DataSetOptions.serviceApiKey, apiKey)
    .load(dataSetId)
```

**Nouvelle façon de lire un jeu de données**

Avec les mises à jour des [!DNL Spark] recettes, un certain nombre de valeurs doivent être ajoutées et modifiées. Tout d&#39;abord, `DataSetOptions` n&#39;est plus utilisé. Replace `DataSetOptions` with `QSOption`. En outre, de nouveaux `option` paramètres sont requis. Les deux `QSOption.mode` et `QSOption.datasetId` sont nécessaires. Enfin, `orgId` et `serviceApiKey` doit être remplacé par `imsOrg` et `apiKey`. Examinez l&#39;exemple suivant pour comparer la lecture des jeux de données :

```scala
import com.adobe.platform.query.QSOption
var df = sparkSession.read.format("com.adobe.platform.query")
  .option(QSOption.userToken", {userToken})
  .option(QSOption.serviceToken, {serviceToken})
  .option(QSOption.imsOrg, {orgId})
  .option(QSOption.apiKey, {apiKey})
  .option(QSOption.mode, "interactive")
  .option(QSOption.datasetId, {dataSetId})
  .load()
```

>[!TIP]
> Le mode interactif expire si les requêtes durent plus de 10 minutes. Si vous ingérez plus de quelques gigaoctets de données, il est recommandé de passer en mode &quot;batch&quot;. Le mode de traitement par lots prend plus de temps à début, mais il peut gérer des ensembles de données plus volumineux.

#### Écrire dans un jeu de données

Cette section décrit les modifications nécessaires à la création d&#39;un jeu de données à l&#39;aide de l&#39;exemple [ScoringDataSaver.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/ScoringDataSaver.scala) fourni par Adobe.

**Ancienne méthode d&#39;écriture d&#39;un jeu de données**

```scala
df.write.format("com.adobe.platform.dataset")
    .option(DataSetOptions.orgId, orgId)
    .option(DataSetOptions.serviceToken, serviceToken)
    .option(DataSetOptions.userToken, userToken)
    .option(DataSetOptions.serviceApiKey, apiKey)
    .save(scoringResultsDataSetId)
```

**Nouvelle méthode d&#39;écriture d&#39;un jeu de données**

Avec les mises à jour des [!DNL Spark] recettes, un certain nombre de valeurs doivent être ajoutées et modifiées. Tout d&#39;abord, `DataSetOptions` n&#39;est plus utilisé. Replace `DataSetOptions` with `QSOption`. En outre, de nouveaux `option` paramètres sont requis. `QSOption.datasetId` est nécessaire et remplace la nécessité de charger le `{dataSetId}` dans `.save()`. Enfin, `orgId` et `serviceApiKey` doit être remplacé par `imsOrg` et `apiKey`. Consultez l&#39;exemple suivant pour obtenir une comparaison sur l&#39;écriture de jeux de données :

```scala
import com.adobe.platform.query.QSOption
df.write.format("com.adobe.platform.query")
  .option(QSOption.userToken", {userToken})
  .option(QSOption.serviceToken, {serviceToken})
  .option(QSOption.imsOrg, {orgId})
  .option(QSOption.apiKey, {apiKey})
  .option(QSOption.datasetId, {dataSetId})
  .save()
```

### compresser les fichiers source basés sur le dossier ([!DNL Spark]) {#package-docker-spark}

Début en accédant au répertoire où se trouve votre recette.

Les sections suivantes utilisent la nouvelle recette Ventes au détail de Scala qui se trouve dans le référentiel [public Github de](https://github.com/adobe/experience-platform-dsw-reference)Data Science Workspace.

### Télécharger l&#39;exemple de recette ([!DNL Spark]) {#download-sample-spark}

L&#39;exemple de recette contient des fichiers qui doivent être copiés vers votre recette existante. Pour cloner le Github public qui contient tous les exemples de recettes, entrez ce qui suit en terminal :

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

La recette Scala se trouve dans le répertoire suivant `experience-platform-dsw-reference/recipes/scala/retail`.

### ajouter le fichier Dockerfile ([!DNL Spark]) {#add-dockerfile-spark}

Un nouveau fichier est nécessaire dans votre dossier de recette pour utiliser le flux de travail basé sur le docker. Copiez et collez le fichier Dockerfile du dossier des recettes situé dans `experience-platform-dsw-reference/recipes/scala/Dockerfile`. Vous pouvez également copier et coller le code ci-dessous dans un nouveau fichier appelé `Dockerfile`.

>[!IMPORTANT]
> L&#39;exemple de fichier jar illustré ci-dessous `ml-retail-sample-spark-*-jar-with-dependencies.jar` doit être remplacé par le nom du fichier jar de votre recette.

```scala
FROM adobe/acp-dsw-ml-runtime-spark:0.0.1

COPY target/ml-retail-sample-spark-*-jar-with-dependencies.jar /application.jar
```

### Modifier les dépendances ([!DNL Spark]) {#change-dependencies-spark}

Si vous utilisez une recette existante, des modifications sont requises dans le fichier pom.xml pour les dépendances. Remplacez la version de dépendance model-authoring-sdk par 2.0.0. Ensuite, mettez à jour la [!DNL Spark] version du fichier pom vers 2.4.3 et la version Scala vers 2.11.12.

```json
<groupId>com.adobe.platform.ml</groupId>
<artifactId>authoring-sdk_2.11</artifactId>
<version>2.0.0</version>
<classifier>jar-with-dependencies</classifier>
```

### Préparation de vos scripts Docker ([!DNL Spark]) {#prepare-docker-spark}

[!DNL Spark] les recettes n&#39;utilisent plus d&#39;artefacts binaires et nécessitent à la place la création d&#39;une image Docker. Si vous ne l&#39;avez pas fait, [téléchargez et installez Docker](https://www.docker.com/products/docker-desktop).

Dans l&#39;exemple de recette Scala fourni, vous pouvez trouver les scripts `login.sh` et `build.sh` se trouver dans `experience-platform-dsw-reference/recipes/scala/` . Copiez et collez ces fichiers dans votre recette existante.

Votre structure de dossiers doit maintenant ressembler à l’exemple suivant (les fichiers récemment ajoutés sont mis en surbrillance) :

![structure de dossiers](./images/migration/scala-folder.png)

L&#39;étape suivante consiste à suivre les fichiers source du [package dans un didacticiel de recette](./models-recipes/package-source-files-recipe.md) . Ce didacticiel comporte une section qui décrit la création d&#39;une image de docker pour une recette Scala (Spark). Une fois l&#39;opération terminée, vous recevez l&#39;image du Docker dans un Registre de Conteneur Azure avec l&#39;URL de l&#39;image correspondante.

### Création d’une recette ([!DNL Spark]) {#create-recipe-spark}

Pour créer une recette, vous devez d&#39;abord compléter le didacticiel sur les fichiers [source du](./models-recipes/package-source-files-recipe.md) package et disposer de l&#39;URL de l&#39;image du dossier. Vous pouvez créer une recette à l&#39;aide de l&#39;interface utilisateur ou de l&#39;API.

Pour créer votre recette à l&#39;aide de l&#39;interface utilisateur, suivez le didacticiel [d&#39;importation d&#39;une recette emballée (IU)](./models-recipes/import-packaged-recipe-ui.md) pour Scala.

Pour créer votre recette à l&#39;aide de l&#39;API, suivez le didacticiel [d&#39;importation de recette (API)](./models-recipes/import-packaged-recipe-api.md) emballée pour Scala.

## Guide de migration PySpark {#pyspark-migration-guide}

L&#39;artefact de recette généré par les étapes de création est maintenant une image Docker qui contient votre fichier binaire .egg. De plus, la syntaxe utilisée pour lire et écrire des jeux de données à l&#39;aide du [!DNL Platform] SDK a été modifiée et nécessite la modification du code de la recette.

La vidéo suivante est conçue pour aider à mieux comprendre les modifications requises pour les recettes PySpark :

>[!VIDEO](https://video.tv.adobe.com/v/33048?learn=on&quality=12)

### Lecture et écriture de jeux de données (PySpark) {#pyspark-read-write}

Avant de créer l&#39;image Docker, consultez les exemples de lecture et d&#39;écriture de jeux de données dans le [!DNL Platform] SDK, fournis dans les sections ci-dessous. Si vous convertissez des recettes existantes, votre code [!DNL Platform] SDK doit être mis à jour.

#### Lecture d’un jeu de données

Cette section décrit les modifications nécessaires à la lecture d&#39;un jeu de données à l&#39;aide de l&#39;exemple [helper.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/pyspark/pysparkretailapp/helper.py) fourni par Adobe.

**Ancienne manière de lire un jeu de données**

```python
dataset_options = get_dataset_options(spark.sparkContext)
pd = spark.read.format("com.adobe.platform.dataset") 
  .option(dataset_options.serviceToken(), service_token) 
  .option(dataset_options.userToken(), user_token) 
  .option(dataset_options.orgId(), org_id) 
  .option(dataset_options.serviceApiKey(), api_key)
  .load(dataset_id)
```

**Nouvelle façon de lire un jeu de données**

Avec les mises à jour des [!DNL Spark] recettes, un certain nombre de valeurs doivent être ajoutées et modifiées. Tout d&#39;abord, `DataSetOptions` n&#39;est plus utilisé. Replace `DataSetOptions` with `qs_option`. En outre, de nouveaux `option` paramètres sont requis. Les deux `qs_option.mode` et `qs_option.datasetId` sont nécessaires. Enfin, `orgId` et `serviceApiKey` doit être remplacé par `imsOrg` et `apiKey`. Examinez l&#39;exemple suivant pour comparer la lecture des jeux de données :

```python
qs_option = spark_context._jvm.com.adobe.platform.query.QSOption
pd = sparkSession.read.format("com.adobe.platform.query") 
  .option(qs_option.userToken, {userToken}) 
  .option(qs_option.serviceToken, {serviceToken}) 
  .option(qs_option.imsOrg, {orgId}) 
  .option(qs_option.apiKey, {apiKey}) 
  .option(qs_option.mode, "interactive") 
  .option(qs_option.datasetId, {dataSetId}) 
  .load()
```

>[!TIP]
> Le mode interactif expire si les requêtes durent plus de 10 minutes. Si vous ingérez plus de quelques gigaoctets de données, il est recommandé de passer en mode &quot;batch&quot;. Le mode de traitement par lots prend plus de temps à début, mais il peut gérer des ensembles de données plus volumineux.

#### Écrire dans un jeu de données

Cette section décrit les modifications nécessaires à la création d&#39;un jeu de données à l&#39;aide de l&#39;exemple [data_saver.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/pyspark/pysparkretailapp/data_saver.py) fourni par Adobe.

**Ancienne méthode d&#39;écriture d&#39;un jeu de données**

```python
df.write.format("com.adobe.platform.dataset")
  .option(DataSetOptions.orgId, orgId)
  .option(DataSetOptions.serviceToken, serviceToken)
  .option(DataSetOptions.userToken, userToken)
  .option(DataSetOptions.serviceApiKey, apiKey)
  .save(scoringResultsDataSetId)
```

**Nouvelle méthode d&#39;écriture d&#39;un jeu de données**

Avec les mises à jour des recettes PySpark, un certain nombre de valeurs doivent être ajoutées et modifiées. Tout d&#39;abord, `DataSetOptions` n&#39;est plus utilisé. Replace `DataSetOptions` with `qs_option`. En outre, de nouveaux `option` paramètres sont requis.  `qs_option.datasetId` est nécessaire et remplace la nécessité de charger le `{dataSetId}` dans `.save()` . Enfin, `orgId` et `serviceApiKey` doit être remplacé par `imsOrg` et `apiKey`. Examinez l&#39;exemple suivant pour comparer la lecture des jeux de données :

```python
qs_option = spark_context._jvm.com.adobe.platform.query.QSOption
scored_df.write.format("com.adobe.platform.query") 
  .option(qs_option.userToken, {userToken}) 
  .option(qs_option.serviceToken, {serviceToken}) 
  .option(qs_option.imsOrg, {orgId}) 
  .option(qs_option.apiKey, {apiKey}) 
  .option(qs_option.datasetId, {dataSetId}) 
  .save()
```

### Fichiers source basés sur le dossier d’assemblage (PySpark) {#pyspark-package-docker}

Début en accédant au répertoire où se trouve votre recette.

Pour cet exemple, la nouvelle recette Ventes au détail de PySpark est utilisée et se trouve dans le référentiel [Github public de](https://github.com/adobe/experience-platform-dsw-reference)Data Science Workspace.

### Télécharger l&#39;exemple de recette (PySpark) {#pyspark-download-sample}

L&#39;exemple de recette contient des fichiers qui doivent être copiés vers votre recette existante. Pour cloner le public [!DNL Github] qui contient tous les exemples de recettes, entrez ce qui suit en terminal.

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

La recette PySpark se trouve dans le répertoire suivant `experience-platform-dsw-reference/recipes/pyspark`.

### ajouter le fichier Dockerfile (PySpark) {#pyspark-add-dockerfile}

Un nouveau fichier est nécessaire dans votre dossier de recette pour utiliser le flux de travail basé sur le docker. Copiez et collez le fichier Dockerfile du dossier des recettes situé dans `experience-platform-dsw-reference/recipes/pyspark/Dockerfile`. Vous pouvez également copier et coller le code ci-dessous et créer un nouveau fichier appelé `Dockerfile`.

>[!IMPORTANT]
> L&#39;exemple de fichier d&#39;oeufs illustré ci-dessous `pysparkretailapp-*.egg` doit être remplacé par le nom du fichier d&#39;oeufs de votre recette.

```scala
FROM adobe/acp-dsw-ml-runtime-pyspark:0.0.1
RUN mkdir /recipe

COPY . /recipe

RUN cd /recipe && \
    ${PYTHON} setup.py clean install && \
    rm -rf /recipe

RUN cp /databricks/conda/envs/${DEFAULT_DATABRICKS_ROOT_CONDA_ENV}/lib/python3.6/site-packages/pysparkretailapp-*.egg /application.egg
```

### Préparation de vos scripts Docker (PySpark) {#pyspark-prepare-docker}

Les recettes PySpark n&#39;utilisent plus d&#39;artefacts binaires et nécessitent à la place la création d&#39;une image Docker. Si vous ne l&#39;avez pas fait, téléchargez et installez [Docker](https://www.docker.com/products/docker-desktop).

Dans l&#39;exemple de recette fournie par PySpark, vous pouvez trouver les scripts `login.sh` et les `build.sh` trouver dans `experience-platform-dsw-reference/recipes/pyspark` . Copiez et collez ces fichiers dans votre recette existante.

Votre structure de dossiers doit maintenant ressembler à l’exemple suivant (les fichiers récemment ajoutés sont mis en surbrillance) :

![structure de dossiers](./images/migration/folder.png)

Votre recette est maintenant prête à être créée à l&#39;aide d&#39;une image Docker. L&#39;étape suivante consiste à suivre les fichiers source du [package dans un didacticiel de recette](./models-recipes/package-source-files-recipe.md) . Ce didacticiel comporte une section qui décrit la création d&#39;une image de docker pour une recette PySpark (Spark 2.4). Une fois l&#39;opération terminée, vous recevez l&#39;image du Docker dans un Registre de Conteneur Azure avec l&#39;URL de l&#39;image correspondante.

### Créer une recette (PySpark) {#pyspark-create-recipe}

Pour créer une recette, vous devez d&#39;abord compléter le didacticiel sur les fichiers [source du](./models-recipes/package-source-files-recipe.md) package et disposer de l&#39;URL de l&#39;image du dossier. Vous pouvez créer une recette à l&#39;aide de l&#39;interface utilisateur ou de l&#39;API.

Pour créer votre recette à l&#39;aide de l&#39;interface utilisateur, suivez le didacticiel [d&#39;importation d&#39;une recette emballée (IU)](./models-recipes/import-packaged-recipe-ui.md) pour PySpark.

Pour créer votre recette à l&#39;aide de l&#39;API, suivez le didacticiel [d&#39;importation de recette (API)](./models-recipes/import-packaged-recipe-api.md) emballée pour PySpark.

## Guides de migration vers les ordinateurs portables {#notebook-migration}

Les dernières modifications apportées aux [!DNL JupyterLab] portables nécessitent la mise à jour de vos PC portables PySpark et [!DNL Spark] 2.3 vers la version 2.4. Grâce à cette modification, [!DNL JupyterLab Launcher] a été mis à jour avec de nouveaux PC portables de démarrage. Pour obtenir un guide détaillé sur la conversion de vos blocs-notes, sélectionnez l&#39;un des guides suivants :

- [Guide de migration de PySpark 2.3 à 2.4](#pyspark-notebook-migration)
- [Guide de migration de Spark 2.3 vers Spark 2.4 (Scala)](#spark-notebook-migration)

La vidéo suivante est conçue pour aider à mieux comprendre les modifications requises pour [!DNL JupyterLab Notebooks]:

>[!VIDEO](https://video.tv.adobe.com/v/33444?quality=12&learn=on)

## Guide de migration des ordinateurs portables PySpark 2.3 à 2.4 {#pyspark-notebook-migration}

Avec l&#39;introduction de PySpark 2.4 à [!DNL JupyterLab Notebooks], de nouveaux [!DNL Python] portables avec PySpark 2.4 utilisent maintenant le noyau [!DNL Python] 3 au lieu du noyau PySpark 3. Cela signifie que le code existant s’exécutant sur PySpark 2.3 n’est pas pris en charge dans PySpark 2.4.

>[!IMPORTANT]
>
>PySpark 2.3 est obsolète et doit être supprimé dans une version ultérieure. Tous les exemples existants sont définis pour être remplacés par des exemples PySpark 2.4.

Pour convertir vos blocs-notes PySpark 3 ([!DNL Spark] 2.3) existants en [!DNL Spark] 2.4, suivez les exemples ci-dessous :

### Noyau

Les portables PySpark 3 ([!DNL Spark] 2.4) utilisent le noyau Python 3 plutôt que le noyau PySpark déconseillé utilisé dans les portables PySpark 3 (Spark 2.3 - désapprouvé).

Pour confirmer ou modifier le noyau dans l&#39; [!DNL JupyterLab] interface utilisateur, sélectionnez le bouton du noyau situé dans la barre de navigation supérieure droite de votre bloc-notes. Si vous utilisez l&#39;un des portables de lanceur prédéfinis, le noyau est présélectionné. L&#39;exemple ci-dessous utilise le démarrage du bloc-notes[!DNL Spark] Agrégation *PySpark 3 (* 2.4).

![vérifier le noyau](./images/migration/pyspark-migration/check-kernel.png)

La sélection du menu déroulant ouvre une liste de noyaux disponibles.

![sélectionner le noyau](./images/migration/pyspark-migration/kernel-click.png)

![liste déroulante du noyau](./images/migration/pyspark-migration/select-kernel.png)

Pour les blocs-notes PySpark 3 ([!DNL Spark] 2.4), sélectionnez le noyau Python 3 et confirmez en cliquant sur le bouton **Sélectionner** .

![confirmer le noyau](./images/migration/pyspark-migration/confirm-kernel.png)

## Initialisation de sparkSession

Tous les [!DNL Spark] ordinateurs portables 2.4 nécessitent que vous initialisiez la session avec le nouveau code standard.

<table>
  <th>Ordinateur portable</th>
  <th>PySpark 3 ([!DNL Spark] 2.3 - désapprouvée)</th>
  <th>PySpark 3 ([!DNL Spark] 2.4)</th>
  <tr>
  <th>Noyau</th>
  <td align="center">PySpark 3</td>
  <td align="center">Python 3</td>
  </tr>
  <tr>
  <th>Code</th>
  <td>
  <pre class="JSON language-JSON hljs">
  [ !étincelle DNL]
</pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
à partir de pyspark.sql, importez SparkSessionspark = SparkSession.builder.getOrCreate()
</pre>
  </td>
  </tr>
</table>

Les images suivantes mettent en évidence les différences de configuration pour PySpark 2.3 et PySpark 2.4. Cet exemple utilise les blocs-notes de démarrage *Aggregation* fournis dans [!DNL JupyterLab Launcher].

**Exemple de configuration pour la version 2.3 (obsolète)**

![config 1](./images/migration/pyspark-migration/2.3-config.png)![config 2](./images/migration/pyspark-migration/2.3-config-import.png)

**Exemple de configuration pour la version 2.4**

![config 3](./images/migration/pyspark-migration/2.4-config.png)

## Utilisation de la magie %dataset {#magic}

Avec l&#39;introduction de la [!DNL Spark] 2.4, `%dataset` la magie personnalisée est fournie pour l&#39;utilisation dans les nouveaux portables PySpark 3 ([!DNL Spark] 2.4) (noyau[!DNL Python] 3).

**Utilisation**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Description**

Commande [!DNL Data Science Workspace] magique personnalisée pour lire ou écrire un jeu de données à partir d&#39;un [!DNL Python] bloc-notes (noyau[!DNL Python] 3).

- **{action}**: Type d’action à exécuter sur le jeu de données. Deux actions sont disponibles &quot;read&quot; ou &quot;write&quot;.
- **—datasetId {id}**: Utilisé pour fournir l&#39;identifiant du jeu de données à lire ou à écrire. Il s&#39;agit d&#39;un argument obligatoire.
- **—dataFrame {df}**: La base de données des pandas. Il s&#39;agit d&#39;un argument obligatoire.
   - Lorsque l&#39;action est &quot;read&quot;, {df} est la variable où les résultats de l&#39;opération de lecture du jeu de données sont disponibles.
   - Lorsque l&#39;action est &quot;write&quot;, ce dataframe {df} est écrit dans le dataset.
- **—mode (facultatif)**: Les paramètres autorisés sont &quot;batch&quot; et &quot;interactive&quot;. Par défaut, le mode est défini sur &quot;interactif&quot;. Il est recommandé d’utiliser le mode &quot;batch&quot; lors de la lecture de grandes quantités de données.

**Exemples**

- **Exemple** de lecture : `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
- **Exemple** d&#39;écriture : `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

## Charger dans un cadre de données dans LocalContext

Avec l&#39;introduction de la [!DNL Spark] 2.4, la magie [`%dataset`](#magic) personnalisée est fournie. L&#39;exemple suivant illustre les principales différences de chargement de la base de données dans les blocs-notes PySpark ([!DNL Spark] 2.3) et PySpark ([!DNL Spark] 2.4) :

**Utilisation de PySpark 3 ([!DNL Spark]2.3 - désapprouvée) - Noyau PySpark 3**

```python
dataset_options = sc._jvm.com.adobe.platform.dataset.DataSetOptions
pd0 = spark.read.format("com.adobe.platform.dataset")
  .option(dataset_options.orgId(), "310C6D375BA5248F0A494212@AdobeOrg")
  .load("5e68141134492718af974844")
```

**Utilisation de PySpark 3 ([!DNL Spark]2.4) - noyau Python 3**

```python
%dataset read --datasetId 5e68141134492718af974844 --dataFrame pd0
```

| Élément | Description |
| ------- | ----------- |
| pd0 | Nom de l’objet de dataframe pandas à utiliser ou à créer. |
| [%dataset](#magic) | Magie personnalisée pour l&#39;accès aux données dans le noyau [!DNL Python] 3. |

Les images suivantes mettent en évidence les principales différences de chargement des données pour PySpark 2.3 et PySpark 2.4. Cet exemple utilise les blocs-notes de démarrage *Aggregation* fournis dans [!DNL JupyterLab Launcher].

**Chargement de données dans PySpark 2.3 (jeu de données Luma) - obsolète**

![Charger 1](./images/migration/pyspark-migration/2.3-load.png)

**Chargement de données dans PySpark 2.4 (jeu de données Luma)**

Avec PySpark 3 (Spark 2.4) `sc = spark.sparkContext` est défini lors du chargement.

![Charger 1](./images/migration/pyspark-migration/2.4-load.png)

**Chargement[!DNL Experience Cloud Platform]de données dans PySpark 2.3 - obsolète**

![Charger 2](./images/migration/pyspark-migration/2.3-load-alt.png)

**Chargement[!DNL Experience Cloud Platform]des données dans PySpark 2.4**

Avec PySpark 3 ([!DNL Spark] 2.4), il n&#39; `org_id` est plus nécessaire de définir la variable `dataset_id` et non plus. De plus, `df = spark.read.format` a été remplacé par une magie personnalisée [`%dataset`](#magic) pour faciliter la lecture et l&#39;écriture des jeux de données.

![Charger 2](./images/migration/pyspark-migration/2.4-load-alt.png)

| Élément | description |
| ------- | ----------- |
| [%dataset](#magic) | Magie personnalisée pour l&#39;accès aux données dans le noyau [!DNL Python] 3. |

>[!TIP]
>
>—mode peut être défini sur `interactive` ou `batch`. La valeur par défaut de —mode est `interactive`. Il est recommandé d’utiliser `batch` le mode lors de la lecture de grandes quantités de données.

## Création d’un cadre de données local

Avec PySpark 3 ([!DNL Spark] 2.4), `%%` sparkMagic n&#39;est plus pris en charge. Les opérations suivantes ne peuvent plus être utilisées :

- `%%help`
- `%%info`
- `%%cleanup`
- `%%delete`
- `%%configure`
- `%%local`

Le tableau suivant présente les modifications nécessaires à la conversion des requêtes `%%sql` sparkmiracle :

<table>
  <th>Ordinateur portable</th>
  <th>PySpark 3 ([!DNL Spark] 2.3 - désapprouvée)</th>
  <th>PySpark 3 ([!DNL Spark] 2.4)</th>
  <tr>
  <th>Noyau</th>
  <td align="center">PySpark 3</td>
  <td align="center">[ ! DNL Python] 3</td>
  </tr>
  <tr>
  <th>Code</th>
      <td>
         <pre class="JSON language-JSON hljs">%%sql -o dfselect * from sparkdf
</pre>
         <pre class="JSON language-JSON hljs"> %%sql -o df -n limitselect * from sparkdf
</pre>
         <pre class="JSON language-JSON hljs">%%sql -o df -qselect * from sparkdf
</pre>
         <pre class="JSON language-JSON hljs"> %%sql -o df -r fractionselect * from sparkdf
</pre>
      </td>
      <td>
         <pre class="JSON language-JSON hljs">
df = spark.sql(''' SELECT * FROM sparkdf''')
</pre>
         <pre class="JSON language-JSON hljs">
df = spark.sql(''' SELECT * FROM sparkdf LIMIT limit'')
</pre>
         <pre class="JSON language-JSON hljs">
df = spark.sql(''' SELECT * FROM sparkdf LIMIT limit'')
</pre>
         <pre class="JSON language-JSON hljs">
sample_df = df.sample(fraction)
</pre>
      </td>
   </tr>
</table>

>[!TIP]
>
>Vous pouvez également spécifier un échantillon de semences facultatif, tel qu’un booléen avec remplacement, une fraction de doublon ou une graine longue.

Les images suivantes mettent en évidence les principales différences de création d&#39;une base de données locale dans PySpark 2.3 et PySpark 2.4. Cet exemple utilise les blocs-notes de démarrage *Agrégation* fournis dans [!DNL JupyterLab Launcher].

**Création d&#39;une base de données locale PySpark 2.3 - obsolète**

![dataframe 1](./images/migration/pyspark-migration/2.3-dataframe.png)

**Création d’une base de données locale PySpark 2.4**

Avec PySpark 3 ([!DNL Spark] 2.4) `%%sql` SparkMagic n’est plus pris en charge et a été remplacé par le texte suivant :

![dataframe 2](./images/migration/pyspark-migration/2.4-dataframe.png)

## Écrire dans un jeu de données

Avec l&#39;introduction de la [!DNL Spark] 2.4, la magie [`%dataset`](#magic) personnalisée est fournie ce qui rend l&#39;écriture des jeux de données plus propre. Pour écrire dans un jeu de données, utilisez l&#39;exemple 2.4 [!DNL Spark] :

**Utilisation de PySpark 3 ([!DNL Spark]2.3 - désapprouvée) - Noyau PySpark 3**

```python
userToken = spark.sparkContext.getConf().get("spark.yarn.appMasterEnv.USER_TOKEN")
serviceToken = spark.sparkContext.getConf().get("spark.yarn.appMasterEnv.SERVICE_TOKEN")
serviceApiKey = spark.sparkContext.getConf().get("spark.yarn.appMasterEnv.SERVICE_API_KEY")

dataset_options = sc._jvm.com.adobe.platform.dataset.DataSetOptions

pd0.write.format("com.adobe.platform.dataset")
  .option(dataset_options.orgId(), "310C6D375BA5248F0A494212@AdobeOrg")
  .option(dataset_options.userToken(), userToken)
  .option(dataset_options.serviceToken(), serviceToken)
  .option(dataset_options.serviceApiKey(), serviceApiKey)
  .save("5e68141134492718af974844")
```

**Utilisation de PySpark 3 ([!DNL Spark]2.4) -[!DNL Python]3 noyau**

```python
%dataset write --datasetId 5e68141134492718af974844 --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

| Élément | description |
| ------- | ----------- |
| pd0 | Nom de l’objet de dataframe pandas à utiliser ou à créer. |
| [%dataset](#magic) | Magie personnalisée pour l&#39;accès aux données dans le noyau [!DNL Python] 3. |

>[!TIP]
>
>—mode peut être défini sur `interactive` ou `batch`. La valeur par défaut de —mode est `interactive`. Il est recommandé d’utiliser `batch` le mode lors de la lecture de grandes quantités de données.

Les illustrations suivantes mettent en évidence les principales différences d&#39;écriture des données dans [!DNL Platform] PySpark 2.3 et PySpark 2.4. Cet exemple utilise les blocs-notes de démarrage *Agrégation* fournis dans [!DNL JupyterLab Launcher].

**Rédaction de données dans[!DNL Platform]PySpark 2.3 - obsolète**

![dataframe 1](./images/migration/pyspark-migration/2.3-write.png)![](./images/migration/pyspark-migration/2.3-write-2.png)dataframe 1![dataframe 1](./images/migration/pyspark-migration/2.3-write-3.png)

**Rédaction de données dans[!DNL Platform]PySpark 2.4**

Avec PySpark 3 ([!DNL Spark] 2.4), la magie `%dataset` personnalisée élimine la nécessité de définir des valeurs telles que `userToken`, `serviceToken`, `serviceApiKey`et `.option`. En outre, `orgId` il n&#39;est plus nécessaire de définir ce qui suit.

![dataframe 2](./images/migration/pyspark-migration/2.4-write.png)![dataframe 2](./images/migration/pyspark-migration/2.4-write-2.png)

## [!DNL Spark] Guide de migration des ordinateurs portables 2.3 à [!DNL Spark] 2.4 (Scala) {#spark-notebook-migration}

Avec l&#39;introduction de [!DNL Spark] 2.4 à [!DNL JupyterLab Notebooks], les portables [!DNL Spark] existants ([!DNL Spark] 2.3) utilisent maintenant le noyau Scala au lieu du noyau [!DNL Spark] . Cela signifie que le code existant s’exécutant sur [!DNL Spark] ([!DNL Spark] 2.3) n’est pas pris en charge dans Scala ([!DNL Spark] 2.4). De plus, tous les nouveaux [!DNL Spark] portables doivent utiliser Scala ([!DNL Spark] 2.4) dans le [!DNL JupyterLab Launcher].

>[!IMPORTANT]
>
>[!DNL Spark] ([!DNL Spark] 2.3) est obsolète et doit être supprimé dans une version ultérieure. Tous les exemples existants sont définis pour être remplacés par des exemples Scala ([!DNL Spark] 2.4).

Pour convertir vos blocs-notes [!DNL Spark] ([!DNL Spark] 2.3) existants en Scala ([!DNL Spark] 2.4), suivez les exemples ci-dessous :

## Noyau

Les portables Scala (Spark 2.4) utilisent le noyau Scala plutôt que le [!DNL Spark] noyau obsolète utilisé dans les [!DNL Spark] portables ([!DNL Spark] 2.3 - désapprouvé).

Pour confirmer ou modifier le noyau dans l&#39; [!DNL JupyterLab] interface utilisateur, sélectionnez le bouton du noyau situé dans la barre de navigation supérieure droite de votre bloc-notes. La fenêtre contextuelle *Sélectionner le noyau* s&#39;affiche. Si vous utilisez l&#39;un des portables de lanceur prédéfinis, le noyau est présélectionné. L&#39;exemple ci-dessous utilise le bloc-notes Scala *Clustering* dans [!DNL JupyterLab Launcher].

![vérifier le noyau](./images/migration/spark-scala/scala-kernel.png)

La sélection du menu déroulant ouvre une liste de noyaux disponibles.

![liste déroulante du noyau](./images/migration/spark-scala/select-dropdown.png)

![sélectionner le noyau](./images/migration/spark-scala/dropdown.png)

Pour les blocs-notes Scala (Spark 2.4), sélectionnez le noyau Scala et confirmez en cliquant sur le bouton **Sélectionner** .

![confirmer le noyau](./images/migration/spark-scala/select.png)

## Initialisation de SparkSession {#initialize-sparksession-scala}

Tous les ordinateurs portables Scala ([!DNL Spark] 2.4) nécessitent que vous initialisiez la session avec le code standard suivant :

<table>
  <th>Ordinateur portable</th>
  <th>Spark ([!DNL Spark] 2.3 - désapprouvée)</th>
  <th>Scala ([!DNL Spark] 2.4)</th>
  <tr>
  <th>Noyau</th>
  <td align="center">[ ! DNL Spark]</td>
  <td align="center">Scala</td>
  </tr>
  <tr>
  <th>code</th>
  <td align="center">
  aucun code requis
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
import org.apache.spark.sql.{ SparkSession}val spark = SparkSession.builder() .master("local") .getOrCreate()
</pre>
  </td>
  </tr>
</table>

L&#39;image Scala ([!DNL Spark] 2.4) ci-dessous illustre la différence clé dans l&#39;initialisation de sparkSession avec le noyau [!DNL Spark] 2.3 [!DNL Spark] et le noyau [!DNL Spark] 2.4 Scala. Cet exemple utilise les blocs-notes de démarrage *Mise en grappe* fournis dans [!DNL JupyterLab Launcher].

**[!DNL Spark]([!DNL Spark]2.3 - obsolète)**

[!DNL Spark] ([!DNL Spark] 2.3 - désapprouvée) utilise le [!DNL Spark] noyau, et par conséquent, vous n&#39;étiez pas obligé de définir [!DNL Spark].

**Scala ([!DNL Spark]2.4)**

L&#39;utilisation de [!DNL Spark] la version 2.4 avec le noyau Scala requiert que vous définissiez `val spark` et importiez `SparkSesson` pour lire ou écrire :

![importation et définition de spark](./images/migration/spark-scala/start-session.png)

## Données de requête

Avec Scala ([!DNL Spark] 2.4) `%%` sparkmagic n&#39;est plus pris en charge. Les opérations suivantes ne peuvent plus être utilisées :

- `%%help`
- `%%info`
- `%%cleanup`
- `%%delete`
- `%%configure`
- `%%local`

Le tableau suivant présente les modifications nécessaires à la conversion des requêtes `%%sql` sparkmiracle :

<table>
  <th>Ordinateur portable</th>
  <th>[!DNL Spark] ([!DNL Spark] 2.3 - désapprouvée)</th>
  <th>Scala ([!DNL Spark] 2.4)</th>
  <tr>
  <th>Noyau</th>
  <td align="center">[ ! DNL Spark]</td>
  <td align="center">Scala</td>
  </tr>
  <tr>
  <th>code</th>
    <td>
       <pre class="JSON language-JSON hljs">
%%sql -o dfselect * from sparkdf
</pre>
         <pre class="JSON language-JSON hljs">
%%sql -o df -n limitselect * from sparkdf
</pre>
         <pre class="JSON language-JSON hljs">
%%sql -o df -qselect * from sparkdf
</pre>
         <pre class="JSON language-JSON hljs">
%%sql -o df -r fractionselect * from sparkdf
</pre>
      </td>
      <td>
         <pre class="JSON language-JSON hljs">
val df = spark.sql('''' SELECT * FROM sparkdf''')
</pre>
         <pre class="JSON language-JSON hljs">
val df = spark.sql('''' SELECT * FROM sparkdf LIMIT limit'')
</pre>
         <pre class="JSON language-JSON hljs">
val df = spark.sql('''' SELECT * FROM sparkdf LIMIT limit'')
</pre>
         <pre class="JSON language-JSON hljs">
val sample_df = df.sample(fraction) </pre>
      </td>
   </tr>
</table>

L&#39;image Scala ([!DNL Spark] 2.4) ci-dessous illustre les différences clés dans la création de requêtes avec le noyau [!DNL Spark] 2.3 [!DNL Spark] et le noyau Spark 2.4 Scala. Cet exemple utilise les blocs-notes de démarrage *Mise en grappe* fournis dans [!DNL JupyterLab Launcher].

**[!DNL Spark]([!DNL Spark]2.3 - obsolète)**

Le [!DNL Spark] bloc-notes ([!DNL Spark] 2.3 - désapprouvé) utilise le [!DNL Spark] noyau. Le [!DNL Spark] noyau prend en charge et utilise `%%sql` sparkmiracle.

![](./images/migration/spark-scala/sql-2.3.png)

**Scala ([!DNL Spark]2.4)**

Le noyau Scala ne prend plus en charge `%%sql` sparkmiracle. Le code sparkmagic existant doit être converti.

![importation et définition de spark](./images/migration/spark-scala/sql-2.4.png)

## Lecture d’un jeu de données {#notebook-read-dataset-spark}

Dans la [!DNL Spark] version 2.3, vous deviez définir des variables pour `option` les valeurs utilisées pour lire les données ou utiliser les valeurs brutes dans la cellule de code. Dans Scala, vous pouvez utiliser `sys.env("PYDASDK_IMS_USER_TOKEN")` pour déclarer et renvoyer une valeur, ce qui élimine la nécessité de définir des variables telles que `var userToken`. Dans l’exemple Scala (Spark 2.4) ci-dessous, `sys.env` est utilisé pour définir et renvoyer toutes les valeurs requises pour lire un jeu de données.

**Utilisation[!DNL Spark]([!DNL Spark]2.3 - obsolète) -[!DNL Spark]Noyau**

```scala
import com.adobe.platform.dataset.DataSetOptions
var df1 = spark.read.format("com.adobe.platform.dataset")
  .option(DataSetOptions.orgId, "310C6D375BA5248F0A494212@AdobeOrg")
  .option(DataSetOptions.batchId, "dbe154d3-197a-4e6c-80f8-9b7025eea2b9")
  .load("5e68141134492718af974844")
```

**Utilisation de Scala ([!DNL Spark]2.4) - Noyau Scala**

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
  .option("ims-org", sys.env("IMS_ORG_ID"))
  .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
  .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .load()
```

| element   | description |
| ------- | ----------- |
| df1 | Variable qui représente la base de données Pandas utilisée pour lire et écrire des données. |
| user-token | Votre jeton utilisateur qui est automatiquement récupéré à l’aide de `sys.env("PYDASDK_IMS_USER_TOKEN")`. |
| service-token | Votre jeton de service automatiquement récupéré à l’aide de `sys.env("PYDASDK_IMS_SERVICE_TOKEN")`. |
| ims-org | Votre identifiant ims-org automatiquement récupéré à l’aide de `sys.env("IMS_ORG_ID")`. |
| api-key | Votre clé api automatiquement récupérée à l’aide de `sys.env("PYDASDK_IMS_CLIENT_ID")`. |

Les images ci-dessous mettent en évidence les principales différences de chargement des données avec les versions [!DNL Spark] .3 et [!DNL Spark] 2.4. Cet exemple utilise les blocs-notes de démarrage *Clustering* fournis dans [!DNL JupyterLab Launcher].

**[!DNL Spark]([!DNL Spark]2.3 - obsolète)**

Le [!DNL Spark] bloc-notes ([!DNL Spark] 2.3 - désapprouvé) utilise le [!DNL Spark] noyau. Les deux cellules suivantes présentent un exemple de chargement du jeu de données avec un ID de jeu de données spécifié dans la plage de dates (3-21/2019-3-29).

![chargement de spark 2.3](./images/migration/spark-scala/load-2.3.png)

**Scala ([!DNL Spark]2.4)**

Le bloc-notes Scala ([!DNL Spark] 2.4) utilise le noyau Scala qui nécessite plus de valeurs lors de la configuration, comme indiqué dans la première cellule de code. En outre, `var mdata` il faut `option` remplir davantage de valeurs. Dans ce bloc-notes, le code mentionné précédemment pour [initialiser SparkSession](#initialize-sparksession-scala) est inclus dans la cellule de `var mdata` code.

![chargement de spark 2.4](./images/migration/spark-scala/load-2.4.png)

>[!TIP]
>
>Dans Scala, vous pouvez utiliser `sys.env()` pour déclarer et renvoyer une valeur de l’intérieur `option`. Cela évite de définir des variables si vous savez qu’elles ne seront utilisées qu’une seule fois. L’exemple suivant illustre `val userToken` l’exemple ci-dessus et le déclare en ligne dans `option`:
> `.option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))`

## Écrire dans un jeu de données

Comme pour [lire un jeu de données](#notebook-read-dataset-spark), l’écriture dans un jeu de données nécessite des `option` valeurs supplémentaires décrites dans l’exemple ci-dessous. Dans Scala, vous pouvez utiliser `sys.env("PYDASDK_IMS_USER_TOKEN")` pour déclarer et renvoyer une valeur, ce qui élimine la nécessité de définir des variables telles que `var userToken`. Dans l&#39;exemple Scala ci-dessous, `sys.env` est utilisé pour définir et renvoyer toutes les valeurs requises pour écrire dans un jeu de données.

**Utilisation[!DNL Spark]([!DNL Spark]2.3 - obsolète) -[!DNL Spark]Noyau**

```scala
import com.adobe.platform.dataset.DataSetOptions

var userToken = spark.sparkContext.getConf.getOption("spark.yarn.appMasterEnv.USER_TOKEN").get
var serviceToken = spark.sparkContext.getConf.getOption("spark.yarn.appMasterEnv.SERVICE_TOKEN").get
var serviceApiKey = spark.sparkContext.getConf.getOption("spark.yarn.appMasterEnv.SERVICE_API_KEY").get

df1.write.format("com.adobe.platform.dataset")
  .option(DataSetOptions.orgId, "310C6D375BA5248F0A494212@AdobeOrg")
  .option(DataSetOptions.userToken, userToken)
  .option(DataSetOptions.serviceToken, serviceToken)
  .option(DataSetOptions.serviceApiKey, serviceApiKey)
  .save("5e68141134492718af974844")
```

**Utilisation de Scala ([!DNL Spark]2.4) - Noyau Scala**

```scala
import org.apache.spark.sql.{Dataset, SparkSession}

val spark = SparkSession.builder().master("local").getOrCreate()

df1.write.format("com.adobe.platform.query")
  .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
  .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
  .option("ims-org", sys.env("IMS_ORG_ID"))
  .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| element   | description |
| ------- | ----------- |
| df1 | Variable qui représente la base de données Pandas utilisée pour lire et écrire des données. |
| user-token | Votre jeton utilisateur qui est automatiquement récupéré à l’aide de `sys.env("PYDASDK_IMS_USER_TOKEN")`. |
| service-token | Votre jeton de service automatiquement récupéré à l’aide de `sys.env("PYDASDK_IMS_SERVICE_TOKEN")`. |
| ims-org | Votre identifiant ims-org automatiquement récupéré à l’aide de `sys.env("IMS_ORG_ID")`. |
| api-key | Votre clé api automatiquement récupérée à l’aide de `sys.env("PYDASDK_IMS_CLIENT_ID")`. |