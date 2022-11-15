---
title: Guide de l’API Data Hygiene
description: Découvrez comment corriger ou supprimer par programmation les données personnelles des clients stockées dans Adobe Experience Platform.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 7679de9d30c00873b279c5315aa652870d8c34fd
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 80%

---

# Guide de l’API Data Hygiene

>[!IMPORTANT]
>
>Les fonctionnalités d’hygiène des données de Adobe Experience Platform ne sont actuellement disponibles que pour les organisations qui ont acheté **Adobe Health Care Shield** ou **Adobe de la confidentialité et de la sécurité**.

L’API Data Hygiene vous permet de corriger ou de supprimer par programmation les données personnelles des clients stockées dans Adobe Experience Platform, ainsi que de planifier des dates d’expiration pour les jeux de données. Ce guide décrit les étapes préalables requises pour utiliser l’API et contient des liens vers une documentation plus spécifique aux points d’entrée.

## Prise en main

Vous pouvez accéder à l’API Data Hygiene via le chemin racine suivant : `https://platform.adobe.io/data/core/hygiene/`.

Les sections ci-dessous présentent les concepts de base que vous devez connaître avant d’effectuer des appels à l’API.

### Collecte des valeurs des en-têtes requis

Pour effectuer des appels à l’API Data Hygiene, vous devez d’abord rassembler vos informations d’authentification. Suivez le [Guide d’authentification des API](../../landing/api-authentication.md) afin de générer des valeurs pour chacun des en-têtes obligatoires pour l’API Data Hygiene, comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

### Lecture d’exemples d’appels API

Ce document fournit un exemple d’appel API pour illustrer la manière dont vous devez formater vos requêtes. Pour en savoir plus sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section relative à la [lecture d’exemples d’appels API](../../landing/api-guide.md#sample-api) dans le guide de prise en main des API d’Experience Platform.

## Expirations de jeux de données

Une expiration de jeu de données correspond à une action « supprimer un jeu de données » différée. En créant une expiration de jeu de données, vous spécifiez une heure ultérieure à laquelle ce jeu de données doit être supprimé. Consultez le [Guide de point d’entrée d’expiration de jeux de données](./dataset-expiration.md) pour plus d’informations sur la planification des expirations de jeux de données dans l’API.

## Suppressions de consommateurs

>[!IMPORTANT]
>
>Les demandes de suppression de clients ne sont disponibles que pour les organisations qui ont acheté **Adobe Health Care Shield**.
>
>
>Les suppressions par les consommateurs sont destinées à être utilisées pour la normalisation des données, la suppression des données anonymes ou la minimisation des données. Ils sont **not** à utiliser pour les demandes de droits des titulaires de données (conformité) en ce qui concerne les réglementations de confidentialité comme le Règlement général sur la protection des données (RGPD). Pour tous les cas d’utilisation de conformité, utilisez [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) au lieu de .

L’API Data Hygiene vous permet de supprimer tous les enregistrements associés à une identité de consommateur dans un ou tous les jeux de données. Toutes les tâches d’hygiène des données qui suppriment les identités des consommateurs sont représentées par un concept appelé ordre de travail. Consultez le [guide de point d’entrée d’ordre de travail](./workorder.md) pour plus d’informations sur l’utilisation des suppressions de consommateurs dans l’API.

## Quota

Votre entreprise est limitée à un quota mensuel de traitements prédéterminé pour chaque type d’opération d’hygiène des données, ce qui peut varier en fonction des licences. Voir [Guide du point d’entrée du quota](./quota.md) pour plus d’informations sur l’état actuel du quota de vos processus d’hygiène des données.

## Étapes suivantes

Ce guide explique comment gérer les demandes de nettoyage de données à l’aide d’appels API. Pour plus d’informations sur l’exécution de ces actions dans l’interface utilisateur de Platform, consultez le [Guide de l’interface utilisateur de nettoyage de données](../ui/overview.md).
