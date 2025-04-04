---
title: Protections des performances pour l’API du serveur réseau Edge
description: Découvrez comment utiliser l’API du serveur dans des mécanismes de sécurisation de performances optimales.
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 5%

---


# Protections des performances pour l’API du serveur réseau Edge

## Vue d’ensemble {#overview}

Les mécanismes de sécurisation de performances définissent des limites d’utilisation liées à vos cas d’utilisation de l’API Server. Le dépassement des mécanismes de sécurisation des performances décrits dans cet article peut entraîner une dégradation des performances.

Adobe n’est pas responsable de la dégradation des performances causée par des limites d’utilisation dépassées. Les clients qui dépassent régulièrement les mécanismes de sécurisation des performances peuvent demander une capacité de traitement supplémentaire pour éviter une dégradation des performances.

>[!IMPORTANT]
>
>Vérifiez vos droits de licence dans votre commande client et la [Description du produit](https://helpx.adobe.com/fr/legal/product-descriptions.html) correspondante sur les limites d’utilisation réelles en plus de cette page de mécanismes de sécurisation.

Tous les mécanismes de sécurisation des performances décrits dans cette page s’appliquent au niveau de l’organisation IMS. Pour les utilisateurs disposant de plusieurs organisations IMS configurées, chaque organisation est individuellement soumise aux mécanismes de sécurisation de performances ci-dessous. Voir le [glossaire Experience Platform](../landing/glossary.md) pour plus d’informations sur [!DNL IMS Organizations].

## Définitions

* Le paramètre **Disponibilité** est calculé pour chaque intervalle de cinq minutes comme le pourcentage de requêtes traitées par Experience Platform Edge Network qui n’échouent pas en raison d’erreurs et qui se rapportent uniquement aux API Edge Network configurées. Si un client n’a effectué aucune requête dans un intervalle de cinq minutes donné, cet intervalle est considéré comme 100 % disponible.
* Le **pourcentage de disponibilité mensuelle** pour une région donnée est calculé comme la moyenne de la disponibilité pour tous les intervalles de cinq minutes d’un mois.
* Un **en amont** est un service derrière Edge Network, activé pour un flux de données spécifique, tel que le transfert côté serveur Adobe, la segmentation Adobe Edge ou Adobe Target.
* Une **unité de requête** correspond à un fragment de 8 Ko d’une requête et à une unité en amont configurée pour un flux de données.
* Une **requête** est un message unique envoyé à l’[!DNL Server API] par une application détenue par le client. Une requête peut contenir une ou plusieurs unités de requête.
* Une **erreur** désigne toute requête qui échoue en raison d’une [erreur de service interne](error-handling.md) Edge Network.

## Limites de service

Tous les flux de données appliquent certaines limites d’utilisation, qui contrôlent principalement le nombre d’événements pouvant être envoyés simultanément, leur taille et le nombre de services en amont vers lesquels ces requêtes sont acheminées.

### Unités de requête

Toutes les limites sont appliquées et normalisées sur une **unité de requête (RU)**, définie comme un fragment de **8 Ko** d’une requête allant à un service en amont configuré dans un flux de données.

#### Exemples

| Amont configuré par flux de données | Taille moyenne de la requête | Unités de requête |
| --- | --- | --- |
| 1 (Adobe Experience Platform) | 8 Ko (1 fragment) | 1 |
| 2 (Adobe Experience Platform, Adobe Target) | 8 Ko (1 fragment) | 2 |
| 2 (Adobe Experience Platform, Adobe Target) | 16 Ko (2 fragments) | 4 |
| 2 (Adobe Experience Platform, Adobe Target) | 64 Ko (8 fragments) | 16 |

### Limites d’unités de requête

Le tableau ci-dessous présente les valeurs limites par défaut. Si vous avez besoin de limites d’unité de requête plus élevées, contactez votre représentant de compte.

| Point d’entrée | Unités de requêtes par seconde |
| --- | --- |
| `/v2/interact` | 4 000 |
| `/v2/collect` | 6000 |

### Limite de taille des requêtes HTTP

| Format de la payload | Taille max. d’une requête | Fragments de requête max. 8 Ko |
| --- | --- | --- |
| Texte brut JSON | 64 KO | 8 |


>[!NOTE]
>
>En fonction de la payload elle-même, les formats binaires sont généralement 20 à 40 % plus compacts, ce qui vous permet d’envoyer plus de données que vous ne le feriez dans un fichier JSON en texte brut. Contactez votre représentant de l’assistance clientèle si vous avez besoin d’une capacité supérieure pour vos flux de données.

## Étapes suivantes

Consultez la documentation suivante pour plus d’informations sur les autres mécanismes de sécurisation des services Experience Platform, sur les informations de latence de bout en bout et les informations de licence dans les documents de description du produit Real-Time CDP :

* [Mécanismes de sécurisation de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammes de latence de bout en bout](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) pour divers services Experience Platform.
* [Real-Time Customer Data Platform (édition B2C - packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
