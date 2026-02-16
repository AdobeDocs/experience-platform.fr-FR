---
description: Découvrez comment afficher des informations détaillées sur les jeux de données et les exécutions de tâches individuelles dans les planifications de tâches.
solution: Experience Platform
title: Afficher les détails de planification des tâches
type: Tutorial
hide: true
source-git-commit: 436ce6843e96b76dac0595ff5ab8a6067fb521ea
workflow-type: tm+mt
source-wordcount: '1783'
ht-degree: 1%

---


# Afficher les détails de la planification des tâches

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] sont actuellement disponibles en tant que version limitée et uniquement pour les tâches Real-Time CDP suivantes :
>
> * Ingestion du lac de données par lots
> * Ingestion de profils par lots
> * Segmentation par lots
> * Activation de la destination par lots.

Lors du dépannage des échecs de tâche ou de l’examen des problèmes de performances, vous avez besoin d’informations détaillées sur des jeux de données spécifiques et leurs exécutions de tâche. L’interface [Planifications de tâches](job-schedules.md) vous permet d’analyser en profondeur les jeux de données et les tâches individuels à partir de la vue chronologique afin de comprendre l’historique d’exécution, la synchronisation et le statut.

Utilisez cette vue détaillée pour :

* Recherchez pourquoi une tâche spécifique a échoué ou a pris plus de temps que prévu
* Vérifier l’historique d’exécution d’un jeu de données au fil du temps
* Comprendre les modèles de durée et de durée des traitements par lots
* Identifier les lots spécifiques à l’origine des problèmes de pipeline
* Collectez les informations nécessaires à la résolution des problèmes avec l’assistance Adobe

## Conditions préalables {#prerequisites}

Avant d’afficher les détails de la tâche, vous devez :

