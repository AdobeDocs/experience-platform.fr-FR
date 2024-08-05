---
keywords: Experience Platform;formation et évaluation;Data Science Workspace;rubriques les plus consultées;créer un modèle;créer une session de formation
solution: Experience Platform
title: Formation et évaluation d’un modèle dans l’interface utilisateur de Data Science Workspace
type: Tutorial
description: Dans l’espace de travail de science des données d’Adobe Experience Platform, un modèle de machine learning est créé en incorporant une recette existante adéquate au but du modèle. Le modèle est ensuite formé et évalué afin d’optimiser son efficience et son efficacité opérationnelles en affinant ses hyperparamètres associés. Les recettes sont réutilisables, ce qui signifie que plusieurs modèles peuvent être créés et adaptés à des fins spécifiques à l’aide d’une seule recette.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 53%

---

# Formation et évaluation d’un modèle dans l’interface utilisateur de Data Science Workspace

>[!NOTE]
>
>Data Science Workspace ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs à Data Science Workspace.

Dans l’espace de travail de science des données d’Adobe Experience Platform, un modèle de machine learning est créé en incorporant une recette existante adéquate au but du modèle. Le modèle est ensuite formé et évalué afin d’optimiser son efficience et son efficacité opérationnelles en affinant ses hyperparamètres associés. Les recettes sont réutilisables, ce qui signifie que plusieurs modèles peuvent être créés et adaptés à des fins spécifiques à l’aide d’une seule recette.

Ce tutoriel décrit les étapes à suivre pour créer, former et évaluer un modèle.

## Prise en main

Pour suivre ce tutoriel, vous devez avoir accès à [!DNL Experience Platform]. Si vous n’avez pas accès à une organisation dans [!DNL Experience Platform], contactez votre administrateur système avant de poursuivre.

Ce tutoriel nécessite une recette existante. Si vous ne possédez aucune recette, suivez le tutoriel [Importation d’une recette empaquetée dans l’interface utilisateur](./import-packaged-recipe-ui.md) avant de continuer.

## Création d’un modèle

Dans Experience Platform, sélectionnez l’onglet **[!UICONTROL Modèles]** situé dans le volet de navigation de gauche, puis sélectionnez l’onglet Parcourir pour afficher vos modèles existants. Sélectionnez **[!UICONTROL Créer un modèle]** près du coin supérieur droit de la page pour lancer un processus de création de modèle.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

Parcourez la liste des recettes existantes, recherchez et sélectionnez la recette à utiliser pour créer le modèle, puis sélectionnez **[!UICONTROL Suivant]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

Sélectionnez un jeu de données d’entrée approprié, puis **[!UICONTROL Suivant]**. Cela définit le jeu de données de formation d’entrée par défaut pour le modèle.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

Attribuez un nom au modèle et passez en revue les configurations de modèle par défaut. Les configurations par défaut ont été appliquées lors de la création de la recette. Vérifiez et modifiez les valeurs de configuration en double-cliquant sur les valeurs.

Pour fournir un nouvel ensemble de configurations, sélectionnez **[!UICONTROL Upload New Config]** et faites glisser un fichier JSON contenant des configurations de modèle dans la fenêtre du navigateur. Sélectionnez **[!UICONTROL Terminer]** pour créer le modèle.

