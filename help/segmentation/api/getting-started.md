---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de développement de Segmentation Service
topic: developer guide
translation-type: tm+mt
source-git-commit: aff81a4f3243ef77cbdfc776220a5de46e360084
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 50%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Le service de segmentation des Adobes Experience Platform vous permet de créer des segments et de générer des audiences dans l’Adobe Experience Platform à partir de vos [!DNL Real-time Customer Profile] données.

The developer guide requires a working understanding of the various Experience Platform services involved with using [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md) : permet de créer des segments d’audience à partir de données Real-time Customer Profile.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
- [!DNL Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Environnements de test](../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

The following sections provide additional information that you will need to know in order to successfully work with the [!DNL Segmentation] API.

## Lecture d’exemples d’appels API

The [!DNL Segmentation Service] API documentation provides example API calls to demonstrate how to format your requests. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](../../tutorials/authentication.md) pour lancer des appels vers des points de terminaison Platform. Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels API Experience Platform, comme illustré ci-dessous :

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