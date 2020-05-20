---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un mixin
topic: developer guide
translation-type: tm+mt
source-git-commit: b2ceac3de73ac622dc885eb388e46e93551f43a8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Création d’un mixin

Les mixins sont un ensemble de champs utilisés pour décrire un concept particulier, tel que &quot;adresse&quot; ou &quot;préférences de profil&quot;. De nombreux mixins standard sont disponibles ou vous pouvez définir les vôtres lorsque vous souhaitez capturer des informations propres à votre entreprise. Chaque mixin contient un `meta:intendedToExtend` champ qui liste les classes avec lesquelles le mixin est compatible.

Il peut s&#39;avérer utile de consulter tous les mixins disponibles pour se familiariser avec les champs inclus dans chacun d&#39;eux. Vous pouvez liste (GET) tous les mixins compatibles avec une classe particulière en exécutant une requête sur chacun des conteneurs &quot;global&quot; et &quot;locataire&quot;, en renvoyant uniquement les mixins dont le champ &quot;meta:intentToExtend&quot; correspond à la classe que vous utilisez. Les exemples ci-dessous renvoient tous les mixins qui peuvent être utilisés avec la classe de Profil XDM Individuel :

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

L’exemple de demande d’API ci-dessous crée un nouveau mixin dans le conteneur client.

**Format d’API**

```http
POST /tenant/mixins
```

**Requête**

Lors de la définition d’un nouveau mixin, il doit inclure un `meta:intendedToExtend` attribut, répertoriant les classes `$id` avec lesquelles le mixin est compatible. Dans cet exemple, le mixin est compatible avec la classe Property que vous avez définie précédemment. Les champs personnalisés doivent être imbriqués sous `_{TENANT_ID}` (comme illustré dans l&#39;exemple) pour éviter toute collision avec d&#39;autres mixins ou champs des schémas de classe. Notez que le `propertyConstruction` champ est une référence au type de données créé lors de l’appel précédent.

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

Une réponse réussie renvoie l’état HTTP 201 (Créé) et une charge utile contenant les détails du mixin nouvellement créé, y compris le `$id`, `meta:altId`et `version`. Ces valeurs sont en lecture seule et sont affectées par le Registre du Schéma.

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

L’exécution d’une requête GET pour liste de tous les mixins du conteneur locataire inclurait désormais le mixin Détails du véhicule, ou vous pouvez effectuer une requête GET (lookup) à l’aide de l’ `$id` URI codé en URL pour vue directement le nouveau mixin. N’oubliez pas d’inclure le dans l’en-tête Accepter `version` pour toutes les requêtes de recherche.
