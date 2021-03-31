---
keywords: Experience Platform;accueil;rubriques populaires;Sandbox;sandbox
solution: Experience Platform
title: Création d’un sandbox dans l’API
topic: guide du développeur
description: Vous pouvez créer un nouveau sandbox en envoyant une requête POST au point de terminaison `/sandbox`.
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 49%

---


# Création d’un sandbox dans l’API

Vous pouvez créer un sandbox de développement ou de production en envoyant une requête de POST au point de terminaison `/sandboxes`.

## Création d’un sandbox de développement

Pour créer un sandbox de développement, envoyez une requête de POST au point de terminaison `/sandboxes` et indiquez la valeur `development` pour la propriété `type`.

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
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Identifiant qui sera utilisé pour accéder à l’environnement de test lors de futures requêtes. Cette valeur doit être unique, et il est recommandé de la décrire le plus précisément possible. Cette valeur ne peut pas contenir d’espaces ni de caractères spéciaux. |
| `title` | Nom compréhensible utilisé à des fins d’affichage dans l’interface utilisateur de Platform. |
| `type` | Type d’environnement de test à créer. La valeur de la propriété `type` peut être développement ou production. |

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

## Création d’un sandbox de production

>[!NOTE]
>
>La fonctionnalité de sandbox de production multiple est en version bêta.

Pour créer un sandbox de production, envoyez une requête de POST au point de terminaison `/sandboxes` et indiquez la valeur `production` pour la propriété `type`.

**Format d’API**

```http
POST /sandboxes
```

**Requête**

La requête suivante crée un nouveau sandbox de production nommé &quot;test-prod-sandbox&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "test-prod-sandbox",
    "title": "Test Production Sandbox",
    "type": "production"
}'
```

| Propriété | Description |
| --- | --- |
| `name` | Identifiant qui sera utilisé pour accéder à l’environnement de test lors de futures requêtes. Cette valeur doit être unique, et il est recommandé de la décrire le plus précisément possible. Cette valeur ne peut pas contenir d’espaces ni de caractères spéciaux. |
| `title` | Nom compréhensible utilisé à des fins d’affichage dans l’interface utilisateur de Platform. |
| `type` | Type d’environnement de test à créer. La valeur de la propriété `type` peut être développement ou production. |

**Réponse**

Une réponse réussie renvoie les détails du nouvel environnement de test, indiquant que son `state` est « création ».

```json
{
    "name": "test-production-sandbox",
    "title": "Test Production Sandbox",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```
