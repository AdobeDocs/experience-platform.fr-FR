---
description: Découvrez comment inspecter et résoudre les problèmes liés aux traitements par lots planifiés à l’aide de l’outil Planifications de tâches dans Adobe Experience Platform.
solution: Experience Platform
title: Inspecter les planifications de tâches
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3696ebffc4bd1e588a04e5789ff0c7971e636b56
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 1%

---


# Inspecter les plannings de tâches

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] sont actuellement disponibles en tant que version limitée et uniquement pour les tâches Real-Time CDP suivantes :
>
> * Ingestion du lac de données par lots
> * Ingestion de profils par lots
> * Segmentation par lots
> * Activation de la destination par lots.

[!UICONTROL Job Schedules] offre une vue unifiée de toutes les tâches de traitement par lots planifiées sur votre pipeline de données, de l’ingestion à l’activation de la destination. Inspectez le statut d’exécution, identifiez les conflits de planification et diagnostiquez les problèmes de configuration avant qu’ils n’affectent les opérations de votre entreprise.

Utilisez les planifications de tâches pour enquêter sur les échecs, optimiser la synchronisation des tâches et comprendre les dépendances entre l’ingestion du lac de données, le traitement des profils, la segmentation et l’activation de destination. Pour obtenir des conseils sur la résolution de problèmes de configuration courants, consultez la documentation sur l&#39;[identification des antimodèles de planification des tâches](job-schedules-anti-patterns.md).

## Conditions préalables {#prerequisites}

Pour accéder à [!UICONTROL Job Schedules], vous avez besoin des **[!UICONTROL View Job Schedules]** et **[!UICONTROL View Profile Management]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions).

Contactez votre administrateur système pour vous assurer que vous disposez des autorisations appropriées.

## Prise en main {#getting-started}

Avant d’utiliser [!UICONTROL Job Schedules], vous devez connaître les concepts d’Experience Platform suivants :

* **[Ingestion par lots](../ingestion/batch-ingestion/overview.md)** : méthode de chargement des données dans le lac de données et la banque de profils à des intervalles planifiés.
* **[Segmentation](../segmentation/home.md)** : méthode d’évaluation et de mise à jour des audiences en fonction des données de profil et des définitions de segment.
* **[Real-Time Customer Profile](../profile/home.md)** : méthode d’unification des données de profil et de mise à disposition pour la segmentation et l’activation.
* **[Destinations](../destinations/home.md)** : où et comment les données sont activées sur les systèmes en aval et les plateformes marketing.

La compréhension de ces composants vous aide à interpréter les modèles d’exécution de tâche et à diagnostiquer les problèmes lorsqu’ils se produisent.

## Présentation de l’interface des planifications de tâches {#understanding-interface}

Pour accéder à [!UICONTROL Job Schedules] :

1. Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Run and Operate]** dans le volet de navigation de gauche.
2. Sélectionnez **[!UICONTROL Job Schedules]**.

La page [!UICONTROL Job Schedules] donne un aperçu de toutes les tâches de traitement par lots planifiées.

![Exécuter et utiliser le volet de navigation de gauche](assets/job-schedules/run-and-operate-left-nav.png)

### Cartes récapitulatives {#summary-cards}

En haut de la page, vous pouvez voir des cartes récapitulatives qui fournissent des informations rapides sur vos tâches de traitement par lots.

![Cartes récapitulatives des planifications de tâches présentant des informations sur les tâches de traitement par lots](assets/job-schedules/job-schedules-cards.png)

* **Traitements d’ingestion de lac** : nombre de traitements d’ingestion de lac de données ayant été exécutés.
* **Traitements d’ingestion de profil** : nombre de traitements d’ingestion de profil qui ont été exécutés.
* **Segmentation suivante** : date d’exécution de la prochaine tâche de segmentation planifiée.
* **Prochaine activation de destination** : date d’exécution de la prochaine tâche d’activation de destination planifiée.

Ces cartes vous aident à comprendre l’activité et les planifications à venir dans votre pipeline de données. Les valeurs de **Exécutions d’ingestion de lac** et **Exécutions d’ingestion de profil** changent en fonction de l’intervalle de temps sélectionné (Aujourd’hui, Hier ou 7 derniers jours) ; les cartes à exécuter ensuite (**Segmentation suivante** et **Activation de destination suivante**) ne sont pas affectées par le sélecteur d’heure.

