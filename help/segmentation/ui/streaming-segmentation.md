---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation par flux;Segmentation;Segmentation Service;service de segmentation;guide de l’interface utilisateur;guide de segmentation
solution: Experience Platform
title: Guide de l’interface utilisateur de la segmentation par flux
topic-legacy: ui guide
description: La segmentation par flux sur Adobe Experience Platform vous permet d’effectuer une segmentation en temps quasi réel tout en vous concentrant sur la richesse des données. Avec la segmentation par flux, la qualification de segment se produit désormais lorsque les données entrent dans Platform, ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées au fur et à mesure que les données sont transmises à Platform, ce qui signifie que l’adhésion au segment sera conservée à jour sans exécuter les tâches de segmentation planifiées.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: e6b5ea1878631fa88f907fd4aec64cf040e76e95
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# Segmentation par flux

>[!NOTE]
>
>Le document suivant indique comment utiliser la segmentation par flux à l’aide de l’interface utilisateur. Pour plus d’informations sur l’utilisation de la segmentation par flux à l’aide de l’API, veuillez lire le [guide de l’API de segmentation par flux](../api/streaming-segmentation.md).

Segmentation par flux sur [!DNL Adobe Experience Platform] permet aux clients d’effectuer une segmentation en temps quasi réel tout en se concentrant sur la richesse des données. Avec la segmentation par flux, la qualification de segment se produit maintenant lorsque les données en continu entrent dans [!DNL Platform], ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées au fur et à mesure de la transmission des données. [!DNL Platform], ce qui signifie que l’adhésion au segment sera maintenue à jour sans exécuter les tâches de segmentation planifiées.

>[!NOTE]
>
>La segmentation par flux fonctionne sur toutes les données ingérées à l’aide d’une source de diffusion en continu. Les données ingérées à l’aide d’une source par lots seront évaluées de nuit, même si elles sont admissibles pour la segmentation par flux.
>
>En outre, les segments évalués avec la segmentation par flux peuvent dériver entre l’adhésion idéale et l’adhésion réelle si le segment est basé sur un autre segment évalué à l’aide de la segmentation par lots. Si, par exemple, le segment A est basé sur le segment B et le segment B est évalué à l’aide de la segmentation par lots, puisque le segment B n’est mis à jour que toutes les 24 heures, le segment A s’éloigne davantage des données réelles jusqu’à ce qu’il se resynchronise avec la mise à jour du segment B.

## Types de requête de segmentation par flux {#query-types}

