---
keywords: Experience Platform;publier un modèle;Data Science Workspace;rubriques les plus consultées;noter un service
solution: Experience Platform
title: Publication d’un modèle en tant que service dans l’interface utilisateur de Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace vous permet de publier un modèle formé et noté en tant que service et permet ainsi aux utilisateurs de votre organisation IMS de noter des données sans avoir besoin de créer leurs propres modèles.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 50%

---

# Publication d’un modèle en tant que service dans l’interface utilisateur de Data Science Workspace

Adobe Experience Platform Data Science Workspace vous permet de publier un modèle formé et noté en tant que service et permet ainsi aux utilisateurs de votre organisation IMS de noter des données sans avoir besoin de créer leurs propres modèles.

## Prise en main

Pour suivre ce tutoriel, vous devez avoir accès à [!DNL Experience Platform]. Si vous n’avez pas accès à une organisation IMS dans [!DNL Experience Platform], contactez votre administrateur système avant de continuer.

Ce tutoriel nécessite un modèle existant avec une opération de formation réussie. Si vous ne disposez pas d’un modèle publiable, suivez le tutoriel [Formation et notation d’un modèle dans l’interface utilisateur](./train-evaluate-model-ui.md) avant de poursuivre.

Si vous préférez publier un modèle à l’aide des API Sensei Machine Learning, reportez-vous au [tutoriel sur l’API](./publish-model-service-api.md).

## Publication d’un modèle {#publish-a-model}

Dans Adobe Experience Platform, sélectionnez **[!UICONTROL Modèles]** situé dans la colonne de navigation de gauche, puis sélectionnez l’option **[!UICONTROL Parcourir]** pour répertorier tous les modèles existants. Sélectionnez le nom du modèle que vous souhaitez publier en tant que service.

![](../images/models-recipes/publish-model/browse_model.png)

Sélectionner **[!UICONTROL Publier]** près du coin supérieur droit de la page d’aperçu du modèle pour lancer un processus de création de service.

![](../images/models-recipes/publish-model/view_training.png)

Saisissez un nom pour le service et éventuellement une description du service, puis sélectionnez **[!UICONTROL Suivant]** lorsque vous avez terminé.

![](../images/models-recipes/publish-model/configure_training.png)

Toutes les opérations de formation réussies du modèle sont répertoriées. Le nouveau service héritera des configurations de formation et de notation de l’opération de formation sélectionnée.

![](../images/models-recipes/publish-model/select_training_run.png)

Sélectionner **[!UICONTROL Terminer]** pour créer le service et accéder à la fonction **[!UICONTROL Galerie de services]** pour afficher tous les services disponibles, y compris le service nouvellement créé.

![](../images/models-recipes/publish-model/service_gallery.png)

## Notation à l’aide d’un service {#access-a-service}

Dans Adobe Experience Platform, sélectionnez la variable **[!UICONTROL Services]** situé dans la colonne de navigation de gauche pour accéder au **[!UICONTROL Galerie de services]**. Recherchez le service que vous souhaitez utiliser et sélectionnez **[!UICONTROL Ouvrir]**.

![](../images/models-recipes/publish-model/open_service.png)

Dans la page de présentation du service, sélectionnez **[!UICONTROL Score]**.

![](../images/models-recipes/publish-model/score_service.png)

Sélectionnez un jeu de données d’entrée approprié pour l’opération de notation, puis sélectionnez **[!UICONTROL Suivant]**. Vous êtes invité à effectuer la même étape pour le jeu de données de notation. Une fois que vous avez sélectionné le jeu de données d’entrée et de sortie, vous pouvez mettre à jour les configurations.

![](../images/models-recipes/publish-model/select_datasets.png)

Lorsqu’un service est créé, il hérite des configurations de notation par défaut. Vous pouvez revoir ces configurations et les ajuster selon les besoins en double-cliquant sur les valeurs. Une fois les configurations satisfaites, sélectionnez **[!UICONTROL Terminer]** pour lancer l’opération de notation.

![](../images/models-recipes/publish-model/scoring_configs.png)

Sur la page **Présentation** du service, vous retrouvez les détails de la nouvelle tâche de notation et sa progression. Une fois la tâche terminée, la variable **[!UICONTROL Le plus récent]** dans l’en-tête **[!UICONTROL Notation]** Le conteneur est mis à jour.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez publié avec succès un modèle en tant que service accessible et noté des données à l’aide du nouveau service, par le biais de la [!UICONTROL Galerie de services]. Passez au tutoriel suivant pour apprendre à [planifier des opérations de formation et de notation automatisées sur un service](./schedule-models-ui.md).
