---
keywords: Experience Platform ; accueil ; sujets populaires ; liste d'espace de nommage ; espace de nommage liste
solution: Experience Platform
title: Espaces de nommage d'identité disponibles pour la liste
topic-legacy: API guide
description: Liste de tous les espaces de nommage disponibles.
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 44%

---

# Espaces de nommage d&#39;identité liste disponibles

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

La réponse comprend un tableau d’objets, chaque objet représentant un espace de noms disponible. Les Espaces de nommage dont la valeur &quot;[!UICONTROL custom]&quot; est &quot;[!UICONTROL false]&quot; sont des espaces de nommage standard, tandis que ceux dont la valeur &quot;[!UICONTROL custom]&quot; est &quot;[!UICONTROL true]&quot; sont des espaces de nommage créés par votre organisation.

>[!NOTE]
>
>Cette réponse a été tronquée pour l’espace.

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

Passez au tutoriel suivant pour [créer un espace de noms personnalisé](./create-custom-namespace.md).
