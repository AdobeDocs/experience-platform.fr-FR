---
keywords: Experience Platform;planification d’un modèle;Data Science Workspace;rubriques les plus consultées;planification de la notation;planification de la formation
solution: Experience Platform
title: Planification d’un modèle dans l’interface utilisateur de Data Science Workspace
type: Tutorial
description: Adobe Experience Platform Data Science Workspace vous permet de configurer des exécutions de notation et de formation planifiées sur un service d’apprentissage automatique. L’automatisation du processus de formation et de notation peut aider à maintenir et à améliorer l’efficacité d’un service avec le temps en suivant les motifs de vos données.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 18%

---

# Planification d’un modèle dans l’interface utilisateur de Data Science Workspace

Adobe Experience Platform [!DNL Data Science Workspace] vous permet de configurer des exécutions de notation et de formation planifiées sur un service d’apprentissage automatique. L’automatisation du processus de formation et de notation peut contribuer à maintenir et à améliorer l’efficacité d’un service tout au long du temps en suivant les schémas de vos données.

Ce tutoriel décrit les étapes à suivre pour configurer les plannings de formation et de notation sur un service existant par le biais de la [!UICONTROL Galerie de services]. Il est composé des sections principales suivantes :

- [Configuration d’une notation planifiée](#configure-scheduled-scoring)
- [Configuration d’une formation planifiée](#configure-scheduled-training)

## Commencer

Pour suivre ce tutoriel, vous devez avoir accès à [!DNL Experience Platform]. Si vous n’avez pas accès à une organisation dans [!DNL Experience Platform], contactez votre administrateur système avant de poursuivre.

Ce tutoriel nécessite un service existant. Si vous ne disposez pas d’un service accessible, vous pouvez en créer un en suivant le tutoriel de [publication d’un modèle en tant que service](./publish-model-service-ui.md).

## Configuration d’une notation planifiée {#configure-scheduled-scoring}

Vous pouvez configurer la notation du modèle de sorte que le processus soit automatisé sur une base planifiée. Une fois un service créé, vous pouvez suivre les étapes ci-dessous pour configurer et appliquer un planning de notation :

Dans Adobe Experience Platform, sélectionnez l’onglet **[!UICONTROL Services]** situé dans la colonne de navigation de gauche pour accéder à **[!DNL Service Gallery]**. Recherchez le service sur lequel vous souhaitez planifier des exécutions de notation et sélectionnez **[!UICONTROL Ouvrir]** pour afficher sa page **[!UICONTROL Aperçu]**.

![](../images/models-recipes/schedule/select_service.png)

La page de présentation affiche les informations de notation du service. Sélectionnez le lien **[!UICONTROL Mettre à jour le planning]** pour configurer un planning de notation.

![](../images/models-recipes/schedule/update_scoring.png)

Configurez la fréquence, la date de début, la date de fin, le jeu de données d’entrée et le jeu de données de sortie pour le planning de notation. Une fois les configurations satisfaites, sélectionnez **[!UICONTROL Créer]** pour mettre à jour le planning de notation du service.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

Votre planning de notation mis à jour s’affiche sur la page **[!UICONTROL Overview]** du service.

![](../images/models-recipes/schedule/scoring_set.png)

## Configuration d’une formation planifiée {#configure-scheduled-training}

La configuration des exécutions de formation planifiées sur un service garantit que le modèle d’apprentissage automatique est mis à jour selon les schémas de données les plus récents. Chaque fois qu’une opération de formation planifiée se termine, le modèle formé qui en résulte est utilisé pour mettre le service en service jusqu’à la prochaine opération de formation planifiée.

Une fois un service créé, vous pouvez suivre les étapes ci-dessous pour configurer et appliquer un planning de formation :

Dans Adobe Experience Platform, sélectionnez l’onglet **[!UICONTROL Services]** situé dans la colonne de navigation de gauche pour accéder à la **[!UICONTROL Galerie de services]**. Recherchez le service sur lequel vous souhaitez planifier des exécutions de formation et sélectionnez **[!UICONTROL Ouvrir]** pour afficher sa page **[!UICONTROL Aperçu]**.

![](../images/models-recipes/schedule/select_service.png)

La page Aperçu affiche les informations de formation du service. Sélectionnez le lien **[!UICONTROL Mettre à jour le planning]** pour configurer un planning de formation.

![](../images/models-recipes/schedule/update_training.png)

Configurez la fréquence, la date de début, la date de fin et le jeu de données d’entrée utilisés pour le planning de formation. Une fois les configurations satisfaites, sélectionnez **[!UICONTROL Créer]** pour mettre à jour le planning de formation du service.

![](../images/models-recipes/schedule/set_training_schedule.png)

Votre planning de formation mis à jour s’affiche sur la page **[!UICONTROL Overview]** du service.

![](../images/models-recipes/schedule/training_set.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez correctement planifié les exécutions de formation et de notation automatisées sur un service, et terminé le workflow d’interface utilisateur du tutoriel [!DNL Data Science Workspace]. Si vous ne l’avez pas déjà fait, pensez à [redémarrer le tutoriel](./create-retails-sales-dataset.md) et suivez le processus d’API pour créer, former, noter et publier un modèle.
