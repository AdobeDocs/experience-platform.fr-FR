---
keywords: Experience Platform;accueil;rubriques les plus consultées;comptes de contrôle;flux de données de surveillance;flux de données;sources
description: Ce tutoriel décrit les étapes à suivre pour surveiller votre flux de données à l’aide de la vue de surveillance agrégée et de la surveillance inter-services.
solution: Experience Platform
title: Surveillance des flux de données pour les sources dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: ed88ebe7822f60ace2babd7d5a04d2d92d83cf49
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 17%

---

# Surveillance des flux de données pour les sources dans l’interface utilisateur

>[!IMPORTANT]
>
>Sources de diffusion en continu, telles que [Source de l’API HTTP](../../sources/connectors/streaming/http.md) ne sont actuellement pas pris en charge par le tableau de bord de surveillance. Actuellement, vous ne pouvez utiliser que le tableau de bord pour surveiller les sources de lots.

Dans Adobe Experience Platform, les données sont ingérées à partir d’une grande variété de sources, analysées dans Experience Platform et activées vers un grand nombre de destinations. En offrant de la transparence au niveau des flux de données, Platform facilite le processus de suivi de ce flux de données potentiellement non linéaire.

Le tableau de bord de surveillance vous fournit une représentation visuelle du parcours d’un flux de données. Vous pouvez utiliser une vue de surveillance agrégée et naviguer verticalement du niveau source à un flux de données et à une exécution de flux de données, ce qui vous permet d’afficher les mesures correspondantes qui contribuent au succès ou à l’échec d’un flux de données. Vous pouvez également utiliser la capacité de surveillance inter-services du tableau de bord de surveillance pour surveiller le parcours d’un flux de données à partir d’une source, à [!DNL Identity Service]et à [!DNL Profile].

Ce tutoriel décrit les étapes à suivre pour surveiller votre flux de données à l’aide de la vue de surveillance agrégée et de la surveillance inter-services.

## Prise en main {#getting-started}

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Flux de données](../home.md) : les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Platform. Les flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, vers [!DNL Identity] et [!DNL Profile], et vers [!DNL Destinations].
   * [Exécutions de flux de données](../../sources/notifications.md): Les exécutions de flux de données sont les tâches planifiées récurrentes en fonction de la configuration de fréquence des flux de données sélectionnés.