* Disposer d’un accès à [!UICONTROL Job Schedules] avec les **[!UICONTROL View Job Schedules]** et **[!UICONTROL View Profile Management]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions).
* Familiarisez-vous avec l’[interface des planifications de tâches](job-schedules.md#understanding-interface) et la vue chronologique.
* comprendre les différents [types de tâche](job-schedules.md#job-schedules-details) (ingestion de lac, ingestion de profil, segmentation, activation) ;

## Présentation de la hiérarchie des détails {#details-hierarchy}

Les planifications de tâches fournissent trois niveaux de détail, ce qui vous permet de passer de modèles généraux à des problèmes spécifiques :

| Niveau d’affichage | Ce qu’il montre | Quand l’utiliser |
|------------|---------------|----------------|
| **Mode Chronologie** | Tous les jeux de données et leurs tâches planifiées sur la période sélectionnée | Identification de modèles, repérage [anti-modèles](job-schedules-anti-patterns.md) et obtention d’une vue d’ensemble de votre pipeline entier |
| **Informations sur le jeu de données** | Mesures agrégées et historique d’exécution pour un seul jeu de données | Suivi des performances globales d’un jeu de données, compréhension des volumes de données et révision de la fréquence des tâches |
| **Détails de l’exécution de tâche** | Informations d’exécution spécifiques pour une exécution de tâche individuelle | Recherche des raisons de l’échec d’une tâche particulière, vérification de la durée exacte et vérification des enregistrements traités |

**Flux de navigation** : commencez par la vue chronologique pour identifier les problèmes → Sélectionnez un jeu de données pour afficher ses détails → Sélectionnez une exécution de tâche spécifique pour en examiner les détails.

### Comprendre la vue chronologique {#timeline-visualization}

La vue chronologique utilise une disposition horizontale et verticale pour vous aider à comprendre les planifications de tâches et les temps de traitement critiques :

* **Axe horizontal (progression temporelle)** : les jeux de données et leurs exécutions de tâches s’affichent dans la chronologie de gauche à droite, indiquant le moment où les tâches s’exécutent sur la période sélectionnée (aujourd’hui, hier ou les 7 derniers jours). Chaque barre de couleur représente une exécution de tâche, positionnée horizontalement en fonction de son heure de début et de fin.

* **Axe vertical (heures de début planifiées)** : les heures de début planifiées critiques sont affichées sous la forme de lignes verticales qui s’étendent sur tous les jeux de données, ce qui facilite la visibilité de la relation de minutage entre les tâches en amont et le traitement en aval :
   * **Ligne verticale bleue** : représente le moment où la segmentation doit commencer
   * **Ligne verticale noire** : représente le moment où l’activation de la destination est planifiée pour commencer

Cette disposition vous permet d’identifier rapidement les relations de minutage entre vos tâches de pipeline de données et le traitement en aval. Idéalement, les tâches en amont (telles que l’ingestion du lac de données et du profil) doivent se terminer à gauche de ces marqueurs verticaux, en s’assurant que les données sont prêtes avant le début de la segmentation et de l’activation. Les tâches qui s’étendent au-delà de ces marqueurs indiquent des problèmes de minutage potentiels lorsque les processus en aval peuvent commencer avant que les données ne soient entièrement préparées.

### Quelle vue dois-je utiliser ? {#which-view}

Utilisez le tableau ci-dessous pour choisir la vue qui convient à votre tâche. Conservez les majuscules et les minuscules nécessaires dans la vue recommandée pour naviguer efficacement.

| Je dois... | Utiliser cette vue |
|--------------|---------------|
| Afficher tous mes jeux de données activés pour le profil et leurs plannings à la fois | [Mode Chronologie](job-schedules.md) |
| Identifier les conflits de planification ou les anti-modèles | [Mode Chronologie](job-schedules.md) |
| Suivre les performances globales d’un jeu de données | [Informations sur le jeu de données](#view-dataset-details) |
| Afficher le nombre total d’enregistrements traités par un jeu de données | [Informations sur le jeu de données](#view-dataset-details) |
| Comparer les performances des tâches dans le temps pour un jeu de données | [Informations sur le jeu de données](#view-dataset-details) |
| Rechercher pourquoi une tâche spécifique a échoué | [Détails de l’exécution de tâche](#view-job-details) |
| Vérifier le timing exact de l’exécution d’un traitement spécifique | [Détails de l’exécution de tâche](#view-job-details) |
| Vérifier les enregistrements traités en une seule exécution | [Détails de l’exécution de tâche](#view-job-details) |
| Accéder aux messages d’erreur détaillés | [Détails de l’exécution de la tâche](#view-job-details) → Sélectionnez l’identifiant d’exécution du flux de données |

## Afficher les détails du jeu de données {#view-dataset-details}

Pour afficher les détails d’un jeu de données spécifique :

1. Dans la vue chronologique **[!UICONTROL Job Schedules]**, recherchez le jeu de données que vous souhaitez étudier.
2. Sélectionnez le nom du jeu de données dans la colonne de gauche.

La vue des détails du jeu de données s’ouvre dans un panneau de droite, affichant des informations sur toutes les tâches associées à ce jeu de données.

![Panneau Détails du jeu de données affichant les mesures agrégées d’ingestion de lac et de profil pour un jeu de données sélectionné.](assets/job-schedules/view-dataset-details.png)

Le panneau Détails du jeu de données affiche le nom, l’identifiant du jeu de données et les mesures spécifiques à la tâche organisées par type de tâche. En haut du panneau, l’identifiant du jeu de données s’affiche sous la forme d’un lien cliquable. Sélectionnez cet identifiant pour accéder à la page des détails du jeu de données complet.

Chaque panneau des détails du jeu de données comprend les mesures suivantes :

### Mesures d’ingestion du lac {#lake-ingestion-metrics}

Pour les jeux de données avec des tâches d’ingestion de lac de données, le panneau affiche les mesures suivantes :

| Mesure | Description | Utiliser pour |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | Nombre total de traitements d’ingestion de lac de données terminés pour ce jeu de données | Suivi des activités |
| **[!UICONTROL Runs in progress]** | Nombre de traitements d’ingestion de lac en cours d’exécution | Détection des goulets d’étranglement |
| **[!UICONTROL Total records added]** | Nombre cumulé de nouveaux enregistrements ajoutés au lac de données lors de toutes les exécutions de tâche | Surveillance du volume |
| **[!UICONTROL Total ingestion time]** | Durée combinée de toutes les tâches d’ingestion du lac de données | Évaluation du temps de traitement |
| **[!UICONTROL Total records updated]** | Le nombre cumulé d’enregistrements existants qui ont été mis à jour lors de l’ingestion | Actualiser l’analyse des motifs |
| **[!UICONTROL Avg. ingestion speed (records/second)]** | Taux de débit moyen des tâches d’ingestion du lac de données | Comparaison des performances |

### Mesures d’ingestion de profil {#profile-ingestion-metrics}

Pour les jeux de données avec des tâches d’ingestion de profil, le panneau affiche les mesures suivantes :

| Mesure | Description | Utiliser pour |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | Nombre total de traitements d’ingestion de profil terminés pour ce jeu de données | Suivi des activités |
| **[!UICONTROL Runs in progress]** | Nombre de traitements d’ingestion de profil en cours d’exécution | Détection de délai |
| **[!UICONTROL Total profiles created]** | Nombre cumulé de nouveaux profils créés à partir de ce jeu de données lors de toutes les exécutions de tâche | Suivi de la croissance des profils |
| **[!UICONTROL Total profile ingestion time]** | Durée combinée de toutes les tâches d’ingestion de profil | Identification du problème de minutage |
| **[!UICONTROL Total profiles updated]** | Le nombre cumulé de profils existants qui ont été mis à jour avec des données de ce jeu de données | Mise à jour du suivi de la fréquence |
| **[!UICONTROL Avg. profile ingestion speed (profiles/second)]** | Taux de débit moyen des tâches d’ingestion de profil | Suivi des performances |

>[!NOTE]
>
> Ces mesures affichent les totaux cumulés de toutes les exécutions de tâches pour ce jeu de données. Pour afficher les détails d’une exécution spécifique, sélectionnez une tâche directement dans la chronologie.

## Filtrer les jeux de données dans la chronologie {#filter-datasets}

Lorsque vous disposez de nombreux jeux de données avec des tâches planifiées, vous pouvez vous concentrer sur des jeux de données spécifiques plutôt que de les afficher tous en même temps. Le filtre du jeu de données vous permet de sélectionner les jeux de données qui apparaissent dans la vue chronologique.

![Le panneau de filtrage des jeux de données vous permettant de sélectionner les jeux de données qui apparaissent dans la vue chronologique.](assets/job-schedules/view-datasets.gif)

Pour filtrer les jeux de données affichés dans le journal :

1. Recherchez le compteur de jeux de données dans le coin supérieur gauche de la vue chronologique (par exemple, « 2 jeux de données »).
2. Sélectionnez l’icône de filtre en regard du compteur du jeu de données.
3. Un panneau de sélection de jeux de données s’ouvre, affichant tous les jeux de données activés pour le profil disponibles avec des tâches planifiées.
4. Sélectionnez ou désélectionnez des jeux de données pour les afficher ou les masquer dans la vue chronologique.
5. La chronologie se met immédiatement à jour pour afficher uniquement les jeux de données sélectionnés.

Utilisez le filtrage pour :

* **Se concentrer sur des sources de données spécifiques** : lors de la résolution des problèmes d’un pipeline de données spécifique, filtrez pour afficher uniquement les jeux de données pertinents.
* **Réduire l’encombrement visuel** : si vous disposez de nombreux jeux de données, le filtrage vous permet de voir plus clairement les modèles pour un sous-ensemble de données.
* **Comparer les jeux de données associés** : sélectionnez uniquement les jeux de données associés pour comprendre leur relation de planification.
* **Étude des anti-modèles** : lorsque vous identifiez un [problème de configuration](job-schedules-anti-patterns.md) potentiel, filtrez vers les jeux de données affectés pour les examiner de plus près.

Le filtre persiste pendant votre session afin que vous puissiez naviguer entre les périodes (aujourd’hui, hier, 7 derniers jours) tout en conservant votre sélection de jeux de données.

## Afficher les détails de l’exécution de tâche individuelle {#view-job-details}

Lorsque vous devez enquêter sur une exécution de tâche spécifique, sélectionnez-la dans la chronologie pour afficher les informations d’exécution détaillées pour cette exécution particulière.

### Accéder aux détails de l’exécution de tâche {#access-job-details}

Pour afficher les détails d’une exécution de tâche spécifique :

1. Dans la vue chronologique [!UICONTROL Job Schedules], recherchez l’exécution de tâche spécifique que vous souhaitez étudier.
2. Sélectionnez l’indicateur de tâche dans le journal (la barre colorée représentant la tâche).

Le panneau **[!UICONTROL Dataflow run details]** s’ouvre et affiche des informations sur cette exécution de tâche spécifique.

![Panneau Détails de l’exécution du flux de données affichant les informations d’exécution pour une exécution de tâche spécifique.](assets/job-schedules/job-details.png)

### Détails de l’exécution du flux de données {#dataflow-run-details}

Le panneau Détails de l’exécution du flux de données affiche des informations sur l’exécution de tâche spécifique, organisée par type de tâche. Pour les tâches d’ingestion, vous verrez des détails sur les étapes d’ingestion de lac et d’ingestion de profil.

#### Détails de la tâche d’ingestion de lac {#lake-ingestion-job-details}

| Champ | Description |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | Identifiant unique de cette exécution de tâche d’ingestion de lac spécifique. Sélectionnez l’ID pour afficher les détails complets de la surveillance du flux de données. |
| **[!UICONTROL Run status]** | Résultat de la tâche (Succès, Échec, En cours, En file d’attente). Un indicateur vert indique la réussite de l’opération. |
| **[!UICONTROL Started at]** | Date et heure auxquelles la tâche d’ingestion du lac a commencé à s’exécuter. |
| **[!UICONTROL Completed at]** | Date et heure auxquelles la tâche d’ingestion du lac a terminé son exécution. |
| **[!UICONTROL Records added]** | Nombre de nouveaux enregistrements ajoutés au lac de données pendant cette exécution de tâche. |
| **[!UICONTROL Records updated]** | Nombre d’enregistrements existants qui ont été mis à jour dans le lac de données au cours de cette exécution de tâche. |

#### Détails de la tâche d’ingestion de profil {#profile-ingestion-job-details}

| Champ | Description |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | Identifiant unique de cette exécution de tâche d’ingestion de profil spécifique. Sélectionnez l’ID pour afficher les détails complets de la surveillance du flux de données. |
| **[!UICONTROL Run status]** | Résultat de la tâche (Succès, Échec, En cours, En file d’attente). Un indicateur vert indique la réussite de l’opération. |
| **[!UICONTROL Started at]** | Date et heure auxquelles la tâche d’ingestion de profil a commencé à s’exécuter. |
| **[!UICONTROL Completed at]** | Date et heure auxquelles la tâche d’ingestion de profil a terminé son exécution. |
| **[!UICONTROL Records added]** | Nombre de nouveaux profils créés pendant l’exécution de cette tâche. |
| **[!UICONTROL Records updated]** | Nombre de profils existants qui ont été mis à jour pendant cette exécution de tâche. |

### Comprendre le flux d’exécution de tâche {#job-execution-flow}

Lors de l’affichage d’une exécution de tâche spécifique, vous pouvez voir la relation entre l’ingestion de lac et l’ingestion de profil :

* **L’ingestion du lac s’exécute en premier** : les données sont chargées dans le lac de données et validées.
* **L’ingestion de profil suit** : une fois l’ingestion de lac terminée, les enregistrements éligibles sont traités dans la banque de profils.
* **Le minutage a son importance** : notez la différence de temps entre la fin de l’ingestion du lac et le début de l’ingestion du profil. Les lacunes ici peuvent avoir un impact sur les processus en aval comme la segmentation.

**Utilisez les détails de l’exécution de tâche pour** :

* Vérifier qu’une tâche spécifique s’est terminée correctement
* Calculer la durée réelle d’une exécution de tâche (durée terminée moins heure de début)
* Comprendre le nombre d’enregistrements traités au cours d’une exécution spécifique
* Comparer les performances sur différentes exécutions de tâche
* Accéder à la surveillance détaillée des flux de données pour résoudre les problèmes
* Identifier les problèmes de minutage entre les étapes d’ingestion de lac et de profil

## Résolution des problèmes liés aux détails de la tâche {#troubleshooting}

Utilisez les détails de la tâche pour examiner les problèmes et déterminer les étapes suivantes :

**Tâches ayant échoué** : sélectionnez l’identifiant d’exécution du flux de données pour afficher les détails de l’erreur dans le tableau de bord de surveillance. Vérifiez [détails du jeu de données](#view-dataset-details) les modèles récurrents, passez en revue la [chronologie](job-schedules.md) pour détecter les conflits de ressources et identifiez [anti-modèles](job-schedules-anti-patterns.md) dans votre configuration.

**Tâches lentes** : comparez la durée aux moyennes historiques dans [mesures du jeu de données](#view-dataset-details). Les causes courantes comprennent [chevauchement de planification](job-schedules-anti-patterns.md#schedule-overlap-pattern), [empilement dense de lots](job-schedules-anti-patterns.md#scheduled-density) ou augmentation du volume de données.

**Incohérences d’enregistrement** : comparez les enregistrements d’ingestion du lac aux enregistrements d’ingestion de profil dans les détails de l’exécution de la tâche. L’ingestion de profils affiche généralement moins d’enregistrements en raison des exigences d’identité et des règles de qualité des données.

Pour obtenir des informations détaillées sur le statut des flux de données, consultez [Surveillance de l’ingestion du lac de données](../dataflows/ui/monitor-sources.md), [Surveillance des flux de données pour les profils](../dataflows/ui/monitor-profiles.md), [Surveillance des flux de données pour les audiences](../dataflows/ui/monitor-audiences.md) et [Surveillance des flux de données pour les destinations](../dataflows/ui/monitor-destinations.md).

## Étapes suivantes {#next-steps}

Après avoir appris à afficher les détails de la tâche :

* Consultez la [présentation des planifications de tâches](job-schedules.md) pour comprendre la vue et l’interface de la chronologie.
* Découvrez les [anti-modèles](job-schedules-anti-patterns.md) pour éviter les problèmes de configuration courants.
* Découvrez [ingestion par lots](../ingestion/batch-ingestion/overview.md) pour optimiser vos plannings de chargement des données.
* Explorez la [surveillance des flux de données de destination](../dataflows/ui/monitor-destinations.md) pour une visibilité de bout en bout du pipeline.
