---
keywords: Experience Platform ; accueil ; rubriques populaires ; supprimer un sandbox
solution: Experience Platform
title: Suppression d’un sandbox dans l’API
topic: guide du développeur
description: Vous pouvez supprimer un sandbox en effectuant une requête DELETE qui inclut le nom du sandbox dans le chemin de la requête.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 66%

---


# Suppression d’un sandbox dans l’API

Vous pouvez supprimer un environnement de test en effectuant une requête DELETE qui inclut le `name` de l’environnement de test dans le chemin de la requête.

>[!NOTE]
>
>L’appel de cette API met à jour la propriété `status` de l’environnement de test sur « supprimé » et la désactive. Les requêtes GET peuvent toujours récupérer les détails de l’environnement de test après sa suppression.

**Format d’API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | `name` de l’environnement de test que vous souhaitez supprimer. |

**Requête**

La requête suivante supprime un environnement de test nommé « dev-2 ».

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails mis à jour de l’environnement de test, indiquant que son `state` est « supprimé ».

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
