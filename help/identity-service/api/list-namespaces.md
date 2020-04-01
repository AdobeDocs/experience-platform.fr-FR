---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' disponible '
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


#  disponible 

**Format API**

```http
GET /idnamespace/identities
```

**Requête**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/idnamespace/identities' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse comprend un tableau d’objets, chaque objet représentant un   disponible.   avec une valeur &quot;personnalisée&quot; de &quot;false&quot; sont des  standard, tandis que ceux avec une valeur &quot;personnalisé&quot; de &quot;true&quot; sont des que votre organisation a créés.

>[!NOTE] Cette réponse a été tronquée pour l&#39;espace.

```json
[
  {
        "updateTime": 1441122419000,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "CORE Namespace",
        "id": 0,
        "createTime": 1441122419000,
        "idType": "COOKIE",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1495153678000,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "ECID Namespace",
        "id": 4,
        "createTime": 1495153678000,
        "idType": "COOKIE",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1522783145000,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1522783145000,
        "idType": "COOKIE",
        "name": "AdCloud",
        "custom": false
    }
]
```

## Étapes suivantes

Passez au didacticiel suivant pour [créer un  personnalisé](./create-custom-namespace.md)