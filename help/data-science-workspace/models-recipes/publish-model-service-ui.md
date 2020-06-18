---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Publication d’un modèle en tant que service (interface utilisateur)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 7dc5075d3101b4780af92897c0381e73a9c5aef0
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# Publication d’un modèle en tant que service (interface utilisateur)

Adobe Experience Platform Data Science Workspace vous permet de publier votre modèle en tant que service, formé et évalué, ce qui permet aux utilisateurs de votre organisation IMS de noter des données sans avoir à créer leurs propres modèles.

## Prise en main

Pour terminer ce didacticiel, vous devez avoir accès à [!DNL Experience Platform]. Si vous n&#39;avez pas accès à une organisation IMS dans [!DNL Experience Platform]votre entreprise, contactez votre administrateur système avant de continuer.

Ce didacticiel nécessite un modèle existant avec une formation réussie. Si vous ne disposez pas d’un modèle publiable, suivez le [didacticiel Formation et évaluez un modèle dans le didacticiel sur l’interface utilisateur](./train-evaluate-model-ui.md) avant de continuer.

Si vous préférez publier un modèle à l’aide des API d’apprentissage automatique Sensei, reportez-vous au didacticiel [](./publish-model-service-api.md)API.

## Publication d’un modèle {#publish-a-model}

1. Dans Adobe Experience Platform, cliquez sur le lien **[!UICONTROL Modèles]** situé dans la colonne de navigation de gauche pour liste tous les modèles existants. Recherchez et cliquez sur le nom du modèle à publier en tant que service.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. Cliquez sur **[!UICONTROL Publier]** en haut à droite de la page d’aperçu du modèle pour début d’un processus de création de service.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. Saisissez un nom pour le service et éventuellement une description du service, puis cliquez sur **[!UICONTROL Suivant]** une fois terminé.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. Tous les exercices de formation réussis pour le modèle sont répertoriés. Le nouveau service héritera des configurations de formation et de notation de la série de formation sélectionnée.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. Cliquez sur **[!UICONTROL Terminer]** pour créer le service et rediriger vers la Galerie **[!UICONTROL de]** services pour afficher tous les services disponibles, y compris le service nouvellement créé.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Score à l’aide d’un service {#access-a-service}

1. Dans Adobe Experience Platform, cliquez sur l’onglet **[!UICONTROL Services]** situé dans la colonne de navigation de gauche pour accéder à la Galerie *de* services. Recherchez le service que vous souhaitez utiliser et cliquez sur **[!UICONTROL Score]**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. Sélectionnez un jeu de données d’entrée approprié pour l’exécution de score, puis cliquez sur **[!UICONTROL Suivant]**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. Sélectionnez un jeu de données de sortie approprié pour les résultats de score, puis cliquez sur **[!UICONTROL Suivant]**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. Lorsqu’un service est créé, il hérite des configurations d’évaluation par défaut. Vous pouvez examiner ces configurations et les ajuster en fonction des besoins en cliquant sur les valeurs en doublon. Une fois que vous êtes satisfait des configurations, cliquez sur **[!UICONTROL Terminer]** pour commencer l’exécution de score.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. Sur la page *Aperçu* du service, les détails de la nouvelle tâche de notation et de son avancement sont affichés. Une fois la tâche terminée, la tâche d’évaluation **[!UICONTROL La plus récente]** sera mise à jour.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Étapes suivantes {#next-steps}

En suivant ce didacticiel, vous avez publié avec succès un modèle en tant que service accessible et marqué des données à l’aide du nouveau service par l’intermédiaire de la Galerie *de* services. Passez au didacticiel suivant pour découvrir comment [planifier des sessions de formation et de notation automatisées sur un service](./schedule-models-ui.md).
