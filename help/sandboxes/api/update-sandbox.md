---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mise à jour d’un sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 4%

---


# Mise à jour d’un sandbox

Vous pouvez mettre à jour un ou plusieurs champs d’un sandbox en exécutant une requête PATCH qui inclut le sandbox dans le chemin de la requête et la propriété à mettre à jour dans la charge utile de la requête. `name`

>[!NOTE] Actuellement, seule la `title` propriété d’un sandbox peut être mise à jour.

**Format d’API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | Propriété `name` du sandbox à mettre à jour. |

**Requête**

La requête suivante met à jour la propriété `title` du sandbox nommé &quot;dev-2&quot;.

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

Une réponse réussie renvoie l’état HTTP 200 (OK) avec les détails du sandbox nouvellement mis à jour.

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
