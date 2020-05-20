---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Importer une recette emballée (interface utilisateur)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c
workflow-type: tm+mt
source-wordcount: '2451'
ht-degree: 0%

---


# Importer une recette emballée (interface utilisateur)

Ce didacticiel explique comment configurer et importer une recette assemblée à l&#39;aide de l&#39;exemple Ventes au détail fourni. D’ici la fin de ce didacticiel, vous serez prêt à créer, à former et à évaluer un modèle dans l’espace de travail des données de la plateforme Adobe Experience Platform.

## Conditions préalables

Ce didacticiel nécessite une recette empaquetée sous la forme d&#39;une URL d&#39;image Docker. Pour plus d&#39;informations, consultez le didacticiel sur la façon de [compresser les fichiers source dans une recette](./package-source-files-recipe.md) .

## Processus de l’interface utilisateur

L&#39;importation d&#39;une recette empaquetée dans Data Science Workspace requiert des configurations de recette spécifiques, compilées dans un seul fichier JSON (JavaScript Object Notation), cette compilation de configurations de recette est appelée fichier **de** configuration. Une recette assemblée avec un ensemble particulier de configurations est appelée instance **de** recette. Une recette peut être utilisée pour créer de nombreuses instances de recette dans Data Science Workspace.

Le processus d&#39;importation d&#39;une recette de package comprend les étapes suivantes :
- [Configurer une recette](#configure)
- [Importer une recette basée sur un Docker - Python](#python)
- [Importer une recette basée sur un Docker - R](#r)
- [Importer une recette basée sur un Docker - PySpark](#pyspark)
- [Recette basée sur un Docker d&#39;importation - Scala](#scala)

workflows obsolètes :
- [Importer une recette binaire - PySpark](#pyspark-deprecated)
- [Importer une recette binaire - Scala Spark](#scala-deprecated)

### Configurer une recette {#configure}

Chaque instance de recette dans Data Science Workspace est accompagnée d’un ensemble de configurations qui adaptent l’instance de recette à un cas d’utilisation particulier. Les fichiers de configuration définissent les comportements de formation et de notation par défaut d&#39;un modèle créé à l&#39;aide de cette instance de recette.

>[!NOTE] Les fichiers de configuration sont spécifiques à la recette et à la casse.

Vous trouverez ci-dessous un exemple de fichier de configuration présentant les comportements de formation et de notation par défaut pour la recette Ventes au détail.

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

| Clé de paramètre | Type | Description |
| ----- | ----- | ----- |
| `learning_rate` | Nombre | Échelle pour la multiplication des dégradés. |
| `n_estimators` | Nombre | Nombre d&#39;arbres dans la forêt pour le classificateur de forêt aléatoire. |
| `max_depth` | Nombre | Profondeur maximale d’un arbre dans le classificateur de forêt aléatoire. |
| `ACP_DSW_INPUT_FEATURES` | Chaîne | Liste d’attributs de schéma d’entrée séparés par des virgules. |
| `ACP_DSW_TARGET_FEATURES` | Chaîne | Liste des attributs de schéma de sortie séparés par des virgules. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booléen | Détermine si les fonctions d’entrée et de sortie peuvent être modifiées. |
| `tenantId` | Chaîne | Cet identifiant permet de s’assurer que les ressources que vous créez sont correctement espacées de noms et qu’elles sont contenues dans votre organisation IMS. [Suivez les étapes ci-dessous](../../xdm/api/getting-started.md#know-your-tenant_id) pour trouver votre ID de client. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Chaîne | schéma d&#39;entrée utilisé pour la formation d&#39;un modèle. Laissez ce champ vide lors de l’importation dans l’interface utilisateur, remplacez-le par l’ID de schéma de formation lors de l’importation à l’aide de l’API. |
| `evaluation.labelColumn` | Chaîne | Libellé de colonne pour les visualisations d’évaluation. |
| `evaluation.metrics` | Chaîne | liste séparée par des virgules des mesures d&#39;évaluation à utiliser pour évaluer un modèle. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Chaîne | schéma de sortie utilisé pour marquer un modèle. Laissez ce champ vide lors de l’importation dans l’interface utilisateur, remplacez-le par un ID de schéma d’évaluation lors de l’importation à l’aide de l’API. |

Pour les besoins de ce didacticiel, vous pouvez laisser les fichiers de configuration par défaut de la recette Ventes au détail dans Data Science Workspace Reference comme ils sont.

### Importer une recette basée sur un Docker - Python {#python}

Début en naviguant et en sélectionnant **[!UICONTROL des Workflows]** situés dans le coin supérieur gauche de l’interface utilisateur de la plate-forme. Ensuite, sélectionnez *Importer la recette* et cliquez sur **[!UICONTROL Lancer]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

La page *Configurer* pour le flux de travail *Importer une recette* s&#39;affiche. Entrez un nom et une description pour la recette, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit.

![configurer le workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> Dans les fichiers source du [package dans un didacticiel Recette](./package-source-files-recipe.md) , une URL Docker a été fournie à la fin de la création de la recette Ventes au détail à l&#39;aide de fichiers source Python.

Une fois que vous êtes sur la page *Sélectionner la source* , collez l&#39;URL du Docker correspondant à la recette empaquetée créée à l&#39;aide de fichiers source Python dans le champ URL **** source. Importez ensuite le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le **navigateur** du système de fichiers. Le fichier de configuration fourni se trouve sur `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Sélectionnez **[!UICONTROL Python]** dans la liste déroulante *Runtime* et **[!UICONTROL Classification]** dans la liste déroulante *Type.* Une fois que tout a été renseigné, cliquez sur **[!UICONTROL Suivant]** dans le coin supérieur droit pour accéder à *Gérer les schémas*.

>[!NOTE]
> *Type *prend en charge la **[!UICONTROL classification]**et **[!UICONTROL la régression]**. Si votre modèle ne tombe pas sous l&#39;un de ces types, sélectionnez **[!UICONTROL Personnalisé]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Ensuite, sélectionnez les schémas d&#39;entrée et de sortie des ventes au détail sous la section *Gérer les Schémas*, ils ont été créés à l&#39;aide du script d&#39;amorçage fourni dans le didacticiel [Création du schéma de vente au détail et du jeu de données](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Sous la section Gestion des *fonctionnalités* , cliquez sur votre identification de client dans le lecteur de schéma pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctions d’entrée et de sortie en mettant en surbrillance la fonction souhaitée et en sélectionnant Fonction **[!UICONTROL d’]** entrée ou Fonction **[!UICONTROL de]** Cible dans la fenêtre Propriétés **[!UICONTROL du]** champ de droite. Pour les besoins de ce didacticiel, définissez **[!UICONTROL weeklySales]** comme fonction **[!UICONTROL de]** Cible et tout le reste comme fonction **[!UICONTROL de]** saisie. Cliquez sur **[!UICONTROL Suivant]** pour examiner votre nouvelle recette configurée.

Consultez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Cliquez sur **[!UICONTROL Terminer]** pour créer la recette.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez aux étapes [](#next-steps) suivantes pour découvrir comment créer un modèle dans Data Science Workspace à l’aide de la nouvelle recette Ventes au détail.

### Importer une recette basée sur un Docker - R {#r}

Début en naviguant et en sélectionnant **[!UICONTROL des Workflows]** situés dans le coin supérieur gauche de l’interface utilisateur de la plate-forme. Ensuite, sélectionnez *Importer la recette* et cliquez sur **[!UICONTROL Lancer]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

La page *Configurer* pour le flux de travail *Importer une recette* s&#39;affiche. Entrez un nom et une description pour la recette, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit.

![configurer le workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> Dans le didacticiel Recette [des fichiers source du](./package-source-files-recipe.md) package, une URL du Docker a été fournie à la fin de la création de la recette Ventes au détail à l&#39;aide de fichiers source R.

Une fois que vous êtes sur la page *Sélectionner la source* , collez l&#39;URL du Docker correspondant à la recette assemblée générée à l&#39;aide des fichiers source R dans le champ URL **** source. Importez ensuite le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le **navigateur** du système de fichiers. Le fichier de configuration fourni se trouve sur `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Sélectionnez **[!UICONTROL R]** dans la liste déroulante *Exécution* et **[!UICONTROL Classification]** dans la liste déroulante *Type.* Une fois que tout a été renseigné, cliquez sur **[!UICONTROL Suivant]** dans le coin supérieur droit pour accéder à *Gérer les schémas*.

>[!NOTE]
> *Type *prend en charge la **[!UICONTROL classification]**et **[!UICONTROL la régression]**. Si votre modèle ne tombe pas sous l&#39;un de ces types, sélectionnez **[!UICONTROL Personnalisé]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Ensuite, sélectionnez les schémas d&#39;entrée et de sortie des ventes au détail sous la section *Gérer les Schémas*, ils ont été créés à l&#39;aide du script d&#39;amorçage fourni dans le didacticiel [Création du schéma de vente au détail et du jeu de données](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Sous la section Gestion des *fonctionnalités* , cliquez sur votre identification de client dans le lecteur de schéma pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctions d’entrée et de sortie en mettant en surbrillance la fonction souhaitée et en sélectionnant Fonction **[!UICONTROL d’]** entrée ou Fonction **[!UICONTROL de]** Cible dans la fenêtre Propriétés **[!UICONTROL du]** champ de droite. Pour les besoins de ce didacticiel, définissez **[!UICONTROL weeklySales]** comme fonction **[!UICONTROL de]** Cible et tout le reste comme fonction **[!UICONTROL de]** saisie. Cliquez sur **[!UICONTROL Suivant]** pour passer en revue votre nouvelle recette configurée.

Consultez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Cliquez sur **Terminer** pour créer la recette.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez aux étapes [](#next-steps) suivantes pour découvrir comment créer un modèle dans Data Science Workspace à l’aide de la nouvelle recette Ventes au détail.

### Importer une recette basée sur un Docker - PySpark {#pyspark}

Début en naviguant et en sélectionnant **[!UICONTROL des Workflows]** situés dans le coin supérieur gauche de l’interface utilisateur de la plate-forme. Ensuite, sélectionnez *Importer la recette* et cliquez sur **[!UICONTROL Lancer]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

La page *Configurer* pour le flux de travail *Importer une recette* s&#39;affiche. Entrez un nom et une description pour la recette, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![configurer le workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> Dans le didacticiel Recette [des fichiers source du](./package-source-files-recipe.md) package, une URL de Docker a été fournie à la fin de la création de la recette Ventes au détail à l’aide des fichiers source PySpark.

Une fois que vous êtes sur la page *Sélectionner la source* , collez l&#39;URL du Docker correspondant à la recette assemblée générée à l&#39;aide des fichiers source PySpark dans le champ URL **** source. Importez ensuite le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le **navigateur** du système de fichiers. Le fichier de configuration fourni se trouve sur `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Sélectionnez **[!UICONTROL PySpark]** dans la liste déroulante *Runtime* . Une fois l&#39;exécution de PySpark sélectionnée, l&#39;artefact par défaut est automatiquement renseigné sur **[!UICONTROL Docker]**. Ensuite, sélectionnez **[!UICONTROL Classification]** dans la liste déroulante *Type* . Une fois que tout a été renseigné, cliquez sur **[!UICONTROL Suivant]** dans le coin supérieur droit pour accéder à *Gérer les schémas*.

>[!NOTE]
> *Type *prend en charge la **[!UICONTROL classification]**et **[!UICONTROL la régression]**. Si votre modèle ne tombe pas sous l&#39;un de ces types, sélectionnez **[!UICONTROL Personnalisé]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Ensuite, sélectionnez les schémas d&#39;entrée et de sortie des ventes au détail sous la section *Gérer les Schémas*, ils ont été créés à l&#39;aide du script d&#39;amorçage fourni dans le didacticiel [Création du schéma de vente au détail et du jeu de données](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Sous la section Gestion des *fonctionnalités* , cliquez sur votre identification de client dans le lecteur de schéma pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctions d’entrée et de sortie en mettant en surbrillance la fonction souhaitée et en sélectionnant Fonction **[!UICONTROL d’]** entrée ou Fonction **[!UICONTROL de]** Cible dans la fenêtre Propriétés **[!UICONTROL du]** champ de droite. Pour les besoins de ce didacticiel, définissez **[!UICONTROL weeklySales]** comme fonction **[!UICONTROL de]** Cible et tout le reste comme fonction **[!UICONTROL de]** saisie. Cliquez sur **[!UICONTROL Suivant]** pour examiner votre nouvelle recette configurée.

Consultez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Cliquez sur **[!UICONTROL Terminer]** pour créer la recette.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez aux étapes [](#next-steps) suivantes pour découvrir comment créer un modèle dans Data Science Workspace à l’aide de la nouvelle recette Ventes au détail.

### Recette basée sur un Docker d&#39;importation - Scala {#scala}

Début en naviguant et en sélectionnant **[!UICONTROL des Workflows]** situés dans le coin supérieur gauche de l’interface utilisateur de la plate-forme. Ensuite, sélectionnez *Importer la recette* et cliquez sur **[!UICONTROL Lancer]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

La page *Configurer* pour le flux de travail *Importer une recette* s&#39;affiche. Entrez un nom et une description pour la recette, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![configurer le workflow](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> Dans les fichiers source du [package dans un didacticiel Recette](./package-source-files-recipe.md) , une URL Docker a été fournie à la fin de la création de la recette Ventes au détail à l’aide des fichiers source Scala (Spark).

Une fois que vous êtes sur la page *Sélectionner la source* , collez l&#39;URL du Docker correspondant à la recette assemblée générée à l&#39;aide des fichiers source Scala dans le champ URL ** source. Importez ensuite le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le **navigateur** du système de fichiers. Le fichier de configuration fourni se trouve sur `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Sélectionnez **[!UICONTROL Spark]** dans la liste déroulante *Runtime* . Une fois l&#39;exécution Spark sélectionnée, l&#39;artefact par défaut est automatiquement renseigné sur **[!UICONTROL Docker]**. Ensuite, sélectionnez **[!UICONTROL Régression]** dans la liste déroulante *Type* . Une fois que tout a été renseigné, cliquez sur **[!UICONTROL Suivant]** dans le coin supérieur droit pour accéder à *Gérer les schémas*.

>[!NOTE]
> *Type *prend en charge la **[!UICONTROL classification]**et **[!UICONTROL la régression]**. Si votre modèle ne tombe pas sous l&#39;un de ces types, sélectionnez **[!UICONTROL Personnalisé]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Ensuite, sélectionnez les schémas d&#39;entrée et de sortie des ventes au détail sous la section *Gérer les Schémas*, ils ont été créés à l&#39;aide du script d&#39;amorçage fourni dans le didacticiel [Création du schéma de vente au détail et du jeu de données](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Sous la section Gestion des *fonctionnalités* , cliquez sur votre identification de client dans le lecteur de schéma pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctions d’entrée et de sortie en mettant en surbrillance la fonction souhaitée et en sélectionnant Fonction **[!UICONTROL d’]** entrée ou Fonction **[!UICONTROL de]** Cible dans la fenêtre Propriétés **[!UICONTROL du]** champ de droite. Pour les besoins de ce didacticiel, définissez **[!UICONTROL weeklySales]** comme fonction **[!UICONTROL de]** Cible et tout le reste comme fonction **[!UICONTROL de]** saisie. Cliquez sur **[!UICONTROL Suivant]** pour examiner votre nouvelle recette configurée.

Consultez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Cliquez sur **[!UICONTROL Terminer]** pour créer la recette.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez aux étapes [](#next-steps) suivantes pour découvrir comment créer un modèle dans Data Science Workspace à l’aide de la nouvelle recette Ventes au détail.

## Étapes suivantes {#next-steps}

Ce didacticiel fournit des informations sur la configuration et l&#39;importation d&#39;une recette dans Data Science Workspace. Vous pouvez désormais créer, former et évaluer un modèle à l&#39;aide de la recette nouvellement créée.

- [Formation et évaluation d&#39;un modèle dans l&#39;interface utilisateur](./train-evaluate-model-ui.md)
- [Formation et évaluation d&#39;un modèle à l&#39;aide de l&#39;API](./train-evaluate-model-api.md)

## workflows obsolètes

>[!CAUTION]
>L&#39;importation de recettes binaires n&#39;est plus prise en charge dans PySpark 3 (Spark 2.4) et Scala (Spark 2.4).

### Importer une recette binaire - PySpark {#pyspark-deprecated}

Dans le didacticiel Recette [des fichiers source du](./package-source-files-recipe.md) package, un fichier binaire **EGG** a été créé à l’aide des fichiers source PySpark des ventes au détail.

1. Dans [Adobe Experience Platform](https://platform.adobe.com/), recherchez le panneau de navigation de gauche et cliquez sur **Workflows**. Dans l&#39;interface Workflows, **lancez** un nouveau processus **Importer la recette à partir du fichier** source.
   ![](../images/models-recipes/import-package-ui/workflow_ss.png)
2. Saisissez un nom approprié pour la recette Ventes au détail. Par exemple, &quot;Recette de vente au détail PySpark&quot;. Vous pouvez éventuellement inclure une description de recette et une URL de documentation. Cliquez sur **Suivant** lorsque vous avez terminé.
   ![](../images/models-recipes/import-package-ui/recipe_info.png)
3. Importez la recette Ventes au détail PySpark qui a été créée dans les fichiers source du [package dans un didacticiel Recette](./package-source-files-recipe.md) en la faisant glisser et en la déposant, ou utilisez le **navigateur** du système de fichiers. La recette emballée doit être située dans `experience-platform-dsw-reference/recipes/pyspark/dist`.
De même, importez le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le **Navigateur** du système de fichiers. Le fichier de configuration fourni se trouve sur `experience-platform-dsw-reference/recipes/pyspark/pipeline.json`. Cliquez sur **Suivant** lorsque les deux fichiers ont été fournis.
   ![](../images/models-recipes/import-package-ui/recipe_source.png)
4. Vous pouvez rencontrer des erreurs à ce stade. Il s&#39;agit d&#39;un comportement normal et il faut s&#39;y attendre. Sélectionnez les schémas d&#39;entrée et de sortie des ventes au détail sous la section **Gérer les Schémas**, ils ont été créés à l&#39;aide du script d&#39;amorçage fourni dans le didacticiel [Création du schéma de vente au détail et du jeu de données](../models-recipes/create-retails-sales-dataset.md) .
   ![](../images/models-recipes/import-package-ui/recipe_schema.png)
Sous la section Gestion des **fonctionnalités** , cliquez sur votre identification de client dans le lecteur de schéma pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctions d’entrée et de sortie en mettant en surbrillance la fonction souhaitée et en sélectionnant Fonction **d’** entrée ou Fonction **de** Cible dans la fenêtre Propriétés **du** champ de droite. Pour les besoins de ce didacticiel, définissez **weeklySales** comme fonction **de** Cible et tout le reste comme fonction **de** saisie. Cliquez sur **Suivant** pour examiner votre nouvelle recette configurée.
5. Consultez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Cliquez sur **Terminer** pour créer la recette.
   ![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez aux étapes [](#next-steps) suivantes pour découvrir comment créer un modèle dans Data Science Workspace à l’aide de la nouvelle recette Ventes au détail.


### Importer une recette binaire - Scala Spark {#scala-deprecated}

Dans le didacticiel Recette [des fichiers source du](./package-source-files-recipe.md) package, un fichier binaire **JAR** a été créé à l’aide des fichiers source Scala Spark de vente au détail.

1. Dans [Adobe Experience Platform](https://platform.adobe.com/), recherchez le panneau de navigation de gauche et cliquez sur **Workflows**. Dans l&#39;interface Workflows, **lancez** un nouveau processus **Importer la recette à partir du fichier** source.
   ![](../images/models-recipes/import-package-ui/workflow_ss.png)
2. Saisissez un nom approprié pour la recette Ventes au détail. Par exemple, &quot;Recette de vente au détail Scala Spark&quot;. Vous pouvez éventuellement inclure une description de recette et une URL de documentation. Cliquez sur **Suivant** lorsque vous avez terminé.
   ![](../images/models-recipes/import-package-ui/recipe_info_scala.png)
3. Importez la recette Ventes au détail Scala Spark qui a été créée dans les fichiers source du [package dans un didacticiel Recette](./package-source-files-recipe.md) en faisant glisser et en déposant, ou utilisez le **navigateur** du système de fichiers. La recette emballée **avec dépendances** se trouve dans `experience-platform-dsw-reference/recipes/scala/target`. De même, importez le fichier de configuration fourni en le faisant glisser et en le déposant, ou utilisez le **Navigateur** du système de fichiers. Le fichier de configuration fourni se trouve sur `experience-platform-dsw-reference/recipes/scala/src/main/resources/pipelineservice.json`. Cliquez sur **Suivant** lorsque les deux fichiers ont été fournis.
   ![](../images/models-recipes/import-package-ui/recipe_source_scala.png)
4. Vous pouvez rencontrer des erreurs à ce stade. Il s&#39;agit d&#39;un comportement normal et il faut s&#39;y attendre. Sélectionnez les schémas d&#39;entrée et de sortie des ventes au détail sous la section **Gérer les Schémas**, ils ont été créés à l&#39;aide du script d&#39;amorçage fourni dans le didacticiel [Création du schéma de vente au détail et du jeu de données](../models-recipes/create-retails-sales-dataset.md) .
   ![](../images/models-recipes/import-package-ui/recipe_schema.png)
Sous la section Gestion des **fonctionnalités** , cliquez sur votre identification de client dans le lecteur de schéma pour développer le schéma d’entrée Ventes au détail. Sélectionnez les fonctions d’entrée et de sortie en mettant en surbrillance la fonction souhaitée et en sélectionnant Fonction **d’** entrée ou Fonction **de** Cible dans la fenêtre Propriétés **du** champ de droite. Pour les besoins de ce didacticiel, définissez **weeklySales** comme fonction **de** Cible et tout le reste comme fonction **de** saisie. Cliquez sur **Suivant** pour examiner votre nouvelle recette configurée.
5. Consultez la recette, ajoutez, modifiez ou supprimez des configurations si nécessaire. Cliquez sur **Terminer** pour créer la recette.
   ![](../images/models-recipes/import-package-ui/recipe_review.png)

Passez aux étapes [](#next-steps) suivantes pour découvrir comment créer un modèle dans Data Science Workspace à l’aide de la nouvelle recette Ventes au détail.