---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre de schémas;registre de schémas;schéma;schémas;schémas;schémas;relation;descripteur de relation;descripteur de relation;identité de référence;identité de référence;
title: Définir une relation entre deux schémas à l’aide de l’API Schema Registry
description: Ce document fournit un tutoriel expliquant comment définir une relation un-à-un entre deux schémas définis par votre organisation à l’aide de l’API Schema Registry.
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 27%

---

# Définir une relation entre deux schémas à l’aide de l’API [!DNL Schema Registry]

Comprendre les relations entre vos clients et leurs interactions avec votre marque sur divers canaux est un aspect important d’Adobe Experience Platform. La définition de ces relations dans la structure de vos schémas [!DNL Experience Data Model] (XDM) vous permet d’obtenir des informations complexes sur vos données client.

Bien que les relations de schéma puissent être déduites par l’utilisation du schéma d’union et [!DNL Real-Time Customer Profile], cela s’applique uniquement aux schémas partageant la même classe. Pour établir une relation entre deux schémas appartenant à des classes différentes, un champ de relation dédié doit être ajouté à un **schéma source**, qui indique l’identité d’un **schéma de référence** distinct.

>[!NOTE]
>
>L’API Schema Registry fait référence aux schémas de référence en tant que « schémas de destination ». Ils ne doivent pas être confondus avec les schémas de destination dans les [jeux de mappages de la préparation des données](../../data-prep/mapping-set.md) ou les schémas pour les [connexions de destination](../../destinations/home.md).

Ce document fournit un tutoriel expliquant comment définir une relation un-à-un entre deux schémas définis par votre organisation à l’aide de l’[[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) .

## Commencer

Ce tutoriel nécessite une compréhension pratique de [!DNL Experience Data Model] (XDM) et de [!DNL XDM System]. Avant de commencer ce tutoriel, consultez la documentation suivante :

* [Système XDM dans Experience Platform](../home.md) : présentation de XDM et de sa mise en œuvre dans [!DNL Experience Platform].
   * [Principes de base de composition des schémas](../schema/composition.md) : une présentation des blocs de création de schémas XDM.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Sandbox](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Avant de commencer ce tutoriel, consultez le [guide de développement](../api/getting-started.md) pour obtenir les informations importantes à connaître afin d’effectuer avec succès des appels vers l’API [!DNL Schema Registry]. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête [!DNL Accept] et à ses valeurs possibles).

## Définition d’un schéma source et de référence {#define-schemas}

Vous devez avoir déjà créé les deux schémas qui seront définis dans la relation. Ce tutoriel crée une relation entre les membres du programme de fidélité actuel d’une organisation (défini dans un schéma « [!DNL Loyalty Members] ») et leurs hôtels préférés (définis dans un schéma « [!DNL Hotels] »).

Les relations de schéma sont représentées par un **schéma source** dont un champ fait référence à un autre champ dans un **schéma de référence**. Dans les étapes qui suivent, « [!DNL Loyalty Members] » sera le schéma source, tandis que « [!DNL Hotels] » agira comme schéma de référence.

