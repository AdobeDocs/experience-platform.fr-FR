---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics;create a model;create a training run
solution: Experience Platform
title: Formation et évaluation d’un modèle (interface utilisateur)
topic: tutorial
type: Tutorial
description: Dans Adobe Experience Platform Data Science Workspace, un modèle d’apprentissage automatique est créé en incorporant une recette existante adéquate au but du modèle. Le modèle est ensuite formé et évalué afin d’optimiser son efficience et son efficacité opérationnelles en affinant ses hyperparamètres associés. Les recettes sont réutilisables, ce qui signifie que plusieurs modèles peuvent être créés et adaptés à des fins spécifiques à l’aide d’une seule recette.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 95%

---


# Formation et évaluation d’un modèle (interface utilisateur)

Dans Adobe Experience Platform Data Science Workspace, un modèle d’apprentissage automatique est créé en incorporant une recette existante adéquate au but du modèle. Le modèle est ensuite formé et évalué afin d’optimiser son efficience et son efficacité opérationnelles en affinant ses hyperparamètres associés. Les recettes sont réutilisables, ce qui signifie que plusieurs modèles peuvent être créés et adaptés à des fins spécifiques à l’aide d’une seule recette.

Ce tutoriel décrit les étapes à suivre pour créer, former et évaluer un modèle.

## Prise en main

Pour suivre ce tutoriel, vous devez avoir accès à [!DNL Experience Platform]. If you do not have access to an IMS Organization in [!DNL Experience Platform], please speak to your system administrator before proceeding.

Ce tutoriel nécessite une recette existante. Si vous ne possédez aucune recette, suivez le tutoriel [Importation d’une recette empaquetée dans l’interface utilisateur](./import-packaged-recipe-ui.md) avant de continuer.

## Création d’un modèle

