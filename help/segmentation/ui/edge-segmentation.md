---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation Edge;Segmentation;Segmentation Service;service de segmentation;guide de l’interface utilisateur;périphérie de diffusion
solution: Experience Platform
title: Guide de l’interface utilisateur d’Edge Segmentation
topic-legacy: ui guide
description: La segmentation Edge permet d’évaluer instantanément les segments dans Platform, ce qui permet d’utiliser des cas de personnalisation de page et de page suivante.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: bb5a56557ce162395511ca9a3a2b98726ce6c190
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 2%

---

# Guide de l’interface utilisateur de la segmentation Edge (version bêta)

>[!IMPORTANT]
>
>La segmentation Edge est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

La segmentation Edge permet d’évaluer instantanément les segments dans Adobe Experience Platform. [sur le bord](../../edge/home.md), activation des cas d’utilisation de la personnalisation de la même page et de la page suivante.

## Types de requête de segmentation Edge

Actuellement, seuls certains types de requête peuvent être évalués avec la segmentation Edge. Les sections suivantes répertorient les types de requête qui peuvent être évalués avec la segmentation Edge et ceux qui ne sont actuellement pas pris en charge.

### Types de requête pris en charge

Une requête peut être évaluée avec une segmentation Edge si elle répond à l’un des critères décrits dans le tableau suivant.

>[!NOTE]
>
>Si la requête correspond à l’un des types de requête du tableau suivant, elle sera automatiquement évaluée à l’aide de la segmentation Edge. Le système détermine automatiquement cette fonctionnalité en fonction de l’expression de requête.

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Événement unique | Toute définition de segment qui fait référence à un seul événement entrant sans restriction temporelle. | Les personnes qui ont ajouté un article à leur panier. |
| Événement unique qui fait référence à un profil | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un seul événement entrant sans restriction temporelle. | Des personnes qui vivent aux États-Unis et ont visité la page d&#39;accueil. |
| Événement unique dégradé avec un attribut de profil | Toute définition de segment qui fait référence à un seul événement entrant négatif et à un ou plusieurs attributs de profil | Personnes qui vivent aux Etats-Unis et qui ont **not** a visité la page d’accueil. |
| Événement unique dans une fenêtre de temps de 24 heures | Toute définition de segment qui fait référence à un seul événement entrant dans les 24 heures. | Les personnes qui ont consulté la page d’accueil au cours des dernières 24 heures. |
| Événement unique avec un attribut de profil dans une fenêtre de temps de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement entrant unique annulé dans les 24 heures. | Des personnes qui vivent aux États-Unis et ont visité la page d&#39;accueil au cours des dernières 24 heures. |
| Evénement unique dégradé avec un attribut de profil dans une fenêtre de temps de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement entrant unique annulé dans les 24 heures. | Personnes qui vivent aux Etats-Unis et qui ont **not** a visité la page d’accueil au cours des dernières 24 heures. |
| Événement de fréquence dans un intervalle de temps de 24 heures | Toute définition de segment qui fait référence à un événement qui se produit un certain nombre de fois dans une fenêtre temporelle de 24 heures. | Personnes ayant consulté la page d’accueil **au moins** cinq fois au cours des dernières 24 heures. |
| Événement de fréquence avec un attribut de profil dans un intervalle de temps de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement qui se produit un certain nombre de fois dans une fenêtre temporelle de 24 heures. | Personnes des Etats-Unis qui ont visité la page d&#39;accueil **au moins** cinq fois au cours des dernières 24 heures. |
| Événement de fréquence associé à un profil dans une fenêtre temporelle de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement négatif qui se produit un certain nombre de fois dans une fenêtre temporelle de 24 heures. | Personnes qui n’ont pas consulté la page d’accueil **more** plus de cinq fois au cours des dernières 24 heures. |
| Plusieurs accès entrants dans un profil temporel de 24 heures | Toute définition de segment qui fait référence à plusieurs événements qui se produisent dans une fenêtre temporelle de 24 heures. | Personnes ayant consulté la page d’accueil **ou** a consulté la page de passage en caisse au cours des dernières 24 heures. |
| Plusieurs événements avec un profil dans un intervalle de temps de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à plusieurs événements se produisant dans une fenêtre temporelle de 24 heures. | Personnes des Etats-Unis qui ont visité la page d&#39;accueil **et** a consulté la page de passage en caisse au cours des dernières 24 heures. |

## Étapes suivantes

Ce guide explique comment évaluer les segments avec la segmentation Edge sur Adobe Experience Platform. Pour en savoir plus sur l’utilisation de l’interface utilisateur de l’Experience Platform, veuillez lire le [Guide d’utilisation de la segmentation](./overview.md). Pour savoir comment effectuer des actions similaires et utiliser des segments à l’aide d’API Experience Platform, consultez la page [Guide de l’API de segmentation Edge](../api/edge-segmentation.md).
