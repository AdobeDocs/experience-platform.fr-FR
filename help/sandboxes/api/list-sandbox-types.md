---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Types de sandbox pris en charge par la Liste
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 4%

---


# Types de sandbox pris en charge par la Liste

Vous pouvez récupérer une liste de types de sandbox pris en charge pour votre organisation en envoyant une requête GET au point de `/sandboxTypes` terminaison.

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

Une réponse réussie renvoie une liste de types de sandbox pris en charge pour votre entreprise.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
