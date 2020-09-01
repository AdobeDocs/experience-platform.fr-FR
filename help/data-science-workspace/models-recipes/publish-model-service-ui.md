---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics;score a service
solution: Experience Platform
title: Publication d’un modèle en tant que service (interface utilisateur)
topic: Tutorial
description: Adobe Experience Platform Data Science Workspace vous permet de publier un modèle formé et noté en tant que service et permet ainsi aux utilisateurs de votre organisation IMS de noter des données sans avoir besoin de créer leurs propres modèles.
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 95%

---


# Publication d’un modèle en tant que service (interface utilisateur)

Adobe Experience Platform Data Science Workspace vous permet de publier un modèle formé et noté en tant que service et permet ainsi aux utilisateurs de votre organisation IMS de noter des données sans avoir besoin de créer leurs propres modèles.

## Prise en main

Pour suivre ce tutoriel, vous devez avoir accès à [!DNL Experience Platform]. If you do not have access to an IMS Organization in [!DNL Experience Platform], please speak to your system administrator before proceeding.

Ce tutoriel nécessite un modèle existant avec une opération de formation réussie. Si vous ne disposez pas d’un modèle publiable, suivez le tutoriel [Formation et notation d’un modèle dans l’interface utilisateur](./train-evaluate-model-ui.md) avant de poursuivre.

Si vous préférez publier un modèle à l’aide des API Sensei Machine Learning, reportez-vous au [tutoriel sur l’API](./publish-model-service-api.md).

## Publication d’un modèle {#publish-a-model}

1. Dans Adobe Experience Platform, cliquez sur le lien **[!UICONTROL Modèles]** situé dans la colonne de navigation de gauche pour tous les modèles existants. Recherchez le modèle à publier en tant que service et cliquez sur son nom.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. Cliquez sur **[!UICONTROL Publier]** dans la partie supérieure droite de la page de présentation du modèle pour lancer le processus de création de service.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. Saisissez un nom pour le service et éventuellement une description du service, puis cliquez sur **[!UICONTROL Suivant]** quand vous avez terminé.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. Toutes les opérations de formation réussies du modèle sont répertoriées. Le nouveau service héritera des configurations de formation et de notation de l’opération de formation sélectionnée.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. Cliquez sur **[!UICONTROL Terminer]** pour créer le service et revenez à la **[!UICONTROL Galerie de services]** afin d’afficher tous les services disponibles, y compris le service nouvellement créé.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Notation à l’aide d’un service {#access-a-service}

1. Dans Adobe Experience Platform, cliquez sur l’onglet **[!UICONTROL Services]** situé dans la colonne de navigation de gauche pour accéder à la **[!UICONTROL Galerie de services]**. Recherchez le service à utiliser, puis cliquez sur **[!UICONTROL Noter]**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. Sélectionnez un jeu de données d’entrée approprié pour l’opération de notation, puis cliquez sur **[!UICONTROL Suivant]**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. Sélectionnez un jeu de données de sortie approprié pour les résultats de la notation, puis cliquez sur **[!UICONTROL Suivant]**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. Lorsqu’un service est créé, il hérite des configurations de notation par défaut. Vous pouvez revoir ces configurations et les ajuster selon les besoins en double-cliquant sur les valeurs. Lorsque vous trouvez les configurations satisfaisantes, cliquez sur **[!UICONTROL Terminer]** pour lancer l’opération de notation.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. Sur la page *Présentation* du service, vous retrouvez les détails de la nouvelle tâche de notation et sa progression. Une fois la tâche terminée, la tâche de notation **[!UICONTROL la plus récente]** est mise à jour.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez publié avec succès un modèle en tant que service accessible et noté des données à l’aide du nouveau service, par le biais de la **[!UICONTROL Galerie de services]**. Passez au tutoriel suivant pour apprendre à [planifier des opérations de formation et de notation automatisées sur un service](./schedule-models-ui.md).
