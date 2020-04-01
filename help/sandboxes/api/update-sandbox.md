---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mise à jour d’un sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578

---


# Mise à jour d’un sandbox

Vous pouvez mettre à jour un ou plusieurs champs d’un sandbox en effectuant une requête PATCH qui inclut les sandbox `name` dans le chemin de requête et la propriété à mettre à jour dans la charge utile de la requête.

>[!NOTE] Actuellement, seule la `title` propriété d’un sandbox peut être mise à jour.

**Format API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | La `name` propriété du sandbox à mettre à jour. |

**Requête**

La requête suivante met à jour la `title` propriété du sandbox nommé &quot;dev-2&quot;.

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
