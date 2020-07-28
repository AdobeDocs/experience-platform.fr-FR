---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Réinitialisation d’un environnement de test
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 100%

---


# Réinitialisation d’un environnement de test

Les environnements de test de développement disposent d’une fonctionnalité de réinitialisation supprimant toutes les ressources de l’environnement de test autres que celles par défaut. Vous pouvez réinitialiser un environnement de test en effectuant une requête PUT comprenant le `name` de l’environnement de test dans le chemin d’accès de la requête.

**Format d’API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | La propriété `name` de l’environnement de test que vous souhaitez réinitialiser. |

**Requête**

La requête suivante réinitialise un environnement de test nommé « dev-2 ».

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| Propriété | Description |
| --- | --- |
| `action` | Ce paramètre doit être fourni dans le payload de la requête avec une valeur « reset » pour réinitialiser l’environnement de test. |

**Réponse**

Une réponse réussie renvoie les détails de l’environnement de test mis à jour, indiquant que son `state` est « resetting ».

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "dev-2",
    "title": "Development 2",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Une fois qu’un environnement de test est réinitialisé, il faut compter environ 15 minutes pour qu’il soit configuré par le système. Une fois la configuration effectuée, le `state` de l’environnement de test prend la valeur « active » ou « failed ».