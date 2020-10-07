---
keywords: Experience Platform;home;popular topics;identity service api;identity service developer guide;region
solution: Experience Platform
title: Prise en main
topic: API guide
description: 'Adobe Experience Platform Identity Service gère l’identification inter-appareils, inter-canaux et en temps quasi réel de vos clients, dans ce qu’on appelle un graphique d’identités dans Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: fa667d86c089c692f22cfd1b46f3f11b6e9a68d7
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 62%

---


# [!DNL Identity Service] Guide du développeur d’API

Adobe Experience Platform [!DNL Identity Service] manages the cross-device, cross-channel, and near real-time identification of your customers in what is known as an identity graph within Adobe Experience Platform.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [[ !Service d&#39;identité DNL]](../home.md): Résout le défi fondamental posé par la fragmentation des données du profil client. Pour ce faire, il rapproche les identités entre les appareils et les systèmes sur lesquels les clients interagissent avec votre marque.
- [[ !Profil client en temps réel DNL]](../../profile/home.md): Fournit un profil unifié et en temps réel pour les consommateurs, basé sur des données agrégées provenant de plusieurs sources.
- [[ ! Modèle de données d’expérience DNL (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.

The following sections provide additional information that you will need to know or have on-hand in order to successfully make calls to the [!DNL Identity Service] API.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

### Acheminement basé sur la région

The [!DNL Identity Service] API employs region-specific endpoints that require the inclusion of a `{REGION}` as part of the request path. Pendant la mise en service de votre organisation IMS, une région est déterminée et stockée dans votre profil d’organisation IMS. Using the correct region with each endpoint ensures that all requests made using the [!DNL Identity Service] API are routed to the appropriate region.

There are two regions currently supported by [!DNL Identity Service] APIs: VA7 and NLD2.

Le tableau ci-dessous présente des exemples de chemins qui utilisent les régions :

| Service | Région : VA7 | Région : NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Les requêtes effectuées sans spécifier de région peuvent entraîner le routage des appels vers une région incorrecte ou entraîner l’échec inattendu des appels.

Si vous ne parvenez pas à localiser la région dans votre profil d’organisation IMS, contactez votre administrateur système pour obtenir de l’aide.

## Using the [!DNL Identity Service] API

Les paramètres d’identité utilisés dans ces services peuvent être exprimés de l’une des deux manières suivantes : composite ou XID.

Les identités composites sont des éléments incluant à la fois la valeur d’identifiant et l’espace de noms. Lors de l’utilisation d’identités composites, l’espace de noms peut être fourni soit par nom (`namespace.code`), soit par identifiant (`namespace.id`).

When an identity is persisted, [!DNL Identity Service] generates and assigns an ID to that identity, called the native ID, or XID. Toutes les variations des API de cluster et de mappage prennent en charge les identités composites et les XID dans leurs requêtes et leurs réponses. L’un des paramètres est requis pour utiliser ces API : `xid` ou une combinaison de [`ns` ou `nsid`] et `id`.

Pour limiter le payload dans les réponses, les API adaptent leurs réponses au type de construction d’identité utilisée. En d’autres termes, si vous transmettez un XID, vos réponses auront des XID, si vous transmettez des identités composites, la réponse suivra la structure utilisée dans la requête.

The examples in this document do not cover the complete functionality of the [!DNL Identity Service] API. Pour l’API complète, voir le [guide de référence de l’API Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml).

>[!NOTE]
>
>Toutes les identités renvoyées seront compilées dans un formulaire XID natif lorsque le XID natif est utilisé dans la requête. Il est recommandé d’utiliser le formulaire d’identifiant ou d’espace de noms. Pour plus d’informations, voir la section relative à l’[obtention du XID d’une identité](./create-custom-namespace.md).

## Étapes suivantes

Maintenant que vous avez collecté les informations d’identification requises, vous pouvez passer au reste du guide de développement. Chaque section fournit des informations importantes sur les points de terminaison et inclut des exemples d’appels API pour effectuer des opérations CRUD. Chaque appel comprend le format général de l’API, un exemple de requête montrant les en-têtes requis et les payloads correctement formatés, ainsi qu’un exemple de réponse pour un appel réussi.
