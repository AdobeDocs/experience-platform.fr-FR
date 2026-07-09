---
title: Point d’entrée des profils
description: Découvrez comment effectuer des appels vers le point d’entrée /profiles dans l’API Reactor.
exl-id: d0434098-f49a-45f3-9772-488bd3c134aa
TQID: https://experienceleague.adobe.com/qmx6UXQJvXkpRrmY3S5djSvzUMcfji2c8vTCYF7IFR8
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 9eb5b266c15495d852a671829d46fd127ad33ac9
workflow-type: tm+mt
source-wordcount: 172
ht-degree: 74%

---

# Point d’entrée de profil

Dans l’API Reactor, un profil représente un utilisateur d’Adobe Experience Platform. L’API Reactor ne conserve pas sa propre base de données d’utilisateurs et d’autorisations. Elle repose plutôt sur les Adobe ID gérés par [le système IMS (Identity Management System)](https://helpx.adobe.com/fr/enterprise/using/identity.html) d’Adobe.

Un profil contient toutes les informations sur l’utilisateur connecté, y compris toutes les organisations auxquelles il appartient, les profils de produit auxquels il appartient au sein de chaque organisation ainsi que les droits dont il dispose sur chaque profil de produit.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://developer.adobe.com/experience-platform-apis/references/reactor). Avant de poursuivre, veuillez consulter le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la façon de s’authentifier auprès de l’API.

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
