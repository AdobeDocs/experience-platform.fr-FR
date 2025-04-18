---
keywords: Experience Platform;publier un modèle;Workspace de science des données;rubriques populaires;noter un service
solution: Experience Platform
title: Publication d’un modèle en tant que service dans l’interface utilisateur de Workspace de science des données
type: Tutorial
description: Le Workspace de science des données de Adobe Experience Platform vous permet de publier votre modèle formé et évalué en tant que service, ce qui permet aux utilisateurs de votre organisation de noter des données sans avoir à créer leurs propres modèles.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 35%

---

# Publier un modèle en tant que service dans l’interface d’utilisation de l’espace de travail de science des données {#publish-a-model-as-a-service}

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

>[!CONTEXTUALHELP]
>id="platform_intelligentservices_publishmodel"
>title="Publier un modèle en tant que service"
>abstract=""

Le Workspace de science des données de Adobe Experience Platform vous permet de publier votre modèle formé et évalué en tant que service, ce qui permet aux utilisateurs de votre organisation de noter des données sans avoir à créer leurs propres modèles.

## Commencer

Pour suivre ce tutoriel, vous devez avoir accès à [!DNL Experience Platform]. Si vous n’avez pas accès à une organisation dans [!DNL Experience Platform], contactez votre administrateur système avant de continuer.

Ce tutoriel nécessite un modèle existant avec une opération de formation réussie. Si vous ne disposez pas d’un modèle publiable, suivez le tutoriel [Formation et notation d’un modèle dans l’interface utilisateur](./train-evaluate-model-ui.md) avant de poursuivre.

Si vous préférez publier un modèle à l’aide des API Sensei Machine Learning, reportez-vous au [tutoriel sur l’API](./publish-model-service-api.md).

## Publication d’un modèle {#publish-a-model}

Dans Adobe Experience Platform, sélectionnez **[!UICONTROL Modèles]** dans la colonne de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Parcourir]** pour tous les modèles existants. Sélectionnez le nom du modèle que vous souhaitez publier en tant que service.

![](../images/models-recipes/publish-model/browse_model.png)

Sélectionnez **[!UICONTROL Publier]** en haut à droite de la page Aperçu du modèle pour lancer un processus de création de service.

![](../images/models-recipes/publish-model/view_training.png)

Saisissez le nom souhaité pour le service et éventuellement fournissez une description du service, puis sélectionnez **[!UICONTROL Suivant]** lorsque vous avez terminé.

![](../images/models-recipes/publish-model/configure_training.png)

Toutes les opérations de formation réussies du modèle sont répertoriées. Le nouveau service héritera des configurations de formation et de notation de l’opération de formation sélectionnée.

![](../images/models-recipes/publish-model/select_training_run.png)

Sélectionnez **[!UICONTROL Terminer]** pour créer le service et rediriger vers la **[!UICONTROL Galerie de services]** pour afficher tous les services disponibles, y compris le service nouvellement créé.

![](../images/models-recipes/publish-model/service_gallery.png)

## Notation à l’aide d’un service {#access-a-service}

Dans Adobe Experience Platform, sélectionnez l’onglet **[!UICONTROL Services]** situé dans la colonne de navigation de gauche pour accéder à la **[!UICONTROL Galerie de services]**. Recherchez le service que vous souhaitez utiliser, puis sélectionnez **[!UICONTROL Ouvrir]**.

![](../images/models-recipes/publish-model/open_service.png)

Dans la page d’aperçu du service, sélectionnez **[!UICONTROL Score]**.

![](../images/models-recipes/publish-model/score_service.png)

Sélectionnez un jeu de données d’entrée approprié pour l’exécution de notation, puis sélectionnez **[!UICONTROL Suivant]**. Il vous est demandé d’effectuer la même étape pour le jeu de données de notation. Une fois que vous avez sélectionné le jeu de données d’entrée et de sortie, vous pouvez mettre à jour les configurations.

![](../images/models-recipes/publish-model/select_datasets.png)

Lorsqu’un service est créé, il hérite des configurations de notation par défaut. Vous pouvez revoir ces configurations et les ajuster selon les besoins en double-cliquant sur les valeurs. Une fois que les configurations vous conviennent, sélectionnez **[!UICONTROL Terminer]** pour lancer l’exécution de notation.

![](../images/models-recipes/publish-model/scoring_configs.png)

Sur la page **Présentation** du service, vous retrouvez les détails de la nouvelle tâche de notation et sa progression. Une fois la tâche terminée, l’en-tête **[!UICONTROL Le plus récent]** du conteneur **[!UICONTROL Notation]** est mis à jour.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez publié avec succès un modèle en tant que service accessible et noté des données à l’aide du nouveau service, par le biais de la [!UICONTROL Galerie de services]. Passez au tutoriel suivant pour apprendre à [planifier des opérations de formation et de notation automatisées sur un service](./schedule-models-ui.md).
