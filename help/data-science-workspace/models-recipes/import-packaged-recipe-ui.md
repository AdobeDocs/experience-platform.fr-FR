---
keywords: Experience Platform;importer une recette empaquetée;Data Science Workspace;rubriques populaires;recettes;ui;créer un moteur
solution: Experience Platform
title: Importation d’une recette empaquetée dans l’interface utilisateur de Data Science Workspace
type: Tutorial
description: Ce tutoriel explique comment configurer et importer une recette empaquetée à l’aide de l’exemple de ventes au détail fourni. Après avoir terminé ce tutoriel, vous serez prêt à créer, à former et à évaluer un modèle dans l’espace de travail de science des données d’Adobe Experience Platform.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 38%

---

# Importation d’une recette empaquetée dans l’interface utilisateur de Data Science Workspace

Ce tutoriel explique comment configurer et importer une recette empaquetée à l’aide de l’exemple de ventes au détail fourni. D’ici la fin de ce tutoriel, vous serez prêt à créer, former et évaluer un modèle dans Adobe Experience Platform. [!DNL Data Science Workspace].

## Conditions préalables

Ce tutoriel nécessite une recette empaquetée sous la forme d’une URL d’image Docker. Pour plus d’informations, consultez le tutoriel expliquant comment [Former une recette empaquetée à partir de fichiers sources](./package-source-files-recipe.md).

## Workflow de l’interface utilisateur

Importation d’une recette empaquetée dans [!DNL Data Science Workspace] nécessite des configurations de recette spécifiques, compilées dans un seul fichier JSON (JavaScript Object Notation). Cette compilation des configurations de recette est appelée fichier de configuration. Une recette empaquetée avec un ensemble particulier de configurations est appelée instance de recette. Une recette peut être utilisée pour créer de nombreuses instances de recette dans [!DNL Data Science Workspace].

Voici les différentes étapes du workflow d’importation d’une recette empaquetée :
- [Configuration d’une recette](#configure)
- [Importation d’une recette Docker - Python](#python)
- [Importation d’une recette Docker - R](#r)
- [Importation d’une recette Docker - PySpark](#pyspark)
- [Importation d’une recette Docker - Scala](#scala)

### Configuration d’une recette {#configure}

Chaque instance de recette dans [!DNL Data Science Workspace] est accompagné d’un ensemble de configurations qui adaptent l’instance de recette à un cas d’utilisation particulier. Les fichiers de configuration définissent les comportements de formation et de notation par défaut d’un modèle créé à l’aide de cette instance de recette.

>[!NOTE]
>
>Les fichiers de configuration sont spécifiques à la recette et au cas.

Vous trouverez ci-dessous un échantillon de fichier de configuration présentant les comportements de formation et de notation par défaut de la recette Ventes au détail.

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "learning_rate",
                "value": "0.1"  
            },
            {
                "key": "n_estimators",
                "value": "100"
            },
            {
                "key": "max_depth",
                "value": "3"
            },
            {
                "key": "ACP_DSW_INPUT_FEATURES",
                "value": "date,store,storeType,storeSize,temperature,regionalFuelPrice,markdown,cpi,unemployment,isHoliday"
            },
            {
                "key": "ACP_DSW_TARGET_FEATURES",
                "value": "weeklySales"
            },
            {
                "key": "ACP_DSW_FEATURE_UPDATE_SUPPORT",
                "value": false
            },
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key": "ACP_DSW_TRAINING_XDM_SCHEMA",
                "value": "{SEE BELOW FOR DETAILS}"
            },
            {
                "key": "evaluation.labelColumn",
                "value": "weeklySalesAhead"
            },
            {
                "key": "evaluation.metrics",
                "value": "MAPE,MAE,RMSE,MASE"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key":"ACP_DSW_SCORING_RESULTS_XDM_SCHEMA",
                "value":"{SEE BELOW FOR DETAILS}"
            }
        ]
    }
]
```

| Clé paramètre | Type | Description |
| ----- | ----- | ----- |
| `learning_rate` | Nombre | Scalaire pour la multiplication des gradients. |
| `n_estimators` | Nombre | Nombre d’arbres dans la forêt pour le classificateur Forêt aléatoire. |
| `max_depth` | Nombre | Profondeur maximale d’un arbre dans le classificateur Forêt aléatoire. |
| `ACP_DSW_INPUT_FEATURES` | Chaîne | Liste d’attributs de schéma d’entrée séparés par des virgules. |
| `ACP_DSW_TARGET_FEATURES` | Chaîne | Liste d’attributs de schéma de sortie séparés par des virgules. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booléen | Détermine si les fonctionnalités d’entrée et de sortie peuvent être modifiées. |
| `tenantId` | Chaîne | Cet identifiant permet de garantir que les ressources que vous créez sont des espaces de noms corrects et contenus dans votre organisation IMS. [Suivez ces étapes](../../xdm/api/getting-started.md#know-your-tenant_id) pour trouver votre identifiant client. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Chaîne | Le schéma d’entrée utilisé pour la formation d’un modèle. Laissez ce champ vide lors de l’importation dans l’interface utilisateur ; remplacez-le par l’identifiant du schéma de formation lors de l’importation à l’aide de l’API. |
| `evaluation.labelColumn` | Chaîne | Libellé de colonne pour visualiser les évaluations. |
| `evaluation.metrics` | Chaîne | Liste de mesures d’évaluation séparées par des virgules à utiliser pour l’évaluation d’un modèle. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Chaîne | Le schéma de sortie utilisé pour la notation d’un modèle. Laissez ce champ vide lors de l’importation dans l’interface utilisateur ; remplacez-le par l’identifiant du schéma de notation lors de l’importation à l’aide de l’API. |

Pour les besoins de ce tutoriel, vous pouvez laisser les fichiers de configuration par défaut de la recette Ventes au détail dans la variable [!DNL Data Science Workspace] Référencez leur manière d&#39;être.

### Importation d’une recette Docker - [!DNL Python] {#python}

Commencez par naviguer et sélectionner **[!UICONTROL Workflows]** situé dans le coin supérieur gauche de la [!DNL Platform] Interface utilisateur. Ensuite, sélectionnez **Importation de recette** et sélectionnez **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Le **Configurer** pour la **Importation de recette** le workflow s’affiche. Saisissez un nom et une description pour la recette, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit.

![configurer le workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Dans le tutoriel [Former une recette empaquetée à partir de fichiers sources](./package-source-files-recipe.md), une URL Docker a été fournie à la fin de la création de la recette Ventes au détail à l’aide de fichiers sources Python.

Une fois que vous avez activé la variable **Sélectionner la source** collez l’URL Docker correspondant à la recette empaquetée créée à l’aide de [!DNL Python] fichiers source dans le **[!UICONTROL URL source]** champ . Importez ensuite le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le **Navigateur** du système de fichiers. Le fichier de configuration fourni se trouve ici : `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Sélectionner **[!UICONTROL Python]** dans le **Exécution** déroulant et **[!UICONTROL Classification]** dans le **Type** déroulant. Une fois que tout a été rempli, sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour passer à **Gestion des schémas**.

