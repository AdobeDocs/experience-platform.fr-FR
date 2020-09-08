---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Prise en main de l’API Observability Insights
topic: developer guide
description: L’API Observability Insights vous permet de récupérer des données de mesure pour différentes fonctionnalités Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant de tenter d'appeler l'API Observability Insights.
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 11%

---


# Getting started with the [!DNL Observability Insights] API

L’ [!DNL Observability Insights] API vous permet de récupérer des données de mesure pour différentes fonctionnalités Adobe Experience Platform. This document provides an introduction to the core concepts you need to know before attempting to make calls to the [!DNL Observability Insights] API.

## Lecture d’exemples d’appels API

The [!DNL Observability Insights] API documentation provides example API calls to demonstrate how to format your requests. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on how to read example API calls in the [Experience Platform troubleshooting guide](../../landing/troubleshooting.md).

## En-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in. For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’ [!DNL Observability Insights] API, passez au guide [des points de terminaison des](./metrics.md)mesures.