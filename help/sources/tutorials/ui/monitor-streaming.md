---
keywords: Experience Platform;accueil;rubriques les plus consultées;comptes de contrôle;flux de données de surveillance;flux de données
description: Les connecteurs source d’Adobe Experience Platform permettent d’ingérer des données externes selon un calendrier précis. Ce tutoriel décrit les étapes de surveillance des flux de données en continu à partir de l’espace de travail Sources .
title: Surveillance des flux de données pour les sources de diffusion en continu dans l’interface utilisateur
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 16%

---

# Surveillance des flux de données pour les sources de diffusion en continu dans l’interface utilisateur

Ce tutoriel décrit les étapes de surveillance des flux de données pour les sources de diffusion en continu à l’aide du [!UICONTROL Sources] workspace.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Flux de données](../../../dataflows/home.md) : les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Platform. Les flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, vers [!DNL Identity] et [!DNL Profile], et vers [!DNL Destinations].
   * [Exécutions de flux de données](../../notifications.md): Les exécutions de flux de données sont les tâches planifiées récurrentes en fonction de la configuration de fréquence des flux de données sélectionnés.
* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Surveillance des flux de données pour les sources de diffusion en continu

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Pour afficher les flux de données existants pour les sources en continu, sélectionnez **[!UICONTROL Flux de données]** dans l’en-tête supérieur.

![catalogue](../../images/tutorials/monitor-streaming/catalog.png)

Le [!UICONTROL Flux de données] contient une liste de tous les flux de données existants de votre organisation, y compris des informations sur leurs données source, leur nom de compte et leur état d’exécution.

Sélectionnez le nom du flux de données à afficher.

![flux de données](../../images/tutorials/monitor-streaming/dataflows.png)

Le tableau suivant contient plus d’informations sur les états d’exécution du flux de données :

| État | Description |
| ------ | ----------- |
| Terminé | Le `Completed` Le statut indique que tous les enregistrements de l’exécution de flux de données correspondante ont été traités pendant la période d’une heure. A `Completed` L’état peut toujours contenir des erreurs lors des exécutions du flux de données. |
| Réussite | Le `Success` Le statut indique que tous les enregistrements de l’exécution de flux de données correspondante ont été traités pendant la période d’une heure et qu’aucune erreur n’a été rencontrée au cours de l’exécution de flux de données. |
| En cours de traitement | Le `Processing` Le statut indique qu’un flux de données n’est pas encore principal. Cet état est souvent rencontré immédiatement après la création d’un nouveau flux de données. |
| Erreur | Le `Error` Le statut indique que le processus d’activation d’un flux de données a été interrompu. |
| Aucune exécution | Le `No runs` L’état indique que le flux de données a été créé mais qu’aucune exécution de flux de données n’a été lancée. |

Le [!UICONTROL Activité du flux de données] affiche des informations spécifiques sur votre flux de données en continu. La bannière supérieure contient le nombre cumulé d’enregistrements ingérés et d’enregistrements ayant échoué pour l’ensemble de vos flux de données de diffusion en continu s’exécutant au cours de la période sélectionnée.

![dataflow-activity](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Par défaut, les données affichées contiennent les taux d’ingestion des sept derniers jours. Sélectionner **[!UICONTROL 7 derniers jours]** pour ajuster la période des enregistrements affichés.

Une fenêtre contextuelle de calendrier s’affiche, vous permettant d’accéder à d’autres options de périodes d’ingestion. Vous pouvez configurer la période d’exécution du flux de données pour afficher les exécutions de flux des sept derniers jours ou des 30 derniers jours. Vous pouvez également configurer le calendrier interactif pour définir une période personnalisée de votre choix. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]**.

![calendar](../../images/tutorials/monitor-streaming/calendar.png)

La moitié inférieure de la page affiche des informations sur le nombre d’enregistrements reçus, ingérés et en échec, par exécution de flux. Chaque exécution de flux est enregistrée dans une fenêtre horaire.

![dataflow-run](../../images/tutorials/monitor-streaming/dataflow-run.png)

