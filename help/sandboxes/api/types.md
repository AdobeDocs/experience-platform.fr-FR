---
keywords: Experience Platform;accueil;rubriques populaires;lister des sandbox
solution: Experience Platform
title: Point d’entrée de l’API des types de sandbox
description: Vous pouvez récupérer une liste des types de sandbox pris en charge pour votre organisation en envoyant une requête GET au point d’entrée /sandboxTypes.
role: Developer
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
TQID: https://experienceleague.adobe.com/XMFMjrBV82u5kZJwQ2HbjNs3jRMTlftVFwR9RFUUB10
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: cb424651efb1b4d71717c06a4b0d6e9354f0dcc7
workflow-type: tm+mt
source-wordcount: 164
ht-degree: 70%

---

# Point d’entrée des types de sandbox

Vous pouvez récupérer une liste des types de sandbox pris en charge pour votre organisation en envoyant une requête GET au point d’entrée `/sandboxTypes`.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼ [[!DNL Sandbox] API](https://developer.adobe.com/experience-platform-apis/references/sandbox). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupération d’une liste des types de sandbox pris en charge

Vous pouvez récupérer une liste des types de sandbox pris en charge pour votre organisation en envoyant une requête GET au point d’entrée `/sandboxTypes`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Réponse**

Une réponse réussie renvoie une liste des types de sandbox pris en charge pour votre organisation.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```

