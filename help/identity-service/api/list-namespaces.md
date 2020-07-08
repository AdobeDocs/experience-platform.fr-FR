---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: espaces de nommage Listes disponibles
topic: API guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 8%

---


# espaces de nommage Listes disponibles

**Format d’API**

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

La réponse comprend un tableau d’objets, chaque objet représentant un espace de nommage disponible. Les Espaces de nommage dont la valeur &quot;[!UICONTROL personnalisée]&quot; est &quot;[!UICONTROL false]&quot; sont des espaces de nommage standard, tandis que ceux dont la valeur &quot;[!UICONTROL personnalisée]&quot; est &quot;[!UICONTROL true&quot; sont des espaces de nommage créés par votre entreprise.]

>[!NOTE]
>
>Cette réponse a été tronquée pour l&#39;espace.

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

Passez au didacticiel suivant pour [créer un espace de nommage personnalisé](./create-custom-namespace.md)