>[!NOTE]
>
>Les configurations sont uniques et spécifiques à leur recette prévue. Cela signifie que les configurations de la recette Ventes au détail ne fonctionneront pas pour la recette Recommendations du produit. Reportez-vous à la section [référence](#reference) pour une liste des configurations de la recette de ventes au détail.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Création d’une opération de formation

Dans Experience Platform, sélectionnez l’onglet **[!UICONTROL Modèles]** situé dans le volet de navigation de gauche, puis sélectionnez l’onglet Parcourir pour afficher vos modèles existants. Recherchez et sélectionnez le lien hypertexte associé au nom du modèle que vous souhaitez entraîner.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Toutes les sessions de formation existantes ainsi que leur état actuel sont répertoriées. Pour les modèles créés à l’aide de l’interface utilisateur [!DNL Data Science Workspace], une session d’entraînement est automatiquement générée et exécutée à l’aide des configurations par défaut et du jeu de données de formation d’entrée.

Créez une nouvelle opération de formation en sélectionnant **[!UICONTROL Former]** près du coin supérieur droit de la page d’aperçu du modèle.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Sélectionnez le jeu de données d’entrée de formation pour l’opération de formation, puis sélectionnez **[!UICONTROL Suivant]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

Les configurations par défaut fournies lors de la création du modèle s’affichent : modifiez-les en conséquence en double-cliquant sur les valeurs. Sélectionnez **[!UICONTROL Terminer]** pour créer et exécuter l’opération de formation.

>[!NOTE]
>
>Les configurations sont uniques et spécifiques à leur recette prévue. Cela signifie que les configurations de la recette Ventes au détail ne fonctionneront pas pour la recette Recommendations du produit. Reportez-vous à la section [référence](#reference) pour une liste des configurations de la recette de ventes au détail.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Évaluation du modèle

Dans Experience Platform, sélectionnez l’onglet **[!UICONTROL Modèles]** situé dans le volet de navigation de gauche, puis sélectionnez l’onglet Parcourir pour afficher vos modèles existants. Recherchez et sélectionnez l’hyperlien associé au nom du modèle que vous souhaitez évaluer.

![select model](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Toutes les sessions de formation existantes ainsi que leur état actuel sont répertoriées. Avec plusieurs opérations de formation terminées, les mesures d’évaluation peuvent être comparées entre différentes opérations de formation dans le graphique d’évaluation du modèle. Sélectionnez une mesure d’évaluation à l’aide de la liste déroulante au-dessus du graphique.

La mesure Pourcentage d’erreur absolue moyen (MAPE) exprime la précision sous forme de pourcentage d’erreur. Elle permet d’identifier l’expérience la plus performante. Plus la valeur MAPE est faible, meilleures sont les performances de l’expérience.

![présentation des opérations de formation](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

La mesure « Précision » décrit le pourcentage d’instances pertinentes par rapport au total des instances *récupérées*. La précision peut être considérée comme la probabilité qu’un résultat sélectionné de manière aléatoire soit correct.

![exécution de plusieurs exécutions](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

La sélection d’une opération de formation spécifique fournit les détails de cette opération en ouvrant la page d’évaluation. Cette action peut être effectuée avant la fin de l’opération. Sur la page d’évaluation, vous pouvez voir d’autres mesures d’évaluation, paramètres de configuration et visualisations spécifiques à l’opération de formation.

![journaux d’aperçu](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

Vous pouvez également télécharger des journaux d’activités pour afficher les détails de l’opération. Les journaux sont particulièrement utiles pour comprendre ce qui s’est mal passé lors des échecs d’opération.

![journaux d’activité](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Les hyperparamètres ne peuvent pas être formés, et un modèle doit être optimisé en testant différentes combinaisons d’hyperparamètres. Répétez ce processus de formation et d’évaluation du modèle jusqu’à ce que vous parveniez à obtenir un modèle optimisé.

## Étapes suivantes

Ce tutoriel vous a guidé tout au long des étapes de création, de formation et d’évaluation d’un modèle dans [!DNL Data Science Workspace]. Une fois que vous êtes parvenu à obtenir un modèle optimisé, vous pouvez utiliser le modèle formé pour générer des informations en suivant le tutoriel [Notation d’un modèle dans l’interface utilisateur](./score-model-ui.md).

## Référence {#reference}

### Configurations de la recette de ventes au détail

Les hyperparamètres déterminent le comportement de formation du modèle : les modifier aura une incidence sur l’exactitude et la précision du modèle.

| Hyperparamètre | Description | Plage recommandée |
| --- | --- | --- |
| learning_rate | Le taux d’apprentissage réduit la contribution de chaque arborescence par learning_rate. Un compromis est fait entre le taux d’apprentissage et le nombre d’estimateurs. | 0.1 |
| n_estimators | Le nombre d’étapes d’amplification à exécuter. Une amplification progressive est assez résistante au surajustement, de sorte qu’un nombre important donne généralement une meilleure performance. | 100 |
| max_depth | Profondeur maximale des estimateurs de régression individuels. La profondeur maximale limite le nombre de nœuds dans l’arborescence. Ajustez ce paramètre pour obtenir une meilleure performance. La meilleure valeur dépend de l’interaction des variables d’entrée. | 3 |

Des paramètres supplémentaires déterminent les propriétés techniques du modèle :

| Clé paramètre | Type | Description |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Chaîne | Liste d’attributs de schéma d’entrée séparés par des virgules. |
| `ACP_DSW_TARGET_FEATURES` | Chaîne | Liste d’attributs de schéma de sortie séparés par des virgules. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booléen | Détermine si les fonctionnalités d’entrée et de sortie peuvent être modifiées. |
| `tenantId` | Chaîne | Cet identifiant permet de s’assurer que les ressources que vous créez sont des espaces de noms corrects et contenus dans votre organisation. [Suivez ces étapes](../../xdm/api/getting-started.md#know-your-tenant_id) pour trouver votre identifiant client. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Chaîne | Le schéma d’entrée utilisé pour la formation d’un modèle. |
| `evaluation.labelColumn` | Chaîne | Libellé de colonne pour visualiser les évaluations. |
| `evaluation.metrics` | Chaîne | Liste de mesures d’évaluation séparées par des virgules à utiliser pour l’évaluation d’un modèle. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Chaîne | Le schéma de sortie utilisé pour la notation d’un modèle. |