>[!IMPORTANT]
>
>Pour établir une relation, les deux schémas doivent avoir défini des identités principales et être activés pour la [!DNL Real-Time Customer Profile]. Consultez la section relative à l’[activation d’un schéma à utiliser dans Profile](./create-schema-api.md#profile) dans le tutoriel sur la création de schémas si vous avez besoin de conseils sur la configuration de vos schémas en conséquence.

Pour définir une relation entre deux schémas, vous devez d’abord acquérir les valeurs `$id` des deux schémas. Si vous connaissez les noms d’affichage (`title`) des schémas, vous pouvez rechercher leurs valeurs `$id` en adressant une requête GET au point d’entrée `/tenant/schemas` dans l’API [!DNL Schema Registry].

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>Le `application/vnd.adobe.xed-id+json` d’en-tête [!DNL Accept] renvoie uniquement les titres, les identifiants et les versions des schémas résultants.

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

Dans le [!DNL Schema Registry], les descripteurs de relation fonctionnent de la même manière que les clés étrangères dans les tables de la base de données relationnelle : un champ du schéma source fait office de référence au champ d’identité principale d’un schéma de référence. Si votre schéma source ne comporte pas de champ à cet effet, vous devrez peut-être créer un groupe de champs de schéma avec le nouveau champ et l’ajouter au schéma. Ce nouveau champ doit avoir une valeur `type` de `string`.

>[!IMPORTANT]
>
>Le schéma source ne peut pas utiliser son identité principale comme champ de référence.

Dans ce tutoriel, le schéma de référence « [!DNL Hotels] » contient un champ `hotelId` qui sert d’identité principale au schéma. Cependant, le schéma source « [!DNL Loyalty Members] » ne dispose pas d’un champ dédié à utiliser comme référence à `hotelId`. Par conséquent, un groupe de champs personnalisé doit être créé pour ajouter un nouveau champ au schéma : `favoriteHotel`.

>[!NOTE]
>
>Si votre schéma source comporte déjà un champ dédié que vous prévoyez d’utiliser comme champ de référence, vous pouvez passer à l’étape de [création d’un descripteur de référence](#reference-identity).

### Créer un groupe de champs

Pour ajouter un nouveau champ à un schéma, il doit d’abord être défini dans un groupe de champs. Vous pouvez créer un groupe de champs en effectuant une requête POST vers le point d’entrée `/tenant/fieldgroups`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Une réponse réussie renvoie les détails du groupe de champs nouvellement créé.

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
| `$id` | Identifiant unique, généré par le système et en lecture seule, du nouveau groupe de champs. Il prend la forme d’un URI. |

{style="table-layout:auto"}

Enregistrez l’URI `$id` du groupe de champs, qui sera utilisé à l’étape suivante de l’ajout du groupe de champs au schéma source.

### Ajouter le groupe de champs au schéma source

Une fois que vous avez créé un groupe de champs, vous pouvez l’ajouter au schéma source en envoyant une requête PATCH au point d’entrée `/tenant/schemas/{SCHEMA_ID}`.

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | L’URI `$id` encodé URL ou `meta:altId` du schéma source. |

{style="table-layout:auto"}

**Requête**

La requête suivante ajoute le groupe de champs « [!DNL Favorite Hotel] » au schéma « [!DNL Loyalty Members] ».

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | Le chemin d’accès au champ de schéma où la nouvelle ressource sera ajoutée. Lors de l’ajout de groupes de champs aux schémas, la valeur doit être « /allOf/- ». |
| `value.$ref` | `$id` du groupe de champs à ajouter. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails du schéma mis à jour, qui inclut désormais la valeur `$ref` du groupe de champs ajouté sous son tableau de `allOf`.

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
    "imsOrg": "{ORG_ID}",
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

Un descripteur d’identité de référence doit être appliqué aux champs de schéma s’ils sont utilisés comme référence à un autre schéma dans une relation. Étant donné que le champ `favoriteHotel` dans « [!DNL Loyalty Members] » fait référence au champ `hotelId` dans « [!DNL Hotels] », `favoriteHotel` doit se voir attribuer un descripteur d’identité de référence.

Créez un descripteur de référence pour le schéma source en effectuant une requête POST vers le point d’entrée `/tenant/descriptors`.

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un descripteur de référence pour le champ `favoriteHotel` dans le schéma source « [!DNL Loyalty Members] ».

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| Paramètre | Description |
| --- | --- |
| `@type` | Type de descripteur en cours de définition. Pour les descripteurs de référence, la valeur doit être `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | L’URL `$id` du schéma source. |
| `xdm:sourceVersion` | Le numéro de version du schéma source. |
| `sourceProperty` | Chemin d’accès au champ dans le schéma source qui sera utilisé pour faire référence à l’identité principale du schéma de référence. |
| `xdm:identityNamespace` | L’espace de noms d’identité du champ de référence. Il doit s’agir du même espace de noms que l’identité principale du schéma de référence. Pour plus d’informations, voir [Présentation des espaces de noms d’identité](../../identity-service/home.md). |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails du descripteur de référence nouvellement créé pour le champ source.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Créer un descripteur de relation {#create-descriptor}

Les descripteurs de relation établissent une relation un-à-un entre un schéma source et un schéma de référence. Une fois que vous avez défini un descripteur d’identité de référence pour le champ approprié dans le schéma source, vous pouvez créer un nouveau descripteur de relation en effectuant une requête POST au point d’entrée `/tenant/descriptors`.

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un descripteur de relation, avec « [!DNL Loyalty Members] » comme schéma source et « [!DNL Hotels] » comme schéma de référence.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `@type` | Le type de descripteur à créer. La valeur `@type` des descripteurs de relation est `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | L’URL `$id` du schéma source. |
| `xdm:sourceVersion` | Le numéro de version du schéma source. |
| `xdm:sourceProperty` | Chemin d’accès au champ de référence dans le schéma source. |
| `xdm:destinationSchema` | URL `$id` du schéma de référence. |
| `xdm:destinationVersion` | Numéro de version du schéma de référence. |
| `xdm:destinationProperty` | Chemin d’accès au champ Identité principale dans le schéma de référence. |

{style="table-layout:auto"}

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

En suivant ce tutoriel, vous avez réussi à créer une relation un-à-un entre deux schémas. Pour plus d’informations sur l’utilisation des descripteurs à l’aide de l’API [!DNL Schema Registry], consultez le guide de développement du registre des schémas [&#128279;](../api/descriptors.md). Pour savoir comment définir des relations de schémas dans l’interface utilisateur, consultez le tutoriel sur la [définition de relations de schémas à l’aide de l’éditeur de schémas](relationship-ui.md).
