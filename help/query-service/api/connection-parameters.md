---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Guide du développeur du service '
topic: connection parameters
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Paramètres de connexion

## Exemples d’appels d’API

Maintenant que vous comprenez les en-têtes à utiliser, vous êtes prêt à commencer à lancer des appels à l’API du service . Les sections suivantes décrivent les différents appels d’API que vous pouvez effectuer à l’aide de l’API de service . Chaque appel comprend le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Demander des paramètres de connexion pour le service interactif

Vous pouvez récupérer vos paramètres de connexion pour utiliser le service [](../creating-queries/writing-queries.md) interactif en envoyant une requête GET au `/connection_parameters` point de terminaison. Pour plus d&#39;informations sur les clients qui utilisent des paramètres de connexion pour se connecter via le service interactif, veuillez lire la documentation sur les clients [du service](../clients/overview.md).

**Format API**

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
