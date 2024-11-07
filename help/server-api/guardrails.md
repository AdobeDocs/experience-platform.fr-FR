---
title: Protections des performances pour l’API du serveur réseau Edge
description: Découvrez comment utiliser l’API du serveur dans des barrières de sécurité de performances optimales.
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 316efe577274b389bd1bf50e896ad6ef53e44b7b
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 5%

---


# Protections des performances pour l’API du serveur réseau Edge

## Vue d’ensemble {#overview}

Les barrières de performance définissent les limites d’utilisation liées à vos cas d’utilisation de l’API de serveur. Le dépassement des barrières de performance décrites dans cet article peut entraîner une dégradation des performances.

Adobe n’est pas responsable de la dégradation des performances provoquée par le dépassement des limites d’utilisation. Les clients qui dépassent systématiquement les barrières de performance peuvent demander une capacité de traitement supplémentaire afin d’éviter une dégradation des performances.

>[!IMPORTANT]
>
>Vérifiez vos droits de licence dans votre commande de ventes et la [description du produit](https://helpx.adobe.com/fr/legal/product-descriptions.html) correspondante sur les limites d’utilisation réelles en plus de cette page de garde-fous.

Toutes les barrières de performance décrites dans cette page s’appliquent au niveau de l’organisation IMS. Pour les utilisateurs disposant de plusieurs organisations IMS configurées, chaque organisation est soumise individuellement aux barrières de performance ci-dessous. Pour plus d’informations sur [!DNL IMS Organizations], consultez le [glossaire Experience Platform](../landing/glossary.md) .

## Définitions

* **Disponibilité** est calculé pour chaque intervalle de cinq minutes en tant que pourcentage des demandes traitées par l’Edge Network Experience Platform qui ne échouent pas en erreur et se rapportent uniquement aux API Edge Network configurées. Si un client n’a effectué aucune requête au cours d’un intervalle de cinq minutes donné, cet intervalle est considéré comme 100 % disponible.
* **Le pourcentage de disponibilité mensuelle** pour une région donnée est calculé comme la moyenne de disponibilité pour tous les intervalles de cinq minutes dans un mois.
* Un **en amont** est un service derrière l’Edge Network, activé pour un flux de données spécifique, tel que le transfert côté serveur d’Adobe, la segmentation Adobe Edge ou Adobe Target.
* Une **unité de requête** correspond à un fragment de 8 Ko d’une requête et à un élément en amont configuré pour un flux de données.
* Une **requête** est un message unique envoyé par une application détenue par le client à [!DNL Server API]. Une requête peut contenir une ou plusieurs unités de requête.
* Une **erreur** est une requête qui échoue en raison d’une [ erreur de service interne ](error-handling.md) de l’Edge Network.

## Limites de service

Toutes les séries de données imposent certaines limites d’utilisation, qui contrôlent principalement le nombre d’événements pouvant être envoyés simultanément, leur taille et le nombre de services en amont vers lesquels ces demandes sont acheminées.

### Unités de requête

Toutes les limites sont appliquées et normalisées sur une **unité de requête (RU)**, définie sous la forme d’un **fragment de 8 Ko** d’une requête dirigée vers un service en amont configuré dans un flux de données.

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
| `/v2/interact` | 4 000 |
| `/v2/collect` | 6000 |


### Limite de taille de requête HTTP

| Format de la payload | Taille maximale d’une requête | Fragments de requête max 8 Ko |
| --- | --- | --- |
| Texte brut JSON | 64 Ko | 8 |


>[!NOTE]
>
>En fonction de la charge utile elle-même, les formats binaires sont généralement 20 à 40 % plus compacts, ce qui vous permet de transmettre plus de données que vous ne le feriez avec le format JSON en texte brut. Contactez votre représentant de l’assistance clientèle si vous avez besoin d’une capacité supérieure pour vos flux de données.

## Étapes suivantes

Pour plus d’informations sur les barrières de sécurité des autres services Experience Platform, sur les informations de latence de bout en bout et les informations de licence des documents Description du produit Real-Time CDP, consultez la documentation suivante :

* [Barrières de sécurité Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammes de latence de bout en bout](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) pour divers services Experience Platform.
* [Real-Time Customer Data Platform (Édition B2C - Packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
