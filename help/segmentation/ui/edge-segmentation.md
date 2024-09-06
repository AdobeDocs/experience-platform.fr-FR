---
solution: Experience Platform
title: Guide de l’interface utilisateur de segmentation Edge
description: Découvrez comment utiliser la segmentation Edge pour évaluer instantanément les définitions de segment dans Platform, en activant les cas d’utilisation de la personnalisation de la même page et de la page suivante.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 057db1432493a8443eb91b0fc371d0bdffb3de86
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 90%

---

# Guide de l’interface utilisateur de segmentation Edge

>[!NOTE]
>
>La segmentation Edge est désormais généralement disponible pour tous les utilisateurs et utilisatrices de Platform. Si vous avez créé des définitions de segments Edge au cours de la version Beta, ces définitions de segments continueront à fonctionner.

La segmentation Edge permet d’évaluer les segments dans Adobe Experience Platform instantanément [sur le serveur Edge](../../web-sdk/home.md), en activant les cas d’utilisation de la personnalisation sur une même page et sur la page suivante.

>[!IMPORTANT]
>
> Les données Edge seront stockées dans l’emplacement de serveur Edge le plus proche de l’emplacement où elles ont été collectées et peuvent être stockées à un autre emplacement que celui désigné comme centre de données Adobe Experience Platform principal (ou hub).
>
> En outre, le moteur de segmentation Edge ne traitera que les requêtes sur le serveur Edge lorsqu’il existe **une** identité marquée principale, qui est cohérente avec les identités principales non basées sur le serveur Edge.

## Types de requête de segmentation Edge {#query-types}

Actuellement, seuls certains types de requête peuvent être évalués avec la segmentation Edge. Les sections suivantes fournissent une liste des types de requête qui peuvent être évalués avec la segmentation Edge et ceux qui ne sont pas actuellement prises en charge.

Une requête peut être évaluée avec une segmentation Edge si elle répond à l’un des critères décrits dans le tableau suivant.

>[!NOTE]
>
>Si la requête correspond à l’un des types de requête du tableau suivant, elle sera automatiquement évaluée à l’aide de la segmentation Edge. Le système détermine automatiquement cette fonctionnalité en fonction de l’expression de requête.

| Type de requête | Détails |
| ---------- | ------- |
| Événement unique | Toute définition de segment qui fait référence à un seul événement entrant sans restriction temporelle. |
| Événement unique dans une fenêtre temporelle relative | Toute définition de segment qui fait référence à un seul événement entrant. |
| Événement unique avec une fenêtre temporelle | Toute définition de segment qui fait référence à un seul événement entrant avec une fenêtre temporelle. |
| Profil uniquement | Toute définition de segment qui ne fait référence qu’à un attribut de profil. |
| Événement unique avec un attribut de profil dans une fenêtre de temps relatif inférieure à 24 heures | Toute définition de segment qui fait référence à un seul événement entrant, avec un ou plusieurs attributs de profil, et qui se produit dans une fenêtre de temps relative de moins de 24 heures. |
| Segment de segments | Toute définition de segment contenant un ou plusieurs segments par lots ou en diffusion en flux continu. **Remarque :** si un segment est utilisé, la disqualification du profil se produit **toutes les 24 heures**. |
| Plusieurs événements avec un attribut de profil | Toute définition de segment qui fait référence à plusieurs événements **au cours des dernières 24 heures** et (éventuellement) comporte un ou plusieurs attributs de profil. |

Une définition de segment ne sera **pas** activée pour la segmentation Edge dans le scénario suivant :

- La définition de segment comprend une combinaison d’un événement unique et d’un événement `inSegment`.
   - Toutefois, si la définition de segment contenue dans l’événement `inSegment` est un segment de profil uniquement, la définition de segment **sera** activée pour la segmentation Edge.
- La définition de segment utilise &quot;Ignorer l’année&quot; dans le cadre de ses contraintes temporelles.

## Étapes suivantes

Ce guide décrit l’évaluation des définitions de segments avec la segmentation Edge sur Adobe Experience Platform. Pour en savoir plus sur l’utilisation de l’interface utilisateur d’Experience Platform, veuillez lire le [Guide d’utilisation de la segmentation](./overview.md). Pour savoir comment effectuer des actions similaires et utiliser des définitions de segments à l’aide des API d’Experience Platform, consultez le [guide de l’API Segmentation Edge](../api/edge-segmentation.md).

## Annexe

La section suivante répertorie les questions fréquentes sur la segmentation Edge :

### Combien de temps faut-il pour qu’une définition de segment soit disponible sur le réseau Edge ?

La disponibilité d’une définition de segment sur le réseau Edge peut prendre jusqu’à une heure.
