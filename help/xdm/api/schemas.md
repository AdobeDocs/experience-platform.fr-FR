---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: Création d’un schéma
description: Le point de terminaison /schémas de l'API Schéma Registry vous permet de gérer par programmation les schémas XDM dans votre application d'expérience.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 20%

---


# Point de terminaison des schémas

Un schéma peut être considéré comme le schéma directeur des données que vous souhaitez intégrer à Adobe Experience Platform. Chaque schéma est composé d’une classe et de zéro ou plusieurs mixins. Le `/schemas` point de terminaison de l’ [!DNL Schema Registry] API vous permet de gérer par programmation les schémas dans votre application d’expérience.

## Prise en main

The API endpoint used in this guide is part of the [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Avant de continuer, consultez le guide [de](./getting-started.md) prise en main pour obtenir des liens vers la documentation connexe, un guide pour lire les exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API Experience Platform.

## Retrieve a list of schemas {#list}

Vous pouvez liste tous les schémas sous le `global` ou le `tenant` conteneur en adressant une demande de GET à `/global/schemas` ou `/tenant/schemas`, respectivement.

>[!NOTE]
>
>Lors de la mise en vente de ressources, le Registre des Schémas limite les résultats à 300 éléments. Pour renvoyer des ressources au-delà de cette limite, vous devez utiliser des paramètres de pagination. Il est également recommandé d’utiliser des paramètres de requête supplémentaires pour filtrer les résultats et réduire le nombre de ressources renvoyées. Pour plus d&#39;informations, consultez la section sur les paramètres [de](./appendix.md#query) requête dans le document de l&#39;appendice.

**Format d’API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur qui héberge les schémas à récupérer : `global` pour les schémas créés par Adobe ou `tenant` pour les schémas appartenant à votre organisation. |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs en fonction desquels filtrer les résultats. Pour obtenir une liste des paramètres disponibles, reportez-vous au document [](./appendix.md#query) annexe. |

**Requête**

La requête suivante récupère une liste de schémas du `tenant` conteneur, en utilisant un paramètre `orderby` de requête pour trier les résultats selon leur `title` attribut.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

The response format depends on the `Accept` header sent in the request. The following `Accept` headers are available for listing schemas:

| En-tête `Accept` | Description |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Renvoie un bref résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour la liste des ressources. (Limite : 300) |
| `application/vnd.adobe.xed+json` | Renvoie la totalité du schéma JSON de chaque ressource, en incluant le `$ref` et l’`allOf` d’origine. (Limite : 300) |

**Réponse**

The request above used the `application/vnd.adobe.xed-id+json` `Accept` header, therefore the response includes only the `title`, `$id`, `meta:altId`, and `version` attributes for each schema. L’utilisation de l’autre `Accept` en-tête (`application/vnd.adobe.xed+json`) renvoie tous les attributs de chaque schéma. Select the appropriate `Accept` header depending on the information you require in your response.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0238be93d3e7a06aec5e0655955901ec",
      "meta:altId": "_{TENANT_ID}.schemas.0238be93d3e7a06aec5e0655955901ec",
      "version": "1.4",
      "title": "Hotels"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0ef4ce0d390f0809fad490802f53d30b",
      "meta:altId": "_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b",
      "version": "1.0",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
        "orderby": "title",
        "next": null,
        "count": 2
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

## Recherche d’un schéma {#lookup}

Vous pouvez rechercher un schéma spécifique en faisant une demande de GET qui inclut l’identifiant du schéma dans le chemin d’accès.

**Format d’API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur qui héberge le schéma à récupérer : `global` pour un schéma créé par un Adobe ou `tenant` pour un schéma appartenant à votre organisation. |
| `{SCHEMA_ID}` | Le code `meta:altId` ou URL `$id` du schéma que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère un schéma spécifié par sa `meta:altId` valeur dans le chemin d’accès.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

The response format depends on the `Accept` header sent in the request. All lookup requests require a `version` be included in the `Accept` header. The following `Accept` headers are available:

| En-tête `Accept` | Description |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Brut avec `$ref` et `allOf`, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolus, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Brut avec `$ref` et `allOf`, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolus, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolus, contient des descripteurs. |

**Réponse**

Une réponse réussie renvoie les détails du schéma. The fields that are returned depend on the `Accept` header sent in the request. Experiment with different `Accept` headers to compare the responses and determine which header is best for your use case.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:altId": "_{TENANT_ID}.schemas.20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Example schema",
  "type": "object",
  "description": "An example schema created within the tenant container.",
  "allOf": [
      {
          "$ref": "https://ns.adobe.com/xdm/context/profile",
          "type": "object",
          "meta:xdmType": "object"
      },
      {
          "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
      "repo:createdDate": 1602872911226,
      "repo:lastModifiedDate": 1603381419889,
      "xdm:createdClientId": "{CLIENT_ID}",
      "xdm:lastModifiedClientId": "{CLIENT_ID}",
      "xdm:createdUserId": "{USER_ID}",
      "xdm:lastModifiedUserId": "{USER_ID}",
      "eTag": "84b4da79b7445a4bf1c59269e718065effddb983c492f48e223d49c049c6d589",
      "meta:globalLibVersion": "1.15.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Création d’un schéma {#create}

Le processus de composition d’un schéma commence par l’affectation d’une classe. La classe définit les principaux aspects comportementaux des données (enregistrement ou série temporelle), ainsi que les champs minimaux requis pour décrire les données qui seront assimilées.

>[!NOTE]
>
>L&#39;exemple d&#39;appel ci-dessous n&#39;est qu&#39;un exemple de base de la façon de créer un schéma dans l&#39;API, avec les exigences minimales de composition d&#39;une classe et pas de mixins. Pour obtenir des instructions complètes sur la création d’un schéma dans l’API, y compris sur l’affectation de champs à l’aide de mixins et de types de données, consultez le didacticiel [sur la création de](../tutorials/create-schema-api.md)schémas.

**Format d’API**

```http
POST /tenant/schemas
```

**Requête**

La requête doit inclure un attribut `allOf` qui fait référence à la clé `$id` d’une classe. Cet attribut définit la « classe de base » que le schéma va mettre en œuvre. Dans cet exemple, la classe de base est une classe « Informations sur les propriétés », qui a été créée précédemment.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `allOf` | Tableau d’objets, chaque objet faisant référence à une classe ou à un mixin dont les champs sont implémentés par le schéma. Chaque objet contient une seule propriété (`$ref`) dont la valeur représente la valeur `$id` de la classe ou du mixin que le nouveau schéma implémentera. Une classe doit être fournie, avec zéro ou plusieurs mixins supplémentaires. Dans l&#39;exemple ci-dessus, l&#39;objet unique du `allOf` tableau est la classe de schéma. |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Créé) et un payload qui contient les détails du schéma créé, y compris le `$id`, l’`meta:altId` et la `version`. These values are read-only and are assigned by the [!DNL Schema Registry].

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Performing a GET request to [list all schemas](#list) in the tenant container would now include the new schema. You can perform a [lookup (GET) request](#lookup) using the URL-encoded `$id` URI to view the new schema directly.

Pour ajouter des champs supplémentaires à un schéma, vous pouvez effectuer une opération [](#patch) PATCH pour ajouter des mixins au schéma `allOf` et aux `meta:extends` baies.

## Mettre à jour un schéma {#put}

Vous pouvez remplacer un schéma entier par une opération de PUT, en réécrivant essentiellement la ressource. Lors de la mise à jour d’un schéma par le biais d’une requête de PUT, le corps doit inclure tous les champs requis lors de la [création d’un nouveau schéma](#create) dans une requête de POST.

>[!NOTE]
>
>If you only want to update part of a schema instead of replacing it entirely, see the section on [updating a portion of a schema](#patch).

**Format d’API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | Codé `meta:altId` ou URL `$id` du schéma que vous souhaitez réécrire. |

**Requête**

La requête suivante remplace un schéma existant, en modifiant ses `title`, `description`et `allOf` attributs.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Commercial Property Information",
        "description": "Information related to commercial properties.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7" 
          } 
        ]
      }'
```

**Réponse**

Une réponse réussie renvoie les détails du schéma mis à jour.

```JSON
{
    "title":"Commercial Property Information",
    "description": "Information related to commercial properties.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
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

## Update a portion of a schema {#patch}

Vous pouvez mettre à jour une partie d’un schéma à l’aide d’une requête de PATCH. Il [!DNL Schema Registry] prend en charge toutes les opérations de correctif JSON standard, y compris `add`, `remove`et `replace`. Pour plus d’informations sur le correctif JSON, voir le guide [des fondamentaux de l’](../../landing/api-fundamentals.md#json-patch)API.

>[!NOTE]
>
>If you want to replace an entire resource with new values instead of updating individual fields, see the section on [replacing a schema using a PUT operation](#put).

L&#39;une des opérations de PATCH les plus courantes consiste à ajouter des mixins précédemment définis à un schéma, comme le montre l&#39;exemple ci-dessous.

**Format d’API**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | The URL-encoded `$id` URI or `meta:altId` of the schema you want to update. |

**Requête**

L’exemple de demande ci-dessous ajoute un nouveau mixin à un schéma en ajoutant la `$id` valeur de ce mixin aux `meta:extends` et `allOf` baies.

Le corps de la requête prend la forme d&#39;un tableau, chaque objet répertorié représentant une modification spécifique à un champ individuel. Chaque objet comprend l&#39;opération à exécuter (`op`), le champ sur lequel l&#39;opération doit être exécutée (`path`) et les informations à inclure dans cette opération (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/meta:extends/-",
          "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
      ]'
```

**Réponse**

La réponse montre que les deux opérations ont été réalisées avec succès. Le mixin `$id` a été ajouté au tableau `meta:extends` et une référence (`$ref`) au mixin `$id` apparaît désormais dans le tableau `allOf`.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Enable a schema for use in Real-time Customer Profile {#union}

Pour qu’un schéma puisse participer au Profil [client en temps](../../profile/home.md)réel, vous devez ajouter une `union` balise au tableau `meta:immutableTags` de schémas. Pour ce faire, vous pouvez faire une demande de PATCH pour le schéma en question.

>[!IMPORTANT]
>
>Les balises immuables sont des balises destinées à être configurées, mais jamais supprimées.

**Format d’API**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | The URL-encoded `$id` URI or `meta:altId` of the schema you want to enable. |

**Requête**

L&#39;exemple de requête ci-dessous ajoute un `meta:immutableTags` tableau à un schéma existant, ce qui lui donne une valeur de chaîne unique de `union` pour l&#39;activer pour l&#39;utiliser dans le Profil.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/meta:immutableTags",
          "value": ["union"]
        }
      ]'
```

**Réponse**

Une réponse réussie renvoie les détails du schéma mis à jour, indiquant que la `meta:immutableTags` baie a été ajoutée.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:immutableTags": [
      "union"
    ]
}
```

Vous pouvez maintenant vue l’union de cette classe de schéma pour confirmer que les champs du schéma sont représentés. See the [unions endpoint guide](./unions.md) for more information.

## Suppression d’un schéma {#delete}

Il peut parfois être nécessaire de retirer un schéma du Registre des Schémas. Pour ce faire, il effectue une demande de DELETE avec l’ID de schéma fourni dans le chemin d’accès.

**Format d’API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | The URL-encoded `$id` URI or `meta:altId` of the schema you want to delete. |

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant d’envoyer une demande de recherche (GET) au schéma. You will need to include an `Accept` header in the request, but should receive an HTTP status 404 (Not Found) because the schema has been removed from the Schema Registry.