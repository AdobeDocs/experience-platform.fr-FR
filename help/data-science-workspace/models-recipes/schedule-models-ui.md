---
keywords: Experience Platform;schedule a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Planification d’un modèle (interface utilisateur)
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# Planification d’un modèle (interface utilisateur)

Adobe Experience Platform Data Science Workspace vous permet de configurer des exécutions planifiées de notation et de formation sur un service d’apprentissage automatique. L&#39;automatisation du processus de formation et de notation peut aider à maintenir et à améliorer l&#39;efficacité d&#39;un Service dans le temps en respectant les schémas de vos données.

Ce didacticiel décrit les étapes de configuration des calendriers de formation et de notation sur un service existant par le biais de la Galerie *de* services. Il est divisé en plusieurs sections principales :

- [Configuration d’un score planifié](#configure-scheduled-scoring)
- [Configuration de la formation planifiée](#configure-scheduled-training)

## Prise en main

Pour terminer ce didacticiel, vous devez avoir accès à Experience Platform. Si vous n’avez pas accès à une organisation IMS dans Experience Platform, contactez votre administrateur système avant de continuer.

Ce didacticiel nécessite un service existant. Si vous ne disposez pas d’un service accessible, vous pouvez en créer un en suivant le didacticiel sur l’interface utilisateur [](./publish-model-service-ui.md) Publier votre modèle en tant que service.

## Configuration d’un score planifié {#configure-scheduled-scoring}

La notation du modèle peut être configurée pour être un processus automatisé sur une base planifiée. Une fois un service créé, vous pouvez suivre les étapes ci-dessous pour configurer et appliquer un calendrier de notation :

1. Dans Adobe Experience Platform, cliquez sur l’ **[!UICONTROL Services]** onglet situé dans la colonne de navigation de gauche pour accéder à la Galerie *de* services. Recherchez le service sur lequel vous souhaitez planifier des exécutions de score et cliquez sur **[!UICONTROL Open]** pour vue à sa page *Aperçu* .
   ![](../images/models-recipes/schedule/click_to_open.png)

2. La page Aperçu affiche les informations d’évaluation du service. Cliquez sur le **[!UICONTROL Update Schedule]** lien pour configurer un calendrier de notation.
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. Configurez la fréquence, la date de début, la date de fin, le jeu de données d’entrée et le jeu de données de sortie pour le calendrier de notation. Une fois les configurations satisfaites, cliquez sur **[!UICONTROL Create]** pour mettre à jour le calendrier de notation du service.
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. Votre calendrier de notation mis à jour est affiché dans la page *Présentation* du service.
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## Configuration de la formation planifiée {#configure-scheduled-training}

La configuration des exécutions de formation planifiées sur un service garantit que le modèle d’apprentissage automatique est mis à jour selon les modèles de données les plus récents. Chaque fois qu&#39;une formation planifiée se termine, le modèle formé qui en résulte est utilisé pour mettre le service sous tension jusqu&#39;à la prochaine formation planifiée.

Une fois un service créé, vous pouvez suivre les étapes ci-dessous pour configurer et appliquer un calendrier de formation :

1. Dans Adobe Experience Platform, cliquez sur l’ **[!UICONTROL Services]** onglet situé dans la colonne de navigation de gauche pour accéder à la Galerie *de* services. Recherchez le service sur lequel vous souhaitez planifier les exécutions de formation et cliquez sur **[!UICONTROL Open]** pour vue à sa page *Aperçu* .
   ![](../images/models-recipes/schedule/click_to_open.png)

2. La page Aperçu affiche les informations de formation du service. Cliquez sur le **[!UICONTROL Update Schedule]** lien pour configurer un calendrier de formation.
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. Configurez la fréquence, la date de début, la date de fin et le jeu de données d’entrée utilisés pour le programme de formation. Une fois les configurations satisfaites, cliquez sur **[!UICONTROL Create]** pour mettre à jour le calendrier de formation du Service.
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. Votre programme de formation mis à jour est affiché dans la page *Présentation* du service.
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez planifié avec succès des exécutions de formation et de notation automatisées sur un service et terminé le processus d’interface utilisateur du didacticiel Data Science Workspace. Si vous ne l’avez pas déjà fait, pensez à [redémarrer le didacticiel](./create-retails-sales-dataset.md) et à suivre le processus de l’API pour créer, former, marquer et publier un modèle.
