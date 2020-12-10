---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;destinations
description: Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour afficher les flux de données existants à partir de l’espace de travail Sources.
solution: Experience Platform
title: Surveiller les flux de données
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 791ad61f2f28da03ef3e5cb5efdd89154e9b1a0b
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 5%

---


# Surveiller les flux de données pour les destinations dans l’interface utilisateur

Les destinations vous permettent d&#39;activer vos données de Adobe Experience Platform vers d&#39;innombrables partenaires externes. Ce didacticiel fournit des instructions sur la manière de surveiller les flux de données pour vos destinations à l’aide de l’interface utilisateur de l’Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Destinations](../../destinations/home.md): Les destinations sont des intégrations préétablies avec les applications couramment utilisées qui permettent l’activation transparente des données de la plate-forme pour les campagnes marketing inter-canaux, les campagnes par courriel, la publicité ciblée et de nombreux autres cas d’utilisation.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

## Surveiller les flux de données

Dans l’espace de travail **[!UICONTROL Destinations]** de l’interface utilisateur de la plate-forme, accédez à l’onglet **[!UICONTROL Parcourir]** et sélectionnez le nom d’une destination à vue.

![](../assets/ui/monitor-destinations/select-destination.png)

Une liste de flux de données existants s’affiche. Cette page contient une liste de flux de données affichables, y compris des informations sur leur destination, leur nom d&#39;utilisateur, le nombre de flux de données et leur état.

Pour plus d’informations sur les états, voir le tableau suivant :

| État | Description |
| ------ | ----------- |
| Activé | L’ `Enabled` état indique qu’un flux de données est principal et qu’il ingère des données selon le calendrier prévu. |
| Désactivé | L’ `Disabled` état indique qu’un flux de données est inactif et n’ingère aucune donnée. |
| En cours de traitement | L’ `Processing` état indique qu’un flux de données n’est pas encore principal. Cet état est souvent rencontré immédiatement après la création d’un nouveau flux de données. |
| Erreur | L’ `Error` état indique que le processus d’activation d’un flux de données a été interrompu. |

## [!UICONTROL Exécutions de flux de données]

L’onglet Exécutions [!UICONTROL de flux de] données fournit des données de mesure sur vos exécutions de flux de données vers des destinations de lot. Une liste d’exécutions individuelles et de leurs mesures particulières s’affiche, ainsi que les totaux suivants pour les enregistrements de profil :

- **[!UICONTROL Enregistrements de profil activés]**: Nombre total d&#39;enregistrements de profil créés ou mis à jour pour l&#39;activation.
- **[!UICONTROL Enregistrements de profil ignorés]**:  Nombre total d’enregistrements de profil qui sont ignorés pour activation en fonction des sorties de profil ou des attributs manquants.

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>Les exécutions de flux de données sont générées en fonction de la fréquence de planification du flux de données de destination. Une exécution de flux de données distincte est effectuée pour chaque stratégie de fusion appliquée à un segment.

Pour vue les détails d&#39;une exécution de flux de données particulière, sélectionnez l&#39;heure de début de l&#39;exécution dans la liste. La page Détails d&#39;une série de flux de données contient des informations supplémentaires, telles que la taille des données traitées et la liste de toute erreur survenue avec des détails pour les diagnostics d&#39;erreur.

![](../assets/ui/monitor-destinations/dataflow.png)