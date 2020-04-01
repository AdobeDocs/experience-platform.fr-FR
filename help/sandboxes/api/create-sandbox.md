---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: ef423a8c1b412315d03cddf7d8c351a232eb509b

---


# Création d’un sandbox

Vous pouvez créer un nouveau sandbox en envoyant une requête POST au point de `/sandboxes` fin.

**Format API**

```http
POST /sandboxes
```

**Requête**

La requête suivante crée un nouveau sandbox de développement nommé &quot;dev-3&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Identifiant qui sera utilisé pour accéder au sandbox dans les futures demandes. Cette valeur doit être unique et la meilleure pratique consiste à la rendre aussi descriptive que possible. Ne peut pas contenir d&#39;espaces ni de majuscules. |
| `title` | Nom compréhensible utilisé à des fins d’affichage dans l’interface utilisateur de la plateforme. |
| `type` | Type de sandbox à créer. Actuellement, seuls les sandbox de type &quot;développement&quot; peuvent être créés par une organisation. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau sandbox créé, indiquant qu’il `state` s’agit d’une &quot;création&quot;.

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE] Les sandbox prennent environ 15 minutes pour être approvisionnées par le système, après quoi elles `state` deviendront &quot;actives&quot; ou &quot;en échec&quot;.
