---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;guide api;paramètres de connexion;service de requête;
solution: Experience Platform
title: Point de terminaison de l’API des paramètres de connexion
topic-legacy: connection parameters
description: Vous pouvez récupérer vos paramètres de connexion pour utiliser le service interactif en envoyant une requête GET au point de terminaison /connection_parameters .
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 38%

---

# Point d’entrée des paramètres de connexion

## Exemples d’appels API

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API [!DNL Query Service]. Les sections suivantes décrivent les différents appels d’API que vous pouvez effectuer à l’aide de l’API [!DNL Query Service]. Chaque appel inclut le format général d’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

### Demande de paramètres de connexion

Vous pouvez récupérer vos paramètres de connexion en effectuant une requête de GET sur le point de terminaison `/connection_parameters`. Pour plus d’informations sur les clients utilisant des paramètres de connexion pour se connecter via le service interactif, consultez la documentation sur les [clients de Query Service](../clients/overview.md).

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
