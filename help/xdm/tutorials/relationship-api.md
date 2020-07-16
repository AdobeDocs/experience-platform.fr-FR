---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Définition d’une relation entre deux schémas à l’aide de l’API Schema Registry
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1467'
ht-degree: 89%

---


# Define a relationship between two schemas using the [!DNL Schema Registry] API


Comprendre les relations entre vos clients et leurs interactions avec votre marque sur divers canaux est un aspect important d’Adobe Experience Platform. Defining these relationships within the structure of your [!DNL Experience Data Model] (XDM) schemas allows you to gain complex insights into your customer data.

This document provides a tutorial for defining a one-to-one relationship between two schemas defined by your organization using the [!DNL Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Prise en main

Ce didacticiel nécessite une bonne compréhension de [!DNL Experience Data Model] (XDM) et [!DNL XDM System]. Avant de commencer ce tutoriel, consultez la documentation suivante :

* [Système XDM dans Experience Platform](../home.md) : présentation de XDM et de sa mise en œuvre dans Experience Platform.
   * [Principes de base de composition des schémas](../schema/composition.md) : une présentation des blocs de création de schémas XDM.
* [!DNL Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

Avant de commencer ce tutoriel, veuillez consulter le [guide de développement](../api/getting-started.md) pour trouver les informations importantes à connaître afin d’effectuer avec succès des appels vers l’API [!DNL Schema Registry] Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête Accept et à ses valeurs possibles).

## Définition d’un schéma source et de destination {#define-schemas}

Vous devez avoir déjà créé les deux schémas qui seront définis dans la relation. Dans ce tutoriel, vous allez apprendre à créer une relation entre les membres du programme de fidélité actuel d’une organisation (définis dans un schéma « Loyalty Members ») et leurs hôtels favoris (définis dans un schéma « Hotels »).

Les relations de schémas sont représentées par un **[!UICONTROL schéma source]** disposant d’un champ qui fait référence à un autre champ dans un **[!UICONTROL schéma de destination]**. In the steps that follow, &quot;[!UICONTROL Loyalty Members]&quot; will be the source schema, while &quot;[!UICONTROL Hotels]&quot; will act as the destination schema.

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
>L’en-tête Accept `application/vnd.adobe.xed-id+json` ne renvoie que les titres, les identifiants et les versions des schémas obtenus.

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

## Définition des champs de référence pour les deux schémas

Within the [!DNL Schema Registry], relationship descriptors work similarly to foreign keys in SQL tables: a field in the source schema acts as a reference to a field of a destination schema. Lors de la définition d’une relation, chaque schéma doit disposer d’un champ spécifique servant de référence à l’autre schéma.

>[!IMPORTANT]
>
>S’il faut activer les schémas pour les utiliser dans [!DNL Real-time Customer Profile](../../profile/home.md), le champ de référence du schéma de destination doit être son **[!UICONTROL identité principale]**. Ce point est abordé plus en détail dans la suite de ce tutoriel.

Si l’un des schémas ne dispose pas d’un champ prévu à cet effet, vous devrez peut-être créer un mixin dans le nouveau champ et l’ajouter au schéma. Ce nouveau champ doit disposer d’une valeur `type` de « chaîne ».

Pour les besoins de ce tutoriel, le schéma de destination « Hotels » dispose déjà d’un champ prévu à cet effet : `hotelId`. Cependant, le schéma source « Loyalty Members » ne disposant pas d’un champ de ce type, il faut lui attribuer un nouveau mixin ajoutant un nouveau champ, `favoriteHotel`, sous son espace de noms `TENANT_ID`.

### Création d’un nouveau mixin

Pour ajouter un nouveau champ à un schéma, ce champ doit d’abord être défini dans un mixin. Vous pouvez créer un mixin en envoyant une requête POST au point de terminaison `/tenant/mixins`.

**Format d’API**

```http
POST /tenant/mixins
```

**Requête**

La requête suivante crée un mixin ajoutant un champ `favoriteHotel` sous l’espace de noms `TENANT_ID` de tout schéma auquel il est ajouté.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel mixin for the Loyalty Members schema.",
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

Une réponse réussie renvoie les détails du nouveau mixin.

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
    "description": "Favorite hotel mixin for the Loyalty Members schema.",
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
| `$id` | L’identifiant unique, généré par le système et en lecture seule du nouveau mixin. Il prend la forme d’un URI. |

Enregistrez l’URI `$id` du mixin à utiliser dans l’étape suivante de l’ajout du mixin au schéma source.

### Ajout du mixin au schéma source

Une fois que vous avez créé un mixin, vous pouvez l’ajouter au schéma source en envoyant une requête PATCH au point de terminaison `/tenant/schemas/{SCHEMA_ID}`.

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | L’URI `$id` encodé URL ou `meta:altId` du schéma source. |

**Requête**

La requête suivante ajoute le mixin « Favorite Hotel » au schéma « Loyalty Members ».

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
| `path` | Le chemin d’accès au champ de schéma où la nouvelle ressource sera ajoutée. Lors de l’ajout de mixins à des schémas, la valeur doit être `/allOf/-`. |
| `value.$ref` | Le `$id` du mixin à ajouter. |

**Réponse**

Une réponse réussie renvoie les détails du schéma mis à jour, qui inclut désormais la valeur `$ref` du mixin ajouté sous son tableau `allOf`.

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

## Définition de champs d’identité principale pour les deux schémas

>[!NOTE]
>
>Cette étape n’est requise que pour les schémas qui seront activés pour une utilisation dans [!DNL Real-time Customer Profile](../../profile/home.md). Si vous ne souhaitez pas que l’un ou l’autre des schémas soit utilisé dans une union, ou si des identités primaires sont déjà définies pour votre schéma, vous pouvez passer à l’étape suivante de [la création d’un descripteur d’identité de référence](#create-descriptor) pour le schéma de destination.

In order for schemas to be enabled for use in [!DNL Real-time Customer Profile], they must have a primary identity defined. De plus, le schéma de destination d’une relation doit utiliser son identité principale comme champ de référence.

Pour les besoins de ce tutoriel, une identité principale est déjà définie pour le schéma source, mais pas pour le schéma de destination. Vous pouvez marquer un champ de schéma comme champ d’identité principale en créant un descripteur d’identité. Pour ce faire, vous devez envoyer une requête POST au point de terminaison `/tenant/descriptors`.

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un descripteur d’identité définissant le champ `hotelId` du schéma de destination « Hotels » comme champ d’identité principale.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true
  }'
```

| Paramètre | Description |
| --- | --- |
| `@type` | Le type de descripteur à créer. La valeur `@type` des descripteurs d’identité est `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | La valeur `$id` du schéma de destination, obtenue à [l’étape précédente](#define-schemas). |
| `xdm:sourceVersion` | Le numéro de version du schéma. |
| `sourceProperty` | Le chemin d’accès au champ spécifique qui servira d’identité principale de schéma. Ce chemin d’accès doit commencer par un « / » et ne pas se terminer par un, tout en excluant les espaces de noms « properties ». Par exemple, la requête ci-dessus utilise `/_{TENANT_ID}/hotelId` au lieu de `/properties/_{TENANT_ID}/properties/hotelId`. |
| `xdm:namespace` | L’espace de noms d’identité du champ d’identité. `hotelId` est une valeur ECID dans cet exemple. Par conséquent, l’espace de noms « ECID » est utilisé. Pour obtenir une liste des espaces de noms disponibles, consultez la [présentation de l’espace de noms d’identité](../../identity-service/home.md). |
| `xdm:isPrimary` | Une propriété booléenne déterminant si le champ d’identité est l’identité principale du schéma. Puisque cette requête définit une identité principale, la valeur est définie sur true. |

**Réponse**

Une réponse réussie renvoie les détails du descripteur d’identité que vous venez de créer.

```json
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "@id": "e3cfa302d06dc27080e6b54663511a02dd61316f"
}
```

## Création d’un descripteur d’identité de référence

Un descripteur d’identité de référence doit être appliqué aux champs du schéma s’ils sont utilisés comme référence par d’autres schémas dans une relation. Puisque le champ `favoriteHotel` dans « Loyalty Members » renvoie au champ `hotelId` dans « Hotels », un descripteur d’identité de référence doit être appliqué à `hotelId`.

Créez un descripteur de référence pour le schéma de destination en envoyant une requête POST au point de terminaison `/tenant/descriptors`.

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un descripteur de référence pour le champ `hotelId` dans le schéma de destination « Hotels ».

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
    "xdm:identityNamespace": "ECID"
  }'
```

| Paramètre | Description |
| --- | --- |
| `xdm:sourceSchema` | L’URL `$id` du schéma de destination. |
| `xdm:sourceVersion` | Le numéro de version du schéma de destination. |
| `sourceProperty` | Le chemin d’accès au champ d’identité principale du schéma de destination. |
| `xdm:identityNamespace` | L’espace de noms d’identité du champ de référence. `hotelId` est une valeur ECID dans cet exemple. Par conséquent, l’espace de noms « ECID » est utilisé. Pour obtenir une liste des espaces de noms disponibles, consultez la [présentation de l’espace de noms d’identité](../../identity-service/home.md). |

**Réponse**

Une réponse réussie renvoie les détails du descripteur d’identité que vous venez de créer pour le schéma de destination.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Création d’un descripteur de relation {#create-descriptor}

Les descripteurs de relation établissent une relation un-à-un entre un schéma source et un schéma de destination. Vous pouvez créer un descripteur de relation en envoyant une requête POST au point de terminaison `/tenant/descriptors`.

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante crée un descripteur de relation, « Loyalty Members » étant le schéma source et « Legacy Loyalty Members », le schéma de destination.

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
| `@type` | Le type de descripteur à créer. La valeur `@type` des descripteurs de relation est `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | L’URL `$id` du schéma source. |
| `xdm:sourceVersion` | Le numéro de version du schéma source. |
| `sourceProperty` : | Le chemin d’accès au champ de référence dans le schéma source. |
| `xdm:destinationSchema` | L’URL `$id` du schéma de destination. |
| `xdm:destinationVersion` | Le numéro de version du schéma de destination. |
| `destinationProperty` : | Le chemin d’accès au champ de référence dans le schéma de destination. |

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

En suivant ce tutoriel, vous avez réussi à créer une relation un-à-un entre deux schémas. For more information on working with descriptors using the [!DNL Schema Registry] API, see the [Schema Registry developer guide](../api/getting-started.md). Pour savoir comment définir des relations de schémas dans l’interface utilisateur, consultez le tutoriel sur la [définition de relations de schémas à l’aide de l’éditeur de schémas](relationship-ui.md).