>[!NOTE]
>
> Prise en charge des types **[!UICONTROL Classification]** et **[!UICONTROL Régression]**. Si votre modèle ne tombe pas sous l’un de ces types, sélectionnez **[!UICONTROL Personnalisé]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Sélectionnez ensuite les schémas d’entrée et de sortie Ventes au détail sous la section . **Gestion des schémas**, ils ont été créés à l’aide du script de bootstrap fourni dans la variable [créer le schéma et le jeu de données des ventes au détail ;](../models-recipes/create-retails-sales-dataset.md) tutoriel .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Sous , **Gestion des fonctionnalités** , sélectionnez sur votre identification client dans la visionneuse de schémas pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctionnalités d’entrée et de sortie en mettant en surbrillance la fonctionnalité souhaitée, puis sélectionnez **[!UICONTROL Fonctionnalité d’entrée]** ou **[!UICONTROL Fonctionnalité cible]** dans la fenêtre **[!UICONTROL Propriétés du champ]** à droite. Pour les besoins de ce tutoriel, définissez **[!UICONTROL weeklySales]** en tant que **[!UICONTROL Fonctionnalité cible]** et tout le reste en tant que **[!UICONTROL Fonctionnalité d’entrée]**. Sélectionner **[!UICONTROL Suivant]** pour consulter votre nouvelle recette configurée.

