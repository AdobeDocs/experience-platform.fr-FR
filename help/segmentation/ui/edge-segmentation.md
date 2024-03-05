---
solution: Experience Platform
title: Guide de l’interface utilisateur de segmentation Edge
description: Découvrez comment utiliser la segmentation Edge pour évaluer instantanément les définitions de segment dans Platform, en activant les cas d’utilisation de la personnalisation de la même page et de la page suivante.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 95%

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

| Type de requête | Détails | Exemple | Exemple PQL |
| ---------- | ------- | ------- | ----------- |
| Événement unique | Toute définition de segment qui fait référence à un seul événement entrant sans restriction temporelle. | Les personnes qui ont ajouté un article à leur panier. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Profil unique | Toute définition de segment qui fait référence à un seul attribut de profil unique | Personnes qui vivent aux États-Unis. | `homeAddress.countryCode = "US"` |
| Événement unique qui fait référence à un profil | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un seul événement entrant sans restriction temporelle. | Personnes qui vivent aux États-Unis et qui ont visité la page d’accueil. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| Événement unique annulé avec un attribut de profil | Toute définition de segment qui fait référence à un seul événement entrant annulé et à un ou plusieurs attributs de profil | Personnes qui vivent aux Etats-Unis et qui n’ont **pas** visité la page d’accueil. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Événement unique dans une fenêtre temporelle | Toute définition de segment qui fait référence à un seul événement entrant au cours d’une période donnée. | Personnes qui ont consulté la page d’accueil au cours des dernières 24 heures. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)])` |
| Événement unique avec un attribut de profil dans une fenêtre de temps relatif inférieure à 24 heures | Toute définition de segment qui fait référence à un seul événement entrant, avec un ou plusieurs attributs de profil, et qui se produit dans une fenêtre de temps relative de moins de 24 heures. | Personnes qui vivent aux États-Unis et qui ont visité la page d’accueil au cours des dernières 24 heures. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)])` |
| Événement unique annulé avec un attribut de profil dans une fenêtre temporelle | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un seul événement entrant annulé sur une période donnée. | Personnes qui vivent aux États-Unis et qui n’ont **pas** visité la page d’accueil au cours des dernières 24 heures. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]))` |
| Événement de fréquence dans une fenêtre temporelle de 24 heures | Toute définition de segment qui fait référence à un événement qui se produit un certain nombre de fois dans une fenêtre temporelle de 24 heures. | Personnes ayant consulté la page d’accueil **au moins** cinq fois au cours des dernières 24 heures. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Événement de fréquence avec un attribut de profil dans une fenêtre temporelle de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement qui se produit un certain nombre de fois dans une fenêtre temporelle de 24 heures. | Personnes originaires des États-Unis qui ont visité la page d’accueil **au moins** cinq fois au cours des dernières 24 heures. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Événement de fréquence associé à un profil dans une fenêtre temporelle de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à un événement annulé qui se produit un certain nombre de fois dans un intervalle de temps de 24 heures. | Personnes qui n’ont pas consulté la page d’accueil **plus** de cinq fois au cours des dernières 24 heures. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Plusieurs accès entrants dans un profil temporel de 24 heures | Toute définition de segment qui fait référence à plusieurs événements qui se produisent dans un intervalle de temps de 24 heures. | Personnes ayant consulté la page d’accueil **ou** ayant consulté la page de passage en caisse au cours des dernières 24 heures. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Plusieurs événements avec un profil dans un intervalle de temps de 24 heures | Toute définition de segment qui fait référence à un ou plusieurs attributs de profil et à plusieurs événements se produisant dans un intervalle de temps de 24 heures. | Personnes originaires des États-Unis qui ont visité la page d’accueil **et** qui ont consulté la page de passage en caisse au cours des dernières 24 heures. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segment de segments | Toute définition de segment contenant un ou plusieurs segments par lots ou en diffusion en flux continu. | Personnes qui vivent aux États-Unis et qui se trouvent dans le segment « segment existant ». | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Requête qui fait référence à une carte | Toute définition de segment qui fait référence à une carte de propriétés. | Personnes ayant effectué un ajout à leur panier en fonction de données de segment externes. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

Une définition de segment ne sera **pas** activée pour la segmentation Edge dans le scénario suivant :

- La définition de segment comprend une combinaison d’un événement unique et d’un événement `inSegment`.
   - Toutefois, si la définition de segment contenue dans l’événement `inSegment` est un segment de profil uniquement, la définition de segment **sera** activée pour la segmentation Edge.

## Étapes suivantes

Ce guide décrit l’évaluation des définitions de segments avec la segmentation Edge sur Adobe Experience Platform. Pour en savoir plus sur l’utilisation de l’interface utilisateur d’Experience Platform, veuillez lire le [Guide d’utilisation de la segmentation](./overview.md). Pour savoir comment effectuer des actions similaires et utiliser des définitions de segments à l’aide des API d’Experience Platform, consultez le [guide de l’API Segmentation Edge](../api/edge-segmentation.md).

## Annexe

La section suivante répertorie les questions fréquentes sur la segmentation Edge :

### Combien de temps faut-il pour qu’une définition de segment soit disponible sur le réseau Edge ?

La disponibilité d’une définition de segment sur le réseau Edge peut prendre jusqu’à une heure.
