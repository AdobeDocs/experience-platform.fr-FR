---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;audit;journal d’audit;changelog;journal des modifications;rpc;
solution: Experience Platform
title: Point de terminaison de l’API du journal d’audit
description: Le point de terminaison /auditlog de l’API Schema Registry vous permet de récupérer une liste chronologique des modifications apportées à une ressource XDM existante.
topic-legacy: developer guide
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 6%

---

# Point d’entrée du journal d’audit

Pour chaque ressource de modèle de données d’expérience (XDM), [!DNL Schema Registry] conserve un journal de toutes les modifications qui se sont produites entre différentes mises à jour. Le point de terminaison `/auditlog` de l’API [!DNL Schema Registry] vous permet de récupérer un journal d’audit pour toute classe, groupe de champs de schéma, type de données ou schéma spécifié par l’ID.

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l’[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture d’exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir les appels à une API Experience Platform.

Le point de terminaison `/auditlog` fait partie des appels de procédure distante (RPC) pris en charge par [!DNL Schema Registry]. Contrairement aux autres points de terminaison de l’API [!DNL Schema Registry], les points de terminaison RPC ne nécessitent pas d’en-têtes supplémentaires tels que `Accept` ou `Content-Type` et n’utilisent pas de `CONTAINER_ID`. Ils doivent plutôt utiliser l’espace de noms `/rpc`, comme illustré dans l’appel API ci-dessous.

## Récupération d’un journal d’audit pour une ressource

Vous pouvez récupérer un journal d’audit pour n’importe quelle classe, groupe de champs, type de données ou schéma dans la bibliothèque de schémas en spécifiant l’identifiant de la ressource dans le chemin d’accès d’une requête de GET au point de terminaison `/auditlog`.

**Format d’API**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_ID}` | `meta:altId` ou `$id` encodé URL de la ressource dont vous souhaitez récupérer le journal d’audit. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante récupère le journal d’audit pour un groupe de champs `Restaurant`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.fieldgroups.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste chronologique des modifications apportées à la ressource, de la plus récente au moins récente.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
    "auditTrails": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "fieldgroups",
        "action": "add",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/brand",
        "value": {
          "title": "Brand",
          "description": "",
          "type": "string",
          "isRequired": false,
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "fieldgroups",
        "action": "add",
        "path": "/meta:usageCount",
        "value": 0
      }
    ],
    "updatedUser": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 1606255582281,
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "{SANDBOX_ID}"
  }
]
```

| Propriété | Description |
| --- | --- |
| `auditTrails` | Tableau d’objets, chaque objet représentant une modification apportée à la ressource spécifiée ou à l’une de ses ressources dépendantes. |
| `id` | `$id` de la ressource qui a été modifiée. Cette valeur représente généralement la ressource spécifiée dans le chemin de requête, mais peut représenter une ressource dépendante si c’est la source de la modification. |
| `action` | Le type de modification qui a été apporté. |
| `path` | Chaîne [JSON Pointer](../../landing/api-fundamentals.md#json-pointer) indiquant le chemin d’accès au champ spécifique qui a été modifié ou ajouté. |
| `value` | Valeur affectée au champ nouveau ou mis à jour. |

{style=&quot;table-layout:auto&quot;}
