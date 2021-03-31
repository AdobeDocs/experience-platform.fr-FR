---
keywords: Experience Platform ; accueil ; rubriques populaires ; sandbox de liste
solution: Experience Platform
title: Types de sandbox pris en charge par la liste dans l’API
topic: guide du développeur
description: Vous pouvez récupérer une liste de types de sandbox pris en charge pour votre organisation en adressant une demande de GET au point de terminaison /sandboxTypes.
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 46%

---


# Types de sandbox pris en charge par la liste dans l’API

Vous pouvez récupérer une liste des types d’environnements de test pris en charge pour votre organisation en envoyant une requête GET au point de terminaison `/sandboxTypes`.

**Format d’API**

```http
GET /sandboxTypes
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie une liste des types d’environnements de test pris en charge pour votre organisation.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
