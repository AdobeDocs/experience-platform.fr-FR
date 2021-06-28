---
keywords: Experience Platform;accueil;rubriques les plus consultées;comptes de contrôle;flux de données de surveillance;flux de données
description: Les connecteurs source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes de surveillance des flux de données en continu à partir de l’espace de travail Sources .
solution: Experience Platform
title: Surveillance des flux de données pour les sources de diffusion en continu dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
source-git-commit: 58761cbe8465f4a00f07f33f751f481d34493cf7
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 12%

---


# Surveillance des flux de données pour les sources de diffusion en continu dans l’interface utilisateur

Ce tutoriel décrit les étapes de surveillance des flux de données pour les sources en continu à l’aide de l’espace de travail [!UICONTROL Sources].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Flux de données](../../../dataflows/home.md) : les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Platform. Les flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, vers [!DNL Identity] et [!DNL Profile], et vers [!DNL Destinations].
   * [Le flux de données s’exécute](../../notifications.md) : Les exécutions de flux de données sont les tâches planifiées récurrentes en fonction de la configuration de fréquence des flux de données sélectionnés.
* [Sources](../../home.md) : Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Environnements de test](../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Surveillance des flux de données pour les sources de diffusion en continu

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Pour afficher les flux de données existants pour les sources de diffusion en continu, sélectionnez **[!UICONTROL Flux de données]** dans l’en-tête supérieur.

![catalogue](../../images/tutorials/monitor-streaming/catalog.png)

La page [!UICONTROL Flux de données] contient une liste de tous les flux de données existants de votre organisation, y compris des informations sur leurs données source, leur nom de compte et leur état d’exécution.

Sélectionnez le nom du flux de données à afficher.

![flux de données](../../images/tutorials/monitor-streaming/dataflows.png)

Le tableau suivant contient plus d’informations sur les états d’exécution du flux de données :

| État | Description |
| ------ | ----------- |
| Terminé | L’état `Completed` indique que tous les enregistrements de l’exécution de flux de données correspondante ont été traités pendant la période d’une heure. Un état `Completed` peut toujours contenir des erreurs lors des exécutions du flux de données. |
| En cours de traitement | L’état `Processing` indique qu’un flux de données n’est pas encore principal. Cet état est souvent rencontré immédiatement après la création d’un nouveau flux de données. |
| Erreur | L’état `Error` indique que le processus d’activation d’un flux de données a été interrompu. |

La page [!UICONTROL Activité du flux de données] affiche des informations spécifiques sur votre flux de données en continu. La bannière supérieure contient le nombre cumulé d’enregistrements ingérés et d’enregistrements ayant échoué pour l’ensemble de vos flux de données de diffusion en continu s’exécutant au cours de la période sélectionnée.

La moitié inférieure de la page affiche des informations sur le nombre d’enregistrements reçus, ingérés et en échec, par exécution de flux. Chaque exécution de flux est enregistrée dans une fenêtre horaire.

![dataflow-activity](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Chaque exécution de flux de données individuelle affiche les détails suivants :

* **[!UICONTROL Démarrage]** de l’exécution du flux de données : Heure à laquelle le flux de données a commencé.
* **[!UICONTROL Temps]** de traitement : Le temps nécessaire au traitement du flux de données.
* **[!UICONTROL Enregistrements reçus]** : Nombre total d’enregistrements reçus dans le flux de données d’un connecteur source.
* **[!UICONTROL Enregistrements ingérés]** : Nombre total d’enregistrements ingérés dans  [!DNL Data Lake].
* **[!UICONTROL Échec]** des enregistrements : Nombre d’enregistrements qui n’ont pas été ingérés en  [!DNL Data Lake] raison d’erreurs dans les données.
* **[!UICONTROL Taux d’ingestion]** : Taux de succès des enregistrements ingérés dans  [!DNL Data Lake]. Cette mesure s’applique lorsque [!UICONTROL Ingestion partielle] est activée.
* **[!UICONTROL État]** : Représente l’état dans lequel se trouve le flux de données :   Terminé ou  [!UICONTROL Traitement].  Terminé signifie que tous les enregistrements de l’exécution de flux de données correspondante ont été traités dans la période d’une heure.  Le traitement signifie que l’exécution du flux de données n’est pas encore terminée.

Par défaut, les données affichées contiennent les taux d’ingestion des sept derniers jours. Sélectionnez **[!UICONTROL Les 7 derniers jours]** pour ajuster la période des enregistrements affichés.

![change-time](../../images/tutorials/monitor-streaming/change-time.png)

Une fenêtre contextuelle de calendrier s’affiche, vous permettant d’accéder à d’autres options de périodes d’ingestion. Sélectionnez **[!UICONTROL 30 derniers jours]**, puis **[!UICONTROL Appliquer]**.

![calendar](../../images/tutorials/monitor-streaming/calendar.png)

Pour afficher les détails d’une exécution de flux de données spécifique, y compris ses erreurs, sélectionnez l’heure de début de l’exécution dans la liste.

![select-fail](../../images/tutorials/monitor-streaming/select-fail.png)

La page [!UICONTROL Présentation de l’exécution du flux de données] contient des informations supplémentaires sur votre flux de données, telles que son identifiant d’exécution de flux de données correspondant, le jeu de données cible et l’identifiant de l’organisation IMS.

Une exécution de flux avec des erreurs contient également le panneau [!UICONTROL Erreurs d’exécution de flux de données], qui affiche l’erreur particulière qui a conduit à l’échec de l’exécution, ainsi que le nombre total d’enregistrements qui ont échoué.

![failure](../../images/tutorials/monitor-streaming/failure.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez utilisé l’espace de travail [!UICONTROL Sources] pour surveiller vos flux de données en continu et identifier les erreurs qui ont entraîné l’échec des flux de données. Consultez les documents suivants pour plus d’informations :

* [Présentation des sources](../../home.md)
* [Présentation des flux de données](../../../dataflows/home.md)