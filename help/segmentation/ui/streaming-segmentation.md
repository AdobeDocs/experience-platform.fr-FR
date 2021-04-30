---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation en flux continu ; Segmentation ; Service de segmentation ; service de segmentation ; guide d'interface ;
solution: Experience Platform
title: Guide de l’interface utilisateur de segmentation en flux continu
topic-legacy: ui guide
description: La segmentation en flux continu sur Adobe Experience Platform vous permet d’effectuer la segmentation en temps quasi réel tout en vous concentrant sur la richesse des données. Avec la segmentation en flux continu, la qualification de segment se produit désormais lorsque les données arrivent dans la plate-forme, ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées lorsque les données sont transmises à la plate-forme, ce qui signifie que l’appartenance à un segment est tenue à jour sans exécuter les tâches de segmentation planifiées.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
translation-type: tm+mt
source-git-commit: b4a04b52ff9a2b7a36fda58d70a2286fea600ff1
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 1%

---

# Segmentation par flux

>[!NOTE]
>
>Le document suivant indique comment utiliser la segmentation en flux continu à l’aide de l’interface utilisateur. Pour plus d’informations sur l’utilisation de la segmentation en flux continu à l’aide de l’API, consultez le [guide de l’API de segmentation en flux continu](../api/streaming-segmentation.md).

La segmentation en flux continu sur [!DNL Adobe Experience Platform] permet aux clients d’effectuer la segmentation en temps quasi réel tout en se concentrant sur la richesse des données. Avec la segmentation en flux continu, la qualification de segment se produit maintenant lorsque les données en flux continu atterrissent dans [!DNL Platform], ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées lorsque les données sont transmises à [!DNL Platform], ce qui signifie que l’appartenance à un segment est tenue à jour sans exécuter de tâches de segmentation planifiées.

>[!NOTE]
>
>La segmentation en flux continu ne peut être utilisée que pour évaluer les données diffusées en continu dans la plate-forme. En d’autres termes, les données ingérées par assimilation par lot ne seront pas évaluées par la segmentation en flux continu et seront évaluées avec la tâche de segment programmée de nuit.
>
>De plus, les segments évalués avec la segmentation en flux continu peuvent dériver entre l’adhésion idéale et l’adhésion réelle si le segment est basé sur un autre segment qui est évalué à l’aide de la segmentation par lot. Par exemple, si le segment A est basé sur le segment B et que le segment B est évalué à l’aide de la segmentation par lot, puisque le segment B n’est mis à jour que toutes les 24 heures, le segment A s’éloigne davantage des données réelles jusqu’à ce qu’il se resynchronise avec la mise à jour du segment B.

## Types de requête de segmentation en flux continu

>[!NOTE]
>
>Pour que la segmentation en flux continu fonctionne, vous devez activer la segmentation planifiée pour l’entreprise. Pour plus d’informations sur l’activation de la segmentation planifiée, reportez-vous à la section [de la segmentation en flux continu du guide de l’utilisateur Segmentation](./overview.md#scheduled-segmentation).

Une requête sera automatiquement évaluée avec la segmentation en flux continu si elle répond à l’un des critères suivants :

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Accès entrant | Toute définition de segment faisant référence à un seul événement entrant sans restriction de temps. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Accès entrant dans une fenêtre de temps relative | Toute définition de segment faisant référence à un seul événement entrant. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Accès entrant avec une fenêtre de temps | Toute définition de segment faisant référence à un seul événement entrant avec une fenêtre de temps. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| Profil uniquement | Toute définition de segment faisant référence uniquement à un attribut de profil. |  |
| Accès entrant faisant référence à un profil | Toute définition de segment faisant référence à un seul événement entrant, sans restriction de temps, et à un ou plusieurs attributs de profil. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Accès entrant faisant référence à un profil dans une fenêtre de temps relative | Toute définition de segment faisant référence à un seul événement entrant et à un ou plusieurs attributs de profil. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segment de segments | Toute définition de segment contenant un ou plusieurs segments par lot ou en flux continu. **Remarque :** si un segment de segments est utilisé, la disqualification du profil se produit  **toutes les 24 heures**. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| Plusieurs événements faisant référence à un profil | Toute définition de segment faisant référence à plusieurs événements **au cours des dernières 24 heures** et (éventuellement) comporte un ou plusieurs attributs de profil. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Une définition de segment **ne sera pas** activée pour la segmentation en flux continu dans les scénarios suivants :

- La définition de segment comprend des segments ou des caractéristiques Adobe Audience Manager (AAM).
- La définition de segment comprend plusieurs entités (requêtes multientités).

En outre, certaines directives s’appliquent lors de la segmentation en flux continu :

| Type de requête | Instruction |
| ---------- | -------- |
| Requête événement unique | Il n&#39;y a aucune limite à la fenêtre de recherche en amont. |
| Requête avec historique des événements | <ul><li>La fenêtre de recherche est limitée à **un jour**.</li><li>Une condition d&#39;ordre temporel **doit** stricte existe entre les événements.</li><li>Les requêtes comportant au moins un événement négatif sont prises en charge. Cependant, le événement entier **ne peut pas** être une négation.</li></ul> |

Si une définition de segment est modifiée de sorte qu’elle ne réponde plus aux critères de la segmentation en flux continu, elle passe automatiquement de &quot;Diffusion en flux continu&quot; à &quot;Lot&quot;.

## Détails du segment de segmentation en flux continu

Après avoir créé un segment compatible avec la diffusion en continu, vous pouvez en vue les détails.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Plus précisément, des détails sur la **[!UICONTROL taille totale de l&#39;audience qualifiée]** s&#39;affichent. La **[!UICONTROL taille totale de l&#39;audience qualifiée]** indique le nombre total d&#39;audiences qualifiées de la dernière exécution de la tâche de segment terminée. Si une tâche de segmentation n&#39;a pas été effectuée au cours des 24 dernières heures, le nombre d&#39;audiences est pris à partir d&#39;une estimation.

Un graphique linéaire indique le nombre de segments qui ont été qualifiés et disqualifiés au cours des dernières 24 heures. La liste déroulante peut être ajustée pour afficher les dernières 24 heures, la semaine dernière ou les 30 derniers jours.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Pour plus d’informations sur l’évaluation du dernier segment, sélectionnez la bulle d’informations.

![](../images/ui/streaming-segmentation/info-bubble.png)

Pour plus d&#39;informations sur les définitions de segment, consultez la section précédente sur [les détails de la définition de segment](#segment-details).

## Étapes suivantes

Ce guide d’utilisateur explique comment fonctionnent les définitions de segment activées pour la diffusion en continu sur Adobe Experience Platform et comment surveiller les segments activés pour la diffusion en continu.

Pour en savoir plus sur l’utilisation de l’interface utilisateur de Adobe Experience Platform, consultez le [Guide de l’utilisateur de la segmentation](./overview.md).
