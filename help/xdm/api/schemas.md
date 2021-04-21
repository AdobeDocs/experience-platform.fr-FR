---
keywords: Experience Platform ; accueil ; rubriques populaires ; api ; API ; XDM ; système XDM ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données ; modèle de données ; modèle de données ; registre des schémas ; registre des Schémas ; schéma ; Schéma ; schémas ; Schémas ; créer
solution: Experience Platform
title: Point de terminaison de l'API schémas
description: Le point de terminaison /schémas de l'API Schéma Registry vous permet de gérer par programmation les schémas XDM dans votre application d'expérience.
topic-legacy: developer guide
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 19%

---

# Point de terminaison des schémas

Un schéma peut être considéré comme le schéma directeur des données que vous souhaitez intégrer à Adobe Experience Platform. Chaque schéma est composé d’une classe et de zéro ou plusieurs mixins. Le point de terminaison `/schemas` de l&#39;API [!DNL Schema Registry] vous permet de gérer par programmation les schémas dans votre application d&#39;expérience.

## Prise en main

Le point de terminaison API utilisé dans ce guide fait partie de l&#39;[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API Experience Platform.

## Récupérer une liste de schémas {#list}

Vous pouvez liste tous les schémas sous le conteneur `global` ou `tenant` en adressant une demande de GET à `/global/schemas` ou `/tenant/schemas`, respectivement.

>[!NOTE]
>
>Lors de la mise en vente de ressources, le Registre des Schémas limite les résultats à 300 éléments. Pour renvoyer des ressources au-delà de cette limite, vous devez utiliser des paramètres de pagination. Il est également recommandé d’utiliser des paramètres de requête supplémentaires pour filtrer les résultats et réduire le nombre de ressources renvoyées. Pour plus d&#39;informations, consultez la section [Paramètres de requête](./appendix.md#query) dans le document de l&#39;annexe.

**Format d’API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur qui héberge les schémas à récupérer : `global` pour les schémas créés par Adobe ou `tenant` pour les schémas appartenant à votre organisation. |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs en fonction desquels filtrer les résultats. Pour obtenir une liste des paramètres disponibles, consultez l&#39;[document ](./appendix.md#query) de l&#39;appendice. |

**Requête**

La requête suivante récupère une liste de schémas du conteneur `tenant`, en utilisant un paramètre de requête `orderby` pour trier les résultats selon leur attribut `title`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Le format de réponse dépend de l&#39;en-tête `Accept` envoyé dans la demande. Les en-têtes `Accept` suivants sont disponibles pour les schémas de liste :

| En-tête `Accept` | Description |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Renvoie un bref résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour la liste des ressources. (Limite : 300) |
| `application/vnd.adobe.xed+json` | Renvoie la totalité du schéma JSON de chaque ressource, en incluant le `$ref` et l’`allOf` d’origine. (Limite : 300) |

**Réponse**

La requête ci-dessus utilisait l&#39;en-tête `application/vnd.adobe.xed-id+json` `Accept`. Par conséquent, la réponse ne comprend que les attributs `title`, `$id`, `meta:altId` et `version` pour chaque schéma. L’utilisation de l’autre en-tête `Accept` (`application/vnd.adobe.xed+json`) renvoie tous les attributs de chaque schéma. Sélectionnez l&#39;en-tête `Accept` approprié en fonction des informations que vous souhaitez obtenir dans votre réponse.

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
| `{SCHEMA_ID}` | `meta:altId` ou `$id` codé URL du schéma que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère un schéma spécifié par sa valeur `meta:altId` dans le chemin d’accès.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Le format de réponse dépend de l&#39;en-tête `Accept` envoyé dans la demande. Toutes les requêtes de recherche nécessitent l&#39;inclusion de `version` dans l&#39;en-tête `Accept`. Les en-têtes `Accept` suivants sont disponibles :

| En-tête `Accept` | Description |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Brut avec `$ref` et `allOf`, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` et `allOf` résolus, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-notext+json; version=1` | Brut avec `$ref` et `allOf`, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` et `allOf` résolus, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` et `allOf` résolus, contient des descripteurs. |

**Réponse**

Une réponse réussie renvoie les détails du schéma. Les champs renvoyés dépendent de l&#39;en-tête `Accept` envoyé dans la demande. Testez différents en-têtes `Accept` pour comparer les réponses et déterminer l&#39;en-tête qui convient le mieux à votre cas d&#39;utilisation.

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
>L&#39;exemple d&#39;appel ci-dessous n&#39;est qu&#39;un exemple de base de la façon de créer un schéma dans l&#39;API, avec les exigences minimales de composition d&#39;une classe et pas de mixins. Pour obtenir des instructions complètes sur la création d’un schéma dans l’API, y compris sur l’affectation de champs à l’aide de mixins et de types de données, consultez le [didacticiel sur la création de schéma](../tutorials/create-schema-api.md).

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
| `allOf` | Tableau d’objets, chaque objet faisant référence à une classe ou à un mixin dont les champs sont implémentés par le schéma. Chaque objet contient une propriété unique (`$ref`) dont la valeur représente `$id` de la classe ou du mixin que le nouveau schéma implémentera. Une classe doit être fournie, avec zéro ou plusieurs mixins supplémentaires. Dans l&#39;exemple ci-dessus, l&#39;objet unique du tableau `allOf` est la classe de schéma. |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Créé) et un payload qui contient les détails du schéma créé, y compris le `$id`, l’`meta:altId` et la `version`. Ces valeurs sont en lecture seule et sont affectées par [!DNL Schema Registry].

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

