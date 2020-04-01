---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Réinitialisation d’un sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578

---


# Réinitialisation d’un sandbox

Les sandbox de développement disposent d’une fonctionnalité de réinitialisation en usine qui supprime toutes les ressources non par défaut d’un sandbox. Vous pouvez réinitialiser un sandbox en effectuant une requête PUT qui inclut les sandbox `name` dans le chemin de la requête.

**Format API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | Propriété `name` du sandbox à réinitialiser. |

**Requête**

La requête suivante réinitialise un sandbox nommé &quot;dev-2&quot;.

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
| `action` | Ce paramètre doit être fourni dans la charge utile de requête avec la valeur &quot;reset&quot; pour réinitialiser le sandbox. |

**Réponse**

Une réponse réussie renvoie les détails du sandbox mis à jour, indiquant qu’il `state` s’agit d’une &quot;réinitialisation&quot;.

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

>[!NOTE] Une fois qu’un sandbox est réinitialisé, il faut environ 15 minutes pour être approvisionné par le système. Une fois l’approvisionnement effectué, le sandbox `state` devient &quot;actif&quot; ou &quot;échec&quot;.