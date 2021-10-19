---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation des bords ; Segmentation ; Service de segmentation ; service de segmentation ; guide d'interface utilisateur ; bord de diffusion ;
solution: Experience Platform
title: Guide de l’interface utilisateur de segmentation des contours
topic-legacy: ui guide
description: La segmentation Edge permet d’évaluer instantanément les segments de la plate-forme sur le bord, ce qui permet d’utiliser des exemples d’utilisation de personnalisation de la même page et de la page suivante.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: c89971668839555347e9b84c7c0a4ff54a394c1a
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 2%

---

# Guide de l’interface utilisateur de segmentation des contours (bêta)

>[!IMPORTANT]
>
>La segmentation des contours est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

La segmentation des contours permet d’évaluer instantanément des segments dans Adobe Experience Platform. [sur le bord](../../edge/home.md), en activant les mêmes cas d’utilisation de personnalisation de page et de page suivante.

## Types de requête de segmentation de contour

Actuellement, seuls les types de requête sélectionnés peuvent être évalués avec la segmentation des contours. Les sections suivantes fournissent une liste des types de requête qui peuvent être évalués avec la segmentation des contours et ceux qui ne sont pas actuellement pris en charge.

### Types de requête pris en charge

Une requête peut être évaluée avec la segmentation des contours si elle répond à l&#39;un des critères décrits dans le tableau suivant.

>[!NOTE]
>
>Si la requête correspond à l&#39;un des types de requête de la table suivante, elle sera automatiquement évaluée à l&#39;aide de la segmentation des contours. Le système détermine automatiquement cette capacité en fonction de l&#39;expression de requête.

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Événement unique | Toute définition de segment qui fait référence à un événement entrant unique sans limitation de temps. | Les personnes qui ont ajouté un article à leur panier. |
| Événement unique faisant référence à un profil | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un seul événement entrant sans restriction de temps. | Des gens qui vivent aux États-Unis et ont visité la page d&#39;accueil. |
| Événement unique négatif avec un attribut de profil | Toute définition de segment faisant référence à un événement entrant unique et à un ou plusieurs attributs de profil négatifs | Personnes vivant aux États-Unis et ayant **non** a visité la page d&#39;accueil. |
| Événement unique dans une période de 24 heures | Toute définition de segment faisant référence à un événement entrant unique dans les 24 heures. | Les personnes qui ont visité la page d&#39;accueil ces dernières 24 heures. |
| Événement unique avec un attribut de profil dans une fenêtre de temps de 24 heures | Toute définition de segment faisant référence à un ou plusieurs attributs de profil et à un événement entrant unique annulé dans les 24 heures. | Des gens qui vivent aux États-Unis et ont visité la page d&#39;accueil ces dernières 24 heures. |
| Événement unique négatif avec un attribut de profil dans une période de 24 heures | Toute définition de segment faisant référence à un ou plusieurs attributs de profil et à un événement entrant unique annulé dans les 24 heures. | Personnes vivant aux États-Unis et ayant **non** a visité la page d&#39;accueil au cours des dernières 24 heures. |
| Événement de fréquence dans une période de 24 heures | Toute définition de segment qui fait référence à un événement qui se produit un certain nombre de fois dans une période de 24 heures. | Personnes ayant visité la page d&#39;accueil **au moins** cinq fois au cours des dernières 24 heures. |
| Événement de fréquence avec un attribut de profil dans une période de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement qui se produit un certain nombre de fois dans une période de 24 heures. | Personnes des États-Unis qui ont visité la page d&#39;accueil **au moins** cinq fois au cours des dernières 24 heures. |
| Événement de fréquence négatif avec un profil dans une période de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement annulé qui se produit un certain nombre de fois dans une période de 24 heures. | Personnes qui n&#39;ont pas visité la page d&#39;accueil **plus** plus de cinq fois au cours des dernières 24 heures. |
| Plusieurs visites entrantes dans un profil temporel de 24 heures | Toute définition de segment qui fait référence à plusieurs événements qui se produisent dans une période de 24 heures. | Personnes ayant visité la page d&#39;accueil **ou** a visité la page de paiement au cours des dernières 24 heures. |
| Plusieurs événements avec un profil dans une période de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et plusieurs événements se produisant dans une période de 24 heures. | Des gens des États-Unis qui ont visité la page d&#39;accueil **et** a visité la page de paiement au cours des dernières 24 heures. |

## Étapes suivantes

Ce guide explique comment évaluer les segments avec la segmentation des contours sur Adobe Experience Platform. Pour en savoir plus sur l’utilisation de l’interface utilisateur de l’Experience Platform, lisez la section [Guide de l’utilisateur de segmentation](./overview.md). Pour savoir comment exécuter des actions similaires et utiliser des segments à l’aide d’API Experience Platform, consultez la page [guide de l’API de segmentation des contours](../api/edge-segmentation.md).
