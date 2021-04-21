---
keywords: Experience Platform ; accueil ; rubriques populaires ; comptes de surveillance ; flux de données de surveillance ; flux de données ; destinations
description: Les destinations vous permettent d'activer vos données de Adobe Experience Platform vers d'innombrables partenaires externes. Ce didacticiel fournit des instructions sur la manière de surveiller les flux de données pour vos destinations à l’aide de l’interface utilisateur de l’Experience Platform.
solution: Experience Platform
title: Surveillance des flux de données pour les destinations dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%

---

# Surveiller les flux de données pour les destinations dans l’interface utilisateur

Les destinations vous permettent d&#39;activer vos données de Adobe Experience Platform vers d&#39;innombrables partenaires externes. Ce didacticiel fournit des instructions sur la manière de surveiller les flux de données pour vos destinations à l’aide de l’interface utilisateur de l’Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Destinations](../../destinations/home.md) : Les destinations sont des intégrations préétablies avec les applications couramment utilisées qui permettent l’activation transparente des données de la plate-forme pour les campagnes marketing inter-canaux, les campagnes par courriel, la publicité ciblée et de nombreux autres cas d’utilisation.
- [Sandbox](../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

## Surveiller les flux de données

Dans l&#39;espace de travail **[!UICONTROL Destinations]** de l&#39;interface utilisateur de la plate-forme, accédez à l&#39;onglet **[!UICONTROL Parcourir]** et sélectionnez le nom d&#39;une destination que vous souhaitez vue.

![](../assets/ui/monitor-destinations/select-destination.png)

Une liste de flux de données existants s’affiche. Cette page contient une liste de flux de données affichables, y compris des informations sur leur destination, leur nom d&#39;utilisateur, le nombre de flux de données et leur état.

Pour plus d’informations sur les états, voir le tableau suivant :

| État | Description |
| ------ | ----------- |
| Activé | L&#39;état `Enabled` indique qu&#39;un flux de données est principal et qu&#39;il ingère des données selon le calendrier indiqué. |
| Désactivé | L&#39;état `Disabled` indique qu&#39;un flux de données est inactif et n&#39;ingère aucune donnée. |
| En cours de traitement | L&#39;état `Processing` indique qu&#39;un flux de données n&#39;est pas encore principal. Cet état est souvent rencontré immédiatement après la création d’un nouveau flux de données. |
| Erreur | L&#39;état `Error` indique que le processus d&#39;activation d&#39;un flux de données a été perturbé. |

## [!UICONTROL Exécutions de flux de données]

L&#39;onglet [!UICONTROL Flux de données] fournit des données de mesure sur vos flux de données s&#39;exécutant vers des destinations de lot. Une liste d’exécutions individuelles et de leurs mesures particulières s’affiche, ainsi que les totaux suivants pour les enregistrements de profil :

- **[!UICONTROL Enregistrements de profil activés]** : Nombre total d&#39;enregistrements de profil créés ou mis à jour pour l&#39;activation.
- **[!UICONTROL Enregistrements de profil ignorés]** : Nombre total d’enregistrements de profil qui sont ignorés pour activation en fonction des sorties de profil ou des attributs manquants.

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>Les exécutions de flux de données sont générées en fonction de la fréquence de planification du flux de données de destination. Une exécution de flux de données distincte est effectuée pour chaque stratégie de fusion appliquée à un segment.

Pour vue les détails d&#39;une exécution de flux de données particulière, sélectionnez l&#39;heure de début de l&#39;exécution dans la liste. La page Détails d&#39;une série de flux de données contient des informations supplémentaires, telles que la taille des données traitées et la liste de toute erreur survenue avec des détails pour les diagnostics d&#39;erreur.

![](../assets/ui/monitor-destinations/dataflow.png)
