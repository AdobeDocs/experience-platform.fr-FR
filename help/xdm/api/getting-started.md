---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Prise en main de l’API de registre de Schéma
description: Ce document présente les concepts de base que vous devez connaître avant de tenter d'appeler l'API de registre du Schéma.
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 50%

---


# Getting started with the [!DNL Schema Registry] API

L’ [!DNL Schema Registry] API vous permet de créer et de gérer diverses ressources de modèle de données d’expérience (XDM). This document provides an introduction to the core concepts you need to know before attempting to make calls to the [!DNL Schema Registry] API.

## Conditions préalables 

L’utilisation du guide du développeur nécessite une compréhension pratique des composants suivants de Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM) System]](../home.md) : Cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
   * [Bases de la composition du schéma](../schema/composition.md) : en savoir plus sur les blocs de création de base des schémas XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

XDM utilise le formatage de Schéma JSON pour décrire et valider la structure des données d’expérience client assimilées. Il est donc fortement recommandé de consulter la documentation [](https://json-schema.org/) officielle du Schéma JSON pour mieux comprendre cette technologie sous-jacente.

## Lecture d’exemples d’appels API

The [!DNL Schema Registry] API documentation provides example API calls to demonstrate how to format your requests. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

## Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](../../tutorials/authentication.md). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Schema Registry], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox documentation](../../sandboxes/home.md).

All lookup (GET) requests to the [!DNL Schema Registry] require an additional `Accept` header, whose value determines the format of information returned by the API. Voir la section [En-tête Accept](#accept) ci-dessous pour plus d’informations.

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

## Connaître votre TENANT_ID {#know-your-tenant_id}

Dans les guides de l&#39;API, vous verrez des références à un `TENANT_ID`. Cet identifiant est utilisé pour assurer que les espaces de noms des ressources que vous créez sont corrects et contenus dans votre organisation IMS. Si vous ne connaissez pas votre identifiant, vous pouvez y accéder en réalisant la requête GET suivante :

**Format d’API**

```http
GET /stats
```

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

A successful response returns information regarding your organization&#39;s use of the [!DNL Schema Registry]. Cela inclut un attribut `tenantId`, dont la valeur est votre `TENANT_ID`.

```JSON
{
  "imsOrg":"{IMS_ORG}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
      "meta:resourceType": "mixins",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
      "meta:resourceType": "mixins",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

## Comprendre le `CONTAINER_ID` {#container}

Calls to the [!DNL Schema Registry] API require the use of a `CONTAINER_ID`. There are two containers against which API calls can be made: the `global` container and the `tenant` container.

### Conteneur mondial

The `global` container holds all standard Adobe and [!DNL Experience Platform] partner provided classes, mixins, data types, and schemas. You may only perform list and lookup (GET) requests against the `global` container.

Voici un exemple d’appel qui utilise le `global` conteneur :

```http
GET /global/classes
```

### Conteneur client

Not to be confused with your unique `TENANT_ID`, the `tenant` container holds all classes, mixins, data types, schemas, and descriptors defined by an IMS Organization. Ils sont spécifiques à chaque organisation, ce qui signifie qu’ils ne sont pas visibles ou gérables par d’autres organisations IMS. You may perform all CRUD operations (GET, POST, PUT, PATCH, DELETE) against resources that you create in the `tenant` container.

Voici un exemple d’appel qui utilise le `tenant` conteneur :

```http
POST /tenant/mixins
```

When you create a class, mixin, schema or data type in the `tenant` container, it is saved to the [!DNL Schema Registry] and assigned an `$id` URI that includes your `TENANT_ID`. Cet `$id` est utilisé sur l’ensemble de l’API pour faire référence à des ressources spécifiques. Des exemples de valeurs `$id` sont fournis à la section suivante.

## Identification des ressources {#resource-identification}

Les ressources XDM sont identifiées avec un `$id` attribut sous la forme d’un URI, comme les exemples suivants :

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Pour rendre l’URI plus REST-friendly, les schémas possèdent également un encodage de notation à point de l’URI dans une propriété intitulée `meta:altId` :

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Calls to the [!DNL Schema Registry] API will support either the URL-encoded `$id` URI or the `meta:altId` (dot-notation format). La bonne pratique est d’utiliser l’URI `$id` encodé par l’URL lorsque vous passez un appel REST à l’API, comme :

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## En-tête Accept {#accept}

When performing list and lookup (GET) operations in the [!DNL Schema Registry] API, an `Accept` header is required to determine the format of the data returned by the API. When looking up specific resources, a version number must also be included in the `Accept` header.

The following table lists compatible `Accept` header values, including those with version numbers, along with descriptions of what the API will return when they are used.

| Accept | Description |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Renvoie uniquement une liste d’identifiants. Il s’agit de l’en-tête le plus souvent utilisé pour répertorier des ressources. |
| `application/vnd.adobe.xed+json` | Renvoie une liste de schémas JSON complets qui incluent le `$ref` et le `allOf` d’origine. Cet en-tête est utilisé pour renvoyer une liste de ressources complètes. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | XDM brut avec `$ref` et `allOf`. Contient des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | Attributs `$ref` et `allOf` résolus. Contient des titres et des descriptions. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | XDM brut avec `$ref` et `allOf`. Aucun titre ni description. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | Attributs `$ref` et `allOf` résolus. Aucun titre ni description. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | Attributs `$ref` et `allOf` résolus. Les descripteurs sont inclus. |

>[!NOTE]
>
>Si vous fournissez la version principale seulement (p. ex. 1, 2, 3), le registre retournera la dernière version mineure (p. ex. .1, .2, .3) automatiquement.

## Contraintes de champ XDM et bonnes pratiques

Les champs d’un schéma sont répertoriés dans son objet `properties`. Chaque champ est lui-même un objet et contient des attributs pour décrire et contraindre les données que le champ peut contenir.

Vous trouverez plus d’informations sur la définition des types de champ dans l’API dans l’[annexe](appendix.md) de ce guide, notamment des exemples de code et des contraintes optionnelles pour les types de données les plus couramment utilisés.

Le champ d’exemple suivant illustre un champ XDM formaté correctement avec de plus amples détails sur les contraintes de dénomination et les bonnes pratiques fournies ci-dessous. Ces pratiques peuvent également s’appliquer lorsque vous définissez les autres ressources pouvant contenir des attributs similaires.

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* Le nom d’un objet de champ peut contenir des caractères alphanumériques, des tirets ou des traits de soulignement, mais **ne peut pas** commencer par un trait de soulignement.
   * **Correct :** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Incorrect :** `_fieldName`
* Le Camel case est préférable pour le nom du champ objet. Exemple : `fieldName`
* Le champ doit inclure un `title`, écrit en Casse Titre. Exemple : `Field Name`
* Le champ nécessite un `type`.
   * La définition de certains types peut nécessiter un `format` facultatif.
   * Lorsqu’une mise en forme spécifique des données est requise, vous pouvez ajouter des `examples` sous la forme d’un tableau.
   * Il est également possible de définir le type de champ à l’aide d’un type de données dans le registre. See the section on [creating a data type](./data-types.md#create) in the data types endpoint guide for more information.
* Le `description` explique le champ et des informations pertinentes concernant les données du champ. Il doit être écrit en phrases complètes dans une langue claire afin que toute personne accédant au schéma puisse comprendre l’intention du champ.

Pour plus d’informations sur la définition de différents types de champs dans l’API, voir le document sur les contraintes [de](../schema/field-constraints.md) champ.

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’ [!DNL Schema Registry] API, sélectionnez l’un des guides de points de terminaison disponibles.
