---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Prise en main de l’API Policy Service
topic: developer guide
translation-type: tm+mt
source-git-commit: cb3a17aa08c67c66101cbf3842bf306ebcca0305
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 22%

---


# Getting started with the [!DNL Policy Service] API

L’ [!DNL Policy Service] API vous permet de créer et de gérer diverses ressources liées à Adobe Experience Platform [!DNL Data Governance]. This document provides an introduction to the core concepts you need to know before attempting to make calls to the [!DNL Policy Service] API.

## Conditions préalables 

L&#39;utilisation du guide du développeur nécessite une compréhension pratique des différents [!DNL Experience Platform] services impliqués dans l&#39;utilisation des capacités de gouvernance des données. Before beginning to work with the [!DNL Policy Service API], please review the documentation for the following services:

* [[ !Gouvernance des données DNL]](../home.md): Cadre selon lequel [!DNL Experience Platform] applique la conformité à l’utilisation des données.
* [[ ! Système de modèle de données d’expérience (XDM) DNL]](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
* [[ !Profil client en temps réel DNL]](../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

## Lecture d’exemples d’appels API

The [!DNL Policy Service] API documentation provides example API calls to demonstrate how to format your requests. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](../../tutorials/authentication.md) pour lancer des appels vers des points de terminaison [!DNL Platform] Completing the authentication tutorial provides the values for each of the required headers in [!DNL Experience Platform] API calls, as shown below:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Data Governance], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

## Ressources de base ou personnalisées

Within the [!DNL Policy Service] API, all policies and marketing actions are referred to as either `core` or `custom` resources.

`core` les ressources sont celles définies et maintenues par l&#39;Adobe, tandis que `custom` les ressources sont celles créées et entretenues par votre organisation et sont donc uniques et visibles uniquement par votre organisation IMS. Les opérations de liste et de recherche (`GET`) sont donc les seules opérations autorisées sur les ressources `core`, alors que les opérations de liste, de recherche et de mise à jour (`POST`, `PUT`, `PATCH` et `DELETE`) sont disponibles pour les ressources `custom`.

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API de service de stratégie, sélectionnez l’un des guides de points de terminaison disponibles.