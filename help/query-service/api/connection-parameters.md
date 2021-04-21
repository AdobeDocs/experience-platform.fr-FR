---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de requête ; guide d'api ; paramètres de connexion ; service de Requête ;
solution: Experience Platform
title: Point de terminaison de l’API Paramètres de connexion
topic-legacy: connection parameters
description: Vous pouvez récupérer vos paramètres de connexion pour utiliser le service interactif en faisant une demande de GET au point de terminaison /connection_parameters.
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 38%

---

# Point de terminaison des paramètres de connexion

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
