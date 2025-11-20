---
keywords: Experience Platform;accueil;rubriques les plus consultées;surveiller les comptes;surveiller les flux de données;flux de données
description: Les connecteurs Source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour surveiller les flux de données en continu à partir de l’espace de travail Sources.
title: Surveillance des flux de données pour les sources de diffusion en continu dans l’interface utilisateur
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 16%

---

# Surveillance des flux de données pour les sources de diffusion en continu dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour surveiller les flux de données des sources en flux continu à l’aide de l’espace de travail [!UICONTROL Sources].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Flux de données](../../../dataflows/home.md) : les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Experience Platform. Les flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, vers [!DNL Identity] et [!DNL Profile], et vers [!DNL Destinations].
   * [Exécutions de flux de données](../../notifications.md) : les exécutions de flux de données sont les tâches planifiées récurrentes en fonction de la configuration de la fréquence des flux de données sélectionnés.
* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Surveillance des flux de données pour les sources de diffusion en continu

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalog] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Pour afficher les flux de données existants pour les sources en flux continu, sélectionnez **[!UICONTROL Dataflows]** dans l’en-tête supérieur.

![catalogue](../../images/tutorials/monitor-streaming/catalog.png)

La page [!UICONTROL Dataflows] contient une liste de tous les flux de données existants de votre organisation, y compris des informations sur leurs données sources, le nom du compte et le statut d’exécution du flux de données.

Sélectionnez le nom du flux de données à afficher.

