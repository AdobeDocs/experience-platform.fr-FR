---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;mixin;Mixin;mixins;Mixins;create
solution: Experience Platform
title: Création d’un mixin
topic: developer guide
description: Les mixins sont un jeu de champs utilisé pour décrire un concept particulier comme « adresse » ou « préférences du profil ». De nombreux mixins standard sont disponibles. Vous pouvez également définir vos propres mixins si vous souhaitez capturer des informations uniques à votre organisation.
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 93%

---


# Création d’un mixin

Les mixins sont un jeu de champs utilisé pour décrire un concept particulier comme « adresse » ou « préférences du profil ». De nombreux mixins standard sont disponibles. Vous pouvez également définir vos propres mixins si vous souhaitez capturer des informations uniques à votre organisation. Chaque mixin contient un champ `meta:intendedToExtend` qui répertorie les classes avec lesquelles le mixin est compatible.

Il vous sera peut être utile de passer en revue tous les mixins disponibles afin de mieux connaître les champs inclus dans chacun d’entre eux. Vous pouvez répertorier (GET) tous les mixins compatibles avec une classe particulière en exécutant une requête sur chacun des conteneurs « global » et « client », en ne renvoyant que les mixins dont le champ « meta:intendedToExtend » correspond à la classe que vous utilisez. The examples below will return all mixins that can be used with the [!DNL XDM Individual Profile] class:

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

L’exemple de requête d’API ci-dessous crée un nouveau mixin dans le conteneur client.

**Format d’API**

```http
POST /tenant/mixins
```

**Requête**

Si vous définissez un nouveau mixin, celui-ci doit inclure un attribut `meta:intendedToExtend`, répertoriant le `$id` des classes avec lesquelles le mixin est compatible. Dans cet exemple, le mixin est compatible avec la classe Propriété que vous avez définie précédemment. Les champs personnalisés doivent être imbriqués dans `_{TENANT_ID}` (comme affiché dans l’exemple) pour éviter toute collision avec d’autres mixins ou champs des schémas de classe. Notez que le champ `propertyConstruction` est une référence au type de données créé lors de l’appel précédent.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Details",
        "description":"Detailed information related to the properties owned and operated by the company.",
        "type":"object",
        "meta:intendedToExtend":["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
              "type":"object",
              "properties": {
                  "propertyName": {
                    "type": "string",
                    "title": "Property Name",
                    "description": "Name of the property"
                  },
                  "propertyCity": {
                    "title": "Property City",
                    "description": "City where the property is located.",
                    "type": "string"
                  },
                  "phoneNumber": {
                    "title": "Phone Number",
                    "description": "Primary phone number for the property.",
                    "type": "string"
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
                    }
                  },
                  "propertyConstruction": {
                    "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                  }
                }
              }
            }
          }
        },
        "allOf": [
            {
                "$ref": "#/definitions/property"
            }
        ]
}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Créé) et un payload qui contient les détails du mixin que vous venez de créer, notamment `$id`, `meta:altId` et `version`. These values are read-only and are assigned by the [!DNL Schema Registry].

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
                        "propertyCity": {
                            "title": "Property City",
                            "description": "City where the property is located.",
                            "type": "string",
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
    "version": "1.0",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552088205144,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

L’exécution d’une requête GET pour répertorier tous les mixins du conteneur client inclurait désormais le mixin Détails du véhicule. Vous pouvez également réaliser une requête de recherche (GET) à l’aide de l’URI `$id` encodé en URL pour afficher directement le nouveau mixin. N’oubliez pas d’inclure la `version` dans l’en-tête Accept pour toutes les requêtes de recherche.
