---
keywords: Experience Platform ; accueil ; rubriques populaires ; mettre à jour sandbox
solution: Experience Platform
title: Mise à jour d’un sandbox dans l’API
topic-legacy: developer guide
description: Vous pouvez mettre à jour un ou plusieurs champs d’un sandbox en exécutant une requête de PATCH qui inclut le nom du sandbox dans le chemin de la requête et la propriété à mettre à jour dans la charge utile de la requête.
exl-id: a8ef4305-5e0c-4d8f-8663-1933c957f122
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 60%

---

# Mise à jour d’un sandbox dans l’API

Vous pouvez mettre à jour un ou plusieurs champs d’un environnement de test en effectuant une requête PATCH incluant le `name` de l’environnement de test dans le chemin de requête et la propriété à mettre à jour dans le payload de la requête.

>[!NOTE]
>
>Actuellement, seule la propriété `title` d’un environnement de test peut être mise à jour.

**Format d’API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | La propriété `name` de l’environnement de test que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour la propriété `title` de l’environnement de test nommé « dev-2 ».

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Development B"
  }'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 (OK) avec les détails de l’environnement de test mis à jour.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
