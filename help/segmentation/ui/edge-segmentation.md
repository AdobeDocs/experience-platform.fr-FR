---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation Edge;Segmentation;Segmentation Service;service de segmentation;guide de l’interface utilisateur;périphérie de diffusion
solution: Experience Platform
title: Guide de l’interface utilisateur d’Edge Segmentation
topic-legacy: ui guide
description: La segmentation Edge permet d’évaluer instantanément les segments dans Platform, ce qui permet d’utiliser des cas de personnalisation de page et de page suivante.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 6bb1f417b5856f153adebe4deaac4fab264ef3a8
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 4%

---

# Guide de l’interface utilisateur de la segmentation Edge (version bêta)

>[!IMPORTANT]
>
>La segmentation Edge est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

La segmentation Edge permet d’évaluer instantanément les segments dans Adobe Experience Platform [sur la périphérie](../../edge/home.md), ce qui permet d’activer les cas d’utilisation de la personnalisation de la même page et de la page suivante.

## Types de requête de segmentation Edge

Actuellement, seuls certains types de requête peuvent être évalués avec la segmentation Edge. Les sections suivantes répertorient les types de requête qui peuvent être évalués avec la segmentation Edge et ceux qui ne sont actuellement pas pris en charge.

### Types de requête pris en charge

Une requête peut être évaluée avec une segmentation Edge si elle répond à l’un des critères décrits dans le tableau suivant.

>[!NOTE]
>
>Si la requête correspond à l’un des types de requête du tableau suivant, elle sera automatiquement évaluée à l’aide de la segmentation Edge. Le système détermine automatiquement cette fonctionnalité en fonction de l’expression de requête.

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Accès entrant | Toute définition de segment qui fait référence à un seul événement entrant sans restriction temporelle. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| Accès entrant qui fait référence à un profil | Toute définition de segment qui fait référence à un seul événement entrant, sans restriction temporelle, et à un ou plusieurs attributs de profil. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| Accès entrant avec une fenêtre temporelle de 24 heures | Toute définition de segment qui fait référence à un seul événement entrant dans les 24 heures |  |
| Accès entrant qui fait référence à un profil avec une fenêtre temporelle de 24 heures | Toute définition de segment qui fait référence à un seul événement entrant dans les 24 heures et à un ou plusieurs attributs de profil |  |

### Types de requête non pris en charge actuellement

Les types de requête suivants sont **non** actuellement pris en charge pour la segmentation Edge :

| Type de requête | Détails |
| ---------- | ------- |
| Événements multiples | Si une requête contient plusieurs événements, elle ne peut pas être évaluée à l’aide de la segmentation Edge. |
| Requête de fréquence | Toute définition de segment qui fait référence à un événement se produisant au moins un certain nombre de fois. |  |
| Requête de fréquence faisant référence à un profil | Toute définition de segment qui fait référence à un événement se produisant au moins un certain nombre de fois et qui possède un ou plusieurs attributs de profil. |  |

## Étapes suivantes

Ce guide explique comment évaluer les segments avec la segmentation Edge sur Adobe Experience Platform. Pour en savoir plus sur l’utilisation de l’interface utilisateur de l’Experience Platform, consultez le [guide d’utilisation de la segmentation](./overview.md). Pour savoir comment effectuer des actions similaires et utiliser des segments à l’aide d’API Experience Platform, consultez le [guide de l’API de segmentation Edge](../api/edge-segmentation.md).
