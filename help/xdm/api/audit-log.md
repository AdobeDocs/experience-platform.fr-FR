---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;audit;journal d’audit;changelog;journal des modifications;rpc;
solution: Experience Platform
title: Point de terminaison de l’API du journal d’audit
description: Le point de terminaison /auditlog de l’API Schema Registry vous permet de récupérer une liste chronologique des modifications apportées à une ressource XDM existante.
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 13%

---

# Point d’entrée du journal d’audit

Pour chaque ressource de modèle de données d’expérience (XDM), [!DNL Schema Registry] conserve un journal de toutes les modifications qui se sont produites entre différentes mises à jour. Le point d’entrée `/auditlog` de l’API [!DNL Schema Registry] vous permet de récupérer un journal d’audit pour toute classe, groupe de champs de schéma, type de données ou schéma spécifié par l’ID.

## Commencer

Le point de terminaison utilisé dans ce guide fait partie de l’ [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

Le point d’entrée `/auditlog` fait partie des appels de procédure distante (RPC) pris en charge par [!DNL Schema Registry]. Contrairement à d’autres points de terminaison dans l’API [!DNL Schema Registry], les points de terminaison RPC ne nécessitent pas d’en-têtes supplémentaires tels que `Accept` ou `Content-Type` et n’utilisent pas un `CONTAINER_ID`. Au lieu de cela, ils doivent utiliser l’espace de noms `/rpc`, comme illustré dans l’appel API ci-dessous.

## Récupération d’un journal d’audit pour une ressource

Vous pouvez récupérer un journal d’audit pour n’importe quelle classe, groupe de champs, type de données ou schéma dans la bibliothèque de schémas en spécifiant l’identifiant de la ressource dans le chemin d’accès d’une requête de GET au point de terminaison `/auditlog`.

**Format d’API**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_ID}` | `meta:altId` ou encodé URL `$id` de la ressource dont vous souhaitez récupérer le journal d’audit. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère le journal d’audit pour un schéma.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste chronologique des modifications apportées à la ressource, de la plus récente au moins récente.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "a14NMF0jd6BIfyXaHdTDl4bC4R0r9rht",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
        "xdmType": "schemas",
        "action": "remove",
        "path": "/meta:usageCount",
        "value": 0
      }
    ]
  },
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "pFQbgmWrdbJrNB9GdxTSGECpXYWspu68",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltySunday_ABC",
        "value": {
          "title": "LoyaltySundayABC",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltyMoxee_XYZ",
        "value": {
          "title": "LoyaltyMoxeeXYZ",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      }
    ]
  }
]
```

| Propriété | Description |
| --- | --- |
| `updates` | Tableau d’objets, chaque objet représentant une modification apportée à la ressource spécifiée ou à l’une de ses ressources dépendantes. |
| `id` | `$id` de la ressource qui a été modifiée. Cette valeur représente généralement la ressource spécifiée dans le chemin de requête, mais peut représenter une ressource dépendante si c’est la source de la modification. |
| `xdmType` | Type de ressource qui a été modifié. |
| `action` | Le type de modification qui a été apporté. |
| `path` | Chaîne [JSON Pointer](../../landing/api-fundamentals.md#json-pointer) indiquant le chemin d’accès au champ spécifique qui a été modifié ou ajouté. |
| `value` | Valeur affectée au champ nouveau ou mis à jour. |

{style="table-layout:auto"}
