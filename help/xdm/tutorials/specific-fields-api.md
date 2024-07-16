---
title: Ajouter des champs spécifiques à un schéma à l’aide de l’API Schema Registry
description: Découvrez comment ajouter des champs individuels de groupes de champs préexistants à un schéma de modèle de données d’expérience (XDM) à l’aide de l’API Schema Registry.
exl-id: 696cce2b-bbde-416a-9f52-12ab4da9c2c6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 100%

---

# Ajouter des champs spécifiques à un schéma à l’aide de l’API Schema Registry

Les schémas de modèle de données d’expérience (XDM) sont composés d’une classe de base, avec des champs supplémentaires inclus par le biais de l’utilisation de groupes de champs standard définis par les groupes de champs personnalisés et d’Adobe définis par votre organisation.

Lors de la création d’un schéma, vous pouvez utiliser certains champs d’un groupe de champs donné tout en excluant d’autres champs du même groupe dont vous n’avez pas besoin. Ce tutoriel vous explique comment ajouter des champs individuels d’un groupe de champs à un schéma à l’aide de l’API Schema Registry.

>[!NOTE]
>
>Pour plus d’informations sur l’ajout et la suppression de champs de schéma individuels dans l’interface utilisateur d’Adobe Experience Platform, consultez le guide sur les [workflows basés sur les champs](../ui/field-based-workflows.md) (actuellement en version bêta).

## Conditions préalables

Ce tutoriel implique d’effectuer des appels à l’[API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Avant de commencer, veuillez consulter le [guide de développement](../api/getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris votre `{TENANT_ID}`, le concept de conteneurs et les en-têtes requis pour effectuer des requêtes.

## Comprendre le champ `meta:refProperty`

Pour tout schéma donné, les groupes de classes et de champs qui constituent sa structure sont référencés sous son tableau `allOf`. Chaque composant est représenté sous la forme d’un objet contenant une propriété `$ref` qui fait référence à l’URI du composant `$id`.

Le fichier JSON suivant représente un schéma simplifié qui utilise une seule classe (`experienceevent`) et un seul groupe de champs (`experienceevent-all`) :

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all"
    }
  ]
}
```

Pour tout objet dans le tableau `allOf` qui fait référence à un groupe de champs, vous pouvez ajouter un champ `meta:refProperty` frère pour spécifier le ou les champs du groupe à inclure dans le schéma.

>[!NOTE]
>
>Chaque champ est spécifié à l’aide d’une chaîne JSON Pointer, représentant le chemin d’accès au champ dans son groupe de champs respectif. La chaîne doit commencer par une barre oblique (`/`) et ne doit pas inclure d’espaces de noms `properties`. Par exemple : `/_experience/campaign/message/id`.

Lorsqu’elle est incluse en tant que chaîne, `meta:refProperty` peut faire référence à un champ unique d’un groupe. Les autres champs du même groupe peuvent être inclus en utilisant la même valeur `$ref` dans un autre objet avec une valeur `meta:refProperty` différente.

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/id"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/size"
    }
  ]
}
```

Alternativement, `meta:refProperty` peut être fourni sous la forme d’un tableau, ce qui vous permet de spécifier plusieurs champs à inclure à partir d’un groupe donné au sein d’un seul élément de liste `allOf` :

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ]
}
```

## Ajouter des champs à l’aide d’une opération PUT

Vous pouvez utiliser une requête PUT pour réécrire un schéma entier et configurer les champs que vous souhaitez inclure sous `allOf`.

**Format d’API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | Le `meta:altId` ou le `$id` encodé URL du schéma que vous souhaitez réécrire. |

**Requête**

La requête suivante met à jour les champs spécifiques inclus dans le groupe de champs sous le tableau `allOf`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "title": "My Sample Schema",
        "description": "My Sample Description",
        "type": "object",
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
          },
          {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        ]
      }'
```

**Réponse**

Une réponse réussie renvoie les détails du schéma mis à jour.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>Pour plus d’informations sur les requêtes PUT pour les schémas, reportez-vous au [guide sur les points d’entrée des schémas](../api/schemas.md#put).

## Ajouter des champs à l’aide d’une opération PATCH

Vous pouvez utiliser une requête PATCH pour ajouter des champs individuels à un schéma sans remplacer les autres. Le registre des schémas prend en charge toutes les opérations standard JSON Patch, notamment `add`, `remove` et `replace`. Pour plus d’informations sur le correctif JSON, voir [Guide de base des API](../../landing/api-fundamentals.md#json-patch).

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | Le `meta:altId` ou le `$id` encodé URL du schéma que vous souhaitez réécrire. |

**Requête**

La requête suivante ajoute un nouvel objet au tableau `allOf` du schéma, spécifiant les champs à ajouter.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        }
      ]'
```

**Réponse**

Une réponse réussie renvoie les détails du schéma mis à jour.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>Pour plus d’informations sur les requêtes PATCH pour les schémas, reportez-vous au [guide sur les points d’entrée des schémas](../api/schemas.md#patch).

## Étapes suivantes

Ce guide explique comment utiliser les appels API pour ajouter des champs individuels d’un groupe de champs existant à un schéma. Pour plus d’informations sur l’exécution de tâches similaires basées sur des champs dans l’interface utilisateur de Platform, consultez le guide sur les [workflows basés sur les champs](../ui/field-based-workflows.md).

Pour plus d’informations sur les fonctionnalités de l’API Schema Registry, reportez-vous à la [Présentation des API](../api/overview.md) pour obtenir une liste complète des points d’entrée et processus.
