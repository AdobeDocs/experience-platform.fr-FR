---
keywords: Experience Platform ; importer la recette emballée ; Espace de travail des sciences de données ; rubriques populaires ; recettes ; ui ; créer un moteur
solution: Experience Platform
title: Importer une recette compressée dans l’interface utilisateur de l’espace de travail Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel explique comment configurer et importer une recette empaquetée à l’aide de l’exemple de ventes au détail fourni. Après avoir terminé ce tutoriel, vous serez prêt à créer, à former et à évaluer un modèle dans Adobe Experience Platform Data Science Workspace.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 39%

---

# Importer une recette assemblée dans l’interface utilisateur de l’espace de travail Data Science Workspace

Ce tutoriel explique comment configurer et importer une recette empaquetée à l’aide de l’exemple de ventes au détail fourni. Après avoir terminé ce tutoriel, vous serez prêt à créer, à former et à évaluer un modèle dans Adobe Experience Platform [!DNL Data Science Workspace].

## Conditions préalables

Ce didacticiel nécessite une recette empaquetée sous la forme d&#39;une URL d&#39;image Docker. Pour plus d’informations, consultez le tutoriel expliquant comment [Former une recette empaquetée à partir de fichiers source](./package-source-files-recipe.md).

## Workflow de l’interface utilisateur

L&#39;importation d&#39;une recette empaquetée dans [!DNL Data Science Workspace] nécessite des configurations de recette spécifiques, compilées dans un seul fichier JSON (JavaScript Object Notation), cette compilation de configurations de recette est appelée fichier de configuration. Une recette empaquetée avec un ensemble particulier de configurations est appelée instance de recette. Une recette peut être utilisée pour créer de nombreuses instances de recette dans [!DNL Data Science Workspace].