* [Sources](../../sources/home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Service d’identités](../../identity-service/home.md) : obtenez une meilleure compréhension des clients individuels et de leurs comportements en reliant les identités entre les appareils et les systèmes.
* [Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Sandboxes](../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Vue de surveillance agrégée {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Ingestion source"
>abstract="La vue Ingestion source contient des informations sur l’état et les mesures de l’activité de données dans le service de lac de données, y compris les enregistrements ingérés et les enregistrements ayant échoué. Consultez le guide de définition des mesures pour en savoir plus sur les mesures et les graphiques."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Détails de l’exécution du flux de données"
>abstract="Le traitement des sources contient des informations sur l’état de l’activité de données et des mesures dans le service de lac de données, y compris les enregistrements ingérés et les enregistrements ayant échoué. Consultez le guide de définition des mesures pour en savoir plus sur les mesures et les graphiques."
>text="Learn more in documentation"

Dans le [Interface utilisateur de Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Surveillance]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Surveillance] tableau de bord. Le [!UICONTROL Surveillance] Le tableau de bord contient des mesures et des informations sur tous les flux de données de sources, y compris des informations sur l’intégrité du trafic de données d’une source à [!DNL Identity Service]et à [!DNL Profile].

Au centre du tableau de bord se trouve l’objet [!UICONTROL Ingestion source] qui contient des mesures et des graphiques qui affichent des données sur les enregistrements ingérés et en échec.

![monitoring-dashboard](../assets/ui/monitor-sources/monitoring-dashboard.png)

Par défaut, les données affichées contiennent les taux d’ingestion des dernières 24 heures. Sélectionner **[!UICONTROL 24 dernières heures]** pour ajuster la période des enregistrements affichés.

![change-date](../assets/ui/monitor-sources/change-date.png)

Une fenêtre contextuelle de calendrier s’affiche, vous permettant d’accéder à d’autres options de périodes d’ingestion. Sélectionner **[!UICONTROL 30 derniers jours]** puis sélectionnez **[!UICONTROL Appliquer]**

![réglage-période](../assets/ui/monitor-sources/adjust-timeframe.png)

Les graphiques sont activés par défaut et vous pouvez les désactiver pour développer la liste des sources ci-dessous. Sélectionnez la **[!UICONTROL Mesures et graphiques]** pour désactiver les graphiques.

![mesures-et-graphiques](../assets/ui/monitor-sources/metrics-graphs.png)

| Ingestion source | Description |
| ---------------- | ----------- |
| [!UICONTROL Enregistrements ingérés ] | Nombre total d’enregistrements ingérés. |
| [!UICONTROL Enregistrements échoués] | Nombre total d’enregistrements qui n’ont pas été ingérés en raison d’erreurs dans les données. |
| [!UICONTROL Total des flux de données ayant échoué] | Le nombre total de flux de données avec un `failed` statut. |

La liste d’ingestion source affiche toutes les sources qui contiennent au moins un compte existant. La liste inclut également des informations sur le taux d’ingestion de chaque source, le nombre d’enregistrements ayant échoué et le nombre total de flux de données ayant échoué en fonction de la période que vous avez appliquée.

![source-ingestion](../assets/ui/monitor-sources/source-ingestion.png)

Pour trier la liste des sources, sélectionnez **[!UICONTROL Mes sources]** puis sélectionnez votre catégorie de choix dans le menu déroulant. Par exemple, pour vous concentrer sur le stockage dans le cloud, sélectionnez  **[!UICONTROL Stockage dans le cloud]**

![tri-par-catégorie](../assets/ui/monitor-sources/sort-by-category.png)

Pour afficher tous les flux de données existants dans toutes les sources, sélectionnez **[!UICONTROL Flux de données]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

Vous pouvez également entrer une source dans la barre de recherche pour isoler une source unique. Une fois votre source identifiée, sélectionnez l’icône de filtre ![filter](../assets/ui/monitor-sources/filter.png) en regard de pour afficher la liste de ses principaux flux de données.

![recherche](../assets/ui/monitor-sources/search.png)

Une liste de flux de données s’affiche. Pour réduire la liste et vous concentrer sur les flux de données contenant des erreurs, sélectionnez **[!UICONTROL Afficher uniquement les échecs]**.

![show-failure-only](../assets/ui/monitor-sources/show-failures-only.png)

Localisez le flux de données à surveiller, puis sélectionnez l’icône de filtre. ![filter](../assets/ui/monitor-sources/filter.png) à côté de lui, pour afficher plus d’informations sur son état d’exécution.

![dataflow](../assets/ui/monitor-sources/dataflow.png)

La page d’exécution du flux de données affiche des informations sur la date de début de l’exécution de votre flux de données, la taille des données, l’état, ainsi que sa durée de traitement. Icône Sélectionner le filtre ![filter](../assets/ui/monitor-sources/filter.png) en regard de l’heure de début d’exécution du flux de données pour afficher les détails d’exécution du flux de données.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

Le [!UICONTROL Détails de l’exécution du flux de données] affiche des informations sur les métadonnées du flux de données, l’état d’ingestion partiel et le résumé de l’erreur. Le résumé de l’erreur contient l’erreur de niveau supérieur spécifique qui indique à quelle étape le processus d’ingestion a rencontré une erreur.

Faites défiler l’écran vers le bas pour afficher des informations plus spécifiques sur l’erreur qui s’est produite.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

Le [!UICONTROL Erreurs d’exécution du flux de données] panneau affiche le code d’erreur et d’erreur spécifique qui a entraîné l’échec de l’ingestion du flux de données. Dans ce scénario, une erreur de transformation du mappeur s’est produite, entraînant l’échec de 24 enregistrements.

Sélectionner **[!UICONTROL Fichiers]** pour plus d’informations.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

Le [!UICONTROL Fichiers] contient des informations sur le nom et le chemin du fichier.

Pour une représentation plus granulaire de l’erreur, sélectionnez **[!UICONTROL Prévisualiser les diagnostics d’erreur]**.

![files](../assets/ui/monitor-sources/files.png)

Le [!UICONTROL Aperçu des diagnostics d’erreur] s’affiche, affichant un aperçu des erreurs jusqu’à 100 dans le flux de données. Vous pouvez sélectionner **[!UICONTROL Télécharger]** pour récupérer une commande curl, qui permet ensuite de télécharger les diagnostics d’erreur.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Fermer]**

![error-diagnostics](../assets/ui/monitor-sources/error-diagnostics.png)

Vous pouvez utiliser le système de chemin de navigation dans l’en-tête supérieur pour revenir au [!UICONTROL Surveillance] tableau de bord. Sélectionner **[!UICONTROL Exécutez le démarrage : 2/14/2021, 21 h 47]** pour revenir à la page précédente, puis sélectionnez **[!UICONTROL Flux de données : Démonstration de l’ingestion des données de fidélité - Échec]** pour revenir à la page des flux de données.

![chemin de navigation](../assets/ui/monitor-sources/breadcrumbs.png)

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez suivi avec succès le flux de données d’ingestion au niveau de la source à l’aide de la variable **[!UICONTROL Surveillance]** tableau de bord. Vous avez également identifié des erreurs qui ont contribué à l’échec des flux de données pendant le processus d’ingestion. Consultez les documents suivants pour plus d’informations :

* [Surveillance des identités dans les flux de données](./monitor-identities.md)
* [Surveillance des profils dans les flux de données](./monitor-profiles.md)
