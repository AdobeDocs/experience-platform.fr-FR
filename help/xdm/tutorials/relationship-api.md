---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre des schémas;schéma;schémas;schémas;schémas;schémas;relation;relation;descripteur de relation;descripteur de relation;identité de référence;identité de référence;
solution: Experience Platform
title: Définition d’une relation entre deux schémas à l’aide de l’API Schema Registry
description: Ce document fournit un tutoriel indiquant comment définir une relation un-à-un entre deux schémas définis par votre organisation à l’aide de l’API Schema Registry.
topic-legacy: tutorial
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 42%

---

# Définition d’une relation entre deux schémas à l’aide de l’API [!DNL Schema Registry]

Comprendre les relations entre vos clients et leurs interactions avec votre marque sur divers canaux est un aspect important d’Adobe Experience Platform. La définition de ces relations au sein de la structure de vos schémas [!DNL Experience Data Model] (XDM) vous permet d’obtenir des informations complexes sur les données de vos clients.

Bien que les relations de schéma puissent être déduites par l’utilisation du schéma d’union et de [!DNL Real-time Customer Profile], cela ne s’applique qu’aux schémas qui partagent la même classe. Pour établir une relation entre deux schémas appartenant à des classes différentes, un champ de relation dédié doit être ajouté à un schéma source, qui référence l’identité d’un schéma de destination.

Ce document fournit un tutoriel pour la définition d’une relation un-à-un entre deux schémas définis par votre organisation à l’aide de [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Prise en main

Ce tutoriel nécessite une compréhension pratique de [!DNL Experience Data Model] (XDM) et [!DNL XDM System]. Avant de commencer ce tutoriel, consultez la documentation suivante :

* [Système XDM en Experience Platform](../home.md) : Présentation de XDM et de sa mise en oeuvre dans  [!DNL Experience Platform].
   * [Principes de base de composition des schémas](../schema/composition.md) : une présentation des blocs de création de schémas XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Environnements de test](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Avant de commencer ce tutoriel, veuillez consulter le [guide de développement](../api/getting-started.md) pour trouver les informations importantes à connaître afin d’effectuer avec succès des appels vers l’API [!DNL Schema Registry] Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête et à ses valeurs possibles).[!DNL Accept]

## Définition d’un schéma source et de destination {#define-schemas}

Vous devez avoir déjà créé les deux schémas qui seront définis dans la relation. Ce tutoriel crée une relation entre les membres du programme de fidélité actuel d’une organisation (définis dans un schéma &quot;[!DNL Loyalty Members]&quot;) et leurs hôtels préférés (définis dans un schéma &quot;[!DNL Hotels]&quot;).

Les relations de schémas sont représentées par un **schéma source** disposant d’un champ qui fait référence à un autre champ dans un **schéma de destination**. Dans les étapes suivantes, &quot;[!DNL Loyalty Members]&quot; sera le schéma source, tandis que &quot;[!DNL Hotels]&quot; agira comme schéma de destination.

