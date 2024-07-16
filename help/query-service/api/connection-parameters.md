---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;guide api;paramètres de connexion;service de requête;
solution: Experience Platform
title: Point de terminaison de l’API des paramètres de connexion
description: Vous pouvez récupérer vos paramètres de connexion pour utiliser le service interactif en envoyant une requête GET au point de terminaison /connection_parameters .
role: Developer
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 29%

---

# Point d’entrée des paramètres de connexion

## Exemple d’appel API

La section suivante vous guide tout au long de l’appel API que vous pouvez effectuer à l’aide de l’API [!DNL Query Service]. L’appel inclut le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
