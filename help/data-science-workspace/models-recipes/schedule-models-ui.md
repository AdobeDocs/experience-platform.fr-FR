---
keywords: Experience Platform ; planifier un modèle ; Espace de travail des données ; rubriques populaires ; programmer la notation ; programmer la formation
solution: Experience Platform
title: Planification d’un modèle dans l’interface utilisateur de Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace vous permet de configurer des exécutions planifiées de notation et de formation sur un service d’apprentissage automatique. L’automatisation du processus de formation et de notation peut aider à maintenir et à améliorer l’efficacité d’un service avec le temps en suivant les motifs de vos données.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 20%

---

# Planification d’un modèle dans l’interface utilisateur de Data Science Workspace

Adobe Experience Platform [!DNL Data Science Workspace] vous permet de configurer des exécutions planifiées de notation et de formation sur un service d’apprentissage automatique. L&#39;automatisation du processus de formation et de notation peut aider à maintenir et à améliorer l&#39;efficacité d&#39;un service dans le temps en respectant les schémas de vos données.

Ce didacticiel décrit les étapes de configuration des calendriers de formation et de notation sur un service existant par le biais de la [!UICONTROL Galerie de services]. Il est composé des sections principales suivantes :

- [Configuration d’une notation planifiée](#configure-scheduled-scoring)
- [Configuration d’une formation planifiée](#configure-scheduled-training)

## Prise en main

Pour suivre ce tutoriel, vous devez avoir accès à [!DNL Experience Platform]. Si vous n&#39;avez pas accès à une organisation IMS dans [!DNL Experience Platform], contactez votre administrateur système avant de continuer.

Ce didacticiel nécessite un service existant. Si vous ne disposez pas d’un service accessible, vous pouvez en créer un en suivant le didacticiel pour [publier un modèle en tant que service](./publish-model-service-ui.md).

## Configuration d’une notation planifiée {#configure-scheduled-scoring}

Vous pouvez configurer la notation du modèle de sorte que le processus soit automatisé sur une base planifiée. Une fois un service créé, vous pouvez suivre les étapes ci-dessous pour configurer et appliquer un calendrier de notation :

Dans Adobe Experience Platform, sélectionnez l&#39;onglet **[!UICONTROL Services]** situé dans la colonne de navigation de gauche pour accéder à **[!DNL Service Gallery]**. Recherchez le service sur lequel vous souhaitez planifier des exécutions de score et sélectionnez **[!UICONTROL Ouvrir]** pour vue sa **[!UICONTROL page Aperçu]**.

![](../images/models-recipes/schedule/select_service.png)

La page de présentation affiche les informations de notation du service. Sélectionnez le lien **[!UICONTROL Mettre à jour le calendrier]** pour configurer un calendrier de notation.

![](../images/models-recipes/schedule/update_scoring.png)

Configurez la fréquence, la date de début, la date de fin, le jeu de données d’entrée et le jeu de données de sortie pour le planning de notation. Une fois que vous êtes satisfait des configurations, sélectionnez **[!UICONTROL Créer]** pour mettre à jour le calendrier de notation du service.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

Votre calendrier de notation mis à jour est affiché dans la page **[!UICONTROL Aperçu]** du service.

![](../images/models-recipes/schedule/scoring_set.png)

## Configuration d’une formation planifiée {#configure-scheduled-training}

La configuration des exécutions de formation planifiées sur un service garantit que le modèle d’apprentissage automatique est mis à jour selon les modèles de données les plus récents. Chaque fois qu&#39;une série de formations planifiées se termine, le modèle de formation qui en résulte est utilisé pour alimenter le service jusqu&#39;à la prochaine série de formations planifiées.

Une fois un service créé, vous pouvez suivre les étapes ci-dessous pour configurer et appliquer un calendrier de formation :

Dans Adobe Experience Platform, sélectionnez l&#39;onglet **[!UICONTROL Services]** situé dans la colonne de navigation de gauche pour accéder à la **[!UICONTROL Galerie de services]**. Recherchez le service sur lequel vous souhaitez planifier les exécutions de formation et sélectionnez **[!UICONTROL Ouvrir]** pour vue sa **[!UICONTROL page Aperçu]**.

![](../images/models-recipes/schedule/select_service.png)

La page Aperçu affiche les informations de formation du service. Sélectionnez le lien **[!UICONTROL Mettre à jour le calendrier]** pour configurer un calendrier de formation.

![](../images/models-recipes/schedule/update_training.png)

Configurez la fréquence, la date de début, la date de fin et le jeu de données d’entrée utilisés pour le planning de formation. Une fois les configurations satisfaites, sélectionnez **[!UICONTROL Créer]** pour mettre à jour le calendrier de formation du service.

![](../images/models-recipes/schedule/set_training_schedule.png)

Votre programme de formation mis à jour est affiché dans la page **[!UICONTROL Aperçu]** du service.

![](../images/models-recipes/schedule/training_set.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez planifié avec succès des exécutions de formation et de notation automatisées sur un service et terminé le processus d&#39;interface utilisateur du didacticiel [!DNL Data Science Workspace]. Si vous ne l’avez pas déjà fait, envisagez de redémarrer [le didacticiel](./create-retails-sales-dataset.md) et de suivre le processus de l’API pour créer, former, marquer et publier un modèle.
