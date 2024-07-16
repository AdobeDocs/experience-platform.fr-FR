---
keywords: Experience Platform;accueil;rubriques populaires;liste d’espaces de noms;espace de noms de liste
solution: Experience Platform
title: Liste des espaces de noms d’identité disponibles
description: Répertorier tous les espaces de noms disponibles.
role: Developer
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 44%

---

# Liste des espaces de noms d’identité disponibles

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse comprend un tableau d’objets, chaque objet représentant un espace de noms disponible. Les espaces de noms avec une valeur &quot;[!UICONTROL custom]&quot; de &quot;[!UICONTROL false]&quot; sont des espaces de noms standard, tandis que ceux avec une valeur &quot;[!UICONTROL custom]&quot; de &quot;[!UICONTROL true]&quot; sont des espaces de noms que votre organisation a créés.

>[!NOTE]
>
>Cette réponse a été tronquée pour des raisons de place.

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
