---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;api;
solution: Experience Platform
title: Guide de développement de Segmentation Service
topic: developer guide
description: La documentation suivante fournit des informations supplémentaires dont vous avez besoin pour travailler avec l’API de segmentation.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 17%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] allows you to build segments and generate audiences in Adobe Experience Platform from your [!DNL Real-time Customer Profile] data.

The developer guide requires a working understanding of the various [!DNL Experience Platform] services involved with using [!DNL Segmentation Service].

- [[ !Segmentation DNL]](../home.md): Permet de créer des segments d’audience à partir de [!DNL Real-time Customer Profile] données.
- [[ ! Système de modèle de données d’expérience (XDM) DNL]](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
- [[ !Profil client en temps réel DNL]](../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully work with the [!DNL Segmentation] API.

## Lecture d’exemples d’appels API

The [!DNL Segmentation Service] API documentation provides example API calls to demonstrate how to format your requests. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](../../tutorials/authentication.md) pour lancer des appels vers des points de terminaison [!DNL Platform] Completing the authentication tutorial provides the values for each of the required headers in [!DNL Experience Platform] API calls, as shown below:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox in which the operation will take place:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on working with sandboxes in [!DNL Experience Platform], see the [sandboxes overview documentation](../../sandboxes/home.md).

## Étapes suivantes

Pour passer des appels à l’aide de l’ [!DNL Segmentation Service] API, sélectionnez l’un des guides de point de terminaison disponibles à l’aide du volet de navigation de gauche ou dans l’aperçu du guide du [développeur.](./overview.md)