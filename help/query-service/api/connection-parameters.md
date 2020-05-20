---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur Requête Service
topic: connection parameters
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 1%

---


# Paramètres de connexion

## Exemples d’appels d’API

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API Requête Service. Les sections suivantes décrivent les différents appels d’API que vous pouvez effectuer à l’aide de l’API Requête Service. Chaque appel comprend le format général de l’API, un exemple de requête indiquant les en-têtes requis et un exemple de réponse.

### Demander des paramètres de connexion pour le service interactif

Vous pouvez récupérer vos paramètres de connexion pour utiliser le service [](../creating-queries/writing-queries.md) interactif en faisant une requête GET au `/connection_parameters` point de terminaison. Pour plus d&#39;informations sur les clients qui utilisent les paramètres de connexion pour se connecter via le service interactif, consultez la documentation sur les clients [de](../clients/overview.md)Requête Service.

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

Une réponse réussie renvoie l’état HTTP 200 avec vos paramètres de connexion.

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