Vérifiez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Sélectionner **[!UICONTROL Terminer]** pour créer la recette.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez à la [étapes suivantes](#next-steps) pour savoir comment créer un modèle dans [!DNL Data Science Workspace] à l’aide de la nouvelle recette Ventes au détail .

### Importation d’une recette Docker - R {#r}

Commencez par naviguer et sélectionner **[!UICONTROL Workflows]** situé dans le coin supérieur gauche de la [!DNL Platform] Interface utilisateur. Ensuite, sélectionnez **Importation de recette** et sélectionnez **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Le **Configurer** pour la **Importation de recette** le workflow s’affiche. Saisissez un nom et une description pour la recette, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit.

![configurer le workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Dans le tutoriel [Former une recette empaquetée à partir de fichiers sources](./package-source-files-recipe.md), une URL Docker a été fournie à la fin de la création de la recette Ventes au détail à l’aide de fichiers sources R.

Une fois que vous avez activé la variable **Sélectionner la source** collez l’URL Docker correspondant à la recette empaquetée créée à l’aide de fichiers source R dans la **[!UICONTROL URL source]** champ . Importez ensuite le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le **Navigateur** du système de fichiers. Le fichier de configuration fourni se trouve ici : `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Sélectionner **[!UICONTROL R]** dans le **Exécution** déroulant et **[!UICONTROL Classification]** dans le **Type** déroulant. Une fois que tout a été rempli, sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour passer à **Gestion des schémas**.

>[!NOTE]
>
> *Type* prend en charge **[!UICONTROL Classification]** et **[!UICONTROL Régression]**. Si votre modèle ne tombe pas sous l’un de ces types, sélectionnez **[!UICONTROL Personnalisé]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Sélectionnez ensuite les schémas d’entrée et de sortie Ventes au détail sous la section . **Gestion des schémas**, ils ont été créés à l’aide du script de bootstrap fourni dans la variable [créer le schéma et le jeu de données des ventes au détail ;](../models-recipes/create-retails-sales-dataset.md) tutoriel .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Sous , *Gestion des fonctionnalités* , sélectionnez sur votre identification client dans la visionneuse de schémas pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctionnalités d’entrée et de sortie en mettant en surbrillance la fonctionnalité souhaitée, puis sélectionnez **[!UICONTROL Fonctionnalité d’entrée]** ou **[!UICONTROL Fonctionnalité cible]** dans la fenêtre **[!UICONTROL Propriétés du champ]** à droite. Pour les besoins de ce tutoriel, définissez **[!UICONTROL weeklySales]** en tant que **[!UICONTROL Fonctionnalité cible]** et tout le reste en tant que **[!UICONTROL Fonctionnalité d’entrée]**. Sélectionner **[!UICONTROL Suivant]** pour consulter votre nouvelle recette configurée.

Vérifiez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Sélectionner **Terminer** pour créer la recette.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez à la [étapes suivantes](#next-steps) pour savoir comment créer un modèle dans [!DNL Data Science Workspace] à l’aide de la nouvelle recette Ventes au détail .

### Importation d’une recette Docker - PySpark {#pyspark}

Commencez par naviguer et sélectionner **[!UICONTROL Workflows]** situé dans le coin supérieur gauche de la [!DNL Platform] Interface utilisateur. Ensuite, sélectionnez **Importation de recette** et sélectionnez **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Le **Configurer** pour la **Importation de recette** le workflow s’affiche. Saisissez un nom et une description pour la recette, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![configurer le workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Dans le [Regroupement des fichiers source dans une recette](./package-source-files-recipe.md) tutoriel, une URL Docker a été fournie à la fin de la création de la recette Ventes au détail à l’aide de fichiers source PySpark.

Une fois que vous avez activé la variable **Sélectionner la source** collez l’URL Docker correspondant à la recette empaquetée créée à l’aide des fichiers source PySpark dans la **[!UICONTROL URL source]** champ . Importez ensuite le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le **Navigateur** du système de fichiers. Le fichier de configuration fourni se trouve ici : `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Sélectionner **[!UICONTROL PySpark]** dans le **Exécution** déroulant. Une fois l’exécution PySpark sélectionnée, l’artefact par défaut est automatiquement renseigné sur **[!UICONTROL Docker]**. Ensuite, sélectionnez **[!UICONTROL Classification]** dans le **Type** déroulant. Une fois que tout a été rempli, sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour passer à **Gestion des schémas**.

>[!NOTE]
>
> *Type* prend en charge **[!UICONTROL Classification]** et **[!UICONTROL Régression]**. Si votre modèle ne tombe pas sous l’un de ces types, sélectionnez **[!UICONTROL Personnalisé]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Sélectionnez ensuite les schémas d’entrée et de sortie de Ventes au détail à l’aide du **Gestion des schémas** sélecteur, les schémas ont été créés à l’aide du script de bootstrap fourni dans la variable [créer le schéma et le jeu de données des ventes au détail ;](../models-recipes/create-retails-sales-dataset.md) tutoriel .

![gestion des schémas](../images/models-recipes/import-package-ui/manage-schemas.png)

Sous , **Gestion des fonctionnalités** , sélectionnez sur votre identification client dans la visionneuse de schémas pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctionnalités d’entrée et de sortie en mettant en surbrillance la fonctionnalité souhaitée, puis sélectionnez **[!UICONTROL Fonctionnalité d’entrée]** ou **[!UICONTROL Fonctionnalité cible]** dans la fenêtre **[!UICONTROL Propriétés du champ]** à droite. Pour les besoins de ce tutoriel, définissez **[!UICONTROL weeklySales]** en tant que **[!UICONTROL Fonctionnalité cible]** et tout le reste en tant que **[!UICONTROL Fonctionnalité d’entrée]**. Sélectionner **[!UICONTROL Suivant]** pour consulter votre nouvelle recette configurée.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Vérifiez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Sélectionner **[!UICONTROL Terminer]** pour créer la recette.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez à la [étapes suivantes](#next-steps) pour savoir comment créer un modèle dans [!DNL Data Science Workspace] à l’aide de la nouvelle recette Ventes au détail .

### Importation d’une recette Docker - Scala {#scala}

Commencez par naviguer et sélectionner **[!UICONTROL Workflows]** situé dans le coin supérieur gauche de la [!DNL Platform] Interface utilisateur. Ensuite, sélectionnez **Importation de recette** et sélectionnez **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Le **Configurer** pour la **Importation de recette** le workflow s’affiche. Saisissez un nom et une description pour la recette, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![configurer le workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Dans le [Regroupement des fichiers source dans une recette](./package-source-files-recipe.md) tutoriel, une URL Docker a été fournie à la fin de la création de la recette Ventes au détail à l’aide de Scala ([!DNL Spark]) les fichiers source.

Une fois que vous avez activé la variable **Sélectionner la source** collez l’URL Docker correspondant à la recette empaquetée créée à l’aide de fichiers source Scala dans le champ URL source . Importez ensuite le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le Navigateur du système de fichiers. Le fichier de configuration fourni se trouve ici : `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Sélectionner **[!UICONTROL Spark]** dans le **Exécution** déroulant. Une fois que la variable [!DNL Spark] l’exécution est sélectionnée. L’artefact par défaut est automatiquement renseigné sur **[!UICONTROL Docker]**. Ensuite, sélectionnez **[!UICONTROL Régression]** de la **Type** déroulant. Une fois que tout a été rempli, sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour passer à **Gestion des schémas**.

>[!NOTE]
>
> Prise en charge des types **[!UICONTROL Classification]** et **[!UICONTROL Régression]**. Si votre modèle ne tombe pas sous l’un de ces types, sélectionnez **[!UICONTROL Personnalisé]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Sélectionnez ensuite les schémas d’entrée et de sortie de Ventes au détail à l’aide du **Gestion des schémas** sélecteur, les schémas ont été créés à l’aide du script de bootstrap fourni dans la variable [créer le schéma et le jeu de données des ventes au détail ;](../models-recipes/create-retails-sales-dataset.md) tutoriel .

![gestion des schémas](../images/models-recipes/import-package-ui/manage-schemas.png)

Sous , **Gestion des fonctionnalités** , sélectionnez sur votre identification client dans la visionneuse de schémas pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctionnalités d’entrée et de sortie en mettant en surbrillance la fonctionnalité souhaitée, puis sélectionnez **[!UICONTROL Fonctionnalité d’entrée]** ou **[!UICONTROL Fonctionnalité cible]** dans la fenêtre **[!UICONTROL Propriétés du champ]** à droite. Pour les besoins de ce tutoriel, définissez &quot;[!UICONTROL weeklySales]&quot; comme  **[!UICONTROL Fonctionnalité Target]** et tout le reste sous la forme **[!UICONTROL Fonctionnalité d’entrée]**. Sélectionner **[!UICONTROL Suivant]** pour consulter votre nouvelle recette configurée.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Vérifiez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Sélectionner **[!UICONTROL Terminer]** pour créer la recette.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez à la [étapes suivantes](#next-steps) pour savoir comment créer un modèle dans [!DNL Data Science Workspace] à l’aide de la nouvelle recette Ventes au détail .

## Étapes suivantes {#next-steps}

Ce tutoriel vous a fourni des informations sur la configuration et l’importation d’une recette dans [!DNL Data Science Workspace]. Vous pouvez désormais créer, former et évaluer un modèle à l’aide de la nouvelle recette créée.

- [Formation et évaluation d’un modèle dans l’interface utilisateur](./train-evaluate-model-ui.md)
- [Formation et évaluation d’un modèle à l’aide de l’API](./train-evaluate-model-api.md)
