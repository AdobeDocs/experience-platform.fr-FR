---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;update;Update;patch;PATCH
solution: Experience Platform
title: Mise à jour d’une ressource
description: 'Vous pouvez modifier ou mettre à jour des ressources dans le conteneur client à l’aide d’une requête PATCH. Le registre des schémas prend en charge toutes les opérations standard JSON Patch, notamment l’ajout, la suppression et le remplacement de valeurs. '
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 92%

---


# Mise à jour d’une ressource

Vous pouvez modifier ou mettre à jour des ressources dans le conteneur client à l’aide d’une requête PATCH. The [!DNL Schema Registry] supports all standard JSON Patch operations, including add, remove, and replace.

Pour plus d’informations sur JSON Patch, notamment les opérations disponibles, consultez la [documentation JSON Patch](http://jsonpatch.com/) officielle.

>[!NOTE]
>
>Si vous souhaitez remplacer une ressource entière par de nouvelles valeurs au lieu de mettre à jour des champs individuels, consultez le document [Remplacement d’une ressource à l’aide d’une opération PUT](replace-resource.md).

## Ajout de mixins à un schéma

L’une des opérations PATCH les plus courantes implique l’ajout de mixins définis précédemment à un schéma XDM comme présenté dans l’exemple ci-dessous.

**Format d’API**

```http
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_TYPE}` | The type of resource to be updated from the [!DNL Schema Library]. Les types valides sont `datatypes`, `mixins`, `schemas` et `classes`. |
| `{RESOURCE_ID}` | URI `$id` encodé par l’URL ou le `meta:altId` de la ressource. |

**Requête**

À l’aide d’une opération PATCH, vous pouvez mettre à jour un schéma pour y inclure des champs définis dans un mixin créé précédemment. Pour ce faire, vous devez effectuer une requête PATCH sur le schéma en utilisant son `meta:altId` ou l’URI `$id` encodé en URL.

Le corps de la requête inclut l’opération (`op`) que vous souhaitez réaliser, l’emplacement (`path`) sur lequel vous souhaitez réaliser l’opération et les informations (`value`) que vous souhaitez inclure dans l’opération. Dans cet exemple, la valeur `$id` du mixin est ajoutée aux champs `meta:extends` et `allOf` du schéma cible.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "add", "path": "/meta:extends/-", "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"}}
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

## Mise à jour des champs individuels pour une ressource

Vous pouvez également envoyer des requêtes PATCH qui apportent plusieurs changements sur des champs individuels au sein d’une ressource du registre des schémas.

**Format d’API**

```SHELL
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_TYPE}` | The type of resource to be updated from the [!DNL Schema Library]. Les types valides sont `datatypes`, `mixins`, `schemas` et `classes`. |
| `{RESOURCE_ID}` | URI `$id` encodé par l’URL ou le `meta:altId` de la ressource. |

**Requête**

Le corps de la requête inclut l’opération (`op`), l’emplacement (`path`), et les informations (`value`) nécessaires pour mettre à jour le mixin. Cette requête met à jour le mixin Détails de propriété pour supprimer le champ « propertyCity » et ajouter un nouveau champ « propertyAddress » qui fait référence à un type de données standard contenant les informations sur l’adresse. Il ajoute également un nouveau champ « emailAddress » qui fait référence à un type de données standard contenant les informations de l’e-mail.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
          { "op": "remove", "path": "/definitions/vehicles/properties/_{TENANT_ID}/properties/propertyCity"},
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyAddress", "value":
            {
              "title": "Property Address",
              "description": "Address of the Property",
              "$ref": "https://ns.adobe.com/xdm/common/address"
            } 
          },
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/emailAddress", "value":
            {
              "title": "Property Email Address",
              "description": "Email address of the Property",
              "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
            } 
          },
      ]'
```

**Réponse**

Une réponse réussie montre que les opérations ont été terminées avec succès, car les nouveaux champs sont présents et le champ « propertyCity » a été supprimé.

```JSON
{
    "title": "Property Details",
    "description": "Detailed information related to the properties owned and operated by the company.",
    "type": "object",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
    ],
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "propertyName": {
                            "type": "string",
                            "title": "Property Name",
                            "description": "Name of the property",
                            "meta:xdmType": "string"
                        },
                        "phoneNumber": {
                            "title": "Phone Number",
                            "description": "Primary phone number for the property.",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "propertyType": {
                            "type": "string",
                            "title": "Property Type",
                            "description": "Type and primary use of property.",
                            "enum": [
                                "retail",
                                "yoga",
                                "fitness"
                            ],
                            "meta:enum": {
                                "retail": "Retail Store",
                                "yoga": "Yoga Studio",
                                "fitness": "Fitness Center"
                            },
                            "meta:xdmType": "string"
                        },
                        "propertyConstruction": {
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                        },
                        "propertyAddress": {
                            "title": "Property Address",
                            "description": "Address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/common/address"
                        },
                        "emailAddress": {
                            "title": "Property Email Address",
                            "description": "Email address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
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
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf",
    "version": "1.1",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552089776535,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