### Sélecteur de période {#time-period}

Utilisez les sélecteurs de période pour choisir la période à prendre en compte pour consulter les tâches planifiées.

![Exemple animé de l’interface utilisateur du sélecteur de période dans les planifications de tâches](assets/job-schedules/time-selector.gif)

* **Today** : affichage des tâches planifiées pour aujourd’hui (vue par défaut).
* **Hier** : affichez les tâches exécutées hier.
* **7 derniers jours** : affichez les tâches de la semaine dernière.

### Détails des plannings de traitement par lots {#job-schedules-details}

La vue principale vous indique le moment où les traitements par lots sont planifiés pour s’exécuter tout au long de la journée. Vous pouvez :

* **Afficher les tâches par jeu de données ou entité** : la colonne de gauche affiche les noms des jeux de données ou des tâches de traitement (par exemple, les jeux de données d’ingestion ou les tâches de segmentation).
* **Voir Durée de la tâche** : la chronologie indique la date d’exécution planifiée de chaque tâche et les indicateurs visuels indiquent cette heure.
* **Tâches de filtrage** : utilisez l’icône de filtre pour filtrer les jeux de données à inclure dans le rapport.
* **Présentation des types de tâche** : la légende codée par des couleurs en bas vous aide à identifier différents types de tâche :
   * **Ingestion du lac** (vert) : ingestion de données dans le lac de données
   * **Ingestion de profil** (rose) : ingestion de données dans la banque de profils
   * **Segmentation** (bleu clair) : traitements d’évaluation d’audience
   * **Exportation des profils** (bleu) : exportation des données de profil
   * **Activation** (gris foncé) : tâches d’activation de destination
   * **En cours** (répartition) : tâches en cours d’exécution ou en file d’attente

Cette vue chronologique vous permet d’identifier les conflits de planification, de comprendre les dépendances entre les tâches et d’optimiser les plannings de traitement par lots.

## Identification des problèmes de configuration {#identifying-issues}

En examinant les planifications de tâches, vous remarquerez peut-être des motifs indiquant des problèmes de configuration. Les problèmes courants sont les suivants :

* Tâches planifiées trop rapprochées, provoquant des conflits de ressources
* Trop de lots exécutés dans la même fenêtre temporelle
* Jeux de données individuels avec trop de traitements par lots quotidiens
* Tâches d’ingestion planifiées immédiatement avant l’exécution de la segmentation

Ces modèles peuvent entraîner des échecs de tâche, un traitement des données incomplet et de mauvaises performances du système. Pour savoir comment identifier et résoudre ces problèmes, consultez la documentation sur l’[identification des modèles de planification des tâches](job-schedules-anti-patterns.md).

Lorsque vous devez examiner des jeux de données ou des exécutions de tâches spécifiques, vous pouvez accéder à des vues détaillées pour afficher l’historique d’exécution, les messages d’erreur, les mesures de performances et les dépendances. Pour plus d’informations sur l’affichage de ces données détaillées, consultez la documentation sur la [affichage des détails de la tâche](job-schedules-details.md).


## Étapes suivantes {#next-steps}

Après avoir appris les planifications de tâches, vous souhaiterez peut-être explorer les sujets suivants :

* [Afficher les détails de la tâche](job-schedules-details.md) : découvrez comment analyser en profondeur les jeux de données individuels et les exécutions de tâche pour une enquête détaillée.
* [Identification des antimodèles de planification des tâches](job-schedules-anti-patterns.md) : découvrez comment repérer et résoudre les problèmes de configuration courants qui affectent les performances du pipeline.
* [Ingestion par lots](../ingestion/batch-ingestion/overview.md) : découvrez comment ingérer des données dans Experience Platform à l’aide du traitement par lots.
* [Segmentation](../segmentation/home.md) : comprenez comment les audiences sont évaluées et mises à jour à des intervalles planifiés.
* [Surveiller les flux de données pour les destinations](../dataflows/ui/monitor-destinations.md) : découvrez comment surveiller les flux de données d’activation de destination.
* [Planifier des exportations d’audience](../destinations/ui/activate-batch-profile-destinations.md) : découvrez comment configurer des activations de destination par lots planifiées.
