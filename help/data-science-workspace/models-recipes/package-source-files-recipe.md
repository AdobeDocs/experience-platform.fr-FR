---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: Regroupement des fichiers source dans une recette
topic: Tutorial
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 49%

---


# Regroupement des fichiers source dans une recette

This tutorial provides instructions on how you can package the provided Retail Sales sample source files into an archive file, which can be used to create a recipe in Adobe Experience Platform [!DNL Data Science Workspace] by following the recipe import workflow either in the UI or using the API.

Concepts à comprendre :

- **Recettes** : une recette est le terme utilisé par Adobe pour désigner une spécification de modèle. Il s’agit d’un conteneur de niveau supérieur qui représente un apprentissage automatique spécifique, un algorithme d’intelligence artificielle ou un ensemble d’algorithmes, une logique de traitement et la configuration nécessaires pour créer et exécuter un modèle formé et ainsi aider à résoudre des problèmes d’entreprise spécifiques.
- **Fichiers source** : fichiers individuels de votre projet contenant la logique pour une recette.

## Conditions préalables

- [[ ! Mémoire DNL]](https://docs.docker.com/install/#supported-platforms)
- [[ ! DNL Python 3 et pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[ ! DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[ ! DNL Maven]](https://maven.apache.org/install.html)

## Création de recettes

La création de recettes commence par le regroupement des fichiers afin de créer un fichier d’archives. Source files define the machine learning logic and algorithms used to solve a specific problem at hand, and are written in either [!DNL Python], R, PySpark, or Scala. Les fichiers d&#39;archives créés prennent la forme d&#39;une image Docker. Once built, the packaged archive file is imported into [!DNL Data Science Workspace] to create a recipe [in the UI](./import-packaged-recipe-ui.md) or [using the API](./import-packaged-recipe-api.md).

### Création de modèles basés sur Docker {#docker-based-model-authoring}

Une image Docker permet au développeur d’empaqueter une application avec tous les éléments dont elle a besoin, comme les bibliothèques et autres dépendances, et de l’expédier sous forme d’un package unique.

L&#39;image Docker construite est envoyée au Registre du Conteneur Azure à l&#39;aide des informations d&#39;identification qui vous ont été fournies pendant le processus de création de la recette.

Pour obtenir vos informations d’identification Azure Container Registry, connectez-vous à [Adobe Experience Platform](https://platform.adobe.com). Dans la colonne de navigation de gauche, accédez aux **[!UICONTROL Workflows]**. Sélectionnez **[!UICONTROL Importer la recette]** , puis sélectionnez **[!UICONTROL Lancement]**. Voir la capture d’écran ci-dessous pour référence.

![](../images/models-recipes/package-source-files/import.png)

La page *Configurer* s’ouvre. Indiquez un *nom de recette* approprié, par exemple « Recette des ventes au détail », et éventuellement une description ou une URL de documentation. Une fois terminé, cliquez sur **[!UICONTROL Suivant]**.

![](../images/models-recipes/package-source-files/configure.png)

Select the appropriate *Runtime*, then choose a **[!UICONTROL Classification]** for *Type*. Les informations d&#39;identification de votre Registre Azure Conteneur sont générées une fois l&#39;opération terminée.

>[!NOTE]
>
>*Type* est la classe de problème d&#39;apprentissage automatique pour laquelle la recette est conçue et est utilisée après la formation pour aider à personnaliser l&#39;évaluation de la course de formation.

>[!TIP]
>
>- Pour [!DNL Python] les recettes, sélectionnez l&#39;exécution **[!UICONTROL Python]** .
>- Pour les recettes R, sélectionnez le **[!UICONTROL runtime R]** .
>- Pour les recettes PySpark, sélectionnez le **[!UICONTROL runtime PySpark]** . Un type d’artefact est renseigné automatiquement.
>- Pour les recettes Scala, sélectionnez le **[!UICONTROL runtime Spark]** . Un type d’artefact est renseigné automatiquement.


![](../images/models-recipes/package-source-files/docker-creds.png)

Notez les valeurs de *Hôte Docker*, *Nom d’utilisateur* et *Mot de passe*. Elles sont utilisées pour créer et pousser votre [!DNL Docker] image dans les workflows décrits ci-dessous.

>[!NOTE]
>
>L’URL source est fournie après avoir exécuté les étapes décrites ci-dessous. Le fichier de configuration est expliqué dans les didacticiels suivants, qui se trouvent dans les étapes [](#next-steps)suivantes.

### Regroupement des fichiers source

Commencez par obtenir l’exemple de code de base trouvé dans le référentiel <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace Reference.</a>

- [Création d’une image Python Docker](#python-docker)
- [Création d’une image R Docker](#r-docker)
- [Création d’une image PySpark Docker](#pyspark-docker)
- [Créer une image Scala (Spark Docker)](#scala-docker)

### Build [!DNL Python] Docker image {#python-docker}

If you have not done so, clone the [!DNL GitHub] repository onto your local system with the following command:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Accédez au répertoire `experience-platform-dsw-reference/recipes/python/retail`. Ici, vous trouverez les scripts `login.sh` et `build.sh` utilisés pour vous connecter à Docker et pour construire l&#39; [!DNL Python Docker] image. Si vos [informations d’identification Docker](#docker-based-model-authoring) sont prêtes, saisissez les commandes suivantes dans l’ordre :

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Notez que lors de l&#39;exécution du script de connexion, vous devez fournir l&#39;hôte, le nom d&#39;utilisateur et le mot de passe du Docker. Lors de la création, vous devez fournir l’hôte Docker et une balise de version pour la génération.

Une fois le script de génération terminé, vous recevez une URL de fichier source Docker dans la sortie de la console. Pour cet exemple spécifique, il se présente comme suit :

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copiez cette URL et passez aux [étapes suivantes](#next-steps).

### Build R [!DNL Docker] image {#r-docker}

If you have not done so, clone the [!DNL GitHub] repository onto your local system with the following command:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Accédez au répertoire `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` dans votre référentiel cloné. Here, you&#39;ll find the files `login.sh` and `build.sh` which you will use to login to Docker and to build the R Docker image. Si vos [informations d’identification Docker](#docker-based-model-authoring) sont prêtes, saisissez les commandes suivantes dans l’ordre :

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Notez que lors de l&#39;exécution du script de connexion, vous devez fournir l&#39;hôte, le nom d&#39;utilisateur et le mot de passe du Docker. Lors de la création, vous devez fournir l’hôte Docker et une balise de version pour la génération.

Une fois le script de génération terminé, vous recevez une URL de fichier source Docker dans la sortie de la console. Pour cet exemple spécifique, il se présente comme suit :

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copiez cette URL et passez aux [étapes suivantes](#next-steps).

### Création d’une image PySpark Docker {#pyspark-docker}

Début en clonant le référentiel [!DNL GitHub] sur votre système local avec la commande suivante :

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Accédez au répertoire `experience-platform-dsw-reference/recipes/pyspark/retail`. Les scripts `login.sh` et `build.sh` sont situés ici et utilisés pour se connecter au Docker et pour créer l&#39;image du Docker. Si vos [informations d’identification Docker](#docker-based-model-authoring) sont prêtes, saisissez les commandes suivantes dans l’ordre :

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Notez que lors de l&#39;exécution du script de connexion, vous devez fournir l&#39;hôte, le nom d&#39;utilisateur et le mot de passe du Docker. Lors de la création, vous devez fournir l’hôte Docker et une balise de version pour la génération.

Une fois le script de génération terminé, vous recevez une URL de fichier source Docker dans la sortie de la console. Pour cet exemple spécifique, il se présente comme suit :

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Copiez cette URL et passez aux [étapes suivantes](#next-steps).

### Création d’une image Scala Docker {#scala-docker}

Début en clonant le référentiel [!DNL GitHub] sur votre système local avec la commande suivante en terminal :

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Accédez ensuite au répertoire `experience-platform-dsw-reference/recipes/scala` dans lequel vous trouverez les scripts `login.sh` et `build.sh`. Ces scripts sont utilisés pour se connecter au Docker et créer l&#39;image du Docker. If you have your [Docker credentials](#docker-based-model-authoring) ready, enter the following commands to terminal in order:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Si vous recevez une erreur d&#39;autorisation lors de la tentative de connexion au Docker à l&#39;aide du `login.sh` script, essayez d&#39;utiliser la commande `bash login.sh`.

Lors de l&#39;exécution du script de connexion, vous devez indiquer l&#39;hôte, le nom d&#39;utilisateur et le mot de passe du Docker. Lors de la création, vous devez fournir l’hôte Docker et une balise de version pour la génération.

Une fois le script de génération terminé, vous recevez une URL de fichier source Docker dans la sortie de la console. Pour cet exemple spécifique, il se présente comme suit :

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copiez cette URL et passez aux [étapes suivantes](#next-steps).

## Étapes suivantes {#next-steps}

Ce tutoriel a passé en revue le regroupement de fichiers source dans une recette, étape préalable à l’importation d’une recette dans [!DNL Data Science Workspace]. Vous devez maintenant avoir une image Docker dans le Registre de Conteneur Azure avec l&#39;URL d&#39;image correspondante. You are now ready to begin the tutorial on importing a packaged recipe into [!DNL Data Science Workspace]. Sélectionnez l’un des liens du tutoriel ci-dessous pour commencer:

- [Importation d’une recette empaquetée dans l’interface utilisateur](./import-packaged-recipe-ui.md)
- [Importation d’une recette empaquetée à l’aide de l’API](./import-packaged-recipe-api.md)