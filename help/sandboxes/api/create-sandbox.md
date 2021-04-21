---
keywords: Experience Platform;accueil;rubriques populaires;Sandbox;sandbox
solution: Experience Platform
title: Création d’un sandbox dans l’API
topic-legacy: developer guide
description: Vous pouvez créer un nouveau sandbox en envoyant une requête POST au point de terminaison `/sandbox`.
exl-id: 676c5de8-2c3a-4612-9dd8-93e01cafe90e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 79%

---

# Création d’un sandbox dans l’API

Vous pouvez créer un nouvel environnement de test en effectuant une requête POST au point de terminaison `/sandboxes`.

**Format d’API**

```http
POST /sandboxes
```

**Requête**

La requête suivante crée un nouvel environnement de test de développement nommé « dev-3 ».

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
| `name` | Identifiant qui sera utilisé pour accéder à l’environnement de test lors de futures requêtes. Cette valeur doit être unique, et il est recommandé de la décrire le plus précisément possible. Elle ne peut pas contenir d’espaces ni de majuscules. |
| `title` | Nom compréhensible utilisé à des fins d’affichage dans l’interface utilisateur de Platform. |
| `type` | Type d’environnement de test à créer. Actuellement, seuls les environnements de test de type « développement » peuvent être créés par une organisation. |

**Réponse**

Une réponse réussie renvoie les détails du nouvel environnement de test, indiquant que son `state` est « création ».

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
> Il faut environ 15 minutes pour que les environnements de test soient configurés par le système, après quoi leur `state` passe en « actif » ou en « échec ».