Voici les différentes étapes du workflow d’importation d’une recette empaquetée :
- [Configuration d’une recette](#configure)
- [Importation d’une recette Docker - Python](#python)
- [Importation d’une recette Docker - R](#r)
- [Importer une recette basée sur un Docker - PySpark](#pyspark)
- [Recette basée sur un Docker d&#39;importation - Scala](#scala)

### Configuration d’une recette {#configure}

Chaque instance de recette dans [!DNL Data Science Workspace] est accompagnée d&#39;un ensemble de configurations qui adaptent l&#39;instance de recette à un cas d&#39;utilisation particulier. Les fichiers de configuration définissent les comportements de formation et de notation par défaut d’un modèle créé à l’aide de cette instance de recette.

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

Pour les besoins de ce didacticiel, vous pouvez laisser les fichiers de configuration par défaut pour la recette Ventes au détail dans la référence [!DNL Data Science Workspace] de la manière dont ils sont.

### Importation d’une recette Docker - [!DNL Python] {#python}

Début en naviguant et en sélectionnant **[!UICONTROL Workflows]** dans le coin supérieur gauche de l&#39;interface utilisateur [!DNL Platform]. Ensuite, sélectionnez **Importer la recette** et sélectionnez **[!UICONTROL Lancer]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

La page **Configurer** du flux de travaux **Importer la recette** s&#39;affiche. Entrez un nom et une description pour la recette, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit.

![configurer le workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Dans le tutoriel [Former une recette empaquetée à partir de fichiers source](./package-source-files-recipe.md), une URL Docker a été fournie à la fin de la création de la recette Ventes au détail à l’aide de fichiers source Python.

Une fois que vous êtes sur la page **Sélectionner la source**, collez l&#39;URL du Docker correspondant à la recette assemblée générée à l&#39;aide des fichiers source [!DNL Python] dans le champ **[!UICONTROL URL de la source]**. Importez ensuite le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le **Navigateur** du système de fichiers. Le fichier de configuration fourni se trouve ici : `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Sélectionnez **[!UICONTROL Python]** dans la liste déroulante **Runtime** et **[!UICONTROL Classification]** dans la liste déroulante **Type**. Une fois que tout a été rempli, sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour passer à **Gérer les schémas**.

>[!NOTE]
>
> Type prend en charge **[!UICONTROL Classification]** et **[!UICONTROL Régression]**. Si votre modèle ne tombe pas sous l&#39;un de ces types, sélectionnez **[!UICONTROL Personnalisé]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Ensuite, sélectionnez les schémas d&#39;entrée et de sortie des ventes au détail sous la section **Gérer les Schémas**, ils ont été créés à l&#39;aide du script d&#39;amorçage fourni dans le didacticiel [créer le schéma de vente au détail et le jeu de données](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Dans la section **Gestion des fonctionnalités**, sélectionnez sur votre identification de client dans le lecteur de schéma pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctionnalités d’entrée et de sortie en mettant en surbrillance la fonctionnalité souhaitée, puis sélectionnez **[!UICONTROL Fonctionnalité d’entrée]** ou **[!UICONTROL Fonctionnalité cible]** dans la fenêtre **[!UICONTROL Propriétés du champ]** à droite. Pour les besoins de ce tutoriel, définissez **[!UICONTROL weeklySales]** en tant que **[!UICONTROL Fonctionnalité cible]** et tout le reste en tant que **[!UICONTROL Fonctionnalité d’entrée]**. Sélectionnez **[!UICONTROL Suivant]** pour examiner votre nouvelle recette configurée.

Vérifiez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Sélectionnez **[!UICONTROL Finish]** pour créer la recette.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez aux [étapes suivantes](#next-steps) pour savoir comment créer un modèle dans [!DNL Data Science Workspace] à l&#39;aide de la recette de vente au détail nouvellement créée.

### Importation d’une recette Docker - R {#r}

Début en naviguant et en sélectionnant **[!UICONTROL Workflows]** dans le coin supérieur gauche de l&#39;interface utilisateur [!DNL Platform]. Ensuite, sélectionnez **Importer la recette** et sélectionnez **[!UICONTROL Lancer]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

La page **Configurer** du flux de travaux **Importer la recette** s&#39;affiche. Entrez un nom et une description pour la recette, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit.

![configurer le workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Dans le tutoriel [Former une recette empaquetée à partir de fichiers source](./package-source-files-recipe.md), une URL Docker a été fournie à la fin de la création de la recette Ventes au détail à l’aide de fichiers source R.

Une fois que vous êtes sur la page **Sélectionner la source**, collez l&#39;URL du Docker correspondant à la recette assemblée générée à l&#39;aide des fichiers source R dans le champ **[!UICONTROL URL source]**. Importez ensuite le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le **Navigateur** du système de fichiers. Le fichier de configuration fourni se trouve ici : `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Sélectionnez **[!UICONTROL R]** dans la liste déroulante **Exécution** et **[!UICONTROL Classification]** dans la liste déroulante **Type**. Une fois que tout a été rempli, sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour passer à **Gérer les schémas**.

>[!NOTE]
>
> ** Typesupports  **** Classification et  **[!UICONTROL Régression]**. Si votre modèle ne tombe pas sous l&#39;un de ces types, sélectionnez **[!UICONTROL Personnalisé]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Ensuite, sélectionnez les schémas d&#39;entrée et de sortie des ventes au détail sous la section **Gérer les Schémas**, ils ont été créés à l&#39;aide du script d&#39;amorçage fourni dans le didacticiel [créer le schéma de vente au détail et le jeu de données](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Dans la section *Gestion des fonctionnalités*, sélectionnez sur votre identification de client dans le lecteur de schéma pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctionnalités d’entrée et de sortie en mettant en surbrillance la fonctionnalité souhaitée, puis sélectionnez **[!UICONTROL Fonctionnalité d’entrée]** ou **[!UICONTROL Fonctionnalité cible]** dans la fenêtre **[!UICONTROL Propriétés du champ]** à droite. Pour les besoins de ce tutoriel, définissez **[!UICONTROL weeklySales]** en tant que **[!UICONTROL Fonctionnalité cible]** et tout le reste en tant que **[!UICONTROL Fonctionnalité d’entrée]**. Sélectionnez **[!UICONTROL Suivant]** pour examiner votre nouvelle recette configurée.

Vérifiez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Sélectionnez **Finish** pour créer la recette.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez aux [étapes suivantes](#next-steps) pour savoir comment créer un modèle dans [!DNL Data Science Workspace] à l&#39;aide de la recette de vente au détail nouvellement créée.

### Recette basée sur un Docker d&#39;importation - PySpark {#pyspark}

Début en naviguant et en sélectionnant **[!UICONTROL Workflows]** dans le coin supérieur gauche de l&#39;interface utilisateur [!DNL Platform]. Ensuite, sélectionnez **Importer la recette** et sélectionnez **[!UICONTROL Lancer]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

La page **Configurer** du flux de travaux **Importer la recette** s&#39;affiche. Entrez un nom et une description pour la recette, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![configurer le workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Dans le [didacticiel Package des fichiers source dans une recette](./package-source-files-recipe.md), une URL Docker a été fournie à la fin de la création de la recette Ventes au détail à l’aide des fichiers source PySpark.

Une fois que vous êtes sur la page **Sélectionner la source**, collez l&#39;URL du Docker correspondant à la recette assemblée générée à l&#39;aide des fichiers source PySpark dans le champ **[!UICONTROL URL de la source]**. Importez ensuite le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le **Navigateur** du système de fichiers. Le fichier de configuration fourni se trouve ici : `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Sélectionnez **[!UICONTROL PySpark]** dans la liste déroulante **Runtime**. Une fois que le runtime PySpark est sélectionné, l&#39;artefact par défaut est automatiquement renseigné sur **[!UICONTROL Docker]**. Ensuite, sélectionnez **[!UICONTROL Classification]** dans la liste déroulante **Type**. Une fois que tout a été rempli, sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour passer à **Gérer les schémas**.

>[!NOTE]
>
> ** Typesupports  **** Classification et  **[!UICONTROL Régression]**. Si votre modèle ne tombe pas sous l&#39;un de ces types, sélectionnez **[!UICONTROL Personnalisé]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Ensuite, sélectionnez les schémas d&#39;entrée et de sortie des ventes au détail à l&#39;aide du sélecteur **Gérer les Schémas**, les schémas ont été créés à l&#39;aide du script d&#39;amorçage fourni dans le didacticiel [créer le schéma de vente au détail et le jeu de données](../models-recipes/create-retails-sales-dataset.md).

![gérer les schémas](../images/models-recipes/import-package-ui/manage-schemas.png)

Dans la section **Gestion des fonctionnalités**, sélectionnez sur votre identification de client dans le lecteur de schéma pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctionnalités d’entrée et de sortie en mettant en surbrillance la fonctionnalité souhaitée, puis sélectionnez **[!UICONTROL Fonctionnalité d’entrée]** ou **[!UICONTROL Fonctionnalité cible]** dans la fenêtre **[!UICONTROL Propriétés du champ]** à droite. Pour les besoins de ce tutoriel, définissez **[!UICONTROL weeklySales]** en tant que **[!UICONTROL Fonctionnalité cible]** et tout le reste en tant que **[!UICONTROL Fonctionnalité d’entrée]**. Sélectionnez **[!UICONTROL Suivant]** pour examiner votre nouvelle recette configurée.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Vérifiez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Sélectionnez **[!UICONTROL Finish]** pour créer la recette.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez aux [étapes suivantes](#next-steps) pour savoir comment créer un modèle dans [!DNL Data Science Workspace] à l&#39;aide de la recette de vente au détail nouvellement créée.

### Recette basée sur un Docker d&#39;importation - Scala {#scala}

Début en naviguant et en sélectionnant **[!UICONTROL Workflows]** dans le coin supérieur gauche de l&#39;interface utilisateur [!DNL Platform]. Ensuite, sélectionnez **Importer la recette** et sélectionnez **[!UICONTROL Lancer]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

La page **Configurer** du flux de travaux **Importer la recette** s&#39;affiche. Entrez un nom et une description pour la recette, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![configurer le workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Dans le didacticiel [compresser les fichiers source dans une recette](./package-source-files-recipe.md), une URL Docker a été fournie à la fin de la création de la recette de vente au détail à l’aide des fichiers source Scala ([!DNL Spark]).

Une fois que vous êtes sur la page **Sélectionner la source**, collez l&#39;URL du Docker correspondant à la recette assemblée générée à l&#39;aide des fichiers source Scala dans le champ URL source. Importez ensuite le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le Navigateur du système de fichiers. Le fichier de configuration fourni se trouve ici : `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Sélectionnez **[!UICONTROL Spark]** dans la liste déroulante **Exécution**. Une fois l&#39;exécution [!DNL Spark] sélectionnée, l&#39;artefact par défaut est automatiquement renseigné en **[!UICONTROL Docker]**. Ensuite, sélectionnez **[!UICONTROL Régression]** dans la liste déroulante **Type**. Une fois que tout a été rempli, sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour passer à **Gérer les schémas**.

>[!NOTE]
>
> Type prend en charge **[!UICONTROL Classification]** et **[!UICONTROL Régression]**. Si votre modèle ne tombe pas sous l&#39;un de ces types, sélectionnez **[!UICONTROL Personnalisé]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Ensuite, sélectionnez les schémas d&#39;entrée et de sortie des ventes au détail à l&#39;aide du sélecteur **Gérer les Schémas**, les schémas ont été créés à l&#39;aide du script d&#39;amorçage fourni dans le didacticiel [créer le schéma de vente au détail et le jeu de données](../models-recipes/create-retails-sales-dataset.md).

![gérer les schémas](../images/models-recipes/import-package-ui/manage-schemas.png)

Dans la section **Gestion des fonctionnalités**, sélectionnez sur votre identification de client dans le lecteur de schéma pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctionnalités d’entrée et de sortie en mettant en surbrillance la fonctionnalité souhaitée, puis sélectionnez **[!UICONTROL Fonctionnalité d’entrée]** ou **[!UICONTROL Fonctionnalité cible]** dans la fenêtre **[!UICONTROL Propriétés du champ]** à droite. Pour les besoins de ce didacticiel, définissez &quot;[!UICONTROL weeklySales]&quot; comme **[!UICONTROL Fonction de Cible]** et tout le reste comme **[!UICONTROL Fonction d&#39;entrée]**. Sélectionnez **[!UICONTROL Suivant]** pour examiner votre nouvelle recette configurée.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Vérifiez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Sélectionnez **[!UICONTROL Finish]** pour créer la recette.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez aux [étapes suivantes](#next-steps) pour savoir comment créer un modèle dans [!DNL Data Science Workspace] à l&#39;aide de la recette de vente au détail nouvellement créée.

## Étapes suivantes {#next-steps}

Ce didacticiel fournit des informations sur la configuration et l&#39;importation d&#39;une recette dans [!DNL Data Science Workspace]. Vous pouvez désormais créer, former et évaluer un modèle à l’aide de la nouvelle recette créée.

- [Formation et évaluation d’un modèle dans l’interface utilisateur](./train-evaluate-model-ui.md)
- [Formation et évaluation d’un modèle à l’aide de l’API](./train-evaluate-model-api.md)
