---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: types de sandbox pris en charge
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c

---


# types de sandbox pris en charge

Vous pouvez récupérer un de types de sandbox pris en charge pour votre entreprise en envoyant une requête GET au point de `/sandboxTypes` fin.

**Format API**

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

Une réponse réussie renvoie un  de types de sandbox pris en charge par votre entreprise.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
