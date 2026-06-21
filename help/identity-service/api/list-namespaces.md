---
keywords: Experience Platform;accueil;rubriques populaires;liste d’espaces de noms;espace de noms de liste
solution: Experience Platform
title: Répertorier les espaces de noms d’identité disponibles
description: Répertoriez tous les espaces de noms disponibles.
role: Developer
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
TQID: https://experienceleague.adobe.com/w0FQUDAE3RlptCj7SCe13CcSEsSDGFM67aF2xg6csSQ
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 83
ht-degree: 44%

---

# Répertorier les espaces de noms d’identité disponibles

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

La réponse comprend un tableau d’objets, chaque objet représentant un espace de noms disponible. Les espaces de noms dont la valeur « [!UICONTROL custom] » est définie sur « [!UICONTROL false] » sont des espaces de noms standard, tandis que ceux dont la valeur « [!UICONTROL custom] » est définie sur « [!UICONTROL true] » sont des espaces de noms créés par votre organisation.

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
