---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Suppression d’un sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578

---


# Suppression d’un sandbox

Vous pouvez supprimer un sandbox en effectuant une requête DELETE qui inclut les sandbox `name` dans le chemin de requête.

>[!NOTE] L’exécution de cet appel d’API met à jour la `status` propriété sandbox sur &quot;delete&quot; et la désactive. Les requêtes GET peuvent toujours récupérer les détails du sandbox après sa suppression.

**Format API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | Le sandbox `name` à supprimer. |

**Requête**

La requête suivante supprime un sandbox nommé &quot;dev-2&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails mis à jour du sandbox, indiquant qu’il `state` est &quot;supprimé&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
