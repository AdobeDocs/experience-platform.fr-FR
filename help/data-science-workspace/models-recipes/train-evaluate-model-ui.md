---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics
solution: Experience Platform
title: Formation et évaluation d’un modèle (IU)
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# Formation et évaluation d’un modèle (IU)

Dans Adobe Experience Platform Data Science Workspace, un modèle d’apprentissage automatique est créé en incorporant une recette existante adaptée à l’intention du modèle. Le modèle est ensuite formé et évalué afin d&#39;optimiser son efficacité et son efficacité d&#39;exploitation en affinant ses Hyperparamètres associés. Les recettes sont réutilisables, ce qui signifie que plusieurs modèles peuvent être créés et adaptés à des fins spécifiques avec une seule Recette.

Ce didacticiel décrit les étapes de création, de formation et d&#39;évaluation d&#39;un modèle.

## Prise en main

Pour terminer ce didacticiel, vous devez avoir accès à Experience Platform. Si vous n’avez pas accès à une organisation IMS dans Experience Platform, contactez votre administrateur système avant de continuer.

Ce didacticiel nécessite une recette existante. Si vous n&#39;avez pas de recette, suivez le didacticiel [Importer une recette empaquetée dans l&#39;interface utilisateur](./import-packaged-recipe-ui.md) avant de continuer.

## Créer un modèle

