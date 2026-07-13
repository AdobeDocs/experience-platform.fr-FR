---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;audit;journal d’audit;journal des modifications;rpc;
solution: Experience Platform
title: Point d’entrée de l’API du journal d’audit
description: Le point d’entrée /auditlog dans l’API Schema Registry vous permet de récupérer une liste chronologique des modifications apportées à une ressource XDM existante.
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
TQID: https://experienceleague.adobe.com/AfEinzGCnILUsnkIdlbFyKB70HIIwF9zjLdQCB-UEag
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: ce1936c345751033beb6901536d6f56467d51fae
workflow-type: tm+mt
source-wordcount: 405
ht-degree: 12%

---

# Point d’entrée du journal d’audit

Pour chaque ressource du modèle de données d’expérience (XDM), le [!DNL Schema Registry] conserve un journal de toutes les modifications qui se sont produites entre différentes mises à jour. Le point d’entrée `/auditlog` de l’API [!DNL Schema Registry] vous permet de récupérer un journal d’audit pour n’importe quelle classe, groupe de champs de schéma, type de données ou schéma spécifié par l’ID.

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de l’API ](https://developer.adobe.com/experience-platform-apis/references/schema-registry). [[!DNL Schema Registry] Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

Le point d&#39;entrée `/auditlog` fait partie des appels de procédure distante (RPC) pris en charge par le [!DNL Schema Registry]. Contrairement aux autres points d&#39;entrée de l&#39;API [!DNL Schema Registry], les points d&#39;entrée RPC ne nécessitent pas d&#39;en-têtes supplémentaires tels que `Accept` ou `Content-Type`, et n&#39;utilisent pas de `CONTAINER_ID`. Ils doivent plutôt utiliser l’espace de noms `/rpc`, comme illustré dans l’appel API ci-dessous.

## Récupération d’un journal d’audit pour une ressource

Vous pouvez récupérer un journal d’audit pour n’importe quelle classe, groupe de champs, type de données ou schéma de la bibliothèque de schémas en spécifiant l’identifiant de la ressource dans le chemin d’accès d’une requête GET au point d’entrée `/auditlog`.

**Format d’API**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_ID}` | `$id` codée en `meta:altId` ou en URL de la ressource dont vous souhaitez récupérer le journal d’audit. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère le journal d’audit d’un schéma.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste chronologique des modifications apportées à la ressource, du plus récent au moins récent.

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
| `updates` | Tableau d’objets, où chaque objet représente une modification apportée à la ressource spécifiée ou à l’une de ses ressources dépendantes. |
| `id` | `$id` de la ressource qui a été modifiée. Cette valeur représente généralement la ressource spécifiée dans le chemin d’accès de la requête, mais peut représenter une ressource dépendante si c’est la source de la modification. |
| `xdmType` | Type de ressource qui a été modifié. |
| `action` | Type de changement qui a été apporté. |
| `path` | Chaîne [pointeur JSON](../../landing/api-fundamentals.md#json-pointer) indiquant le chemin d’accès au champ spécifique qui a été modifié ou ajouté. |
| `value` | Valeur affectée au champ nouveau ou mis à jour. |

{style="table-layout:auto"}


