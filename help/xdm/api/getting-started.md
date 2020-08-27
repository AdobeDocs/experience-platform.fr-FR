---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de développement de l’API Schema Registry
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 68%

---


# [!DNL Schema Registry] Guide du développeur d’API

The [!DNL Schema Registry] is used to access the Schema Library within Adobe Experience Platform, providing a user interface and RESTful API from which all available library resources are accessible.

Grâce à l’API Schema Registry, vous pouvez réaliser des opérations CRUD de base afin d’afficher et de gérer tous les schémas et toutes les ressources associées disponibles pour vous au sein d’Adobe Experience Platform. This includes those defined by Adobe, [!DNL Experience Platform] partners, and vendors whose applications you use. Vous pouvez également utiliser des appels API pour créer de nouveaux schémas et ressources pour votre organisation, ainsi qu’afficher et modifier les ressources que vous avez déjà définies.

This developer guide provides steps to help you start using the [!DNL Schema Registry] API. The guide then provides sample API calls for performing key operations using the [!DNL Schema Registry].

## Conditions préalables

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[ ! Système de modèle de données d’expérience (XDM) DNL]](../home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   * [Bases de la composition du schéma](../schema/composition.md) : en savoir plus sur les blocs de création de base des schémas XDM.
* [[ !Profil client en temps réel DNL]](../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [[ !Sandbox DNL]](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully make calls to the [!DNL Schema Registry] API.

## Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

## Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Schema Registry], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

All lookup (GET) requests to the [!DNL Schema Registry] require an additional Accept header, whose value determines the format of information returned by the API. Voir la section [En-tête Accept](#accept) ci-dessous pour plus d’informations.

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* Content-Type: application/json

## Connaître votre TENANT_ID {#know-your-tenant_id}

Tout au long de ce guide, vous trouverez des références à un `TENANT_ID`. Cet identifiant est utilisé pour assurer que les espaces de noms des ressources que vous créez sont corrects et contenus dans votre organisation IMS. Si vous ne connaissez pas votre identifiant, vous pouvez y accéder en réalisant la requête GET suivante :

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

* `tenantId` : la valeur `TENANT_ID` de votre organisation IMS.

## Comprendre le `CONTAINER_ID` {#container}

Calls to the [!DNL Schema Registry] API require the use of a `CONTAINER_ID`. Il existe deux conteneurs sur lesquels vous pouvez passer des appels API : le **conteneur mondial** et le **conteneur client**.

### Conteneur mondial

The global container holds all standard Adobe and [!DNL Experience Platform] partner provided classes, mixins, data types, and schemas. Vous pouvez uniquement exécuter les requêtes liste et recherche (GET) sur le conteneur mondial.

### Conteneur client

À ne pas confondre avec votre `TENANT_ID` unique, le conteneur client contient l’ensemble des classes, des mixins, des types de données, des schémas et des descripteurs définis par une organisation IMS. Ils sont spécifiques à chaque organisation, ce qui signifie qu’ils ne sont pas visibles ou gérables par d’autres organisations IMS. Vous pouvez réaliser toutes les opérations CRUD (GET, POST, PUT, PATCH, DELETE) sur des ressources que vous avez créées dans le conteneur client.

When you create a class, mixin, schema or data type in the tenant container, it is saved to the [!DNL Schema Registry] and assigned an `$id` URI that includes your `TENANT_ID`. Cet `$id` est utilisé sur l’ensemble de l’API pour faire référence à des ressources spécifiques. Des exemples de valeurs `$id` sont fournis à la section suivante.

## Identification du schéma {#schema-identification}

Les schémas sont identifiés avec un attribut `$id` sous la forme d’un URI, comme :
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Pour rendre l’URI plus REST-friendly, les schémas possèdent également un encodage de notation à point de l’URI dans une propriété intitulée `meta:altId` :
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Les appels vers l’API Schema Registry soutiendront soit l’URI `$id` encodé par l’URL ou le `meta:altId` (format de notation à point). La bonne pratique est d’utiliser l’URI `$id` encodé par l’URL lorsque vous passez un appel REST à l’API, comme :
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## En-tête Accept {#accept}

When performing list and lookup (GET) operations in the [!DNL Schema Registry] API, an Accept header is required to determine the format of the data returned by the API. Lorsque vous recherchez des ressources spécifiques, un numéro de version doit également être inclus dans l’en-tête Accept.

Le tableau suivant répertorie les valeurs de l’en-tête Accept compatibles, incluant celles dont les numéros de version, ainsi que les descriptions de ce que l’API renverra lorsqu’elles sont utilisées.

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
> Si vous ne fournissez que la version `major` (par exemple, 1, 2, 3), le registre renverra automatiquement la dernière version `minor`.

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
   * Il est également possible de définir le type de champ à l’aide d’un type de données dans le registre. Pour plus d’informations, consultez la section [Création d’un type de donnée](create-data-type.md) de ce guide.
* Le `description` explique le champ et des informations pertinentes concernant les données du champ. Il doit être écrit en phrases complètes dans une langue claire afin que toute personne accédant au schéma puisse comprendre l’intention du champ.

Consultez l’[annexe](appendix.md) pour plus d’informations sur la manière de définir des types de champ dans l’API.

## Étapes suivantes

This document covered the prerequisite knowledge required to make calls to the [!DNL Schema Registry] API, including required authentication credentials. Vous pouvez désormais procéder aux appels d’échantillon fournis dans ce guide de développement à suivre avec leurs instructions. Pour obtenir des instructions complètes étape par étape sur la manière dont faire un schéma dans l’API, reportez-vous au [tutoriel](../tutorials/create-schema-api.md) suivant.
