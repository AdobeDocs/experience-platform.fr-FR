---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre des schémas;schéma;schéma;schémas;schémas;schémas;créer
solution: Experience Platform
title: Point d’entrée de l’API Schemas
description: Le point de terminaison /schemas de l’API Schema Registry vous permet de gérer par programmation les schémas XDM dans votre application d’expérience.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 20%

---

# Point d’entrée des schémas

Un schéma peut être considéré comme le plan directeur des données que vous souhaitez ingérer dans Adobe Experience Platform. Chaque schéma est composé d’une classe et de zéro ou plusieurs groupes de champs de schéma. Le point d’entrée `/schemas` de l’API [!DNL Schema Registry] vous permet de gérer par programmation les schémas dans votre application d’expérience.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼ [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupération d’une liste de schémas {#list}

Vous pouvez répertorier tous les schémas sous le conteneur `global` ou `tenant` en effectuant une requête de GET vers `/global/schemas` ou `/tenant/schemas`, respectivement.

>[!NOTE]
>
>Lors de l’énumération des ressources, le registre des schémas limite les résultats à 300 éléments. Pour renvoyer des ressources au-delà de cette limite, vous devez utiliser des paramètres de pagination. Il est également recommandé d’utiliser des paramètres de requête supplémentaires pour filtrer les résultats et réduire le nombre de ressources renvoyées. Pour plus d’informations, consultez la section sur les [paramètres de requête](./appendix.md#query) dans le document de l’annexe.

**Format d’API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur qui héberge les schémas que vous souhaitez récupérer : `global` pour les schémas créés par l’Adobe ou `tenant` pour les schémas détenus par votre organisation. |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs pour filtrer les résultats. Consultez le [document de l’annexe](./appendix.md#query) pour obtenir la liste des paramètres disponibles. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère une liste de schémas du conteneur `tenant`, à l’aide d’un paramètre de requête `orderby` pour trier les résultats selon leur attribut `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Le format de la réponse dépend de l’en-tête `Accept` envoyé dans la requête. Les en-têtes `Accept` suivants sont disponibles pour répertorier les schémas :

| En-tête `Accept` | Description |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Renvoie un court résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour répertorier les ressources. (Limite : 300) |
| `application/vnd.adobe.xed+json` | Renvoie le schéma JSON complet pour chaque ressource, avec les `$ref` et `allOf` d&#39;origine inclus. (Limite : 300) |

{style="table-layout:auto"}

**Réponse**

La requête ci-dessus utilisait l’en-tête `application/vnd.adobe.xed-id+json` `Accept`. Par conséquent, la réponse inclut uniquement les attributs `title`, `$id`, `meta:altId` et `version` pour chaque schéma. L’utilisation de l’autre en-tête `Accept` (`application/vnd.adobe.xed+json`) renvoie tous les attributs de chaque schéma. Sélectionnez l’en-tête `Accept` approprié en fonction des informations dont vous avez besoin dans votre réponse.

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

Vous pouvez rechercher un schéma spécifique en effectuant une requête de GET qui inclut l’identifiant du schéma dans le chemin d’accès.

**Format d’API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur qui héberge le schéma que vous souhaitez récupérer : `global` pour un schéma créé par l’Adobe ou `tenant` pour un schéma détenu par votre organisation. |
| `{SCHEMA_ID}` | `meta:altId` ou encodé URL `$id` du schéma que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère un schéma spécifié par sa valeur `meta:altId` dans le chemin d’accès.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Le format de la réponse dépend de l’en-tête `Accept` envoyé dans la requête. Toutes les requêtes de recherche nécessitent qu’un `version` soit inclus dans l’en-tête `Accept`. Les en-têtes `Accept` suivants sont disponibles :

| En-tête `Accept` | Description |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Brut avec `$ref` et `allOf`, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` et `allOf` résolus, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-notext+json; version=1` | Brut avec `$ref` et `allOf`, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` et `allOf` résolus, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` et `allOf` résolus, contient des descripteurs. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` et `allOf` résolus, contient des titres et des descriptions. Les champs obsolètes sont indiqués avec un attribut `meta:status` de `deprecated`. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails du schéma. Les champs renvoyés dépendent de l’en-tête `Accept` envoyé dans la requête. Testez différents en-têtes `Accept` pour comparer les réponses et déterminer l’en-tête qui convient le mieux à votre cas d’utilisation.

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
  "imsOrg": "{ORG_ID}",
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

## Créer un schéma {#create}

Le processus de composition d’un schéma commence par l’affectation d’une classe. La classe définit les principaux aspects comportementaux des données (enregistrement ou série temporelle), ainsi que les champs minimaux requis pour décrire les données qui seront assimilées.

>[!NOTE]
>
>L’exemple d’appel ci-dessous n’est qu’un exemple de base de la création d’un schéma dans l’API, avec les exigences de composition minimales d’une classe et aucun groupe de champs. Pour obtenir des instructions complètes sur la création d’un schéma dans l’API, y compris sur l’affectation de champs à l’aide de groupes de champs et de types de données, consultez le [tutoriel sur la création de schémas](../tutorials/create-schema-api.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `allOf` | Tableau d’objets, chaque objet faisant référence à une classe ou à un groupe de champs dont les champs sont implémentés par le schéma. Chaque objet contient une propriété unique (`$ref`) dont la valeur représente le `$id` de la classe ou du groupe de champs que le nouveau schéma va implémenter. Une classe doit être fournie avec zéro ou plusieurs groupes de champs supplémentaires. Dans l’exemple ci-dessus, l’objet unique du tableau `allOf` est la classe du schéma. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Créé) et un payload qui contient les détails du schéma créé, y compris le `$id`, l’`meta:altId` et la `version`. Ces valeurs sont en lecture seule et sont attribuées par le [!DNL Schema Registry].

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
    "imsOrg": "{ORG_ID}",
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

L’exécution d’une requête de GET à [répertorier tous les schémas](#list) dans le conteneur client inclurait désormais le nouveau schéma. Vous pouvez effectuer une [requête de recherche (GET)](#lookup) à l’aide de l’URI `$id` encodé URL pour afficher directement le nouveau schéma.

Pour ajouter des champs supplémentaires à un schéma, vous pouvez effectuer une [opération de PATCH](#patch) pour ajouter des groupes de champs aux tableaux `allOf` et `meta:extends` du schéma.

## Mettre à jour un schéma {#put}

Vous pouvez remplacer un schéma entier par le biais d’une opération de PUT, en réécrivant essentiellement la ressource. Lors de la mise à jour d’un schéma par le biais d’une requête de PUT, le corps doit inclure tous les champs requis lors de la [création d’un nouveau schéma](#create) dans une requête de POST.

>[!NOTE]
>
>Si vous souhaitez uniquement mettre à jour une partie d’un schéma au lieu de le remplacer entièrement, reportez-vous à la section sur la [mise à jour d’une partie d’un schéma](#patch).

**Format d’API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | `meta:altId` ou encodé URL `$id` du schéma que vous souhaitez réécrire. |

{style="table-layout:auto"}

**Requête**

La requête suivante remplace un schéma existant, en modifiant ses attributs `title`, `description` et `allOf`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Mettre à jour une partie d’un schéma {#patch}

Vous pouvez mettre à jour une partie d’un schéma à l’aide d’une requête de PATCH. [!DNL Schema Registry] prend en charge toutes les opérations JSON Patch standard, y compris `add`, `remove` et `replace`. Pour plus d’informations sur le correctif JSON, voir [Guide de base des API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Si vous souhaitez remplacer une ressource entière par de nouvelles valeurs au lieu de mettre à jour des champs individuels, reportez-vous à la section [Remplacement d’un schéma à l’aide d’une opération de PUT](#put).

L’une des opérations de PATCH les plus courantes consiste à ajouter des groupes de champs définis précédemment à un schéma, comme le montre l’exemple ci-dessous.

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` encodé URL ou `meta:altId` du schéma que vous souhaitez mettre à jour. |

{style="table-layout:auto"}

**Requête**

L’exemple de requête ci-dessous ajoute un nouveau groupe de champs à un schéma en ajoutant la valeur `$id` de ce groupe de champs aux tableaux `meta:extends` et `allOf`.

Le corps de la requête se présente sous la forme d’un tableau, chaque objet répertorié représentant une modification spécifique à un champ individuel. Chaque objet inclut l’opération à effectuer (`op`), le champ sur lequel l’opération doit être effectuée (`path`) et les informations qui doivent être incluses dans cette opération (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

La réponse montre que les deux opérations ont été réalisées avec succès. Le groupe de champs `$id` a été ajouté au tableau `meta:extends` et une référence (`$ref`) au groupe de champs `$id` apparaît désormais dans le tableau `allOf`.

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
    "imsOrg": "{ORG_ID}",
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

## Activation d’un schéma à utiliser dans Real-time Customer Profile {#union}

Pour qu’un schéma participe à [Real-Time Customer Profile](../../profile/home.md), vous devez ajouter une balise `union` au tableau `meta:immutableTags` du schéma. Pour ce faire, vous pouvez effectuer une requête de PATCH pour le schéma en question.

>[!IMPORTANT]
>
>Les balises immuables sont des balises destinées à être définies, mais jamais supprimées.

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` encodé URL ou `meta:altId` du schéma que vous souhaitez activer. |

{style="table-layout:auto"}

**Requête**

L’exemple de requête ci-dessous ajoute un tableau `meta:immutableTags` à un schéma existant, ce qui donne au tableau une seule valeur de chaîne `union` pour l’activer pour l’utiliser dans Profile.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Une réponse réussie renvoie les détails du schéma mis à jour, indiquant que le tableau `meta:immutableTags` a été ajouté.

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
    "imsOrg": "{ORG_ID}",
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

Vous pouvez maintenant afficher l’union de la classe de ce schéma pour confirmer que les champs du schéma sont représentés. Pour plus d’informations, consultez le [guide de point de terminaison d’unions](./unions.md) .

## Supprimer un schéma {#delete}

Il peut parfois être nécessaire de supprimer un schéma du registre des schémas. Pour ce faire, il vous suffit d’effectuer une requête de DELETE avec l’identifiant de schéma fourni dans le chemin d’accès.

**Format d’API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` encodé URL ou `meta:altId` du schéma que vous souhaitez supprimer. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) au schéma. Vous devez inclure un en-tête `Accept` dans la requête, mais vous devriez recevoir le statut HTTP 404 (Introuvable) car le schéma a été supprimé du registre des schémas.
