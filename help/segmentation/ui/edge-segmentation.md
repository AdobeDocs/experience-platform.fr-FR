---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation des arêtes ; Segmentation ; Service de segmentation ; service de segmentation ; guide ui ; arête de diffusion ;
solution: Experience Platform
title: Guide de l’interface utilisateur de segmentation Edge
topic-legacy: ui guide
description: La segmentation Edge permet d’évaluer instantanément les segments dans la plate-forme, ce qui permet d’utiliser des cas de personnalisation de la même page et de la page suivante.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 5%

---

# Guide de l’interface utilisateur de segmentation Edge (bêta)

>[!NOTE]
>
>La segmentation Edge est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

La segmentation Edge permet d’évaluer instantanément les segments dans Adobe Experience Platform en périphérie, ce qui permet d’utiliser les mêmes cas de personnalisation de page et de page suivante.

## Types de requête de segmentation Edge

Une requête peut être évaluée avec la segmentation des arêtes si elle répond à l’un des critères suivants :

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Accès entrant | Toute définition de segment faisant référence à un seul événement entrant sans restriction de temps. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| Accès entrant faisant référence à un profil | Toute définition de segment faisant référence à un seul événement entrant, sans restriction de temps, et à un ou plusieurs attributs de profil. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| Requête de fréquence | Toute définition de segment faisant référence à un événement survenant au moins un certain nombre de fois. |  |
| Requête de fréquence faisant référence à un profil | Toute définition de segment faisant référence à un événement survenant au moins un certain nombre de fois et ayant un ou plusieurs attributs de profil. |  |

Si la requête correspond à l’un des types de requête ci-dessus, vous pouvez l’activer pour la segmentation des arêtes en activant l’option **[!UICONTROL Évaluer en tant que segment de diffusion en continu sur le bord]**.

![](../images/ui/edge-segmentation/mark-on-edge.png)

Les types de requête suivants sont **non** actuellement pris en charge pour la segmentation des arêtes :

| Type de requête | Détails |
| ---------- | ------- |
| Fenêtre relative | Si une requête fait référence à une fenêtre temporelle, elle ne peut pas être évaluée à l’aide de la segmentation des arêtes. |
| Négation | Si une requête contient une négation, elle ne peut pas être évaluée à l’aide de la segmentation des arêtes. |
| Plusieurs événements | Si une requête contient plusieurs événements, elle ne peut pas être évaluée à l’aide de la segmentation des arêtes. |

## Étapes suivantes

Ce guide d’utilisateur explique comment évaluer les segments avec la segmentation Edge sur Adobe Experience Platform.

Pour en savoir plus sur l’utilisation de l’interface utilisateur de Adobe Experience Platform, consultez le [Guide de l’utilisateur de la segmentation](./overview.md). Pour savoir comment exécuter des actions similaires et utiliser des segments à l’aide de l’interface utilisateur de Adobe Experience Platform, consultez le [guide de l’API de segmentation des arêtes](../api/edge-segmentation.md).
