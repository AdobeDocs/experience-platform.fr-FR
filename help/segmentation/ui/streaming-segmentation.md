---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentation par flux
topic: ui guide
translation-type: tm+mt
source-git-commit: 2adadad855edd01436a6961cc9be3e58e6483732
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 2%

---


# Segmentation par flux

>[!NOTE]
>
>Le document suivant indique comment utiliser la segmentation en flux continu à l’aide de l’interface utilisateur. Pour plus d’informations sur l’utilisation de la segmentation en flux continu à l’aide de l’API, consultez le guide [de l’API de segmentation en](../api/streaming-segmentation.md)flux continu.

La segmentation en flux continu sur [!DNL Adobe Experience Platform] permet aux clients d’effectuer la segmentation en temps quasi réel tout en se concentrant sur la richesse des données. Avec la segmentation en flux continu, la qualification de segment se produit désormais lorsque les données entrent en [!DNL Platform]jeu, ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation. With this capability, most segment rules can now be evaluated as the data is passed into [!DNL Platform], meaning segment membership will be kept up-to-date without running scheduled segmentation jobs.

## Types de requête de segmentation en flux continu

>[!NOTE]
>
>Pour que la segmentation en flux continu fonctionne, vous devez activer la segmentation planifiée pour l’entreprise. For details on enabling scheduled segmentation, please refer to [the streaming segmentation section in the Segmentation user guide](./overview.md#scheduled-segmentation).

Une requête sera automatiquement évaluée avec la segmentation en flux continu si elle répond à l’un des critères suivants :

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Accès entrant | Toute définition de segment faisant référence à un seul événement entrant sans restriction de temps. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Accès entrant dans une fenêtre de temps relative | Toute définition de segment faisant référence à un seul événement entrant **au cours des sept derniers jours**. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Profil uniquement | Toute définition de segment faisant référence uniquement à un attribut de profil. |  |
| Accès entrant faisant référence à un profil | Toute définition de segment faisant référence à un seul événement entrant, sans restriction de temps, et à un ou plusieurs attributs de profil. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Accès entrant faisant référence à un profil dans une fenêtre de temps relative | Toute définition de segment faisant référence à un seul événement entrant et à un ou plusieurs attributs de profil, **au cours des sept derniers jours**. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Plusieurs événements faisant référence à un profil | Toute définition de segment qui fait référence à plusieurs événements **au cours des dernières 24 heures** et (éventuellement) comporte un ou plusieurs attributs de profil. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

La section suivante liste des exemples de définition de segment qui **ne seront pas** activés pour la segmentation en flux continu.

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Accès entrant dans une fenêtre de temps relative | Si la définition de segment fait référence à un événement entrant **qui ne se trouve pas** dans la **dernière période** de sept jours. Par exemple, au cours des deux **dernières semaines**. | ![](../images/ui/streaming-segmentation/relative-hit-failure.png) |
| Accès entrant faisant référence à un profil dans une fenêtre relative | Les options suivantes **ne prennent pas** en charge la segmentation en flux continu :<ul><li>Événement entrant **non** compris dans la **dernière période** de sept jours.</li><li>Définition de segment qui inclut [!DNL Adobe Audience Manager (AAM)] des segments ou des caractéristiques.</li></ul> | ![](../images/ui/streaming-segmentation/profile-relative-failure.png) |
| Plusieurs événements faisant référence à un profil | Les options suivantes **ne prennent pas** en charge la segmentation en flux continu :<ul><li>Événement qui **ne se produit pas** au cours **des dernières 24 heures**.</li><li>Définition de segment qui comprend des segments ou des caractéristiques Adobe Audience Manager (AAM).</li></ul> | ![](../images/ui/streaming-segmentation/event-history-failure.png) |
| Requêtes multientité | Les requêtes multientités **ne sont pas** prises en charge dans leur ensemble par la segmentation en flux continu. |  |

En outre, certaines directives s’appliquent lors de la segmentation en flux continu :

| Type de requête | Ligne directrice |
| ---------- | -------- |
| Requête événement unique | La fenêtre de rétrospective est limitée à **sept jours**. |
| Requête avec historique des événements | <ul><li>La fenêtre de rétrospective est limitée à **un jour**.</li><li>Une condition d’ordre temporel strict **doit** exister entre les événements.</li><li>Seules les commandes de temps simples (avant et après) entre les événements sont autorisées.</li><li>Les événements individuels **ne peuvent** être annulés. Cependant, toute la requête **peut** être annulée.</li></ul> |

## Détails du segment de segmentation en flux continu

Après avoir créé un segment compatible avec la diffusion en continu, vous pouvez en vue les détails.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Plus précisément, des détails sur la taille **** totale des audiences qualifiées sont affichés. Si une tâche a été exécutée au cours des 24 dernières heures, la taille **** totale de l’audience qualifiée de la tâche s’affiche, en plus d’un graphique linéaire pour l’audience ajoutée. Sinon, la taille **[!UICONTROL estimée de l’audience]** totale s’affiche, en plus d’une ligne de tendance de visualisation.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Pour plus d’informations sur l’évaluation du dernier segment, sélectionnez la bulle d’informations.

![](../images/ui/streaming-segmentation/info-bubble.png)

Pour plus d&#39;informations sur les définitions de segment, veuillez lire la section précédente sur les détails [de la définition de](#segment-details)segment.

## Démo vidéo de segmentation en flux continu

La vidéo suivante est destinée à vous aider à comprendre la segmentation en flux continu. Il présente un exemple d’expérience client suivie d’une visite rapide des principales fonctionnalités de l’ [!DNL Platform] interface.

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## Étapes suivantes

Ce guide d’utilisateur explique comment fonctionnent les définitions de segment activées pour la diffusion en continu sur Adobe Experience Platform et comment surveiller les segments activés pour la diffusion en continu.

Pour en savoir plus sur l’utilisation de l’interface utilisateur de Adobe Experience Platform, consultez le guide [d’utilisation de la](./overview.md)segmentation.