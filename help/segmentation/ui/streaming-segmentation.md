---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation par flux;Segmentation;Segmentation Service;service de segmentation;guide de l’interface utilisateur;guide de segmentation
solution: Experience Platform
title: Guide de l’interface utilisateur de la segmentation par flux
topic-legacy: ui guide
description: La segmentation par flux sur Adobe Experience Platform vous permet d’effectuer une segmentation en temps quasi réel tout en vous concentrant sur la richesse des données. Avec la segmentation par flux, la qualification de segment se produit désormais lorsque les données entrent dans Platform, ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées au fur et à mesure que les données sont transmises à Platform, ce qui signifie que l’adhésion au segment sera conservée à jour sans exécuter les tâches de segmentation planifiées.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: b4a04b52ff9a2b7a36fda58d70a2286fea600ff1
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 1%

---

# Segmentation par flux

>[!NOTE]
>
>Le document suivant indique comment utiliser la segmentation par flux à l’aide de l’interface utilisateur. Pour plus d’informations sur l’utilisation de la segmentation par flux à l’aide de l’API, consultez le [guide de l’API de segmentation par flux](../api/streaming-segmentation.md).

La segmentation par flux sur [!DNL Adobe Experience Platform] permet aux clients d’effectuer une segmentation en temps quasi réel tout en se concentrant sur la richesse des données. Avec la segmentation par flux, la qualification de segment se produit maintenant lorsque les données en continu arrivent dans [!DNL Platform], ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées au fur et à mesure que les données sont transmises à [!DNL Platform], ce qui signifie que l’adhésion au segment sera conservée à jour sans exécuter les tâches de segmentation planifiées.

>[!NOTE]
>
>La segmentation par flux ne peut être utilisée que pour évaluer les données diffusées dans Platform. En d’autres termes, les données ingérées par l’ingestion par lots ne seront pas évaluées par la segmentation par flux et seront évaluées avec la tâche de segmentation planifiée de nuit.
>
>En outre, les segments évalués avec la segmentation par flux peuvent dériver entre l’adhésion idéale et l’adhésion réelle si le segment est basé sur un autre segment évalué à l’aide de la segmentation par lots. Si, par exemple, le segment A est basé sur le segment B et le segment B est évalué à l’aide de la segmentation par lots, puisque le segment B n’est mis à jour que toutes les 24 heures, le segment A s’éloigne davantage des données réelles jusqu’à ce qu’il se resynchronise avec la mise à jour du segment B.

## Types de requête de segmentation par flux

>[!NOTE]
>
>Pour que la segmentation par flux fonctionne, vous devez activer la segmentation planifiée pour l’organisation. Pour plus d’informations sur l’activation de la segmentation planifiée, reportez-vous à la [section de la segmentation par flux dans le guide d’utilisation de la segmentation](./overview.md#scheduled-segmentation).

Une requête est automatiquement évaluée avec la segmentation par flux si elle répond à l’un des critères suivants :

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Accès entrant | Toute définition de segment qui fait référence à un seul événement entrant sans restriction temporelle. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Accès entrant dans un intervalle de temps relatif | Toute définition de segment qui fait référence à un seul événement entrant. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Accès entrant avec intervalle de temps | Toute définition de segment qui fait référence à un seul événement entrant avec une fenêtre temporelle. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| Profil uniquement | Toute définition de segment qui ne fait référence qu’à un attribut de profil. |  |
| Accès entrant qui fait référence à un profil | Toute définition de segment qui fait référence à un seul événement entrant, sans restriction temporelle, et à un ou plusieurs attributs de profil. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Accès entrant qui fait référence à un profil dans une fenêtre temporelle relative | Toute définition de segment qui fait référence à un seul événement entrant et à un ou plusieurs attributs de profil. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segment de segments | Toute définition de segment contenant un ou plusieurs segments par lot ou en flux continu. **Remarque :** Si un segment de segments est utilisé, la disqualification du profil se produit  **toutes les 24 heures**. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| Plusieurs événements faisant référence à un profil | Toute définition de segment qui fait référence à plusieurs événements **au cours des dernières 24 heures** et (éventuellement) comporte un ou plusieurs attributs de profil. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Une définition de segment **et** ne sera pas activée pour la segmentation par flux dans les scénarios suivants :

- La définition de segment inclut des segments ou des caractéristiques Adobe Audience Manager (AAM).
- La définition de segment comprend plusieurs entités (requêtes d’entités multiples).

En outre, certaines instructions s’appliquent lors de la segmentation par flux :

| Type de requête | Instruction |
| ---------- | -------- |
| Requête d’événement unique | Il n’existe aucune limite à l’intervalle de recherche en amont. |
| Requête avec historique des événements | <ul><li>L’intervalle de recherche en amont est limité à **un jour**.</li><li>Une condition d’ordre du temps **doit** exister entre les événements.</li><li>Les requêtes comportant au moins un événement annulé sont prises en charge. Cependant, l’événement entier **ne peut pas** être une négation.</li></ul> |

Si une définition de segment est modifiée de sorte qu’elle ne répond plus aux critères de la segmentation par flux, elle passe automatiquement de &quot;Diffusion en continu&quot; à &quot;Lot&quot;.

## Détails des segments de segmentation par flux

Après avoir créé un segment activé dans le flux, vous pouvez afficher les détails de ce segment.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Plus précisément, des détails sur la **[!UICONTROL taille totale de l’audience qualifiée]** s’affichent. La **[!UICONTROL Taille totale de l’audience qualifiée]** indique le nombre total d’audiences qualifiées depuis la dernière exécution de la tâche de segmentation terminée. Si une tâche de segmentation n’a pas été effectuée au cours des dernières 24 heures, le nombre d’audiences sera prélevé dans une estimation à la place.

Un graphique linéaire se trouve en dessous du nombre de segments qui ont été qualifiés et disqualifiés au cours des dernières 24 heures. La liste déroulante peut être ajustée afin d’afficher les dernières 24 heures, la semaine dernière ou les 30 derniers jours.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Vous trouverez des informations supplémentaires sur la dernière évaluation de segment en sélectionnant la bulle d’informations.

![](../images/ui/streaming-segmentation/info-bubble.png)

Pour plus d’informations sur les définitions de segment, consultez la section précédente sur [les détails de la définition de segment](#segment-details).

## Étapes suivantes

Ce guide d’utilisation explique le fonctionnement des définitions de segment activées pour la diffusion en continu sur Adobe Experience Platform et comment surveiller les segments activés pour la diffusion en continu.

Pour en savoir plus sur l’utilisation de l’interface utilisateur de Adobe Experience Platform, consultez le [guide d’utilisation de la segmentation](./overview.md).
