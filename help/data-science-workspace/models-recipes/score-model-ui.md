---
keywords: Experience Platform;score a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Score d’un modèle (interface utilisateur)
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# Score d’un modèle (interface utilisateur)

Pour obtenir un score dans l’espace de travail Data Science d’Adobe Experience Platform, il est possible d’alimenter les données d’entrée dans un modèle existant. Les résultats de score sont ensuite stockés et visibles dans un jeu de données de sortie spécifié en tant que nouveau lot.

Ce didacticiel présente les étapes requises pour marquer un modèle dans l’interface utilisateur de Data Science Workspace.

## Prise en main

Pour terminer ce didacticiel, vous devez avoir accès à Experience Platform. Si vous n’avez pas accès à une organisation IMS dans Experience Platform, contactez votre administrateur système avant de continuer.

Ce didacticiel nécessite un modèle formé. Si vous n&#39;avez pas de modèle formé, suivez le [train et évaluez un modèle dans le didacticiel sur l&#39;interface utilisateur](./train-evaluate-model-ui.md) avant de continuer.

## Créer une nouvelle série de notes

Une série de scores est créée à l’aide de configurations optimisées à partir d’une série de formations précédemment terminée et évaluée. L&#39;ensemble des configurations optimales d&#39;un modèle est généralement déterminé en examinant les mesures d&#39;évaluation des séries de formations.

1. Recherchez la période de formation la plus optimale pour utiliser ses configurations pour la notation. Ouvrez l’exécution de formation souhaitée en cliquant sur son nom.

2. Dans l&#39;onglet Exécution de la formation **[!UICONTROL Evaluation]** , cliquez sur le **[!UICONTROL Score]** bouton en haut à droite de l&#39;écran. Cette opération déclenchera un nouveau processus *d’exécution du score* .
   ![](../images/models-recipes/score/training_run_overview.png)

3. Sélectionnez le jeu de données de score d’entrée et cliquez sur **[!UICONTROL Next]**.
   ![](../images/models-recipes/score/scoring_input.png)

4. Sélectionnez le jeu de données de score de sortie, c&#39;est le jeu de données de sortie dédié dans lequel les résultats de score sont stockés. Confirmez votre sélection et cliquez sur **[!UICONTROL Next]**.
   ![](../images/models-recipes/score/scoring_results.png)

5. L’étape finale du flux de travail vous invite à configurer votre exécution de score. Ces configurations sont utilisées par le modèle pour l&#39;exécution de notation.
Notez que vous ne pourrez pas supprimer les paramètres hérités qui ont été définis lors de la création du modèle. Vous pouvez modifier ou rétablir des paramètres non hérités en cliquant sur la valeur ou en cliquant sur l’icône de rétablissement tout en survolant l’entrée.
   ![](../images/models-recipes/score/configuration.png)
Vérifiez et confirmez les configurations de notation et cliquez sur **[!UICONTROL Finish]** pour créer et exécuter l’exécution de notation. Vous serez dirigé vers l’onglet Exécutions *de* score et la nouvelle série de scores affichera un état.
   ![](../images/models-recipes/score/scoring_runs_tab.png)
Une série de scores affiche l’un des quatre états suivants : En attente, Terminé, Echec ou En cours d’exécution et sont mis à jour automatiquement. Passez à l’étape suivante si l’état est &quot;Terminé&quot; ou &quot;Échec&quot;.

## Résultats du score de Vue

1. Recherchez l’exécution de formation utilisée pour l’exécution de score, puis cliquez sur le nom pour vue de sa **[!UICONTROL Evaluation]** page.

2. Près de la partie supérieure de la page d’évaluation des séries de formations, cliquez sur l’ **[!UICONTROL Scoring Runs]** onglet pour vue d’une liste des séries de scores existantes. Cliquez sur la liste de score pour en vue les détails dans la colonne de droite.
   ![](../images/models-recipes/score/view_details.png)

3. Si l’exécution de score sélectionnée a l’état &quot;Terminé&quot; ou &quot;Échec&quot;, le **[!UICONTROL View Activity Logs]** lien figurant dans la colonne de droite est actif. Cliquez sur le lien vers la vue ou téléchargez les journaux d&#39;exécution. En cas d’échec d’une série de scores, les journaux d’exécution peuvent fournir des informations utiles pour déterminer la raison de l’échec.
   ![](../images/models-recipes/score/activity_logs.png)

4. Cliquez sur le **[!UICONTROL Preview Scoring Results Dataset]** lien situé dans la colonne de droite. Vous pourrez voir une prévisualisation du jeu de données de sortie à partir de l’exécution de score.
   ![](../images/models-recipes/score/preview_results.png)

5. Pour obtenir l’ensemble complet des résultats de score, cliquez sur le **[!UICONTROL Scoring Results Dataset]** lien situé dans la colonne de droite.

## Étapes suivantes

Ce didacticiel vous a guidé tout au long des étapes permettant de marquer des données à l’aide d’un modèle de données dans l’espace de travail des sciences de données. Suivez le didacticiel sur la [publication d’un modèle en tant que service dans l’interface utilisateur](./publish-model-service-ui.md) pour permettre aux utilisateurs de votre entreprise de noter des données en leur fournissant un accès facile à un service d’apprentissage automatique.
