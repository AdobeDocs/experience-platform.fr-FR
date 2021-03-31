---
keywords: Experience Platform ; accueil ; rubriques populaires ; mettre à jour sandbox
solution: Experience Platform
title: Mise à jour d’un sandbox dans l’API
topic: guide du développeur
description: Vous pouvez mettre à jour un ou plusieurs champs d’un sandbox en exécutant une requête de PATCH qui inclut le nom du sandbox dans le chemin de la requête et la propriété à mettre à jour dans la charge utile de la requête.
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '135'
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