1. Dans Adobe Experience Platform, cliquez sur le **[!UICONTROL Models]** lien situé dans la colonne de navigation de gauche pour liste tous les modèles existants. Cliquez **[!UICONTROL Create Model]** en haut à droite de la page pour lancer un processus de création de modèle.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Parcourez la liste des recettes existantes, recherchez et sélectionnez la recette à utiliser pour créer le modèle, puis cliquez sur **[!UICONTROL Next]**.
   ![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

3. Sélectionnez un jeu de données d’entrée approprié, puis cliquez sur **[!UICONTROL Next]**. Ceci définira le jeu de données de formation en entrée par défaut pour le modèle.
   ![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

4. Attribuez un nom au modèle et passez en revue les configurations de modèle par défaut. Les configurations par défaut ont été appliquées lors de la création de Recette, de la révision et de la modification des valeurs de configuration en cliquant sur les valeurs par doublon. Pour fournir un nouveau jeu de configurations, cliquez **[!UICONTROL Upload New Config]** et faites glisser un fichier JSON contenant des configurations de modèle dans la fenêtre du navigateur. Cliquez sur **[!UICONTROL Finish]** pour créer le modèle.
   >[!NOTE]Les configurations sont uniques et spécifiques à la recette prévue, ce qui signifie que les configurations de la recette Ventes au détail ne fonctionneront pas pour la recette Recommandations de produits. Consultez la section de [référence](#reference) pour obtenir une liste des configurations Recette vente au détail.

   ![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Créer une session de formation

1. Dans Adobe Experience Platform, cliquez sur le **[!UICONTROL Models]** lien situé dans la colonne de navigation de gauche pour liste tous les modèles existants. Recherchez et cliquez sur le nom du modèle à former.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Toutes les sessions de formation existantes avec leur statut actuel sont répertoriées. Pour les modèles créés à l’aide de l’interface utilisateur de l’espace de travail Data Science, une session de formation est automatiquement générée et exécutée à l’aide des configurations par défaut et du jeu de données de formation d’entrée.
   ![](../images/models-recipes/train-evaluate-ui/model_overview.png)

3. Créez une nouvelle session de formation en cliquant **[!UICONTROL Train]** près de l&#39;angle supérieur droit de la page d&#39;aperçu du modèle.
   ![](../images/models-recipes/train-evaluate-ui/training_input.png)

4. Sélectionnez le jeu de données d&#39;entrée de formation pour l&#39;exécution de la formation, puis cliquez sur **[!UICONTROL Next]**.
   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

5. Les configurations par défaut fournies lors de la création du modèle sont affichées, modifiées et modifiées en conséquence en cliquant sur les valeurs par doublon. Cliquez sur **[!UICONTROL Finish]** pour créer et exécuter l’exécution de la formation.
   >[!NOTE]Les configurations sont uniques et spécifiques à la recette prévue, ce qui signifie que les configurations de la recette Ventes au détail ne fonctionneront pas pour la recette Recommandations de produits. Consultez la section de [référence](#reference) pour obtenir une liste des configurations Recette vente au détail.

   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

## Évaluer le modèle

1. Dans Adobe Experience Platform, cliquez sur le **[!UICONTROL Models]** lien situé dans la colonne de navigation de gauche pour liste tous les modèles existants. Recherchez et cliquez sur le nom du modèle à évaluer.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Toutes les sessions de formation existantes avec leur statut actuel sont répertoriées. Avec plusieurs séries d&#39;exercices de formation terminés, les mesures d&#39;évaluation peuvent être comparées à différents exercices de formation dans le graphique d&#39;évaluation du modèle, puis sélectionnez une mesure d&#39;évaluation à l&#39;aide de la liste déroulante au-dessus du graphique.

   La mesure Erreur en pourcentage absolu moyen (MAPE) exprime la précision en tant que pourcentage de l’erreur. Elle permet d’identifier l’expérience la plus performante. Plus le MAPE est bas, mieux c&#39;est.

   ![](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

   La mesure &quot;Précision&quot; décrit le pourcentage d’instances pertinentes par rapport au total d’instances *récupérées* . La précision peut être considérée comme la probabilité qu’un résultat sélectionné de manière aléatoire soit correct.
   ![](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

   Cliquez sur un parcours de formation spécifique pour en vue les détails. Cela peut être fait avant même que l&#39;exécution ne soit terminée. Sur la page des détails de l’exécution, vous pouvez afficher d’autres mesures d’évaluation, paramètres de configuration et visualisations spécifiques à l’exécution de la formation. Vous pouvez également télécharger les journaux des activités pour afficher les détails de l’exécution. Les journaux sont particulièrement utiles pour les échecs d’exécution afin de déterminer ce qui s’est mal passé.
   ![](../images/models-recipes/train-evaluate-ui/activity_logs.png)

3. Les hyperparamètres ne peuvent pas être entraînés et un modèle doit être optimisé en testant différentes combinaisons d&#39;hyperparamètres. Répétez ce processus de formation et d&#39;évaluation du modèle jusqu&#39;à ce que vous ayez atteint un modèle optimisé.

## Étapes suivantes

Ce didacticiel vous a guidé tout au long de la création, de la formation et de l’évaluation d’un modèle dans Data Science Workspace. Une fois que vous êtes arrivé à un modèle optimisé, vous pouvez utiliser le modèle formé pour générer des informations en suivant la section [Score a Model du didacticiel sur l’interface utilisateur](./score-model-ui.md) .

## Référence {#reference}

### Configurations des recettes de vente au détail

Les hyperparamètres déterminent le comportement d&#39;entraînement du modèle, en modifiant les hyperparamètres, vous affecterez la précision et la précision du modèle :

| Hyperparamètre | Description | Plage recommandée |
--- | --- | ---
| learning_rate | Le taux d&#39;apprentissage réduit la contribution de chaque arbre en apprenant_rate. Il existe un compromis entre learning_rate et n_estimators. | 0.1 | [2 - 10] / nombre d&#39;estimateurs |
| n_estimateurs | Nombre d’étapes de dynamisation à exécuter. Le gonflement des dégradés est assez robuste pour être trop ajusté, de sorte qu&#39;un grand nombre d&#39;entre eux se traduit généralement par de meilleures performances. | 100 | 100 - 1000 |
| max_depth | Profondeur maximale des estimateurs de régression individuels. La profondeur maximale limite le nombre de noeuds dans l’arborescence. Réglage de ce paramètre pour obtenir de meilleures performances ; la meilleure valeur dépend de l’interaction des variables d’entrée. | 3 | 4 - 10 |

Des paramètres supplémentaires déterminent les propriétés techniques du modèle :

| Clé de paramètre | Type | Description |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | Chaîne | Liste d’attributs de schéma d’entrée séparés par des virgules. |
| `ACP_DSW_TARGET_FEATURES` | Chaîne | Liste des attributs de schéma de sortie séparés par des virgules. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booléen | Détermine si les fonctions d’entrée et de sortie peuvent être modifiées. |
| `tenantId` | Chaîne | Cet identifiant permet de s’assurer que les ressources que vous créez sont correctement espacées de noms et qu’elles sont contenues dans votre organisation IMS. [Suivez les étapes ci-dessous](../../xdm/api/getting-started.md#know-your-tenant_id) pour trouver votre ID de client. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Chaîne | schéma d&#39;entrée utilisé pour la formation d&#39;un modèle. |
| `evaluation.labelColumn` | Chaîne | Libellé de colonne pour les visualisations d’évaluation. |
| `evaluation.metrics` | Chaîne | liste séparée par des virgules des mesures d&#39;évaluation à utiliser pour évaluer un modèle. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Chaîne | schéma de sortie utilisé pour marquer un modèle. |