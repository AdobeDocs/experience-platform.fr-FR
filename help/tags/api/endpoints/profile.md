---
title: Point d’entrée des profils
description: Découvrez comment effectuer des appels vers le point d’entrée /profiles dans l’API Reactor.
exl-id: d0434098-f49a-45f3-9772-488bd3c134aa
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 77%

---

# Point d’entrée de profil

Dans l’API Reactor, un profil représente un utilisateur d’Adobe Experience Platform. L’API Reactor ne conserve pas sa propre base de données d’utilisateurs et d’autorisations. Elle repose plutôt sur les Adobe ID gérés par [le système IMS (Identity Management System)](https://helpx.adobe.com/fr/enterprise/using/identity.html) d’Adobe.

Un profil contient toutes les informations sur l’utilisateur connecté, y compris toutes les organisations auxquelles il appartient, les profils de produit auxquels il appartient dans chaque organisation et les droits dont il dispose de chaque profil de produit.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Avant de poursuivre, veuillez consulter le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la façon de s’authentifier auprès de l’API.

## Récupération du profil actif {#lookup}

Vous pouvez récupérer les détails du profil actuellement connecté en envoyant une requête GET au point d’entrée `/profile`.

**Format d’API**

```http
GET /profile
```

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails du profil.

```json
{
  "data": {
    "id": "UR0bd696624e844d6ba5bfc248ba1eca11",
    "type": "users",
    "attributes": {
      "active_org": "{ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{ORG_1}": {
          "name": "Example organization A",
          "admin": true,
          "active": true,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_audiencemanager_int",
            "dma_tartan",
            "dma_dtm",
            "dma_reactor",
            "dma_auditor"
          ],
          "tenant_id": "{TENANT_ID_1}"
        },
        "{ORG_2}": {
          "name": "Example organization B",
          "admin": false,
          "active": false,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_reactor",
            "dma_auditor",
            "dma_tartan"
          ],
          "tenant_id": "{TENANT_ID_2}"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/profile"
    },
    "meta": {
      "rights": [
        "manage_companies"
      ]
    }
  }
}
```
