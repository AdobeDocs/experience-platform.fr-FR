---
title: Accords et cibles au niveau du service
description: Découvrez comment configurer l’authentification pour l’API Edge Network Server
seo-description: Learn how to configure authentication for the Edge Network Server API
keywords: collecte de données;collection;réseau Edge;api;sla;slt;niveaux de service
hide: true
hidefromtoc: true
source-git-commit: 50a688e2f19f4fda2fc4cca823edb5886ad32bba
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---


# Barrières de sécurité

## Présentation {#overview}

Adobe fera appel à des efforts raisonnables sur le plan commercial pour [!DNL Server API] disponibles dans un pourcentage de disponibilité mensuel d’au moins 99,9 % pour chaque région, au cours d’un cycle de facturation mensuel.

## Définitions

* **Disponibilité** est calculé pour chaque intervalle de cinq minutes sous la forme du pourcentage de requêtes traitées par le réseau Edge Experience Adobe Experience Platform qui n’échouent pas avec des erreurs et se rapportent uniquement aux API réseau Edge Adobe Experience Platform configurées. Si un client n’a effectué aucune requête au cours d’un intervalle de cinq minutes donné, cet intervalle est considéré comme 100 % disponible.
* **Pourcentage de disponibilité mensuelle** pour une région donnée est calculée en moyenne de la disponibilité pour tous les intervalles de cinq minutes d’un mois.
* Un **amont** est un service derrière le réseau Adobe Edge, activé pour un flux de données spécifique, tel que le transfert côté serveur Adobe, la segmentation Adobe Edge ou Adobe Target.
* A **requête** envoyée à l’API du serveur est définie comme une ou plusieurs unités de requête.
* A **unité de requête** correspond à un fragment de 8 Ko d’une requête et un en amont configuré pour un flux de données.
* Un **error** est une requête qui échoue en raison d’un réseau Adobe Experience Platform Edge [erreur de service interne](error-handling.md).

## Cibles internes

Les équipes d’ingénierie d’Adobe déploient des procédures de surveillance, de télésurveillance et d’évolutivité en temps réel proches des cibles suivantes :

* Moins de 1 % des requêtes HTTP renvoient `5xx` erreurs dans les cinq dernières minutes
* Moins de 1 % des connexions en amont renvoient une erreur au cours des cinq dernières minutes.
* Toute capacité de tenant est doublée en moins de 10 minutes à partir du moment où une limite est atteinte.

## Exclusions du contrat de niveau de service

L’engagement au niveau de service décrit ci-dessus ne s’applique pas aux problèmes d’indisponibilité ou de performance causés par les événements suivants :

* Facteurs échappant à notre contrôle raisonnable, y compris l’accès à Internet ou les problèmes connexes au-delà de l’infrastructure d’Adobe.
* Toute utilisation abusive de la variable [!DNL Server API], comme défini par les limites décrites ci-dessous.

## Limites de service

Toutes les séries de données imposent certaines limites d’utilisation, qui contrôlent principalement le nombre d’événements pouvant être envoyés simultanément, leur taille et le nombre de services en amont vers lesquels ces demandes sont acheminées.

### Unités de requête

Toutes les limites sont appliquées et normalisées sur une **unité de demande (RU)**, défini comme **Fragment de 8 Ko** d’une requête adressée à un service en amont configuré dans un flux de données.

#### Exemples

| Flux de mise à jour configurés par flux de données | Taille moyenne de la requête | Unités de requête |
| --- | --- | --- |
| 1 (Adobe Platform) | 8 Ko (1 fragment) | 1 |
| 2 (Adobe Platform, Adobe Target) | 8 Ko (1 fragment) | 2 |
| 2 (Adobe Platform, Adobe Target) | 16 Ko (2 fragments) | 4 |
| 2 (Adobe Platform, Adobe Target) | 64 Ko (8 fragments) | 16 |

### Limites des unités de requête

Le tableau ci-dessous présente les valeurs limites par défaut. Si vous avez besoin de limites d’unité de requête plus élevées, contactez votre gestionnaire de compte.

| Point d’entrée | Demandes d’unités par seconde |
| --- | --- |
| `/v2/interact` | 4 000 |
| `/v2/collect` | 6 000 |


### Limite de taille de requête HTTP

| Format de la payload | Taille maximale d’une requête | Fragments de requête max 8 Ko |
| --- | --- | --- |
| Texte brut JSON | 64 Ko | 8 |


>[!NOTE]
>
>En fonction de la charge utile elle-même, les formats binaires sont généralement 20 à 40 % plus compacts, ce qui vous permet de transmettre plus de données que vous ne le feriez avec le format JSON en texte brut. Contactez votre représentant de l’assistance clientèle si vous avez besoin d’une capacité supérieure pour vos flux de données.

