---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: ef423a8c1b412315d03cddf7d8c351a232eb509b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 2%

---


# Création d’un sandbox

Vous pouvez créer un nouveau sandbox en envoyant une requête POST au point de `/sandboxes` terminaison.

**Format d’API**

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
| `name` | Identifiant qui sera utilisé pour accéder au sandbox dans les futures requêtes. Cette valeur doit être unique et la meilleure pratique consiste à la rendre aussi descriptive que possible. Ne peut pas contenir d&#39;espaces ni de majuscules. |
| `title` | Nom lisible par l’utilisateur utilisé à des fins d’affichage dans l’interface utilisateur de la plate-forme. |
| `type` | Type de sandbox à créer. Actuellement, seuls les sandbox de type &quot;développement&quot; peuvent être créés par une organisation. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau sandbox, indiquant qu’il `state` est en cours de &quot;création&quot;.

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE] Les sandbox prennent environ 15 minutes pour être approvisionnés par le système, après quoi ils `state` deviendront &quot;actifs&quot; ou &quot;échoués&quot;.