1. Dans Adobe Experience Platform, cliquez sur le lien **[!UICONTROL Modèles]** situé dans la colonne de navigation de gauche pour tous les modèles existants. Cliquez sur **[!UICONTROL Créer un modèle]** près du coin supérieur droit de la page pour lancer un processus de création de modèles.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Parcourez la liste des recettes existantes, recherchez et sélectionnez la recette à utiliser pour créer le modèle, puis cliquez sur **[!UICONTROL Suivant]**.
   ![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

3. Sélectionnez le jeu de données d’entrée adéquat, puis cliquez sur **[!UICONTROL Suivant]**. Cette opération définit le jeu de données de formation d’entrée par défaut pour le modèle.
   ![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

4. Attribuez un nom au modèle et passez en revue les configurations de modèle par défaut. Les configurations par défaut ont été appliquées lors de la création de la recette. Vérifiez et modifiez les valeurs de configuration en double-cliquant sur celles-ci. Pour fournir un nouvel ensemble de configurations, cliquez sur **[!UICONTROL Charger une nouvelle configuration]** et faites glisser un fichier JSON contenant des configurations de modèle dans la fenêtre du navigateur. Cliquez sur **[!UICONTROL Terminer]** pour créer le modèle.

   >[!NOTE]
   >
   >Les configurations sont uniques et spécifiques à leur recette de destination : cela signifie que les configurations pour la recette des ventes au détail ne fonctionneront pas pour la recette des recommandations de produit. Reportez-vous à la section [référence](#reference) pour une liste des configurations de la recette de ventes au détail.

   ![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Création d’une opération de formation

1. Dans Adobe Experience Platform, cliquez sur le lien **[!UICONTROL Modèles]** situé dans la colonne de navigation de gauche pour tous les modèles existants. Recherchez et cliquez sur le nom du modèle à former.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Toutes les sessions de formation existantes ainsi que leur état actuel sont répertoriées. For Models created using the [!DNL Data Science Workspace] user interface, a training run is automatically generated and executed using the default configurations and input training dataset.
   ![](../images/models-recipes/train-evaluate-ui/model_overview.png)

3. Créez une nouvelle opération de formation en cliquant sur **[!UICONTROL Former]** près du coin supérieur droit de la page d’aperçu du modèle.
   ![](../images/models-recipes/train-evaluate-ui/training_input.png)

4. Sélectionnez le jeu de données de formation d’entrée pour l’opération de formation, puis cliquez sur **[!UICONTROL Suivant]**.
   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

5. Les configurations par défaut fournies lors de la création du modèle s’affichent : modifiez-les en conséquence en double-cliquant sur les valeurs. Cliquez sur **[!UICONTROL Terminer]** pour créer et exécuter l’opération de formation.

   >[!NOTE]
   >
   >Les configurations sont uniques et spécifiques à leur recette de destination : cela signifie que les configurations pour la recette des ventes au détail ne fonctionneront pas pour la recette des recommandations de produit. Reportez-vous à la section [référence](#reference) pour une liste des configurations de la recette de ventes au détail.

   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

## Évaluation du modèle

1. Dans Adobe Experience Platform, cliquez sur le lien **[!UICONTROL Modèles]** situé dans la colonne de navigation de gauche pour tous les modèles existants. Recherchez et cliquez sur le nom du modèle à évaluer.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Toutes les sessions de formation existantes ainsi que leur état actuel sont répertoriées. Lorsque plusieurs opérations de formation ont été terminées, les mesures d’évaluation peuvent être comparées entre différentes opérations de formation dans le graphique d’évaluation du modèle. Sélectionnez une mesure d’évaluation à l’aide du menu déroulant situé au-dessus du graphique.

   La mesure Pourcentage d’erreur absolue moyen (MAPE) exprime la précision sous forme de pourcentage d’erreur. Elle permet d’identifier l’expérience la plus performante. Plus la valeur MAPE est faible, meilleures sont les performances de l’expérience.

   ![](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

   La mesure « Précision » décrit le pourcentage d’instances pertinentes par rapport au total des instances *récupérées*. La précision peut être considérée comme la probabilité qu’un résultat sélectionné de manière aléatoire soit correct.
   ![](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

   Cliquez sur une opération de formation spécifique pour visualiser les détails de cette opération. Cette action peut être effectuée avant la fin de l’opération. Sur la page des détails de l’opération, vous pouvez consulter d’autres mesures d’évaluation, paramètres de configuration et visualisations spécifiques à l’opération de la formation. Vous pouvez également télécharger des journaux d’activités pour afficher les détails de l’opération. Les journaux sont particulièrement utiles pour comprendre ce qui s’est mal passé lors des échecs d’opération.
   ![](../images/models-recipes/train-evaluate-ui/activity_logs.png)

3. Les hyperparamètres ne peuvent pas être formés, et un modèle doit être optimisé en testant différentes combinaisons d’hyperparamètres. Répétez ce processus de formation et d’évaluation du modèle jusqu’à ce que vous parveniez à obtenir un modèle optimisé.

## Étapes suivantes

Ce tutoriel vous a guidé tout au long des étapes de création, de formation et d’évaluation d’un modèle dans [!DNL Data Science Workspace]. Une fois que vous êtes parvenu à obtenir un modèle optimisé, vous pouvez utiliser le modèle formé pour générer des informations en suivant le tutoriel [Notation d’un modèle dans l’interface utilisateur](./score-model-ui.md).

## Référence {#reference}

### Configurations de la recette de ventes au détail

Les hyperparamètres déterminent le comportement de formation du modèle : les modifier aura une incidence sur l’exactitude et la précision du modèle.

| Hyperparamètre | Description | Plage recommandée |
--- | --- | ---
| learning_rate | Le taux d’apprentissage réduit la contribution de chaque arborescence par learning_rate. Un compromis est fait entre le taux d’apprentissage et le nombre d’estimateurs. | 0.1 | [2 - 10] / nombre d’estimateurs |
| n_estimators | Le nombre d’étapes d’amplification à exécuter. Une amplification progressive est assez résistante au surajustement, de sorte qu’un nombre important donne généralement une meilleure performance. | 100 | 100 - 1000 |
| max_depth | Profondeur maximale des estimateurs de régression individuels. La profondeur maximale limite le nombre de nœuds dans l’arborescence. Ajustez ce paramètre pour obtenir une meilleure performance. La meilleure valeur dépend de l’interaction des variables d’entrée. | 3 | 4 - 10 |

Des paramètres supplémentaires déterminent les propriétés techniques du modèle :

| Clé paramètre | Type | Description |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Chaîne | Liste d’attributs de schéma d’entrée séparés par des virgules. |
| `ACP_DSW_TARGET_FEATURES` | Chaîne | Liste d’attributs de schéma de sortie séparés par des virgules. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booléen | Détermine si les fonctionnalités d’entrée et de sortie peuvent être modifiées. |
| `tenantId` | Chaîne | Cet identifiant permet de garantir que les ressources que vous créez sont des espaces de noms corrects et contenus dans votre organisation IMS. [Suivez ces étapes](../../xdm/api/getting-started.md#know-your-tenant_id) pour trouver votre identifiant client. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Chaîne | Le schéma d’entrée utilisé pour la formation d’un modèle. |
| `evaluation.labelColumn` | Chaîne | Libellé de colonne pour visualiser les évaluations. |
| `evaluation.metrics` | Chaîne | Liste de mesures d’évaluation séparées par des virgules à utiliser pour l’évaluation d’un modèle. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Chaîne | Le schéma de sortie utilisé pour la notation d’un modèle. |