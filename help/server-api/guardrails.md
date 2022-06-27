---
title: Protections des performances pour l’API Edge Network Server
description: Découvrez comment utiliser l’API du serveur dans des barrières de sécurité de performances optimales.
keywords: collecte de données;collection;réseau Edge;api;sla;slt;niveaux de service
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 2%

---

# Protections des performances pour l’API Edge Network Server

## Présentation {#overview}

Les barrières de performance définissent les limites d’utilisation liées à vos cas d’utilisation de l’API de serveur. Le dépassement des barrières de performance décrites dans cet article peut entraîner une dégradation des performances.

Adobe n’est pas responsable de la dégradation des performances provoquée par le dépassement des limites d’utilisation. Les clients qui dépassent systématiquement les barrières de performance peuvent demander une capacité de traitement supplémentaire afin d’éviter une dégradation des performances.

## Définitions

* **Disponibilité** est calculé pour chaque intervalle de cinq minutes en tant que pourcentage des requêtes traitées par le réseau Edge Experience Platform qui ne échouent pas en erreur et se rapportent uniquement aux API réseau Edge configurées. Si un client n’a effectué aucune requête au cours d’un intervalle de cinq minutes donné, cet intervalle est considéré comme 100 % disponible.
* **Pourcentage de disponibilité mensuelle** pour une région donnée est calculée en moyenne de la disponibilité pour tous les intervalles de cinq minutes d’un mois.
* Un **amont** est un service derrière le réseau Edge, activé pour un flux de données spécifique, tel que le transfert côté serveur Adobe, la segmentation Adobe Edge ou Adobe Target.
* A **unité de requête** correspond à un fragment de 8 Ko d’une requête et un en amont configuré pour un flux de données.
* A **requête** est un message unique envoyé par une application détenue par le client à la variable [!DNL Server API]. Une requête peut contenir une ou plusieurs unités de requête.
* Un **error** est une requête qui échoue en raison d’un réseau Edge [erreur de service interne](error-handling.md).

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
| `/v2/interact` | 4000 |
| `/v2/collect` | 6 000 |


### Limite de taille de requête HTTP

| Format de la payload | Taille maximale d’une requête | Fragments de requête max 8 Ko |
| --- | --- | --- |
| Texte brut JSON | 64 Ko | 8 |


>[!NOTE]
>
>En fonction de la charge utile elle-même, les formats binaires sont généralement 20 à 40 % plus compacts, ce qui vous permet de transmettre plus de données que vous ne le feriez avec le format JSON en texte brut. Contactez votre représentant de l’assistance clientèle si vous avez besoin d’une capacité supérieure pour vos flux de données.
