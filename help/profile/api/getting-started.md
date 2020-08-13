---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Prise en main de l’API Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: 6df3e6579139f01d9877c1f033ea7721ca78118c
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 28%

---


# Getting started with the [!DNL Real-time Customer Profile] API {#getting-started}

Using the [!DNL Real-time Customer Profile] API, you can perform basic CRUD operations against Profile resources, such as configuring computed attributes, accessing entities, exporting Profile data, and deleting unneeded datasets or batches.

Using the developer guide requires a working understanding of the various Adobe Experience Platform services involved in working with [!DNL Profile] data. Before beginning to work with the [!DNL Real-time Customer Profile] API, please review the documentation for the following services:

* [!DNL Real-time Customer Profile](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [!DNL Adobe Experience Platform Identity Service](../../identity-service/home.md): Obtenez une meilleure vue de vos clients et de leur comportement en rapprochant les identités entre les périphériques et les systèmes.
* [!DNL Adobe Experience Platform Segmentation Service](../../segmentation/home.md) : permet de créer des segments d’audience à partir de données Real-time Customer Profile.
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully make calls to [!DNL Profile] API endpoints.

## Lecture d’exemples d’appels API

The [!DNL Real-time Customer Profile] API documentation provides example API calls to demonstrate how to properly format requests. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](../../tutorials/authentication.md) pour lancer des appels vers des points de terminaison [!DNL Platform] Completing the authentication tutorial provides the values for each of the required headers in [!DNL Experience Platform] API calls, as shown below:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. Requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes ayant un payload dans le corps de la requête (notamment les appels POST, PUT et PATCH) doivent comporter un en-tête `Content-Type`. Les valeurs acceptées propres à chaque appel sont fournies dans les paramètres d’appel.

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’ [!DNL Real-time Customer Profile] API, sélectionnez l’un des guides de points de terminaison disponibles.