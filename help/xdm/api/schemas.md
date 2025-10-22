---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre de schémas;registre de schémas;schéma;schémas;schémas;schémas;créer
solution: Experience Platform
title: Point d’entrée de l’API Schemas
description: Le point d’entrée /schemas de l’API Schema Registry vous permet de gérer les schémas XDM par programmation dans votre application d’expérience.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: dc5ac5427e1eeef47434c3974235a1900d29b085
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 15%

---

# Point d’entrée des schémas

Un schéma peut être considéré comme le plan directeur des données que vous souhaitez ingérer dans Adobe Experience Platform. Chaque schéma est composé d’une classe et de zéro ou plusieurs groupes de champs. Le point d’entrée `/schemas` de l’API [!DNL Schema Registry] vous permet de gérer par programmation les schémas dans votre application d’expérience.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼ [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupération d’une liste de schémas {#list}

Vous pouvez répertorier tous les schémas sous le conteneur `global` ou `tenant` en effectuant une requête GET à `/global/schemas` ou `/tenant/schemas`, respectivement.

>[!NOTE]
>
>Lors de l’énumération des ressources, le registre des schémas limite les jeux de résultats à 300 éléments. Pour renvoyer des ressources au-delà de cette limite, vous devez utiliser des paramètres de pagination. Il est également recommandé d’utiliser des paramètres de requête supplémentaires pour filtrer les résultats et réduire le nombre de ressources renvoyées. Pour plus d’informations, consultez la section sur les [paramètres de requête](./appendix.md#query) dans le document annexe.

**Format d’API**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Le conteneur qui contient les schémas à récupérer : `global` pour les schémas créés par Adobe ou `tenant` pour les schémas appartenant à votre organisation. |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs pour le filtrage des résultats. Voir le [document annexe](./appendix.md#query) pour obtenir une liste des paramètres disponibles. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère une liste de schémas du conteneur de `tenant` à l’aide d’un paramètre de requête `orderby` pour trier les résultats en fonction de leur attribut `title`.

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
| `application/vnd.adobe.xed-id+json` | Renvoie un bref résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour répertorier les ressources. (Limite : 300) |
| `application/vnd.adobe.xed+json` | Renvoie le schéma JSON complet pour chaque ressource, avec les `$ref` et `allOf` d’origine inclus. (Limite : 300) |

{style="table-layout:auto"}

**Réponse**

La requête ci-dessus a utilisé l’en-tête `application/vnd.adobe.xed-id+json` `Accept`. Par conséquent, la réponse inclut uniquement les attributs `title`, `$id`, `meta:altId` et `version` pour chaque schéma. L’utilisation de l’autre en-tête de `Accept` (`application/vnd.adobe.xed+json`) renvoie tous les attributs de chaque schéma. Sélectionnez l’en-tête de `Accept` approprié en fonction des informations dont vous avez besoin dans votre réponse.

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

Vous pouvez rechercher un schéma spécifique en effectuant une requête GET qui inclut l’identifiant du schéma dans le chemin d’accès.

**Format d’API**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur contenant le schéma à récupérer : `global` pour un schéma créé par Adobe ou `tenant` pour un schéma détenu par votre organisation. |
| `{SCHEMA_ID}` | Le `meta:altId` `$id` ou encodé URL du schéma que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère un schéma spécifié par sa valeur `meta:altId` dans le chemin d’accès .

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
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` et `allOf` résolus, comporte des titres et des descriptions. Les champs obsolètes sont indiqués par un attribut `meta:status` de `deprecated`. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails du schéma. Les champs renvoyés dépendent de l’en-tête `Accept` envoyé dans la requête. Testez différents en-têtes `Accept` pour comparer les réponses et déterminer l’en-tête le mieux adapté à votre cas d’utilisation.

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

Pour plus d’informations sur la création d’un schéma sans classes ni groupes de champs, connu sous le nom de schéma relationnel, consultez la section [Créer un schéma relationnel](#create-relational-schema).

>[!NOTE]
>
>L’exemple d’appel ci-dessous n’est qu’un exemple de référence de la création d’un schéma dans l’API, avec les exigences minimales de composition d’une classe et aucun groupe de champs. Pour obtenir des instructions complètes sur la création d’un schéma dans l’API, y compris sur l’attribution de champs à l’aide de groupes de champs et de types de données, consultez le tutoriel [création de schémas](../tutorials/create-schema-api.md).

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
| `allOf` | Tableau d’objets, où chaque objet fait référence à une classe ou à un groupe de champs dont les champs sont implémentés par le schéma. Chaque objet contient une seule propriété (`$ref`) dont la valeur représente le `$id` de la classe ou du groupe de champs que le nouveau schéma implémentera. Une classe doit être fournie, avec zéro ou plusieurs groupes de champs supplémentaires. Dans l’exemple ci-dessus, l’objet unique dans le tableau `allOf` est la classe du schéma. |

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

L’exécution d’une requête GET pour [répertorier tous les schémas](#list) dans le conteneur du tenant inclut désormais le nouveau schéma. Vous pouvez effectuer une [requête de recherche (GET)](#lookup) à l’aide de l’URI de `$id` codée en URL pour afficher directement le nouveau schéma.

Pour ajouter des champs supplémentaires à un schéma, vous pouvez effectuer une opération [PATCH](#patch) afin d’ajouter des groupes de champs aux tableaux `allOf` et `meta:extends` du schéma.

## Créer un schéma relationnel {#create-relational-schema}

>[!AVAILABILITY]
>
>Les schémas Data Mirror et relationnels sont disponibles pour les détenteurs de licence Adobe Journey Optimizer **Campagnes orchestrées**. Ils sont également disponibles en tant que **version limitée** pour les utilisateurs de Customer Journey Analytics, selon votre licence et l’activation des fonctionnalités. Contactez votre représentant Adobe pour obtenir l’accès.

>[!NOTE]
>
>Les schémas relationnels étaient auparavant appelés schémas basés sur des modèles dans des versions antérieures de la documentation de l’API Adobe Experience Platform. La fonctionnalité reste la même : seule la terminologie a été modifiée pour plus de clarté.

Créez un schéma relationnel en adressant une requête POST au point d’entrée `/schemas`. Les schémas relationnels stockent des données structurées de style relationnel **sans** classes ni groupes de champs. Définissez les champs directement sur le schéma et identifiez le schéma comme relationnel à l’aide d’une balise de comportement logique.

>[!IMPORTANT]
>
>Pour créer un schéma relationnel, définissez `meta:extends` sur `"https://ns.adobe.com/xdm/data/adhoc-v2"`. Il s’agit d’un **identifiant de comportement logique** (et non d’un comportement ou d’une classe physique). N’incluez **pas** les classes de référence ou les groupes de champs dans les `allOf` et n’incluez **pas** les classes ou les groupes de champs dans les `meta:extends`.

Créez d’abord le schéma avec `POST /tenant/schemas`. Ajoutez ensuite les descripteurs requis avec l’[API Descriptors (`POST /tenant/descriptors`)](../api/descriptors.md) :

- [descripteur de clé de Principal &#x200B;](../api/descriptors.md#primary-key-descriptor) : un champ de clé primaire doit être au **niveau racine** et **marqué comme requis**.
- [Descripteur de version](../api/descriptors.md#version-descriptor) : **obligatoire** lorsqu’il existe une clé primaire.
- [Descripteur de relation](../api/descriptors.md#relationship-descriptor) : facultatif, définit les jointures ; la cardinalité n’est pas appliquée lors de l’ingestion.
- [Descripteur d’horodatage](../api/descriptors.md#timestamp-descriptor) : pour les schémas de série temporelle, la clé primaire doit être une clé **composite** qui inclut le champ d’horodatage.

>[!NOTE]
>
>Dans l’éditeur de schéma de l’interface utilisateur, le descripteur de version et les descripteurs d’horodatage apparaissent respectivement sous la forme « [!UICONTROL Version identifier] » et « [!UICONTROL Timestamp identifier] ».

>[!CAUTION]
>
>Les schémas relationnels ne sont **pas compatibles avec les schémas d’union**. N’appliquez pas la balise `union` à `meta:immutableTags` lorsque vous utilisez des schémas relationnels. Cette configuration est bloquée dans l’interface utilisateur, mais n’est pas actuellement bloquée par l’API. Pour plus d’informations sur le comportement du schéma d’union[&#x200B; consultez le &#x200B;](./unions.md) guide des points d’entrée des unions .

**Format d’API**

```http
POST /tenant/schemas
```

**Requête**

```shell
curl --request POST \
  --url https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
  "title": "marketing.customers",
  "type": "object",
  "description": "Schema of the Marketing Customers table.",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "meta:xdmType": "object"
    }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record"
}
'
```

### Propriétés du corps de la requête

| Propriété | Type | Description |
| ------------------------------- | ------ | --------------------------------------------------------- |
| `title` | Chaîne | Nom d’affichage du schéma. |
| `description` | Chaîne | Brève explication de l’objectif du schéma. |
| `type` | Chaîne | Doit être `"object"` pour les schémas relationnels. |
| `definitions` | Objet | Contient le ou les objets de niveau racine qui définissent vos champs de schéma. |
| `definitions.<name>.properties` | Objet | Noms de champs et types de données. |
| `allOf` | Tableau | Fait référence à la définition d’objet au niveau racine (par exemple, `#/definitions/marketing_customers`). |
| `meta:extends` | Tableau | Doit inclure des `"https://ns.adobe.com/xdm/data/adhoc-v2"` pour identifier le schéma comme relationnel. |
| `meta:behaviorType` | Chaîne | Définissez sur `"record"`. Utilisez `"time-series"` uniquement lorsqu’elle est activée et appropriée. |

>[!IMPORTANT]
>
>L’évolution des schémas relationnels suit les mêmes règles d’ajout que les schémas standard. Vous pouvez ajouter de nouveaux champs avec une requête PATCH. Les modifications telles que le changement de nom ou la suppression de champs ne sont autorisées que si aucune donnée n’a été ingérée dans le jeu de données.

**Réponse**

Une requête réussie renvoie **HTTP 201 (Created)** et le schéma créé.

>[!NOTE]
>
>Les schémas relationnels n’héritent pas des champs prédéfinis (par exemple, id, timestamp ou eventType). Définissez explicitement tous les champs obligatoires dans votre schéma.

**Exemple de réponse**

```json
{
  "$id": "https://ns.adobe.com/<TENANT_ID>/schemas/<SCHEMA_UUID>",
  "meta:altId": "_<SCHEMA_ALT_ID>",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "marketing.customers",
  "description": "Schema of the Marketing Customers table.",
  "type": "object",
  "definitions": {
    "marketing_customers": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    { "$ref": "#/definitions/marketing_customers" }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record",
  "meta:containerId": "tenant"
}
```

### Propriétés du corps de la réponse

| Propriété | Type | Description |
| ------------------- | ------ | -------------------------- |
| `$id` | Chaîne | URL unique du schéma créé. À utiliser dans les appels API suivants. |
| `meta:altId` | Chaîne | Identifiant alternatif du schéma. |
| `meta:resourceType` | Chaîne | Type de ressource (toujours `"schemas"`). |
| `version` | Chaîne | Version du schéma affectée lors de la création. |
| `title` | Chaîne | Nom d’affichage du schéma. |
| `description` | Chaîne | Brève explication de l’objectif du schéma. |
| `type` | Chaîne | Type de schéma. |
| `definitions` | Objet | Définit des objets ou des groupes de champs réutilisables utilisés dans le schéma. Cela inclut généralement la structure de données principale et est référencé dans le tableau `allOf` pour définir la racine du schéma. |
| `allOf` | Tableau | Indique l’objet racine du schéma en référençant une ou plusieurs définitions (par exemple, `#/definitions/marketing_customers`). |
| `meta:extends` | Tableau | Identifie le schéma comme relationnel (`adhoc-v2`). |
| `meta:behaviorType` | Chaîne | Type de comportement (`record` ou `time-series`, lorsqu’il est activé). |
| `meta:containerId` | Chaîne | Conteneur dans lequel le schéma est stocké (par exemple, `tenant`). |

Pour ajouter des champs à un schéma relationnel après sa création, effectuez une requête [PATCH](#patch). Les schémas relationnels n’héritent pas et n’évoluent pas automatiquement. Les modifications structurelles telles que le changement de nom ou la suppression de champs ne sont autorisées que si aucune donnée n’a été ingérée dans le jeu de données. Une fois que les données existent, seules les **modifications supplémentaires** (telles que l’ajout de nouveaux champs) sont prises en charge.

Vous pouvez ajouter de nouveaux champs au niveau racine (dans la définition ou le `properties` racine), mais vous ne pouvez pas supprimer, renommer ni modifier le type des champs existants.

>[!CAUTION]
>
>L’évolution des schémas devient limitée une fois qu’un jeu de données est initialisé à l’aide du schéma. Planifiez soigneusement les noms et les types de champs à l’avance, car une fois les données ingérées, les champs ne peuvent pas être supprimés ni modifiés.

## Mise à jour d’un schéma {#put}

Vous pouvez remplacer un schéma entier par une opération PUT, c’est-à-dire réécrire la ressource. Lors de la mise à jour d’un schéma par le biais d’une requête PUT, le corps doit inclure tous les champs requis lors de la [création d’un nouveau schéma](#create) dans une requête POST.

>[!NOTE]
>
>Si vous souhaitez uniquement mettre à jour une partie d’un schéma au lieu de le remplacer entièrement, consultez la section sur la [mise à jour d’une partie d’un schéma](#patch).

**Format d’API**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | Le `meta:altId` `$id` ou encodé URL du schéma que vous souhaitez réécrire. |

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

## Mise à jour d’une partie d’un schéma {#patch}

Vous pouvez mettre à jour une partie d’un schéma à l’aide d’une requête PATCH. Le [!DNL Schema Registry] prend en charge toutes les opérations standard JSON Patch, notamment `add`, `remove` et `replace`. Pour plus d’informations sur le correctif JSON, voir [Guide de base des API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Si vous souhaitez remplacer l’ensemble d’une ressource par de nouvelles valeurs au lieu de mettre à jour des champs individuels, consultez la section sur le [remplacement d’un schéma à l’aide d’une opération PUT](#put).

L’une des opérations PATCH les plus courantes consiste à ajouter des groupes de champs précédemment définis à un schéma, comme le montre l’exemple ci-dessous.

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | L’URI `$id` ou le `meta:altId` du schéma que vous souhaitez mettre à jour encodé URL. |

{style="table-layout:auto"}

**Requête**

L’exemple de requête ci-dessous ajoute un nouveau groupe de champs à un schéma en ajoutant la valeur de `$id` de ce groupe de champs aux tableaux `meta:extends` et `allOf`.

Le corps de la requête se présente sous la forme d’un tableau, où chaque objet répertorié représente une modification spécifique apportée à un champ individuel. Chaque objet inclut l’opération à effectuer (`op`), le champ sur lequel l’opération doit être effectuée (`path`) et les informations à inclure dans cette opération (`value`).

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

La réponse montre que les deux opérations ont été réalisées avec succès. Le groupe de champs `$id` a été ajouté au tableau de `meta:extends` et une référence (`$ref`) au groupe de champs `$id` apparaît désormais dans le tableau de `allOf`.

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

## Activer un schéma à utiliser dans le profil client en temps réel {#union}

Pour qu’un schéma puisse participer au [profil client en temps réel](../../profile/home.md), vous devez ajouter une balise `union` au tableau de `meta:immutableTags` du schéma. Pour ce faire, envoyez une requête PATCH au schéma en question.

>[!IMPORTANT]
>
>Les balises non modifiables sont des balises destinées à être définies, mais jamais supprimées.

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | L’URI ou le `$id` de `meta:altId` codé URL du schéma que vous souhaitez activer. |

{style="table-layout:auto"}

**Requête**

L’exemple de requête ci-dessous ajoute un tableau `meta:immutableTags` à un schéma existant, en donnant au tableau une valeur de chaîne unique de `union` pour l’utiliser dans Profile.

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

Vous pouvez maintenant afficher l’union pour la classe de ce schéma afin de confirmer que les champs du schéma sont représentés. Pour plus d’informations, consultez le [&#x200B; guide des points d’entrée des unions &#x200B;](./unions.md) .

## Supprimer un schéma {#delete}

Il peut parfois être nécessaire de supprimer un schéma du registre des schémas. Pour ce faire, il suffit d’effectuer une requête DELETE avec l’identifiant de schéma fourni dans le chemin d’accès .

**Format d’API**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | L’URI `$id` ou le `meta:altId` du schéma que vous souhaitez supprimer et dont l’URL est codée. |

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

Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) au schéma . Vous devez inclure un en-tête `Accept` dans la requête, mais vous devriez recevoir le statut HTTP 404 (Not Found), car le schéma a été supprimé du registre des schémas.
