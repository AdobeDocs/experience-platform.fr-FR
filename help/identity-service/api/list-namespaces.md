---
keywords: Experience Platform ; accueil ; sujets populaires ; liste d'espace de nommage ; espace de nommage liste
solution: Experience Platform
title: Répertorier les espaces de noms disponibles
topic: API guide
description: Liste de tous les espaces de nommage disponibles.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 53%

---


# Répertorier les espaces de noms disponibles

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