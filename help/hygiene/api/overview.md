---
title: Guide de l’API d’hygiène des données
description: Découvrez comment corriger ou supprimer par programme les données personnelles de vos clients stockées dans Adobe Experience Platform.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 29%

---

# Guide de l’API d’hygiène des données

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités d’hygiène des données de Adobe Experience Platform ne sont disponibles que pour les organisations qui ont acheté Adobe Shield pour les soins de santé.

L’API Data Hygiene vous permet de corriger ou de supprimer par programmation les données personnelles stockées de vos clients dans Adobe Experience Platform, ainsi que de planifier des protocoles TTL (time-to-live) pour les jeux de données. Ce guide décrit les étapes préalables requises pour utiliser l’API et fournit des liens vers une documentation plus spécifique aux points de terminaison.

## Prise en main

Vous pouvez accéder à l’API Data Hygiene à l’aide du chemin racine suivant : `https://platform.adobe.io/data/core/hygiene/`

Cette section décrit les concepts de base que vous devez connaître avant de lancer des appels à l’API.

### Collecte des valeurs des en-têtes requis

Pour effectuer des appels à l’API Data Hygiene, vous devez d’abord rassembler vos informations d’authentification. Suivez la [Guide d’authentification API](../../landing/api-authentication.md) pour générer des valeurs pour chacun des en-têtes requis pour l’API Data Hygiene, comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

### Lecture d&#39;exemples d&#39;appels API

Ce document fournit un exemple d’appel API pour illustrer la manière dont vous devez formater vos requêtes. Pour en savoir plus sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section relative à la [lecture d’exemples d’appels API](../../landing/api-guide.md#sample-api) dans le guide de prise en main des API d’Experience Platform.

## Ordre de travail

Un ordre de travail est une représentation d’une tâche d’hygiène des données qui supprime les identités des consommateurs d’un jeu de données spécifique ou de tous les jeux de données. Voir [guide de point de terminaison des commandes de travail](./workorder.md) pour plus d’informations sur l’utilisation des commandes de travail dans l’API.

## Durée de vie (TTL) des jeux de données

Un TTL de jeu de données est une action &quot;supprimer un jeu de données&quot; différée dans le temps. En créant un TTL, vous spécifiez une heure ultérieure à laquelle ce jeu de données doit être supprimé. Voir [guide de point d’entrée TTL du jeu de données](./ttl.md) pour plus d’informations sur la planification des TTL de jeux de données dans l’API.

## Étapes suivantes

Ce guide explique comment gérer les demandes d’hygiène des données à l’aide d’appels API. Pour plus d’informations sur l’exécution de ces actions dans l’interface utilisateur de Platform, voir [Guide de l’interface utilisateur de l’hygiène des données](../ui/overview.md).
