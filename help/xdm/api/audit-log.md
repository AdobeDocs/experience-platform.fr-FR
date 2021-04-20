---
keywords: Experience Platform ; accueil ; rubriques populaires ; api ; API ; XDM ; système XDM ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données ; modèle de données ; audit ; journal d’audit ; changelog ; journal de modifications ; rpc ;
solution: Experience Platform
title: Point de terminaison de l’API du journal d’audit
description: Le point de terminaison /auditlog de l'API de registre de Schéma vous permet de récupérer une liste chronologique des modifications apportées à une ressource XDM existante.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0727ffa0c72bcb6a85de1a13215b691b97889b70
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 4%

---


# Point de terminaison du journal d&#39;audit

Pour chaque ressource de modèle de données d’expérience (XDM), [!DNL Schema Registry] conserve un journal de toutes les modifications survenues entre différentes mises à jour. Le point de terminaison `/auditlog` de l&#39;API [!DNL Schema Registry] vous permet de récupérer un journal d&#39;audit pour toute classe, mixin, type de données ou schéma spécifié par l&#39;ID.

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l&#39;[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API Experience Platform.

Le point de terminaison `/auditlog` fait partie des appels de procédure distante (RPC) pris en charge par [!DNL Schema Registry]. Contrairement aux autres points de terminaison de l&#39;API [!DNL Schema Registry], les points de terminaison RPC ne nécessitent pas d&#39;en-têtes supplémentaires tels que `Accept` ou `Content-Type` et n&#39;utilisent pas de `CONTAINER_ID`. Ils doivent plutôt utiliser l&#39;espace de nommage `/rpc`, comme indiqué dans l&#39;appel d&#39;API ci-dessous.

## Récupérer un journal d&#39;audit pour une ressource

Vous pouvez récupérer un journal d&#39;audit pour n&#39;importe quelle classe, mixin, type de données ou schéma dans la bibliothèque de Schémas en spécifiant l&#39;identifiant de la ressource dans le chemin d&#39;accès d&#39;une demande de GET au point de terminaison `/auditlog`.

**Format d’API**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_ID}` | `meta:altId` ou encodé en URL `$id` de la ressource dont vous souhaitez récupérer le journal d&#39;audit. |

**Requête**

La requête suivante récupère le journal d&#39;audit pour un mixin `Restaurant`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive renvoie une liste chronologique des changements apportés à la ressource, du plus récent au moins récent.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
    "auditTrails": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
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
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
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
| `auditTrails` | Tableau d&#39;objets, avec chaque objet représentant une modification apportée à la ressource spécifiée ou à l&#39;une de ses ressources dépendantes. |
| `id` | `$id` de la ressource qui a été modifiée. Cette valeur représente généralement la ressource spécifiée dans le chemin de requête, mais peut représenter une ressource dépendante si c&#39;est la source de la modification. |
| `action` | Type de changement qui a été effectué. |
| `path` | Chaîne [Pointeur JSON](../../landing/api-fundamentals.md#json-pointer) indiquant le chemin d’accès au champ spécifique qui a été modifié ou ajouté. |
| `value` | Valeur affectée au champ nouveau ou mis à jour. |