>[!NOTE]
>
>Pour que la segmentation par flux fonctionne, vous devez activer la segmentation planifiée pour l’organisation. Pour plus d’informations sur l’activation de la segmentation planifiée, reportez-vous à la section [la section Segmentation par flux dans le guide d’utilisation de la segmentation ;](./overview.md#scheduled-segmentation).

Une requête est automatiquement évaluée avec la segmentation par flux si elle répond à l’un des critères suivants :

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Événement unique | Toute définition de segment qui fait référence à un seul événement entrant sans restriction temporelle. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Événement unique dans une fenêtre temporelle relative | Toute définition de segment qui fait référence à un seul événement entrant. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Un seul événement avec une fenêtre temporelle | Toute définition de segment qui fait référence à un seul événement entrant avec une fenêtre temporelle. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| Profil uniquement | Toute définition de segment qui ne fait référence qu’à un attribut de profil. |  |
| Événement unique avec un attribut de profil | Toute définition de segment qui fait référence à un seul événement entrant, sans restriction temporelle, et à un ou plusieurs attributs de profil. **Remarque :** La requête est immédiatement évaluée lorsque l’événement arrive. Toutefois, dans le cas d’un événement de profil, il doit attendre 24 heures pour être incorporé. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Événement unique avec un attribut de profil dans une fenêtre de temps relative | Toute définition de segment qui fait référence à un seul événement entrant et à un ou plusieurs attributs de profil. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segment de segments | Toute définition de segment contenant un ou plusieurs segments par lot ou en flux continu. **Remarque :** Si un segment est utilisé, la disqualification du profil se produit. **toutes les 24 heures**. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| Plusieurs événements avec un attribut de profil | Toute définition de segment qui fait référence à plusieurs événements **au cours des dernières 24 heures** et (éventuellement) comporte un ou plusieurs attributs de profil. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Une définition de segment sera **not** être activé pour la segmentation par flux dans les scénarios suivants :

- La définition de segment inclut des segments ou des caractéristiques Adobe Audience Manager (AAM).
- La définition de segment comprend plusieurs entités (requêtes d’entités multiples).

Veuillez noter que les instructions suivantes s’appliquent lors de la segmentation par flux :

| Type de requête | Instruction |
| ---------- | -------- |
| Requête d’événement unique | Il n’existe aucune limite à l’intervalle de recherche en amont. |
| Requête avec historique des événements | <ul><li>L’intervalle de recherche en amont est limité à **un jour**.</li><li>Condition d’ordre du temps stricte **must** existent entre les événements.</li><li>Les requêtes comportant au moins un événement annulé sont prises en charge. Cependant, l’événement entier **cannot** être une négation.</li></ul> |

Si une définition de segment est modifiée de sorte qu’elle ne répond plus aux critères de la segmentation par flux, elle passe automatiquement de &quot;Diffusion en continu&quot; à &quot;Lot&quot;.

De plus, l’exclusion du segment, tout comme la qualification du segment, se produit en temps réel. Par conséquent, si une audience n’est plus admissible pour un segment, elle sera immédiatement non qualifiée. Par exemple, si la définition de segment demande &quot;Tous les utilisateurs qui ont acheté des chaussures rouges au cours des trois dernières heures&quot;, au bout de trois heures, tous les profils initialement qualifiés pour la définition de segment ne seront pas qualifiés.

## Détails des segments de segmentation par flux

Après avoir créé un segment activé dans le flux, vous pouvez afficher les détails de ce segment.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Plus précisément, la variable **[!UICONTROL Total qualifié]** mesure s’affiche, qui indique le nombre total d’audiences qualifiées, en fonction des évaluations de lot et de diffusion en continu pour ce segment.

Un graphique linéaire se trouve en dessous, qui indique le nombre de nouvelles audiences qui ont été mises à jour au cours des dernières 24 heures à l’aide de la méthode d’évaluation par flux. La liste déroulante peut être ajustée afin d’afficher les dernières 24 heures, la semaine dernière ou les 30 derniers jours. Le **[!UICONTROL Nouvelle audience mise à jour]** est basée sur le changement de la taille de l’audience au cours de la période sélectionnée, tel qu’évalué par la segmentation par flux. Cette mesure n’inclut pas l’audience totale qualifiée issue de l’évaluation par lots de segments quotidiens.

>[!NOTE]
>
>Un segment est considéré comme qualifié s’il passe de l’absence d’état à la réalisation ou s’il passe de la sortie à la réalisation. Un segment est considéré comme non qualifié s’il passe de la réalisation à la sortie ou s’il existe à la sortie.
>
>Vous trouverez plus d’informations sur ces statuts dans le tableau des statuts du [présentation de la segmentation](./overview.md#browse).

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Vous trouverez des informations supplémentaires sur l’évaluation du dernier segment en sélectionnant la bulle d’informations en regard de **[!UICONTROL Total qualifié]**.

![](../images/ui/streaming-segmentation/info-bubble.png)

Pour plus d’informations sur les définitions de segment, consultez la section précédente sur [détails sur la définition de segment](#segment-details).

## Étapes suivantes

Ce guide d’utilisation explique le fonctionnement des définitions de segment activées pour la diffusion en continu sur Adobe Experience Platform et comment surveiller les segments activés pour la diffusion en continu.

Pour en savoir plus sur l’utilisation de l’interface utilisateur de Adobe Experience Platform, veuillez lire le [Guide d’utilisation de la segmentation](./overview.md).

## Annexe

La section suivante répertorie les questions fréquentes sur la segmentation par flux :

### La segmentation par flux &quot;non-qualification&quot; se produit-elle également en temps réel ?

Pour la plupart des instances, l’inqualification de la segmentation par flux se produit en temps réel. Toutefois, les segments en flux continu qui utilisent des segments le font **not** non admissible en temps réel, mais non admissible après 24 heures.

### Sur quelles données la segmentation par flux fonctionne-t-elle ?

La segmentation par flux fonctionne sur toutes les données ingérées à l’aide d’une source de diffusion en continu. Les segments ingérés à l’aide d’une source par lots seront évalués de nuit, même s’ils sont qualifiés pour la segmentation par flux. Les événements diffusés dans le système avec un horodatage de plus de 24 heures seront traités dans la tâche par lots suivante.

### Comment les segments sont-ils définis comme segmentation par lots ou par flux ?

Un segment est défini comme une segmentation par lot ou par flux basée sur une combinaison de type de requête et de durée d’historique des événements. Vous trouverez une liste des segments qui seront évalués en tant que segment en continu dans la variable [section types de requête de segmentation par flux](#query-types).

Notez que si un segment contient **both** an `inSegment` et une chaîne d’événement unique directe, elle ne peut pas être admissible pour la segmentation par flux. Si vous souhaitez que ce segment soit admissible pour la segmentation par flux, vous devez faire de la chaîne d’événement unique directe son propre segment.

### Pourquoi le nombre de segments &quot;total qualifié&quot; continue-t-il à augmenter alors que le nombre sous &quot;X derniers jours&quot; reste à zéro dans la section de détails du segment ?

Le nombre total de segments qualifiés est tiré de la tâche de segmentation quotidienne, qui inclut les audiences qui remplissent les critères des segments par lot et par flux. Cette valeur s’affiche pour les segments par lot et en flux continu.

Nombre sous &quot;X derniers jours&quot; **only** inclut les audiences qualifiées en segmentation par flux, et **only** augmente si vous avez diffusé des données en flux continu dans le système et qu’elles sont prises en compte dans cette définition de flux continu. Cette valeur est **only** s’affiche pour les segments en continu. Par conséquent, cette valeur **may** s’affiche comme 0 pour les segments par lot.

Par conséquent, si vous constatez que le nombre sous &quot;X derniers jours&quot; est nul et que le graphique linéaire signale également zéro, vous avez la valeur **not** diffusion en continu de tous les profils dans le système qui répondent aux critères de ce segment.