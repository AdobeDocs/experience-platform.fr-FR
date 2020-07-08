---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Suppression d’un sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 7%

---


# Suppression d’un sandbox

Vous pouvez supprimer un sandbox en effectuant une requête DELETE qui inclut le sandbox `name` dans le chemin de la requête.

>[!NOTE]
>
>L’exécution de cet appel d’API met à jour la propriété `status` du sandbox en &quot;supprimé&quot; et la désactive. Les requêtes GET peuvent toujours récupérer les détails du sandbox après sa suppression.

**Format d’API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | Le `name` sandbox à supprimer. |

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

Une réponse réussie renvoie les détails mis à jour du sandbox, indiquant qu&#39;il `state` est &quot;supprimé&quot;.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
