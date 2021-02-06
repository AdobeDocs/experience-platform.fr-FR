---
keywords: Experience Platform ; accueil ; rubriques populaires ; comptes de surveillance ; flux de données de surveillance ; flux de données ; sources
description: Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour afficher les flux de données existants à partir de l’espace de travail Sources.
solution: Experience Platform
title: Surveillance des flux de données pour les sources dans l’interface utilisateur
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: f8186e467dc982003c6feb01886ed16d23572955
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 4%

---


# Surveiller les flux de données pour les sources dans l’interface utilisateur

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour afficher les flux de données existants à partir de l&#39;espace de travail [!UICONTROL Sources].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Sources](../../sources/home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
- [Sandbox](../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

## Surveiller les flux de données

Connectez-vous à l&#39;[interface utilisateur Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l&#39;espace de travail [!UICONTROL Sources]. Sélectionnez **[!UICONTROL Flux de données]** de l&#39;en-tête supérieur à la vue des flux de données existants.

![catalogue-flux de données](../assets/ui/monitor-sources/catalog-dataflows.png)

Une liste de flux de données existants s’affiche. Cette page contient une liste de flux de données affichables, y compris des informations sur leur source, leur nom d&#39;utilisateur, leur nombre de flux de données et leur état.

Pour plus d’informations sur les états, voir le tableau suivant :

| État | Description |
| ------ | ----------- |
| Activé | L&#39;état `Enabled` indique qu&#39;un flux de données est principal et qu&#39;il ingère des données selon le calendrier indiqué. |
| Désactivé | L&#39;état `Disabled` indique qu&#39;un flux de données est inactif et n&#39;ingère aucune donnée. |
| En cours de traitement | L&#39;état `Processing` indique qu&#39;un flux de données n&#39;est pas encore principal. Cet état est souvent rencontré immédiatement après la création d’un nouveau flux de données. |
| Erreur | L&#39;état `Error` indique que le processus d&#39;activation d&#39;un flux de données a été perturbé. |

Sélectionnez l’icône d’entonnoir en haut à gauche pour effectuer le tri.

![flux de données-liste](../assets/ui/monitor-sources/dataflows-list.png)

Le panneau de tri s’affiche. Sélectionnez la source à laquelle vous souhaitez accéder dans le menu de défilement et sélectionnez le flux de données dans la liste située à droite. Vous pouvez également sélectionner le bouton ellipses (`...`) pour afficher d’autres options disponibles pour le flux de données sélectionné.

![sort-données-flux](../assets/ui/monitor-sources/dataflows-sort.png)

La page **[!UICONTROL activité de flux de données]** contient des détails sur le nombre d&#39;enregistrements ingérés et ayant échoué, ainsi que des informations sur l&#39;état et le temps de traitement du flux de données. Sélectionnez l&#39;icône de calendrier au-dessus du flux de données pour ajuster la période de vos enregistrements d&#39;assimilation.

![datflow-activité](../assets/ui/monitor-sources/dataflow-activity.png)

Le calendrier vous permet de vue les différentes périodes des enregistrements assimilés. Vous pouvez sélectionner l&#39;une des deux options prédéfinies &quot;[!UICONTROL 7 derniers jours]&quot; ou &quot;[!UICONTROL 30 derniers jours]&quot;. Vous pouvez également définir une période personnalisée à l’aide du calendrier. Sélectionnez la période de votre choix et sélectionnez **[!UICONTROL Appliquer]** pour continuer.

![flow-calendar](../assets/ui/monitor-sources/flow-calendar.png)

Par défaut, l&#39;**[!UICONTROL activité de flux de données]** affiche le panneau **[!UICONTROL Propriétés]** associé au flux de données. Sélectionnez l’exécution de flux à partir de la liste pour afficher les métadonnées associées, y compris des informations sur son ID d’exécution unique.

Sélectionnez **[!UICONTROL début d’exécution de flux de données]** pour accéder à l’**[!UICONTROL aperçu d’exécution de flux de données]**.

![exécute](../assets/ui/monitor-sources/run-metadata.png)

L&#39;**[!UICONTROL aperçu de l&#39;exécution de flux de données]** affiche des informations sur le flux de données, y compris ses métadonnées, son état d&#39;assimilation partielle et le seuil d&#39;erreur attribué. L’en-tête supérieur comprend également un résumé des erreurs. Le **[!UICONTROL résumé d&#39;erreur]** contient l&#39;erreur de niveau supérieur spécifique qui indique à quelle étape le processus d&#39;assimilation a rencontré une erreur.

![dataflow-run-overview](../assets/ui/monitor-sources/dataflow-run-overview.png)

Consultez le tableau suivant pour connaître les erreurs répertoriées dans le **[!UICONTROL résumé de l&#39;erreur]**.

| Erreur | Description |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Une erreur s&#39;est produite lors de la copie des données à partir d&#39;une source. |
| `CONNECTOR-2001-500` | Une erreur s&#39;est produite lors du traitement des données copiées dans [!DNL Platform]. Cette erreur peut concerner l’analyse, la validation ou la transformation. |

La moitié inférieure de l’écran contient des informations sur les erreurs d’exécution **[!UICONTROL de flux de données]**. À partir de là, vous pouvez également vue les fichiers assimilés, prévisualisation et télécharger les diagnostics d&#39;erreur, ou télécharger le manifeste de fichier.

La section **[!UICONTROL Erreurs d&#39;exécution de flux de données]** affiche le code d&#39;erreur, le nombre d&#39;enregistrements ayant échoué et les informations décrivant l&#39;erreur.

Sélectionnez **[!UICONTROL diagnostics d&#39;erreur de Prévisualisation]** pour afficher plus d&#39;informations sur l&#39;erreur d&#39;assimilation.

![Erreurs d’exécution de flux de données](../assets/ui/monitor-sources/dataflow-run-errors.png)

Le panneau **[!UICONTROL prévisualisation des diagnostics d&#39;erreur]** s&#39;affiche. Cet écran affiche des informations spécifiques concernant l&#39;échec d&#39;assimilation, notamment le nom de fichier, le code d&#39;erreur, le nom de la colonne dans laquelle l&#39;erreur s&#39;est produite et une description de l&#39;erreur.

Cette section comprend également une prévisualisation de la colonne qui contient l’erreur.

>[!IMPORTANT]
>
>Pour activer la **[!UICONTROL prévisualisation de diagnostics d&#39;erreur]**, vous devez activer **[!UICONTROL l&#39;assimilation partielle]** et **[!UICONTROL les diagnostics d&#39;erreur]** lors de la configuration d&#39;un flux de données. Cela permettra au système d&#39;analyser tous les enregistrements ingérés pendant l&#39;exécution du flux.

![Prévisualisation-erreur-diagnostics](../assets/ui/monitor-sources/preview-error-diagnostics.png)

Après avoir prévisualisé les erreurs, vous pouvez sélectionner **[!UICONTROL Télécharger]** dans le panneau **[!UICONTROL Data aflow run overview]** pour accéder aux diagnostics d&#39;erreur complets et télécharger le manifeste de fichier. Pour plus d’informations, consultez les documents sur [diagnostics d’erreur](../../ingestion/batch-ingestion/partial.md#retrieve-errors) et [le téléchargement des métadonnées](../../ingestion/batch-ingestion/partial.md#download-metadata).

![Prévisualisation-erreur-diagnostics](../assets/ui/monitor-sources/download.png)

Pour plus d&#39;informations sur la surveillance des flux de données et l&#39;assimilation, consultez le didacticiel [surveillance des flux de données en flux continu](../../ingestion/quality/monitor-data-ingestion.md).

## Étapes suivantes

En suivant ce didacticiel, vous avez accédé à des comptes et flux de données existants à partir de l&#39;espace de travail **[!UICONTROL Sources]**. Les données entrantes peuvent désormais être utilisées par les services [!DNL Platform] en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, voir les documents suivants :

- [Présentation du profil client en temps réel](../../profile/home.md)
- [Présentation de Data Science Workspace](../../data-science-workspace/home.md)
