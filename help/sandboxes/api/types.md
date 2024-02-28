---
keywords: Experience Platform;accueil;rubriques les plus consultées;environnements de test de liste
solution: Experience Platform
title: Point de terminaison de l’API des types Sandbox
description: Vous pouvez récupérer une liste des types d’environnements de test pris en charge pour votre organisation en envoyant une requête GET au point de terminaison /sandboxTypes .
role: Developer
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 73%

---

# Point de terminaison des types Sandbox

Vous pouvez récupérer une liste des types de sandbox pris en charge pour votre organisation en envoyant une requête GET au point d’entrée `/sandboxTypes`.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼ [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupération d’une liste de types d’environnements de test pris en charge

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
