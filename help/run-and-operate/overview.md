---
title: Présentation de l’exécution et du fonctionnement
description: Inspectez, dépannez et optimisez vos implémentations Adobe Experience Platform à l’aide des outils Exécuter et exploiter . Gagnez de la visibilité sur les activations par lots planifiées, identifiez les problèmes de configuration et améliorez la fiabilité du système.
hide: true
source-git-commit: 436ce6843e96b76dac0595ff5ab8a6067fb521ea
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 1%

---


# Présentation de l’exécution et du fonctionnement

>[!AVAILABILITY]
>
>Les fonctionnalités d’exécution et d’exploitation sont actuellement disponibles dans une version limitée.

Lorsque les traitements par lots échouent ou envoient des données incomplètes, vous devez rapidement comprendre ce qui a provoqué le problème. La cause principale peut être des problèmes de disponibilité des données, un timing incorrect, des problèmes de configuration ou des contraintes de capacité du système. Sans visibilité claire, vous pouvez passer des heures à enquêter sur plusieurs systèmes avant de trouver la réponse.

Avec [!UICONTROL Run and Operate] outils, vous pouvez :

* **Inspecter vos opérations de données** : obtenez une vue complète du statut et de l’intégrité de l’exécution des tâches dans tous vos workflows.
* **Dépannage plus rapide** : accédez à des informations de diagnostic détaillées et à l’historique d’exécution pour identifier rapidement les causes premières et réduire votre délai moyen de résolution des problèmes.
* **Prévention proactive des problèmes** : analysez les modèles de tâche, détectez les problèmes de configuration avant qu’ils ne provoquent des échecs et optimisez les opérations de données.

## Audiences cibles {#target-audiences}

[!UICONTROL Run and Operate] outils sont conçus pour servir plusieurs audiences dans l’ensemble de votre organisation :

* **Équipes de données et informatiques** : administrateurs système et ingénieurs de données qui gèrent des pipelines de données fiables et résolvent les problèmes techniques.
* **Opérations marketing** : technologues marketing qui inspectent la diffusion des données vers les plateformes marketing et résolvent les problèmes d’activation.
* **Implémentateurs** : professionnels validant l’efficacité et la fiabilité de l’implémentation, et résolvant les problèmes techniques.

## Conditions préalables {#prerequisites}

Pour accéder aux outils d’exécution et d’exploitation, vous avez besoin des **[!UICONTROL View Job Schedules]** et **[!UICONTROL View Profile Management]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions).
La page [!UICONTROL Job Schedules] donne un aperçu de toutes les tâches de traitement par lots planifiées.
Contactez votre administrateur système pour vous assurer que vous disposez des autorisations appropriées.

## Prise en main {#getting-started}

Pour accéder aux outils Exécuter et utiliser à partir de l’interface utilisateur d’Experience Platform :

1. Connectez-vous à votre compte Experience Platform et sélectionnez **[!UICONTROL Run and Operate]** dans le volet de navigation de gauche.
2. Sélectionnez l&#39;outil qui correspond à vos besoins d&#39;inspection ou de dépannage.

   >[!NOTE]
   >
   >Actuellement, la seule fonctionnalité disponible est [planifications de tâches](job-schedules.md).

![Interface utilisateur d’Experience Platform affichant le volet de navigation de gauche Exécuter et utiliser.](assets/overview/run-and-operate.png)

## Outils disponibles {#available-tools}

Les outils suivants vous aident à inspecter et optimiser vos opérations de données.

### Plannings de traitement {#job-schedules}

>[!IMPORTANT]
>
>Actuellement, les [!UICONTROL Job schedules] ne sont disponibles que pour les tâches Real-Time CDP suivantes :
>
> * Ingestion du lac de données par lots
> * Ingestion de profils par lots
> * Segmentation par lots
> * Activation de la destination par lots.

Avec [Planifications de tâches](job-schedules.md) vous pouvez inspecter toutes les opérations par lots planifiées dans votre organisation, par sandbox, y compris l’ingestion du lac de données, l’ingestion du profil, la segmentation et l’activation de destination. Affichez le statut d’exécution de la tâche, les mesures de performances et l’historique d’exécution pour identifier les modèles et diagnostiquer les problèmes de configuration qui affectent la fiabilité.

![Interface utilisateur d’Experience Platform affichant l’écran Plannings de tâches.](assets/overview/job-schedules-interface.png)

Job Schedules propose trois niveaux d’investigation :

* **[Inspecter les planifications de tâches](job-schedules.md)** : affichez tous les jeux de données et leurs tâches planifiées dans un journal pour identifier les modèles et les conflits de planification sur l’ensemble de votre pipeline.
* **[Identification des antimodèles](job-schedules-anti-patterns.md)** : découvrez comment repérer et résoudre les problèmes de configuration courants tels que le chevauchement des planifications, l’empilement dense des lots et les traitements par lots excessifs qui affectent les performances.
* **[Afficher les détails de la tâche](job-schedules-details.md)** : explorez des jeux de données spécifiques et des exécutions de tâche individuelles pour enquêter sur les échecs, vérifier la synchronisation et vérifier les enregistrements traités.

Vous pouvez également comprendre les dépendances entre les étapes de traitement des données, ce qui vous permet d’assurer un flux de données fiable tout au long des workflows Experience Platform.

## Étapes suivantes {#next-steps}

Maintenant que vous comprenez l’objectif et les fonctionnalités de [!UICONTROL Run and Operate] outils, explorez les ressources suivantes pour approfondir vos connaissances :

* Découvrez [ingestion par lots](../ingestion/batch-ingestion/overview.md) pour comprendre comment les données sont ingérées dans Experience Platform
* Découvrez comment [inspecter les planifications de tâches](job-schedules.md) pour l’ingestion et les activations par lots
* Découvrez comment [configurer des activations planifiées](../destinations/ui/activate-batch-profile-destinations.md) pour les destinations par lots
* Explorer [surveillance des flux de données](../dataflows/ui/monitor-destinations.md) pour les destinations

