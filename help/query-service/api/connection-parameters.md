---
keywords: Experience Platform;home;popular topics;query service;api guide;connection parameters;Query service;
solution: Experience Platform
title: Guide de développement de Query Service
topic: connection parameters
description: Vous pouvez récupérer vos paramètres de connexion pour utiliser le service interactif en faisant une demande de GET au point de terminaison /connection_parameters.
translation-type: tm+mt
source-git-commit: 648544bc60c0cee8ca8b167118391980b6c33d91
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 47%

---


# Paramètres de connexion

## Exemples d’appels API

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l&#39;API [!DNL Query Service]. Les sections suivantes décrivent les différents appels d&#39;API que vous pouvez effectuer à l&#39;aide de l&#39;API [!DNL Query Service]. Chaque appel inclut le format général d’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Demander des paramètres de connexion

Vous pouvez récupérer vos paramètres de connexion en faisant une demande de GET au point de terminaison `/connection_parameters`. Pour plus d’informations sur les clients utilisant des paramètres de connexion pour se connecter via le service interactif, consultez la documentation sur les [clients de Query Service](../clients/overview.md).

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
