---
keywords: Experience Platform;accueil;rubriques les plus consultées;environnements de test de liste
solution: Experience Platform
title: Point de terminaison de l’API des types Sandbox
topic-legacy: developer guide
description: Vous pouvez récupérer une liste des types d’environnements de test pris en charge pour votre organisation en envoyant une requête GET au point de terminaison /sandboxTypes .
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: e644fe9a2faf8692617f6bbee2b91a52c323ff5d
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 49%

---

# Point de terminaison des types Sandbox

Vous pouvez récupérer une liste des types d’environnements de test pris en charge pour votre organisation en envoyant une requête GET au point de terminaison `/sandboxTypes`.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼAPI [[!DNL Sandbox] ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml). Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture d’exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir les appels à une API Experience Platform.

## Récupération d’une liste de types d’environnements de test pris en charge

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