L&#39;exécution d&#39;une demande de GET à [liste de tous les schémas](#list) dans le conteneur locataire inclurait désormais le nouveau schéma. Vous pouvez exécuter une requête de recherche [recherche (GET)](#lookup) à l’aide de l’URI `$id` codé en URL pour vue directement le nouveau schéma.

Pour ajouter des champs supplémentaires à un schéma, vous pouvez effectuer une opération [PATCH](#patch) pour ajouter des mixins aux tableaux `allOf` et `meta:extends` du schéma.

## Mettre à jour un schéma {#put}

Vous pouvez remplacer un schéma entier par une opération de PUT, en réécrivant essentiellement la ressource. Lors de la mise à jour d’un schéma par le biais d’une requête de PUT, le corps doit inclure tous les champs requis lors de la création [d’un nouveau schéma](#create) dans une requête de POST.

>[!NOTE]
>
>Si vous souhaitez uniquement mettre à jour une partie d&#39;un schéma au lieu de la remplacer entièrement, consultez la section [Mise à jour d&#39;une partie d&#39;un schéma](#patch).

**Format d’API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | `meta:altId` ou `$id` codé URL du schéma que vous souhaitez réécrire. |

**Requête**

La requête suivante remplace un schéma existant, en modifiant ses attributs `title`, `description` et `allOf`.

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

## Mettre à jour une partie d&#39;un schéma {#patch}

Vous pouvez mettre à jour une partie d’un schéma à l’aide d’une requête de PATCH. [!DNL Schema Registry] prend en charge toutes les opérations de correctif JSON standard, y compris `add`, `remove` et `replace`. Pour plus d’informations sur le correctif JSON, consultez le [guide des fondamentaux de l’API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Si vous souhaitez remplacer une ressource entière par de nouvelles valeurs au lieu de mettre à jour des champs individuels, reportez-vous à la section [remplacement d&#39;un schéma à l&#39;aide d&#39;une opération de PUT](#put).

L&#39;une des opérations de PATCH les plus courantes consiste à ajouter des mixins précédemment définis à un schéma, comme le montre l&#39;exemple ci-dessous.

**Format d’API**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` ou `meta:altId` codés URL du schéma à mettre à jour. |

**Requête**

L&#39;exemple de demande ci-dessous ajoute un nouveau mixin à un schéma en ajoutant la valeur `$id` du mixin aux deux tableaux `meta:extends` et `allOf`.

Le corps de la requête prend la forme d&#39;un tableau, chaque objet répertorié représentant une modification spécifique à un champ individuel. Chaque objet comprend l’opération à exécuter (`op`), le champ sur lequel l’opération doit être exécutée (`path`) et les informations à inclure dans cette opération (`value`).

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

## Activer un schéma à utiliser dans le Profil client en temps réel {#union}

Pour qu’un schéma puisse participer au [Profil client en temps réel](../../profile/home.md), vous devez ajouter une balise `union` à la baie de schémas `meta:immutableTags`. Pour ce faire, vous pouvez faire une demande de PATCH pour le schéma en question.

>[!IMPORTANT]
>
>Les balises immuables sont des balises destinées à être configurées, mais jamais supprimées.

**Format d’API**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` ou `meta:altId` codés URL du schéma à activer. |

**Requête**

L&#39;exemple de requête ci-dessous ajoute un tableau `meta:immutableTags` à un schéma existant, ce qui donne au tableau une valeur de chaîne unique `union` pour l&#39;activer pour une utilisation dans le Profil.

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

Vous pouvez maintenant vue l’union de cette classe de schéma pour confirmer que les champs du schéma sont représentés. Pour plus d&#39;informations, consultez le [guide des points de terminaison des unions](./unions.md).

## Supprimer un schéma {#delete}

Il peut parfois être nécessaire de retirer un schéma du Registre des Schémas. Pour ce faire, il effectue une demande de DELETE avec l’ID de schéma fourni dans le chemin d’accès.

**Format d’API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | URI `$id` ou `meta:altId` codés URL du schéma à supprimer. |

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

Vous pouvez confirmer la suppression en tentant d’envoyer une demande de recherche (GET) au schéma. Vous devez inclure un en-tête `Accept` dans la requête, mais vous devez recevoir l’état HTTP 404 (Non trouvé) car le schéma a été supprimé du Registre du Schéma.
