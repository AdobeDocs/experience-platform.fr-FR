---
description: Découvrez comment identifier et résoudre les antimodèles courants de configuration de la planification des tâches dans Adobe Experience Platform.
solution: Experience Platform
title: Identifier les modèles antiprogramme de travail
type: Tutorial
hide: true
source-git-commit: 9d170fec9b80f0f2e17fc39e8f573cbad515f823
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---


# Identifier les modèles de planification des tâches

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] sont actuellement disponibles en tant que version limitée et uniquement pour les tâches Real-Time CDP suivantes :
>
> * Ingestion du lac de données par lots
> * Ingestion de profils par lots
> * Segmentation par lots
> * Activation de la destination par lots.

La vue chronologique [Planifications de tâches](job-schedules.md) vous permet d’identifier les problèmes de configuration courants susceptibles de nuire aux performances et à la fiabilité de votre pipeline de données. Ces antimodèles entraînent souvent des échecs de tâche, des incohérences de données ou une dégradation des performances du système. En repérant ces modèles dès le début, vous pouvez reconfigurer vos tâches afin d’éviter les problèmes avant qu’ils n’affectent vos activités commerciales.

## Conditions préalables {#prerequisites}

Avant d’identifier les anti-modèles, vous devez :

* Ayez accès à [!UICONTROL Job Schedules] avec l’**[!UICONTROL View Job Schedules]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions).
* Familiarisez-vous avec l’interface [ Planifications de tâches ](job-schedules.md#understanding-interface) et avec la lecture de la vue chronologique.
* comprendre les concepts de base [ingestion par lots](../ingestion/batch-ingestion/overview.md), [segmentation](../segmentation/home.md) et [traitement des profils](../profile/home.md) ;

## Référence rapide {#anti-pattern-quick-reference}

| Anti-motif | Ce que vous verrez sur la chronologie | impact du Principal | Gravité |
|--------------|----------------------------------|----------------|----------|
| [Chevauchement des planifications](#schedule-overlap-pattern) | Plusieurs traitements s’exécutant simultanément | Contention des ressources et échecs des tâches | Élevé |
| [Densité des tâches planifiées](#scheduled-density) | De nombreux jeux de données avec des lots regroupés dans la même heure | Goulets d’étranglement de pipeline et segmentation incomplète | Élevé |
| [Lots excessifs par jeu de données](#excessive-batches-per-dataset) | Jeu de données unique avec des dizaines de lots quotidiens | Traitement inefficace et complexité opérationnelle | Méthode |

## Chevauchement des planifications {#schedule-overlap-pattern}

**Gravité de l’impact** : élevée | **Problème de Principal** : conflit de ressources

**Que rechercher** : plusieurs tâches planifiées pour s’exécuter en même temps ou en succession étroite, en particulier lorsque des tâches gourmandes en ressources se chevauchent.

Dans cet exemple, vous pouvez voir les tâches d’ingestion par lots s’exécuter en même temps qu’une tâche de segmentation planifiée. Cela crée des conflits de ressources car les deux opérations nécessitent une puissance de traitement et une mémoire importantes.

**Pourquoi cela pose problème** :

* **Contention des ressources** : lorsque plusieurs tâches gourmandes en ressources s’exécutent simultanément, elles entrent en concurrence pour les ressources système (CPU, mémoire, E/S), ce qui ralentit l’exécution de toutes les tâches.
* **Performances imprévisibles** : la durée de la tâche devient incohérente, ce qui rend difficile la planification d’horaires fiables.
* **Retards en cascade** : si les tâches prennent plus de temps que prévu, elles peuvent retarder les tâches dépendantes en aval, ce qui crée un effet d’entraînement tout au long de votre pipeline.
* **Risque d’échec accru** : l’épuisement des ressources peut entraîner l’expiration ou l’échec complet des tâches.

**Comment résoudre ce problème** :

* **Échelonner les plannings de tâches** : assurez-vous que les opérations gourmandes en ressources s’exécutent de manière séquentielle plutôt que simultanément.
* **Ajouter une durée de mémoire tampon** : laissez un espacement adéquat entre les tâches pour tenir compte des variations de traitement.
* **Vérifier les dépendances** : identifier les tâches à terminer avant que d’autres puissent commencer en toute sécurité.

## Densité des tâches planifiées {#scheduled-density}

**Gravité de l’impact** : élevée | **Problème de Principal** : goulets d’étranglement du pipeline

**Que rechercher** : trop de jeux de données avec plusieurs lots planifiés au cours d’une même heure, en particulier lorsque ces lots sont empilés de manière rapprochée et planifiés à des fenêtres de traitement critiques, telles que les heures de début de la segmentation.

Dans ce modèle, vous verrez :

* Plusieurs jeux de données exécutant chacun plusieurs lots par jour
* Tâches ETL (ingestion du lac de données et ingestion du profil) en cluster dans la même heure
* Ingestion par lots planifiée immédiatement avant ou pendant les fenêtres de segmentation planifiées

**Pourquoi cela pose problème** :

* **Goulot d’étranglement de pipeline** : lorsque de nombreux lots provenant de différents jeux de données sont empilés dans un court intervalle de temps, un goulot d’étranglement de traitement peut surcharger le pipeline d’ingestion.
* **Disponibilité de profil retardée** : les tâches d’ingestion de profil qui s’exécutent trop près des heures de début de la segmentation peuvent ne pas se terminer à temps, ce qui entraîne des évaluations d’audience incomplètes ou obsolètes.
* **Segmentation imprévisible** : si les traitements d’ingestion en amont sont toujours en cours d’exécution lorsque la segmentation commence, vous risquez d’évaluer les audiences par rapport à des données incomplètes, ce qui entraînerait une appartenance incorrecte aux audiences.
* **Échecs en cascade** : un seul lot retardé dans un planning empilé de manière dense peut provoquer un effet domino, retardant tous les lots suivants et les processus en aval.
* **Mise à rude épreuve des ressources** : le système peut avoir du mal à allouer suffisamment de ressources lors du traitement d’un trop grand nombre de tâches d’ingestion simultanées, ce qui ralentit les temps de traitement ou entraîne des échecs.

**Comment résoudre ce problème** :

* **Consolider les lots** : réduisez la fréquence des lots en combinant plusieurs petits lots en lots moins nombreux et plus volumineux par jeu de données.
* **Répartir uniformément** : répartissez les tâches d’ingestion tout au long de la journée plutôt que de les regrouper en heures spécifiques.
* **Ajouter une durée de mémoire tampon** : assurez-vous qu’une mémoire tampon minimale de 1 à 2 heures sépare la fin de l’ingestion du profil et le début de la segmentation.
* **Exigences en matière de révision** : déterminez si tous les jeux de données ont vraiment besoin de plusieurs lots quotidiens. De nombreux cas d’utilisation fonctionnent avec des mises à jour moins fréquentes.

## Lots excessifs par jeu de données {#excessive-batches-per-dataset}

**Gravité de l’impact** : Medium | **Problème de Principal** : traitement inefficace

**Que rechercher** : un seul jeu de données avec un nombre excessif de traitements par lots individuels planifiés toute la journée, créant une longue pile verticale de traitements sur la chronologie.

Dans ce modèle, vous verrez une ligne de jeu de données avec de nombreuses tâches d’ingestion par lots individuelles planifiées à intervalles fréquents, parfois des dizaines de lots par jour pour un seul jeu de données.

**Pourquoi cela pose problème** :

* **Traitement inefficace** : chaque traitement par lots comporte des frais généraux (initialisation, validation, mises à jour des métadonnées). Le traitement de nombreux petits lots est nettement moins efficace que le traitement de lots plus volumineux.
* **Augmentation de la surface d’échec** : plus d’emplois signifie plus de possibilités d’échec. Chaque lot qui échoue nécessite une investigation et un retraitement potentiel.
* **Charge inutile du système** : de petits lots fréquents maintiennent le système constamment occupé par des tâches fastidieuses plutôt que par un traitement réel des données, ce qui réduit le débit global.
* **Disponibilité des données retardée** : paradoxalement, l’exécution de nombreux petits lots peut retarder le moment où les données sont disponibles pour les processus en aval par rapport aux lots consolidés.
* **Inspection difficile** : le suivi de la réussite et des performances de dizaines de traitements par lots individuels par jeu de données devient complexe sur le plan opérationnel et prend du temps.
* **Retard de traitement des profils** : chaque lot d’ingestion de profil déclenche le traitement des profils. De petits lots fréquents peuvent entraîner l’exécution quasi continue du traitement des profils, ce qui empêche une optimisation efficace des lots.

**Comment résoudre ce problème** :

* **Réduire la fréquence des lots** : consolidez à un nombre inférieur de lots par jour et par jeu de données pour la plupart des cas d’utilisation.
* **Augmenter la taille du lot** : accumulez plus de données avant de déclencher l’ingestion plutôt que de les ingérer immédiatement.
* **S’aligner sur les besoins de l’entreprise** : vérifier si des mises à jour horaires sont vraiment requises ou si des mises à jour quotidiennes/biquotidiennes sont suffisantes.
* **Utiliser la diffusion en continu pour le temps réel** : passez à l’ingestion en continu pour les exigences en temps réel réelles au lieu de la simuler avec des lots fréquents.

## Étapes suivantes {#next-steps}

Après avoir identifié les anti-modèles dans vos planifications de tâches :

* Affichez les [détails de la tâche](job-schedules-details.md) pour examiner des jeux de données et des exécutions de tâche spécifiques susceptibles de provoquer des problèmes.
* Consultez la [présentation des planifications de tâches](job-schedules.md) pour comprendre l’interface et les fonctionnalités de contrôle.
* Découvrez [ingestion par lots](../ingestion/batch-ingestion/overview.md) pour optimiser vos plannings de chargement des données.
* Comprenez les [plannings de segmentation](../segmentation/home.md) pour garantir un timing approprié des évaluations d’audience.
* Explorez la [surveillance des flux de données de destination](../dataflows/ui/monitor-destinations.md) pour une visibilité de bout en bout du pipeline.