### Mesures d’exécution de flux de données {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="Enregistrements reçus"
>abstract="La mesure Enregistrements reçus indique le nombre total d’enregistrements reçus dans le flux de données."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="Enregistrements ingérés"
>abstract="La mesure Enregistrements ingérés indique le nombre total d’enregistrements ingérés dans le lac de données."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="Enregistrements échoués"
>abstract="La mesure Échec des enregistrements indique le nombre total d’enregistrements qui n’ont pas été ingérés dans le lac de données en raison d’erreurs dans les données."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="Enregistrements avec avertissements"
>abstract="Les enregistrements avec avertissement indiquent le nombre total d’enregistrements ingérés avec des avertissements de transformation du mappeur. Toutes les erreurs de transformation de mappage sont signalées sous forme d’avertissements et les lignes partiellement ingérées sont considérées comme réussies avec un avertissement."
>text="Learn more in documentation"

Chaque exécution de flux de données individuelle affiche les détails suivants :

* **[!UICONTROL Démarrage de l’exécution du flux de données]**: Heure à laquelle le flux de données a commencé.
* **[!UICONTROL Temps de traitement]**: Le temps nécessaire au traitement du flux de données.
* **[!UICONTROL Enregistrements reçus]**: Nombre total d’enregistrements reçus dans le flux de données d’un connecteur source.
* **[!UICONTROL Enregistrements ingérés]**: Nombre total d’enregistrements ingérés dans [!DNL Data Lake].
* **[!UICONTROL Enregistrements avec avertissement]**: Nombre total d’enregistrements avec des avertissements ingérés. Toutes les erreurs de transformation de mappage sont signalées sous forme d’avertissements et les lignes partiellement ingérées sont marquées comme `success` avec un avertissement. **Remarque**: La prise en charge de l’ingestion d’enregistrements avec des avertissements est uniquement disponible pour les sources en continu.
* **[!UICONTROL Enregistrements en échec]**: Nombre d’enregistrements qui n’ont pas été ingérés dans [!DNL Data Lake] en raison d’erreurs dans les données.
* **[!UICONTROL Taux d’ingestion]**: Taux de succès des enregistrements ingérés dans [!DNL Data Lake]. Cette mesure s’applique lorsque [!UICONTROL Ingestion partielle] est activée.
* **[!UICONTROL État]**: Représente l’état dans lequel se trouve le flux de données : both [!UICONTROL Terminé] ou [!UICONTROL Traitement]. [!UICONTROL Terminé] signifie que tous les enregistrements de l’exécution de flux de données correspondante ont été traités dans la période d’une heure. [!UICONTROL Traitement] signifie que l’exécution du flux de données n’est pas encore terminée.

Le [!UICONTROL Présentation de l’exécution du flux de données] contient des informations supplémentaires sur votre flux de données, telles que l’identifiant d’exécution de flux de données correspondant, le jeu de données cible et l’identifiant d’organisation.

Un flux exécuté avec des erreurs contient également la variable [!UICONTROL Erreurs d’exécution du flux de données] qui affiche l’erreur particulière qui a entraîné l’échec de l’exécution, ainsi que le nombre total d’enregistrements ayant échoué.

![dataflow-run-overview](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### Afficher les enregistrements avec avertissements {#warnings}

[!UICONTROL Enregistrements avec avertissements] affiche la liste des avertissements de transformation du mappeur qui se sont produits au cours de l’exécution du flux. Les lignes partiellement ingérées sont considérées comme réussies et sont accompagnées d’avertissements en cas d’erreur de transformation du mappeur.

Par défaut, toutes les erreurs de transformation du mappeur sont considérées comme des avertissements, sauf si elles sont l’une des suivantes :

* Erreurs de syntaxe
* Références à des attributs qui n’existent pas
* Une incohérence des types de données XDM

Pour afficher les diagnostics d’erreur, sélectionnez **[!UICONTROL Prévisualiser les diagnostics d’erreur]**.

![records-with-warning](../../images/tutorials/monitor-streaming/records-with-warnings.png)

Le [!UICONTROL Aperçu des diagnostics d’erreur] vous permet de prévisualiser jusqu’à 100 erreurs et/ou avertissements concernant l’exécution de votre flux de données. À partir de là, vous pouvez également télécharger le manifeste d’échec d’ingestion pour plus d’informations, en utilisant la variable [!DNL Data Access] API.

![diagnostics](../../images/tutorials/monitor-streaming/diagnostics.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez utilisé avec succès la méthode [!UICONTROL Sources] workspace pour surveiller vos flux de données en continu et identifier les erreurs qui ont entraîné l’échec des flux de données. Pour plus d’informations, consultez les documents suivants :

* [Présentation des sources](../../home.md)
* [Présentation des flux de données](../../../dataflows/home.md)
