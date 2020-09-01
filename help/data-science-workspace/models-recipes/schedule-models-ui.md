---
keywords: Experience Platform;schedule a model;Data Science Workspace;popular topics;schedule scoring;schedule training
solution: Experience Platform
title: Planification d’un modèle (interface utilisateur)
topic: Tutorial
description: Adobe Experience Platform Data Science Workspace vous permet de configurer des exécutions planifiées de notation et de formation sur un service d’apprentissage automatique. L’automatisation du processus de formation et de notation peut aider à maintenir et à améliorer l’efficacité d’un service avec le temps en suivant les motifs de vos données.
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 81%

---


# Planification d’un modèle (interface utilisateur)

Adobe Experience Platform [!DNL Data Science Workspace] allows you to set up scheduled scoring and training runs on a machine learning Service. L’automatisation du processus de formation et de notation peut aider à maintenir et à améliorer l’efficacité d’un service avec le temps en suivant les motifs de vos données.

Ce tutoriel décrit les étapes à suivre pour configurer les plannings de formation et de notation sur un service existant au moyen de la **[!UICONTROL Galerie de services]**. Il est composé des sections principales suivantes :

- [Configuration d’une notation planifiée](#configure-scheduled-scoring)
- [Configuration d’une formation planifiée](#configure-scheduled-training)

## Prise en main

Pour suivre ce tutoriel, vous devez avoir accès à [!DNL Experience Platform]. If you do not have access to an IMS Organization in [!DNL Experience Platform], please speak to your system administrator before proceeding.

Ce tutoriel nécessite un service déjà existant. Si vous ne disposez pas d’un service accessible, vous pouvez en créer un à l’aide du tutoriel [Publication de votre modèle en tant que service dans l’interface utilisateur](./publish-model-service-ui.md).

## Configuration d’une notation planifiée {#configure-scheduled-scoring}

Vous pouvez configurer la notation du modèle de sorte que le processus soit automatisé sur une base planifiée. Une fois un service créé, vous pouvez suivre les étapes ci-dessous pour configurer et appliquer un planning de notation :

1. In Adobe Experience Platform, click the **[!UICONTROL Services]** tab located in the left navigation column to access the *[!DNL Service Gallery]*. Recherchez le service sur lequel vous souhaitez planifier des opérations de notation et cliquez sur **[!UICONTROL Ouvrir]** pour afficher la page de *Présentation* correspondante.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. La page de présentation affiche les informations de notation du service. Cliquez sur le lien **[!UICONTROL Mettre à jour le planning]** pour configurer un planning de notation.
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. Configurez la fréquence, la date de début, la date de fin, le jeu de données d’entrée et le jeu de données de sortie pour le planning de notation. Lorsque les configurations vous conviennent, cliquez sur **[!UICONTROL Créer]** pour mettre à jour le planning de notation du service.
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. Votre planning de notation mis à jour apparaît dans la page de *Présentation* du service.
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## Configuration d’une formation planifiée {#configure-scheduled-training}

La configuration des opérations de formation planifiées sur un service garantit que le modèle d’apprentissage automatique est mis à jour selon les schémas de données les plus récents. Chaque fois qu’une opération de formation planifiée se termine, le modèle formé qui en résulte est utilisé pour mettre le service en œuvre jusqu’à la prochaine opération de formation planifiée.

Une fois un service créé, vous pouvez suivre les étapes ci-dessous pour configurer et appliquer un planning de formation :

1. Dans Adobe Experience Platform, cliquez sur l’onglet **[!UICONTROL Services]** situé dans la colonne de navigation de gauche pour accéder à la **[!UICONTROL Galerie de services]**. Recherchez le service pour lequel vous souhaitez planifier des opérations d’==e formation, puis cliquez sur **[!UICONTROL Ouvrir]** pour afficher la page de *Présentation* correspondante.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. La page Présentation affiche les informations sur la formation du service. Cliquez sur le lien **[!UICONTROL Mettre à jour le planning]** pour configurer un planning de formation.
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. Configurez la fréquence, la date de début, la date de fin et le jeu de données d’entrée utilisés pour le planning de formation. Lorsque les configurations vous conviennent, cliquez sur **[!UICONTROL Créer]** pour mettre à jour le planning de formation du service.
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. Votre planning de formation mis à jour apparaît dans la page de *Présentation* du service.
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## Étapes suivantes

By following this tutorial, you have successfully scheduled automated training and scoring runs on a Service, and completed the [!DNL Data Science Workspace] tutorial UI workflow. Si vous ne l’avez pas déjà fait, pensez à [recommencer le tutoriel](./create-retails-sales-dataset.md) et suivez le workflow d’API pour créer, former, noter et publier un modèle.
