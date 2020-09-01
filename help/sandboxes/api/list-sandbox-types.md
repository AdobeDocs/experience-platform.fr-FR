---
keywords: Experience Platform;home;popular topics;list sandboxes
solution: Experience Platform
title: Liste des types d’environnements de test pris en charge
topic: developer guide
description: Vous pouvez récupérer une liste de types de sandbox pris en charge pour votre organisation en adressant une demande de GET au point de terminaison /sandboxTypes.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 69%

---


# Liste des types d’environnements de test pris en charge

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
  -H 'x-sandbox-name: {SANDBOX_NAME}'
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
