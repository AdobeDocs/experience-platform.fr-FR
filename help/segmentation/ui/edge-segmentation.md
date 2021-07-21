---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation Edge;Segmentation;Segmentation Service;service de segmentation;guide de l’interface utilisateur;périphérie de diffusion
solution: Experience Platform
title: Guide de l’interface utilisateur d’Edge Segmentation
topic-legacy: ui guide
description: La segmentation Edge permet d’évaluer instantanément les segments dans Platform, ce qui permet d’utiliser des cas de personnalisation de page et de page suivante.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 8375d5a35ef652335c60b4b8b4571bf42ec1924a
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 5%

---

# Guide de l’interface utilisateur de la segmentation Edge (version bêta)

>[!NOTE]
>
>La segmentation Edge est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

La segmentation Edge permet d’évaluer instantanément les segments dans Adobe Experience Platform, ce qui permet d’utiliser les cas de personnalisation de page suivante et de page identique.

## Types de requête de segmentation Edge

Une requête peut être évaluée avec la segmentation Edge si elle répond à l’un des critères suivants :

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Accès entrant | Toute définition de segment qui fait référence à un seul événement entrant sans restriction temporelle. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| Accès entrant qui fait référence à un profil | Toute définition de segment qui fait référence à un seul événement entrant, sans restriction temporelle, et à un ou plusieurs attributs de profil. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| Requête de fréquence | Toute définition de segment qui fait référence à un événement se produisant au moins un certain nombre de fois. |  |
| Requête de fréquence faisant référence à un profil | Toute définition de segment qui fait référence à un événement se produisant au moins un certain nombre de fois et qui possède un ou plusieurs attributs de profil. |  |

Si la requête correspond à l’un des types de requête ci-dessus, elle sera automatiquement évaluée à l’aide de la segmentation Edge.

Les types de requête suivants sont **non** actuellement pris en charge pour la segmentation Edge :

| Type de requête | Détails |
| ---------- | ------- |
| Fenêtre de temps relatif | Si une requête fait référence à une fenêtre temporelle, elle ne peut pas être évaluée à l’aide de la segmentation Edge. |
| Négation | Si une requête contient une négation ou un événement `not`, elle ne peut pas être évaluée à l’aide de la segmentation Edge. |
| Événements multiples | Si une requête contient plusieurs événements, elle ne peut pas être évaluée à l’aide de la segmentation Edge. |

## Étapes suivantes

Ce guide d’utilisation explique comment évaluer les segments avec la segmentation Edge sur Adobe Experience Platform.

Pour en savoir plus sur l’utilisation de l’interface utilisateur de Adobe Experience Platform, consultez le [guide d’utilisation de la segmentation](./overview.md). Pour savoir comment effectuer des actions similaires et utiliser des segments à l’aide de l’interface utilisateur de Adobe Experience Platform, consultez le [guide de l’API de segmentation Edge](../api/edge-segmentation.md).
