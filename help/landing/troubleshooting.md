---
keywords: Experience Platform;home;popular topics;API error codes;API error code;error code API;error codes API;API request error;API troubleshooting;API error
solution: Experience Platform
title: FAQ et guide de dépannage d’Adobe Experience Platform
description: Trouvez des réponses aux questions fréquentes et un guide pour dépanner les erreurs courantes dans l’Experience Platform.
topic: getting started
type: Documentation
user-guide-description: Find answers to frequently asked questions and a guide for troubleshooting common errors in Experience Platform.
translation-type: tm+mt
source-git-commit: bc7c0a5d59c666ba80fac81a859b5ecf4dd37412
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 73%

---


# [!DNL Platform] FAQ et guide de dépannage

This document provides answers to frequently asked questions about Adobe Experience Platform, as well as a high-level troubleshooting guide for common errors that may be encountered in any [!DNL Experience Platform] API. For troubleshooting guides on individual [!DNL Platform] services, see the [service troubleshooting directory](#service-troubleshooting-directory) below.

## FAQ {#faq}

Vous trouverez ci-dessous une liste de réponses aux questions les plus fréquemment posées à propos d’Adobe Experience Platform.

## Que sont [!DNL Experience Platform] les API ? {#what-are-experience-platform-apis}

[!DNL Experience Platform] offre plusieurs API RESTful qui utilisent des requêtes HTTP pour accéder aux [!DNL Platform] ressources. Ces API de service présentent chacune plusieurs points de terminaison et vous permettent d’effectuer des opérations ayant pour but de répertorier (GET), de rechercher (GET), de modifier (PUT et/ou PATCH) et de supprimer (DELETE) des ressources. Pour plus d’informations sur les points de terminaison spécifiques et sur les opérations disponibles pour chaque service, consultez la [documentation de référence sur l’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) sur Adobe I/O.

## Comment formater une requête API ? {#how-do-i-format-an-api-request}

Request formats vary depending on the [!DNL Platform] API being used. The best way to learn how to structure your API calls is by following along with the examples provided in the documentation for the particular [!DNL Platform] service you are using.

### Lecture d’exemples d’appels API

The documentation for [!DNL Experience Platform] shows example API calls in two different ways. Tout d’abord, l’appel est présenté dans son **format d’API**, qui consiste en une représentation de modèle affichant uniquement l’opération (GET, POST, PUT, PATCH, DELETE) et le point de terminaison utilisé (par exemple `/global/classes`). Certains modèles indiquent également l’emplacement des variables pour mieux illustrer la manière dont un appel doit être formulé, comme par exemple `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Les appels sont ensuite affichés sous forme de commandes cURL dans une **Requête**, qui comprend les en-têtes nécessaires et le « chemin racine » complet indispensable pour que l’interaction avec l’API soit réussie. Le chemin racine doit être ajouté à tous les points de terminaison. Par exemple, le point de terminaison `/global/classes` cité plus haut devient `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Le format d’API/modèle de requête est visible dans toute la documentation, et vous devrez utiliser le chemin d’accès complet illustré dans la Requête de l’exemple lors de vos propres appels vers les API de Platform.

### Exemple de requête API

Voici un exemple de requête API illustrant le format que vous rencontrerez dans la documentation.

**Format d’API**

Le format d’API affiche l’opération (GET) et le point de terminaison utilisé. Les variables sont indiquées par des accolades (ici `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Requête**

Dans cet exemple de requête, les variables du format API reçoivent des valeurs réelles dans le chemin de la requête. Tous les en-têtes requis sont également affichés sous la forme d’échantillons de valeurs d’en-tête ou de variables dans lesquels des informations sensibles (telles que des jetons de sécurité et des identifiants d’accès) doivent être incluses.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse illustre ce que vous vous attendez à recevoir après un appel réussi vers l’API en fonction de la requête envoyée. Parfois, la réponse est tronquée en raison d’un espace insuffisant, il est donc possible que vous voyiez plus d’informations ou des informations supplémentaires par rapport à ce qui est affiché dans l’échantillon.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

Pour plus d’informations sur un point de terminaison en particulier dans les API de Platform, y compris sur les en-têtes nécessaires et les corps de requêtes, consultez la [documentation de référence sur l’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html).

## Quelle est mon organisation IMS ? {#what-is-my-ims-organization}

Une organisation IMS est une représentation Adobe d’un client. Toutes les solutions Adobe sous licence intègrent cette organisation client. When an IMS organization is entitled to [!DNL Experience Platform], it can assign access to developers. L’identifiant d’organisation IMS (`x-gw-ims-org-id`) représente l’organisation pour laquelle un appel API devrait être exécuté. Il est donc nécessaire de le place en tant qu’en-tête de toutes les requêtes API. This ID can be found through the [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr): in the **Integrations** tab, navigate to the **Overview** section for any particular integration to find the ID under **Client Credentials**. For a step-by-step walkthrough of how to authenticate into [!DNL Platform], see the [authentication tutorial](../tutorials/authentication.md).

## Où trouver ma clé API ? {#where-can-i-find-my-api-key}

Une clé API doit constituer l’en-tête de toutes les requêtes API. It can be found through the [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr). Dans la console, sous l’onglet **Intégrations**, accédez à la section **Aperçu** pour une intégration spécifique et vous trouverez la clé sous **Informations d’identification client**. For a step-by-step walkthrough of how to authenticate to [!DNL Platform], see the [authentication tutorial](../tutorials/authentication.md).

## Comment obtenir un jeton d’accès ? {#how-do-i-get-an-access-token}

Les jetons d’accès doivent être renseignés dans l’en-tête d’autorisation de tous les appels API. Ils peuvent être générés à l’aide d’une commande `curl`, à condition que vous ayez accès à une intégration pour une organisation IMS. Les jetons d’accès ne sont valides que pendant 24 heures. Après ce délai, un nouveau jeton doit être généré pour continuer à utiliser l’API. Pour plus d’informations sur la génération des jetons d’accès, consultez le [tutoriel sur l’authentification](../tutorials/authentication.md).

## Comment utiliser les paramètres de requête ? {#how-do-i-user-query-parameters}

Some [!DNL Platform] API endpoints accept query parameters to locate specific information and filter the results returned in the response. Les paramètres de requête sont ajoutés aux chemins de requête avec un point d’interrogation (`?`), suivi d’un ou plusieurs paramètres de requête sous le format `paramName=paramValue`. Lorsque vous combinez plusieurs paramètres dans un seul appel, vous devez utiliser une esperluette (`&`) pour les séparer. L’exemple suivant illustre la manière dont une requête qui utilise plusieurs paramètres de requête est représentée dans la documentation.

Voici quelques exemples de paramètres de requête fréquemment utilisés :

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Pour savoir précisément quels paramètres de requête sont disponibles pour un service ou un point de terminaison en particulier, consultez la documentation spécifique au service.

## Comment indiquer un champ JSON à mettre à jour dans une requête PATCH ? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Many PATCH operations in [!DNL Platform] APIs use [JSON Pointer](https://tools.ietf.org/html/rfc6901) strings to indicate JSON properties to update. Elles sont généralement incluses dans les payloads des requêtes au format [JSON Patch](https://tools.ietf.org/html/rfc6902). Pour plus d’informations sur la syntaxe requise pour ces technologies, consultez le [guide de base de l’API](api-fundamentals.md).

## Can I use Postman to make calls to [!DNL Platform] APIs? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) est un outil utile pour visualiser les appels vers les API RESTful. This [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describes how you can set up Postman to automatically perform authentication and use it to consume [!DNL Experience Platform] APIs.

## Quelle est la configuration requise pour [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Selon que vous utilisez l’interface utilisateur ou l’API, la configuration suivante est nécessaire :

**Pour les opérations basées sur l’interface utilisateur :**
- Un navigateur web standard et moderne. While the latest version of [!DNL Chrome] is recommended, current and previous major releases of [!DNL Firefox], [!DNL Internet Explorer], and Safari are also supported.
   - Each time a new major version is released, [!DNL Platform] starts supporting the most recent version while support for the third most recent version is dropped.
- Les cookies et JavaScript doivent être activés pour tous les navigateurs.

**Pour les interactions entre les développeurs et l’API :**
- Un environnement de développement à faire évoluer pour les intégrations de REST, de flux continu et de webhook.

## Erreurs et dépannage {#errors-and-troubleshooting}

The following is a list of errors that you may encounter when using any [!DNL Experience Platform] service. For troubleshooting guides on individual [!DNL Platform] services, see the [service troubleshooting directory](#service-troubleshooting-directory) below.

## Codes d’état API {#api-status-codes}

The following status codes may be encountered on any [!DNL Experience Platform] API. Chacun d’entre eux pouvant être causé par un grand nombre d’éléments, les explications données dans cette section sont générales. For more details regarding specific errors in individual [!DNL Platform] services, please see the [service troubleshooting directory](#service-troubleshooting-directory) below.

| Code d’état | Description | Causes possibles |
--- | --- | ---
| 400 | Mauvaise requête | La requête a été mal construite, des informations de clé étaient absentes et/ou sa syntaxe était incorrecte. |
| 401 | Échec de l’authentification | La requête n’a pas pu être authentifiée. Votre jeton d’accès est peut-être absent ou non valide. Pour plus d’informations, reportez-vous à la section [erreurs de jeton OAuth](#oauth-token-is-missing) ci-dessous. |
| 403 | Interdit | La ressource a été trouvée, mais vous ne possédez pas les informations d’identification appropriées pour la consulter. |
| 404 | Introuvable | La ressource demandée n’a pas été trouvée sur le serveur. La ressource a peut-être été supprimée, ou le chemin d’accès demandé n’a pas été correctement saisi. |
| 500 | Erreur interne du serveur | Il s’agit d’une erreur côté serveur. Si vous effectuez de nombreux appels simultanés, vous pouvez atteindre la limite de l’API et devoir filtrer vos résultats. (See the [!DNL Catalog Service] API developer guide sub-guide on [filtering data](../catalog/api/filter-data.md) to learn more.) Patientez avant de réessayer votre requête et contactez votre administrateur si le problème persiste. |

## Erreurs dans l’en-tête de la requête {#request-header-errors}

All API calls in [!DNL Platform] require specific request headers. Pour connaître les en-têtes nécessaires pour un service en particulier, consultez la [documentation de référence sur l’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html). Pour rechercher les valeurs des en-têtes d’authentification requis, consultez le [tutoriel sur l’authentification](../tutorials/authentication.md). Si l’un de ces en-têtes est absent ou non valide lors d’un appel API, les erreurs suivantes peuvent se produire.

### Jeton OAuth absent {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête `Authorization` est absent d’une requête API. Assurez-vous que l’en-tête d’autorisation comprend un jeton d’accès valide avant de réessayer.

### Jeton OAuth non valide

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Ce message d’erreur s’affiche lorsque le jeton d’accès indiqué dans l’en-tête `Authorization` n’est pas valide. Assurez-vous que le jeton a été saisi correctement ou [générez un nouveau jeton](../tutorials/authentication.md) dans la console Adobe I/O.

### Clé API requise

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête de clé API (`x-api-key`) est absent d’une requête API. Assurez-vous que l’en-tête comprend une clé API valide avant de réessayer.

### Clé API non valide

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Ce message d’erreur s’affiche lorsque la valeur de l’en-tête de clé API indiqué (`x-api-key`) n’est pas valide. Vérifiez que vous avez correctement saisi la clé avant de réessayer. Si vous ne connaissez pas votre clé API, vous pouvez la trouver dans la [console Adobe I/O](https://console.adobe.io) : dans l’onglet **Intégrations**, accédez à la section **Aperçu** pour une intégration spécifique afin de trouver la clé API sous **Informations d’identification du client**.


### En-tête absent

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête d’organisation IMS (`x-gw-ims-org-id`) est absent d’une requête API. Assurez-vous que l’en-tête comprend l’identifiant de votre organisation IMS avant de réessayer.

### Profil non valide

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

This error message displays when the user or Adobe I/O integration (identified by the [access token](#how-do-i-get-an-access-token) in the `Authorization` header) is not entitled to make calls to [!DNL Experience Platform] APIs for the IMS Org provided in the `x-gw-ims-org-id` header. Vérifiez que vous avez indiqué le bon identifiant pour votre organisation IMS dans l’en-tête avant de réessayer. Si vous ne connaissez pas l’identifiant de votre organisation, vous pouvez le trouver dans la [console Adobe I/O](https://console.adobe.io) : dans l’onglet **Intégrations**, accédez à la section **Aperçu** pour une intégration spécifique afin de trouver l’identifiant sous **Informations d’identification du client**.

### Type de contenu valide non spécifié

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Ce message d’erreur s’affiche lorsqu’une requête POST, PUT ou PATCH comporte un en-tête `Content-Type` non valide ou n’en comporte pas. Assurez-vous que l’en-tête est inclus dans la requête et que sa valeur est bien `application/json`.


## Répertoire de dépannage des services {#service-troubleshooting-directory}

The following is a list of troubleshooting guides and API reference documentation for [!DNL Experience Platform] APIs. Each troubleshooting guide provides answers to frequently asked questions and solutions to problems that are specific to individual [!DNL Platform] services. Les documents de référence sur l’API fournissent un guide complet de tous les points de terminaison disponibles pour chaque service et présentent des échantillons de corps de requête, de réponses et de codes d’erreur que vous pouvez recevoir.

| Service | Référence d’API | Dépannage |
| --- | --- | --- |
| Contrôle d’accès | [API Access Control](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Guide de dépannage du contrôle d’accès](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform Data Ingestion | [[ ! API d&#39;importation de données DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guide de dépannage de l&#39;assimilation par lots](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[Guide de dépannage de l&#39;assimilation en flux continu](../ingestion/streaming-ingestion/troubleshooting.md) |
| Espace de travail des données Adobe Experience Platform | [[ ! DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] guide de dépannage](../data-science-workspace/troubleshooting-guide.md) |
| Gouvernance des données d’Adobe Experience Platform | [[ ! API du service de stratégie DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Adobe Experience Platform Identity Service | [[ ! API du service d&#39;identité DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] guide de dépannage](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform Query Service | [[ ! API du service de Requête DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] guide de dépannage](../query-service/troubleshooting-guide.md) |
| Segmentation Adobe Experience Platform | [[ ! API de segmentation DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[ ! API du service de catalogue DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[ ! API de registre de Schéma DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] FAQ et guide de dépannage](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] et [!DNL Destinations]) | [[ ! API du service de flux DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[ ! API de Profil client en temps réel DNL]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] guide de dépannage](../profile/troubleshooting.md) |
| Environnements de test | [API Sandbox](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Guide de dépannage des environnements de test](../sandboxes/troubleshooting-guide.md) |

