---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: compresser les fichiers source dans une recette ;
topic: Tutorial
translation-type: tm+mt
source-git-commit: 4b0f0dda97f044590f55eaf75a220f631f3313ee
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 0%

---


# compresser les fichiers source dans une recette ;

Ce didacticiel fournit des instructions sur la manière de regrouper les exemples de fichiers source fournis par les ventes au détail dans un fichier d&#39;archive, qui peut être utilisé pour créer une recette dans l&#39;Adobe Experience Platform [!DNL Data Science Workspace] en suivant le processus d&#39;importation des recettes dans l&#39;interface utilisateur ou à l&#39;aide de l&#39;API.

Concepts à comprendre :

- **Recettes**: Une recette est un terme Adobe pour une spécification de modèle et est un conteneur de niveau supérieur qui représente un apprentissage automatique, un algorithme d&#39;intelligence artificielle ou un ensemble d&#39;algorithmes, une logique de traitement et une configuration nécessaires pour construire et exécuter un modèle formé et aider ainsi à résoudre des problèmes commerciaux spécifiques.
- **Fichiers** source : Fichiers individuels de votre projet contenant la logique d&#39;une recette.

## Conditions préalables

- [!DNL Docker](https://docs.docker.com/install/#supported-platforms)
- [!DNL Python 3 and pip](https://docs.conda.io/en/latest/miniconda.html)
- [!DNL Scala](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [!DNL Maven](https://maven.apache.org/install.html)

## Création de recettes

débuts de création de recette avec mise en package des fichiers source pour créer un fichier d&#39;archive. Les fichiers source définissent la logique d’apprentissage automatique et les algorithmes utilisés pour résoudre un problème spécifique à l’étude et sont écrits dans [!DNL Python]R, PySpark ou Scala. Les fichiers d&#39;archives créés prennent la forme d&#39;une image Docker. Une fois créé, le fichier d&#39;archive compressé est importé dans [!DNL Data Science Workspace] pour créer une recette [dans l&#39;interface utilisateur](./import-packaged-recipe-ui.md) ou [à l&#39;aide de l&#39;API](./import-packaged-recipe-api.md).

### Création de modèles basés sur un Docker {#docker-based-model-authoring}

Une image Docker permet au développeur d&#39;assembler une application avec toutes les parties dont il a besoin, telles que les bibliothèques et d&#39;autres dépendances, et de l&#39;expédier sous la forme d&#39;un package unique.

L&#39;image Docker construite est envoyée au Registre du Conteneur Azure à l&#39;aide des informations d&#39;identification qui vous ont été fournies pendant le processus de création de la recette.

Pour obtenir vos informations d&#39;identification de Registre Azure Conteneur, connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a>. Dans la colonne de navigation de gauche, accédez aux **[!UICONTROL Workflows]**. Sélectionnez **[!UICONTROL Importer la recette]** , puis sélectionnez **[!UICONTROL Lancement]**. Voir la capture d&#39;écran ci-dessous pour référence.

![](../images/models-recipes/package-source-files/import.png)

La page *Configurer* s’ouvre. Indiquez un nom *de* recette approprié, par exemple &quot;Recette des ventes au détail&quot;, et éventuellement une description ou une URL de documentation. Une fois terminé, cliquez sur **[!UICONTROL Suivant]**.

![](../images/models-recipes/package-source-files/configure.png)

Sélectionnez l’ *exécution* appropriée, puis choisissez une **[!UICONTROL classification]** pour *Type*. Les informations d&#39;identification de votre Registre Azure Conteneur sont générées une fois l&#39;opération terminée.

>[!NOTE]
>*Type *est la classe de problème d&#39;apprentissage automatique pour laquelle la recette est conçue et est utilisée après la formation pour aider à personnaliser l&#39;évaluation de la course de formation.

>[!TIP]
>- Pour [!DNL Python] les recettes, sélectionnez l&#39;exécution **[!UICONTROL Python]** .
>- Pour les recettes R, sélectionnez le **[!UICONTROL runtime R]** .
>- Pour les recettes PySpark, sélectionnez le **[!UICONTROL runtime PySpark]** . Un type d’artefact est renseigné automatiquement.
>- Pour les recettes Scala, sélectionnez le **[!UICONTROL runtime Spark]** . Un type d’artefact est renseigné automatiquement.


![](../images/models-recipes/package-source-files/docker-creds.png)

Notez les valeurs de l&#39;hôte ** Docker, du nom d&#39; *utilisateur* et du *mot de passe*. Elles sont utilisées pour créer et pousser votre [!DNL Docker] image dans les workflows décrits ci-dessous.

>[!NOTE]
>L’URL source est fournie après avoir exécuté les étapes décrites ci-dessous. Le fichier de configuration est expliqué dans les didacticiels suivants, qui se trouvent dans les étapes [](#next-steps)suivantes.

### Assemblage des fichiers source

Début en obtenant l’exemple de code de base trouvé dans le référentiel de référence <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Data Science Workspace</a> Experience Platform.

- [Créer une image Python Dock](#python-docker)
- [Créer une image R Docker](#r-docker)
- [Création d’une image PySpark Docker](#pyspark-docker)
- [Créer une image Scala (Spark Docker)](#scala-docker)

### Créer une image [!DNL Python] Dock {#python-docker}

Si vous ne l’avez pas fait, clonez le référentiel sur votre système local à l’aide de la commande suivante : [!DNL GitHub]

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/python/retail`. Ici, vous trouverez les scripts `login.sh` et `build.sh` utilisés pour vous connecter à Docker et pour construire l&#39; [!DNL Python Docker] image. Si vos informations d&#39;identification [](#docker-based-model-authoring) Docker sont prêtes, saisissez les commandes suivantes dans l&#39;ordre :

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Notez que lors de l&#39;exécution du script de connexion, vous devez fournir l&#39;hôte, le nom d&#39;utilisateur et le mot de passe du Docker. Lors de la création, vous devez fournir l&#39;hôte Docker et une balise de version pour la création.

Une fois le script de création terminé, vous recevez une URL de fichier source Docker dans la sortie de la console. Pour cet exemple spécifique, il se présente comme suit :

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copiez cette URL et passez aux étapes [](#next-steps)suivantes.

### Générer une [!DNL Docker] image R {#r-docker}

Si vous ne l’avez pas fait, clonez le référentiel sur votre système local à l’aide de la commande suivante : [!DNL GitHub]

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Accédez au répertoire `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` dans votre référentiel cloné. Ici, vous trouverez les fichiers `login.sh` et `build.sh` ceux que vous utiliserez pour vous connecter à Docker et pour construire l&#39;image R Docker. Si vos informations d&#39;identification [](#docker-based-model-authoring) Docker sont prêtes, saisissez les commandes suivantes dans l&#39;ordre :

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Notez que lors de l&#39;exécution du script de connexion, vous devez fournir l&#39;hôte, le nom d&#39;utilisateur et le mot de passe du Docker. Lors de la création, vous devez fournir l&#39;hôte Docker et une balise de version pour la création.

Une fois le script de création terminé, vous recevez une URL de fichier source Docker dans la sortie de la console. Pour cet exemple spécifique, il se présente comme suit :

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copiez cette URL et passez aux étapes [](#next-steps)suivantes.

### Création d’une image PySpark Docker {#pyspark-docker}

Début en clonant le référentiel [!DNL GitHub] sur votre système local avec la commande suivante :

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/pyspark/retail`. Les scripts `login.sh` et `build.sh` sont situés ici et utilisés pour se connecter au Docker et pour créer l&#39;image du Docker. Si vos informations d&#39;identification [](#docker-based-model-authoring) Docker sont prêtes, saisissez les commandes suivantes dans l&#39;ordre :

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Notez que lors de l&#39;exécution du script de connexion, vous devez fournir l&#39;hôte, le nom d&#39;utilisateur et le mot de passe du Docker. Lors de la création, vous devez fournir l&#39;hôte Docker et une balise de version pour la création.

Une fois le script de création terminé, vous recevez une URL de fichier source Docker dans la sortie de console. Pour cet exemple spécifique, il se présente comme suit :

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Copiez cette URL et passez aux étapes [](#next-steps)suivantes.

### Création d’une image Scala Docker {#scala-docker}

Début en clonant le référentiel [!DNL GitHub] sur votre système local avec la commande suivante en terminal :

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Accédez ensuite au répertoire `experience-platform-dsw-reference/recipes/scala/retail` dans lequel vous trouverez les scripts `login.sh` et `build.sh`. Ces scripts sont utilisés pour se connecter au Docker et créer l&#39;image du Docker. Si vos informations d&#39;identification [du](#docker-based-model-authoring) Docker sont prêtes, entrez les commandes suivantes dans le terminal dans l&#39;ordre :

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Lors de l&#39;exécution du script de connexion, vous devez indiquer l&#39;hôte, le nom d&#39;utilisateur et le mot de passe du Docker. Lors de la création, vous devez fournir l&#39;hôte Docker et une balise de version pour la création.

Une fois le script de création terminé, vous recevez une URL de fichier source Docker dans la sortie de la console. Pour cet exemple spécifique, il se présente comme suit :

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copiez cette URL et passez aux étapes [](#next-steps)suivantes.

## Étapes suivantes {#next-steps}

Ce didacticiel a été consacré à l&#39;emballage des fichiers source dans une recette, étape préalable à l&#39;importation d&#39;une recette dans [!DNL Data Science Workspace]. Vous devez maintenant avoir une image Docker dans le Registre de Conteneur Azure avec l&#39;URL d&#39;image correspondante. Vous êtes maintenant prêt à commencer le didacticiel sur l&#39;importation d&#39;une recette emballée dans [!DNL Data Science Workspace]. Sélectionnez l’un des liens du didacticiel ci-dessous pour commencer :

- [Importer une recette mise en package dans l&#39;interface utilisateur](./import-packaged-recipe-ui.md)
- [Importer une recette assemblée à l&#39;aide de l&#39;API](./import-packaged-recipe-api.md)