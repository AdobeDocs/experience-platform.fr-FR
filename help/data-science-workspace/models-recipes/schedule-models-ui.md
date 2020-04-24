---
keywords: Experience Platform;schedule a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Planification d’un modèle (interface utilisateur)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Planification d’un modèle (interface utilisateur)

Adobe Experience Platform Data Science Workspace vous permet de configurer des exécutions planifiées de notation et de formation sur un service d’apprentissage automatique. L’automatisation du processus de formation et de notation peut aider à maintenir et à améliorer l’efficacité d’un service dans le temps en respectant les schémas de vos données.

Ce didacticiel décrit les étapes à suivre pour configurer les calendriers de formation et de notation sur un service existant par le biais de la Galerie *de* services. Il est divisé en plusieurs sections principales :

- [Configuration des scores planifiés](#configure-scheduled-scoring)
- [Configuration de la formation planifiée](#configure-scheduled-training)

## Prise en main

Pour terminer ce didacticiel, vous devez avoir accès à Experience Platform. Si vous n’avez pas accès à une organisation IMS dans Experience Platform, contactez votre administrateur système avant de poursuivre.

Ce didacticiel nécessite un service existant. Si vous ne disposez pas d’un service accessible, vous pouvez en créer un en suivant le didacticiel [Publier votre modèle en tant que service dans l’interface utilisateur](./publish-model-service-ui.md) .

## Configuration des scores planifiés {#configure-scheduled-scoring}

La notation du modèle peut être configurée pour être un processus automatisé sur une base planifiée. Une fois un service créé, vous pouvez suivre les étapes ci-dessous pour configurer et appliquer un calendrier de notation :

1. Dans Adobe Experience Platform, cliquez sur l’onglet **Services** situé dans la colonne de navigation de gauche pour accéder à la Galerie *de* services. Recherchez le service sur lequel vous souhaitez programmer des exécutions de score et cliquez sur **Ouvrir** pour  sa page *Aperçu* .
   ![](../images/models-recipes/schedule/click_to_open.png)

2. La page Aperçu affiche les informations de notation du service. Cliquez sur le lien **Mettre à jour le calendrier** pour configurer un calendrier de notation.
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. Configurez la fréquence, la date de  du, la date de fin, le jeu de données d’entrée et le jeu de données de sortie pour le calendrier de notation. Une fois que vous êtes satisfait des configurations, cliquez sur **Créer** pour mettre à jour le calendrier de notation du service.
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. Votre calendrier de notation mis à jour s’affiche dans la page *Aperçu* du service.
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## Configuration de la formation planifiée {#configure-scheduled-training}

La configuration des exécutions de formation planifiées sur un service garantit que le modèle d’apprentissage automatique est mis à jour selon les modèles de données les plus récents. Chaque fois qu’une série de formations planifiées se termine, le modèle formé qui en résulte est utilisé pour mettre le service sous tension jusqu’à la prochaine série de formations planifiées.

Une fois un service créé, vous pouvez suivre les étapes ci-dessous pour configurer et appliquer un calendrier de formation :

1. Dans Adobe Experience Platform, cliquez sur l’onglet **Services** situé dans la colonne de navigation de gauche pour accéder à la Galerie *de* services. Recherchez le service sur lequel vous souhaitez programmer les exécutions de formation, puis cliquez sur **Ouvrir** pour  sa page *Aperçu* .
   ![](../images/models-recipes/schedule/click_to_open.png)

2. La page Aperçu affiche les informations de formation du service. Cliquez sur le lien **Mettre à jour le calendrier** pour configurer un calendrier de formation.
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. Configurez la fréquence, la date de  du, la date de fin et le jeu de données d’entrée utilisé pour le calendrier de formation. Une fois que vous êtes satisfait des configurations, cliquez sur **Créer** pour mettre à jour le calendrier de formation du Service.
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. Votre programme de formation mis à jour est affiché dans la page *Aperçu* du service.
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez planifié avec succès les exécutions automatisées de formation et de notation sur un service et terminé le flux de travaux de l’interface utilisateur du didacticiel de l’espace de travail des sciences des données. Si vous ne l’avez pas déjà fait, pensez à [redémarrer le didacticiel](./create-retails-sales-dataset.md) et suivez le processus de l’API pour créer, former, marquer et publier un modèle.
