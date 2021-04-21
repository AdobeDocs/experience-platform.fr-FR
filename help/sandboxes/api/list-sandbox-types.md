---
keywords: Experience Platform ; accueil ; rubriques populaires ; sandbox de liste
solution: Experience Platform
title: Types de sandbox pris en charge par la liste dans l’API
topic-legacy: developer guide
description: Vous pouvez récupérer une liste de types de sandbox pris en charge pour votre organisation en adressant une demande de GET au point de terminaison /sandboxTypes.
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 48%

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