>[!IMPORTANT]
>
>Pour établir une relation, les deux schémas doivent avoir défini des identités Principales et être activés pour [!DNL Real-time Customer Profile]. Consultez la section [Activation d’un schéma à utiliser dans Profile](./create-schema-api.md#profile) dans le tutoriel de création de schéma si vous avez besoin de conseils sur la manière de configurer vos schémas en conséquence.

Pour définir une relation entre deux schémas, vous devez d’abord acquérir les valeurs `$id` des deux schémas. Si vous connaissez les noms d’affichage (`title`) des schémas, vous pouvez trouver leurs valeurs `$id` en envoyant une requête GET au point de terminaison `/tenant/schemas` dans l’API [!DNL Schema Registry]

**Format d’API**

```http
GET /tenant/schemas
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>L’en-tête [!DNL Accept] `application/vnd.adobe.xed-id+json` renvoie uniquement les titres, les identifiants et les versions des schémas obtenus.

**Réponse**

Une réponse réussie renvoie une liste de schémas définis par votre organisation, y compris les `name`, `$id`, `meta:altId` et `version`.

```json
{
    "results": [
        {
            "title": "Newsletter Subscriptions",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/192a66930afad02408429174c311ae73",
            "meta:altId": "_{TENANT_ID}.schemas.192a66930afad02408429174c311ae73",
            "version": "1.2"
        },
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
            "version": "1.5"
        },
        {
            "title": "Hotels",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
            "meta:altId": "_{TENANT_ID}.schemas.d4ad4b8463a67f6755f2aabbeb9e02c7",
            "version": "1.0"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform-stage.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

Enregistrez les valeurs `$id` des deux schémas entre lesquels que vous souhaitez définir une relation. Ces valeurs seront utilisées ultérieurement.

## Définition d’un champ de référence pour le schéma source

Dans [!DNL Schema Registry], les descripteurs de relation fonctionnent de la même manière que les clés étrangères dans les tables de base de données relationnelle : un champ du schéma source fait office de référence au champ d’identité Principal d’un schéma de destination. Si votre schéma source n’a pas de champ prévu à cet effet, vous devrez peut-être créer un groupe de champs de schéma avec le nouveau champ et l’ajouter au schéma. Ce nouveau champ doit avoir une valeur `type` de &quot;[!DNL string]&quot;.

>[!IMPORTANT]
>
>Contrairement au schéma de destination, le schéma source ne peut pas utiliser son identité Principale comme champ de référence.

Dans ce tutoriel, le schéma de destination &quot;[!DNL Hotels]&quot; contient un champ `hotelId` qui sert d’identité Principale au schéma et servira donc également de champ de référence. Cependant, le schéma source &quot;[!DNL Loyalty Members]&quot; ne possède pas de champ dédié à utiliser comme référence et doit se voir attribuer un nouveau groupe de champs qui ajoute un nouveau champ au schéma : `favoriteHotel`.

>[!NOTE]
>
>Si votre schéma source comporte déjà un champ dédié que vous prévoyez d’utiliser comme champ de référence, vous pouvez passer à l’étape [de la création d’un descripteur de référence](#reference-identity).

### Créer un groupe de champs

Pour ajouter un nouveau champ à un schéma, il doit d&#39;abord être défini dans un groupe de champs. Vous pouvez créer un groupe de champs en envoyant une requête de POST au point de terminaison `/tenant/fieldgroups`.

**Format d’API**

```http
POST /tenant/fieldgroups
```

**Requête**

La requête suivante crée un groupe de champs qui ajoute un champ `favoriteHotel` sous l’espace de noms `_{TENANT_ID}` de tout schéma auquel il est ajouté.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel field group for the Loyalty Members schema.",
        "definitions": {
            "favoriteHotel": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "favoriteHotel": {
                      "title": "Favorite Hotel",
                      "type": "string",
                      "description": "Favorite hotel for a Loyalty Member."
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
              "$ref": "#/definitions/favoriteHotel"
            }
        ]
      }'
```

**Réponse**

Une réponse réussie renvoie les détails du nouveau groupe de champs créé.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.mixins.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel field group for the Loyalty Members schema.",
    "definitions": {
        "favoriteHotel": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "favoriteHotel": {
                            "title": "Favorite Hotel",
                            "type": "string",
                            "description": "Favorite hotel for a Loyalty Member.",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/favoriteHotel"
        }
    ],
    "meta:xdmType": "object",
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:registryMetadata": {
        "eTag": "quM2aMPyb2NkkEiZHNCs/MG34E4=",
        "palm:sandboxName": "prod"
    }
}
```

| Propriété | Description |
| --- | --- |
| `$id` | Identifiant unique généré par le système et en lecture seule du nouveau groupe de champs. Il prend la forme d’un URI. |

{style=&quot;table-layout:auto&quot;}

Enregistrez l’URI `$id` du groupe de champs à utiliser dans l’étape suivante de l’ajout du groupe de champs au schéma source.

### Ajouter le groupe de champs au schéma source

Une fois que vous avez créé un groupe de champs, vous pouvez l’ajouter au schéma source en envoyant une requête de PATCH au point de terminaison `/tenant/schemas/{SCHEMA_ID}` .

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | L’URI `$id` encodé URL ou `meta:altId` du schéma source. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante ajoute le groupe de champs &quot;[!DNL Favorite Hotel]&quot; au schéma &quot;[!DNL Loyalty Members]&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| Propriété | Description |
| --- | --- |
| `op` | Opération PATCH à effectuer. Cette requête utilise l’opération `add`. |
| `path` | Le chemin d’accès au champ de schéma où la nouvelle ressource sera ajoutée. Lors de l’ajout de groupes de champs aux schémas, la valeur doit être &quot;/allOf/-&quot;. |
| `value.$ref` | `$id` du groupe de champs à ajouter. |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails du schéma mis à jour, qui inclut désormais la valeur `$ref` du groupe de champs ajouté sous son tableau `allOf`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "type": "object",
    "title": "Loyalty Members",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{IMS_ORG}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/mixins/61969bc646b66a6230a7e8840f4a4d33"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557525483804,
        "repo:lastModifiedDate": 1566419670915,
        "xdm:createdClientId": "{API_KEY}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "eTag": "ITNzu8BVTO5pw9wfCtTTpk6U4WY="
    }
}
```

## Création d’un descripteur d’identité de référence {#reference-identity}

Un descripteur d’identité de référence doit être appliqué aux champs du schéma s’ils sont utilisés comme référence par d’autres schémas dans une relation. Puisque le champ `favoriteHotel` dans &quot;[!DNL Loyalty Members]&quot; fait référence au champ `hotelId` dans &quot;[!DNL Hotels]&quot;, `hotelId` doit recevoir un descripteur d’identité de référence.

Créez un descripteur de référence pour le schéma de destination en envoyant une requête POST au point de terminaison `/tenant/descriptors`.

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un descripteur de référence pour le champ `hotelId` dans le schéma de destination &quot;[!DNL Hotels]&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| Paramètre | Description |
| --- | --- |
| `@type` | Le type de descripteur en cours de définition. Pour les descripteurs de référence, la valeur doit être &quot;xdm:descriptorReferenceIdentity&quot;. |
| `xdm:sourceSchema` | L’URL `$id` du schéma de destination. |
| `xdm:sourceVersion` | Le numéro de version du schéma de destination. |
| `sourceProperty` | Le chemin d’accès au champ d’identité principale du schéma de destination. |
| `xdm:identityNamespace` | L’espace de noms d’identité du champ de référence. Il doit s’agir du même espace de noms utilisé lors de la définition du champ comme identité Principale du schéma. Pour plus d’informations, voir [Présentation des espaces de noms d’identité](../../identity-service/home.md). |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les détails du descripteur d’identité que vous venez de créer pour le schéma de destination.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Création d’un descripteur de relation {#create-descriptor}

Les descripteurs de relation établissent une relation un-à-un entre un schéma source et un schéma de destination. Une fois que vous avez défini un descripteur de référence pour le schéma de destination, vous pouvez créer un descripteur de relation en envoyant une requête de POST au point de terminaison `/tenant/descriptors` .

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un descripteur de relation, avec &quot;[!DNL Loyalty Members]&quot; comme schéma source et &quot;[!DNL Legacy Loyalty Members]&quot; comme schéma de destination.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| Paramètre | Description |
| --- | --- |
| `@type` | Le type de descripteur à créer. La valeur `@type` des descripteurs de relation est &quot;xdm:descriptorOneToOne&quot;. |
| `xdm:sourceSchema` | L’URL `$id` du schéma source. |
| `xdm:sourceVersion` | Le numéro de version du schéma source. |
| `xdm:sourceProperty` | Le chemin d’accès au champ de référence dans le schéma source. |
| `xdm:destinationSchema` | L’URL `$id` du schéma de destination. |
| `xdm:destinationVersion` | Le numéro de version du schéma de destination. |
| `xdm:destinationProperty` | Le chemin d’accès au champ de référence dans le schéma de destination. |

{style=&quot;table-layout:auto&quot;}

### Réponse

Une réponse réussie renvoie les détails du descripteur de relation que vous venez de créer.

```json
{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId",
    "meta:containerId": "tenant",
    "@id": "76f6cc7105f4eaab7eb4a5e1cb4804cadc741669"
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez réussi à créer une relation un-à-un entre deux schémas. Pour plus d’informations sur l’utilisation des descripteurs à l’aide de l’API [!DNL Schema Registry], consultez le [guide de développement du registre des schémas](../api/descriptors.md). Pour savoir comment définir des relations de schémas dans l’interface utilisateur, consultez le tutoriel sur la [définition de relations de schémas à l’aide de l’éditeur de schémas](relationship-ui.md).
