---
keywords: Experience Platform ; fichiers source du package ; Espace de travail des données ; rubriques populaires ; Docker ; image du dossier
solution: Experience Platform
title: compresser les fichiers source dans une recette
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel explique comment regrouper les fichiers source fournis d’exemples de ventes au détail dans un fichier d’archives, pouvant être utilisé pour créer une recette dans Adobe Experience Platform Data Science Workspace en suivant le processus d’importation des recettes dans l’interface utilisateur ou à l’aide de l’API.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 50%

---

# Regroupement des fichiers source dans une recette

Ce didacticiel fournit des instructions sur la manière de compresser les fichiers source d&#39;exemples de ventes au détail fournis dans un fichier d&#39;archive, qui peut être utilisé pour créer une recette dans Adobe Experience Platform [!DNL Data Science Workspace] en suivant le processus d&#39;importation de la recette dans l&#39;interface utilisateur ou à l&#39;aide de l&#39;API.

Concepts à comprendre :

- **Recettes** : une recette est le terme utilisé par Adobe pour désigner une spécification de modèle. Il s’agit d’un conteneur de niveau supérieur qui représente un apprentissage automatique spécifique, un algorithme d’intelligence artificielle ou un ensemble d’algorithmes, une logique de traitement et la configuration nécessaires pour créer et exécuter un modèle formé et ainsi aider à résoudre des problèmes d’entreprise spécifiques.
- **Fichiers source** : fichiers individuels de votre projet contenant la logique pour une recette.

## Conditions préalables

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Création de recettes

La création de recettes commence par le regroupement des fichiers afin de créer un fichier d’archives. Les fichiers source définissent la logique d’apprentissage automatique et les algorithmes utilisés pour résoudre un problème spécifique à l’étude et sont écrits dans [!DNL Python], R, PySpark ou Scala. Les fichiers d&#39;archives créés prennent la forme d&#39;une image Docker. Une fois créé, le fichier d&#39;archive compressé est importé dans [!DNL Data Science Workspace] pour créer une recette [dans l&#39;interface utilisateur](./import-packaged-recipe-ui.md) ou [à l&#39;aide de l&#39;API](./import-packaged-recipe-api.md).

### Création de modèles basés sur Docker {#docker-based-model-authoring}

Une image Docker permet au développeur d’empaqueter une application avec tous les éléments dont elle a besoin, comme les bibliothèques et autres dépendances, et de l’expédier sous forme d’un package unique.

L&#39;image Docker construite est envoyée au Registre du Conteneur Azure à l&#39;aide des informations d&#39;identification qui vous ont été fournies pendant le processus de création de la recette.