![&#x200B; flux de données &#x200B;](../../images/tutorials/monitor-streaming/dataflows.png)

Le tableau suivant contient des informations supplémentaires sur les statuts d’exécution des flux de données :

| État | Description |
| ------ | ----------- |
| Terminé | Le statut `Completed` indique que tous les enregistrements de l’exécution de flux de données correspondante ont été traités au cours de la période d’une heure. Un statut de `Completed` peut toujours contenir des erreurs dans les exécutions de flux de données. |
| Réussite | Le statut `Success` indique que tous les enregistrements pour l’exécution de flux de données correspondante ont été traités au cours de la période d’une heure et qu’aucune erreur n’a été rencontrée au cours de l’exécution du flux de données. |
| En cours de traitement | Le statut `Processing` indique qu’un flux de données n’est pas encore actif. Ce statut se rencontre souvent immédiatement après la création d’un nouveau flux de données. |
| Erreur | Le statut `Error` indique que le processus d’activation d’un flux de données a été interrompu. |
| Aucune exécution | Le statut `No runs` indique que le flux de données a été créé, mais qu’aucune exécution de flux de données n’a été démarrée. |

La page [!UICONTROL Dataflow Activity] affiche des informations spécifiques sur votre flux de données de diffusion en continu. La bannière supérieure contient le nombre cumulé d’enregistrements ingérés et d’enregistrements ayant échoué pour toutes les exécutions de flux de données de diffusion en continu dans la période sélectionnée.

![dataflow-activity](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Par défaut, les données affichées contiennent les taux d’ingestion des sept derniers jours. Sélectionnez **[!UICONTROL Last 7 days]** pour ajuster la période des enregistrements affichés.

Une fenêtre pop-up de calendrier s’affiche, vous offrant des options pour d’autres périodes d’ingestion. Vous pouvez configurer la période d’exécution du flux de données pour afficher les exécutions de flux des sept jours précédents ou des 30 derniers jours. Vous pouvez également configurer le calendrier interactif pour définir une période personnalisée de votre choix. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Apply]**.

![calendar](../../images/tutorials/monitor-streaming/calendar.png)

La moitié inférieure de la page affiche des informations sur le nombre d’enregistrements reçus, ingérés et ayant échoué, par exécution de flux. Chaque exécution de flux est enregistrée dans une fenêtre horaire.

![dataflow-run](../../images/tutorials/monitor-streaming/dataflow-run.png)

### Mesures d’exécution de flux de données {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="Enregistrements reçus"
>abstract="La mesure Enregistrements reçus indique le nombre total d&#39;enregistrements reçus dans le flux de données."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="Enregistrements ingérés"
>abstract="La mesure Enregistrements ingérés indique le nombre total d&#39;enregistrements ingérés dans le lac de données."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="Enregistrements ayant échoué"
>abstract="La mesure Échec des enregistrements indique le nombre total d&#39;enregistrements qui n&#39;ont pas été ingérés dans le lac de données en raison d&#39;erreurs dans les données."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="Enregistrements avec avertissements"
>abstract="Les Enregistrements avec avertissements indiquent le nombre total d&#39;enregistrements ingérés avec des avertissements de transformation du mappeur. Toutes les erreurs de transformation du mappeur sont signalées comme avertissements et les lignes partiellement ingérées sont considérées comme réussies, avec un avertissement."
>text="Learn more in documentation"

Chaque exécution de flux de données affiche les détails suivants :

* **[!UICONTROL Dataflow run start]** : heure à laquelle l’exécution du flux de données a démarré.
* **[!UICONTROL Processing time]** : durée de traitement du flux de données.
* **[!UICONTROL Records Received]** : nombre total d’enregistrements reçus dans le flux de données d’un connecteur source.
* **[!UICONTROL Records Ingested]** : nombre total d’enregistrements ingérés dans [!DNL Data Lake].
* **[!UICONTROL Records with Warnings]** : nombre total d’enregistrements avec avertissements ingérés. Toutes les erreurs de transformation du mappeur sont signalées comme avertissements et les lignes partiellement ingérées sont étiquetées comme `success` avec un avertissement. **Remarque** : la prise en charge de l’ingestion d’enregistrements avec des avertissements n’est disponible que pour les sources en flux continu.
* **[!UICONTROL Records Failed]** : nombre d’enregistrements qui n’ont pas été ingérés dans [!DNL Data Lake] en raison d’erreurs dans les données.
* **[!UICONTROL Ingestion Rate]** : taux de succès des enregistrements ingérés dans [!DNL Data Lake]. Cette mesure s’applique lorsque [!UICONTROL Partial Ingestion] est activé.
* **[!UICONTROL Status]** : représente le statut du flux de données : [!UICONTROL Completed] ou [!UICONTROL Processing]. [!UICONTROL Completed] signifie que tous les enregistrements pour l’exécution du flux de données correspondant ont été traités dans la période d’une heure. [!UICONTROL Processing] signifie que l’exécution du flux de données n’est pas encore terminée.

La page [!UICONTROL Dataflow run overview] contient des informations supplémentaires sur votre flux de données, telles que l’identifiant d’exécution du flux de données correspondant, le jeu de données cible et l’identifiant d’organisation.

Une exécution de flux avec des erreurs contient également le panneau [!UICONTROL Dataflow run errors], qui affiche l’erreur particulière qui a conduit à l’échec de l’exécution, ainsi que le nombre total d’enregistrements qui ont échoué.

![dataflow-run-overview](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### Afficher les enregistrements avec des avertissements {#warnings}

[!UICONTROL Records with warnings] affiche une liste des avertissements de transformation du mappeur qui se sont produits lors de l’exécution de votre flux. Les lignes partiellement ingérées sont considérées comme réussies et sont accompagnées d’avertissements si des erreurs de transformation du mappeur sont détectées.

Par défaut, toutes les erreurs de transformation du mappeur sont considérées comme des avertissements, sauf si elles sont l’une des suivantes :

* Erreurs de syntaxe
* Références à des attributs qui n’existent pas
* Incompatibilité des types de données XDM

Pour afficher les diagnostics d’erreur, sélectionnez **[!UICONTROL Preview error diagnostics]**.

![enregistrements avec avertissements](../../images/tutorials/monitor-streaming/records-with-warnings.png)

La fenêtre [!UICONTROL Error diagnostics preview] vous permet de prévisualiser jusqu’à 100 erreurs et/ou avertissements concernant l’exécution du flux de données. À partir de là, vous pouvez également télécharger le manifeste d’échec d’ingestion pour plus d’informations, à l’aide de l’API [!DNL Data Access].

![diagnostics](../../images/tutorials/monitor-streaming/diagnostics.png)

## Étapes suivantes

En suivant attentivement ce tutoriel, vous avez utilisé l’espace de travail [!UICONTROL Sources] pour surveiller vos flux de données de diffusion en continu et identifier les erreurs qui ont conduit à des flux de données en échec. Pour plus d’informations, consultez les documents suivants :

* [Présentation des sources](../../home.md)
* [Présentation des flux de données](../../../dataflows/home.md)
