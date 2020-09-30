---
keywords: Experience Platform;home;popular topics;query service;api guide;connection parameters;Query service;
solution: Experience Platform
title: Guide de développement de Query Service
topic: connection parameters
description: Vous pouvez récupérer vos paramètres de connexion pour utiliser le service interactif en faisant une demande de GET au point de terminaison /connection_parameters.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 62%

---


# Paramètres de connexion

## Exemples d’appels API

Now that you understand what headers to use, you are ready to begin making calls to the [!DNL Query Service] API. The following sections walk through the various API calls you can make using the [!DNL Query Service] API. Chaque appel inclut le format général d’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Demande de paramètres de connexion pour le service interactif

Vous pouvez récupérer vos paramètres de connexion pour utiliser le [service interactif](../creating-queries/writing-queries.md) en envoyant une requête GET au point de terminaison `/connection_parameters`. Pour plus d’informations sur les clients utilisant des paramètres de connexion pour se connecter via le service interactif, consultez la documentation sur les [clients de Query Service](../clients/overview.md).

**Format d’API**

```http
GET /connection_parameters
```

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec vos paramètres de connexion.

```json
{
    "username": "{USERNAME}",
    "dbName": "prod:all",
    "host": "{HOSTNAME}",
    "version": 1,
    "port": 80,
    "token": "{TOKEN}",
    "compressedToken": "{COMPRESSED_TOKEN}",
    "websocketHost": "{WEBSOCKET_HOSTNAME}"
}
```