Pour obtenir vos informations d’identification Azure Container Registry, connectez-vous à [Adobe Experience Platform](https://platform.adobe.com). Dans la colonne de navigation de gauche, accédez aux **[!UICONTROL Workflows]**. Sélectionnez **[!UICONTROL Importer la recette]**, puis **[!UICONTROL Lancer]**. Voir la capture d’écran ci-dessous pour référence.

![](../images/models-recipes/package-source-files/import.png)

La page **[!UICONTROL Configurer]** s&#39;affiche. Indiquez un **[!UICONTROL nom de recette]** approprié, par exemple « Recette des ventes au détail », et éventuellement une description ou une URL de documentation. Une fois terminé, cliquez sur **[!UICONTROL Suivant]**.

![](../images/models-recipes/package-source-files/configure.png)

Sélectionnez le *runtime* approprié, puis choisissez une **[!UICONTROL classification]** pour *Type*. Les informations d&#39;identification de votre Registre Azure Conteneur sont générées une fois l&#39;opération terminée.

>[!NOTE]
>
>** Typeis est la classe de problème d&#39;apprentissage automatique pour laquelle la recette est conçue et est utilisée après la formation pour aider à personnaliser l&#39;évaluation de la course de formation.

>[!TIP]
>
>- Pour les recettes [!DNL Python], sélectionnez le runtime **[!UICONTROL Python]**.
>- Pour les recettes R, sélectionnez le runtime **[!UICONTROL R]**.
>- Pour les recettes PySpark, sélectionnez le runtime **[!UICONTROL PySpark]**. Un type d’artefact est renseigné automatiquement.
>- Pour les recettes Scala, sélectionnez le runtime **[!UICONTROL Spark]**. Un type d’artefact est renseigné automatiquement.


![](../images/models-recipes/package-source-files/docker-creds.png)

Notez les valeurs de l&#39;hôte Docker, du nom d&#39;utilisateur et du mot de passe. Ils sont utilisés pour créer et pousser votre image [!DNL Docker] dans les workflows décrits ci-dessous.

>[!NOTE]
>
>L’URL source est fournie après avoir exécuté les étapes décrites ci-dessous. Le fichier de configuration est expliqué dans les didacticiels suivants, qui se trouvent dans [étapes suivantes](#next-steps).

### Regroupement des fichiers source

Commencez par obtenir l’exemple de code de base trouvé dans le référentiel <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace Reference.</a>

- [Création d’une image Python Docker](#python-docker)
- [Création d’une image R Docker](#r-docker)
- [Création d’une image PySpark Docker](#pyspark-docker)
- [Créer une image Scala (Spark Docker)](#scala-docker)

### Créer [!DNL Python] Image de l&#39;ancre {#python-docker}

Si vous ne l&#39;avez pas fait, clonez le référentiel [!DNL GitHub] sur votre système local avec la commande suivante :

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Accédez au répertoire `experience-platform-dsw-reference/recipes/python/retail`. Vous trouverez ici les scripts `login.sh` et `build.sh` utilisés pour vous connecter à Docker et pour créer l&#39;image [!DNL Python Docker]. Si vos [informations d’identification Docker](#docker-based-model-authoring) sont prêtes, saisissez les commandes suivantes dans l’ordre :

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

### Image de build R [!DNL Docker] {#r-docker}

Si vous ne l&#39;avez pas fait, clonez le référentiel [!DNL GitHub] sur votre système local avec la commande suivante :

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Accédez au répertoire `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` dans votre référentiel cloné. Vous trouverez ici les fichiers `login.sh` et `build.sh` que vous utiliserez pour vous connecter à Docker et pour créer l&#39;image R Docker. Si vos [informations d’identification Docker](#docker-based-model-authoring) sont prêtes, saisissez les commandes suivantes dans l’ordre :

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

### Créer une image PySpark Docker {#pyspark-docker}

Début en clonant le référentiel [!DNL GitHub] sur votre système local avec la commande suivante :

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Accédez au répertoire `experience-platform-dsw-reference/recipes/pyspark/retail`. Les scripts `login.sh` et `build.sh` se trouvent ici et servent à se connecter au Docker et à créer l&#39;image du Docker. Si vos [informations d’identification Docker](#docker-based-model-authoring) sont prêtes, saisissez les commandes suivantes dans l’ordre :

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

### Créer une image Scala Docker {#scala-docker}

Début en clonant le référentiel [!DNL GitHub] sur votre système local avec la commande suivante en terminal :

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Accédez ensuite au répertoire `experience-platform-dsw-reference/recipes/scala` où vous trouverez les scripts `login.sh` et `build.sh`. Ces scripts sont utilisés pour se connecter au Docker et créer l&#39;image du Docker. Si vos [informations d&#39;identification du Docker](#docker-based-model-authoring) sont prêtes, entrez les commandes suivantes dans le terminal dans l&#39;ordre :

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Si vous recevez une erreur d&#39;autorisation lors de la tentative de connexion au Docker à l&#39;aide du script `login.sh`, essayez d&#39;utiliser la commande `bash login.sh`.

Lors de l&#39;exécution du script de connexion, vous devez indiquer l&#39;hôte, le nom d&#39;utilisateur et le mot de passe du Docker. Lors de la création, vous devez fournir l’hôte Docker et une balise de version pour la génération.

Une fois le script de génération terminé, vous recevez une URL de fichier source Docker dans la sortie de la console. Pour cet exemple spécifique, il se présente comme suit :

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copiez cette URL et passez aux [étapes suivantes](#next-steps).

## Étapes suivantes {#next-steps}

Ce tutoriel a passé en revue le regroupement de fichiers source dans une recette, étape préalable à l’importation d’une recette dans [!DNL Data Science Workspace]. Vous devez maintenant avoir une image Docker dans le Registre de Conteneur Azure avec l&#39;URL d&#39;image correspondante. Vous êtes maintenant prêt à commencer le didacticiel sur l&#39;importation d&#39;une recette emballée dans [!DNL Data Science Workspace]. Sélectionnez l’un des liens du tutoriel ci-dessous pour commencer:

- [Importation d’une recette empaquetée dans l’interface utilisateur](./import-packaged-recipe-ui.md)
- [Importation d’une recette empaquetée à l’aide de l’API](./import-packaged-recipe-api.md)
