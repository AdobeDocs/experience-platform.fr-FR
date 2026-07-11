---
title: Point d’entrée de l’API d’importation
description: Le point d’entrée /import de l’API Schema Registry vous permet de partager des ressources XDM entre les organisations et les sandbox.
exl-id: 30613535-4770-4f9c-9061-8e3efaf4de48
TQID: https://experienceleague.adobe.com/qBBI2G06HrUXj-JOCg3ZmUUbRiEP9mLZqUMDfXi5ezw
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: cb424651efb1b4d71717c06a4b0d6e9354f0dcc7
workflow-type: tm+mt
source-wordcount: 295
ht-degree: 16%

---

# Importer le point d’entrée

Le point d’entrée `/rpc/import` de l’API [!DNL Schema Registry] vous permet de créer des ressources de modèle de données d’expérience (XDM) à partir des payloads d’exportation générées. Les payloads d’exportation peuvent être créées à partir de deux sources :

* Le point d’entrée [`/rpc/export` crée &#x200B;](./export.md) payloads d’exportation à partir de ressources XDM existantes, ce qui vous permet de partager des ressources entre les sandbox.
* Le point d’entrée [`/rpc/csv2schema` crée &#x200B;](./csv-to-schema.md) payloads d’exportation à partir de modèles CSV.

Une fois que vous avez créé une payload d’exportation, vous pouvez utiliser le point d’entrée `/rpc/import` pour générer la ressource (et toutes les ressources dépendantes) dans le sandbox de votre choix.

## Prise en main

Le point d’entrée `/rpc/import` fait partie de l’[[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

Le point d&#39;entrée `/rpc/import` fait partie des appels de procédure distante (RPC) pris en charge par le [!DNL Schema Registry]. Contrairement aux autres points d&#39;entrée de l&#39;API [!DNL Schema Registry], les points d&#39;entrée RPC ne nécessitent pas d&#39;en-têtes supplémentaires tels que `Accept` ou `Content-Type`, et n&#39;utilisent pas de `CONTAINER_ID`. Ils doivent plutôt utiliser l’espace de noms `/rpc`, comme illustré dans les appels d’API ci-dessous.

## Importer une ressource {#import}

Une fois que vous avez généré une payload d’exportation pour une ressource XDM, vous pouvez utiliser cette payload dans une requête POST vers le point d’entrée `/import` pour importer cette ressource dans une organisation cible et un sandbox.

**Format d’API**

```http
POST /rpc/import
```

**Requête**

La requête suivante prend la payload renvoyée par un appel au point d’entrée [&#128279;](./export.md) pour importer un groupe de champs (`Restaurant`) dans une nouvelle organisation et un nouveau sandbox, tel que déterminé par les en-têtes `x-gw-ims-org-id` et `x-sandbox-name`, respectivement.`/rpc/export`

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/import \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
          "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
          "meta:resourceType": "datatypes",
          "version": "1.0",
          "title": "Property",
          "type": "object",
          "description": "",
          "definitions": {
            "customFields": {
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "description": "ID for a company-owned property.",
                  "type": "string",
                  "isRequired": false,
                  "meta:ui": {
                    "ref": [
                      "schema://5fbc29ec292534000055dd55",
                      "#/definitions/customFields"
                    ],
                    "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.propertyId",
                    "editable": true,
                    "generateDate": 1606168175975
                  },
                  "meta:xdmType": "string"
                },
                "jurisdiction": {
                  "title": "Jurisdiction",
                  "description": "",
                  "type": "string",
                  "isRequired": false,
                  "enum": [
                    "NA",
                    "UK",
                    "EU"
                  ],
                  "meta:enum": {
                    "NA": "North America",
                    "UK": "United Kingdom",
                    "EU": "European Union"
                  },
                  "meta:ui": {
                    "ref": [
                      "schema://5fbc29ec292534000055dd55",
                      "#/definitions/customFields"
                    ],
                    "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.jurisdiction",
                    "editable": true,
                    "generateDate": 1606168175975
                  },
                  "meta:xdmType": "string"
                }
              }
            }
          },
          "allOf": [
            {
              "$ref": "#/definitions/customFields",
              "type": "object",
              "meta:xdmType": "object"
            }
          ],
          "meta:extensible": true,
          "meta:abstract": true,
          "meta:xdmType": "object",
          "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
          "meta:sandboxType": "production"
        },
        {
          "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
          "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
          "meta:resourceType": "mixins",
          "version": "1.0",
          "title": "Restaurant",
          "type": "object",
          "description": "",
          "definitions": {
            "customFields": {
              "type": "object",
              "properties": {
                "_<XDM_TENANTID_PLACEHOLDER>": {
                  "type": "object",
                  "properties": {
                    "capacity": {
                      "title": "Capacity",
                      "description": "Restaurant capacity",
                      "type": "string",
                      "isRequired": false,
                      "meta:xdmType": "string"
                    },
                    "kitchen": {
                      "title": "Kitchen Style",
                      "description": "Style of kitchen",
                      "type": "string",
                      "isRequired": false,
                      "meta:xdmType": "string"
                    },
                    "rating": {
                      "title": "Rating",
                      "description": "",
                      "type": "integer",
                      "isRequired": false,
                      "meta:xdmType": "int"
                    },
                    "property": {
                      "title": "Property",
                      "description": "",
                      "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                      "type": "object",
                      "meta:xdmType": "object"
                    }
                  },
                  "meta:xdmType": "object"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "allOf": [
            {
              "$ref": "#/definitions/customFields",
              "type": "object",
              "meta:xdmType": "object"
            }
          ],
          "meta:extensible": true,
          "meta:abstract": true,
          "meta:intendedToExtend": [
            
          ],
          "meta:xdmType": "object",
          "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
          "meta:sandboxType": "production"
        }
      ]'
```

**Réponse**

Une réponse réussie renvoie une liste des ressources importées, avec l’identifiant client approprié et les valeurs d’organisation appliquées.

```json
[
    {
        "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:altId": "_{TENANT_ID}.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:resourceType": "datatypes",
        "version": "1.0",
        "title": "Property",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "properties": {
                    "propertyId": {
                        "title": "Property ID",
                        "description": "ID for a company-owned property.",
                        "type": "string",
                        "isRequired": false,
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._{TENANT_ID}{}.property{}.propertyId",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    },
                    "jurisdiction": {
                        "title": "Jurisdiction",
                        "description": "",
                        "type": "string",
                        "isRequired": false,
                        "enum": [
                            "NA",
                            "UK",
                            "EU"
                        ],
                        "meta:enum": {
                            "NA": "North America",
                            "UK": "United Kingdom",
                            "EU": "European Union"
                        },
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._{TENANT_ID}{}.property{}.jurisdiction",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "refs": [],
        "imsOrg": "{ORG_ID}",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:xdmType": "object",
        "meta:registryMetadata": {
            "repo:createdDate": 1606250624257,
            "repo:lastModifiedDate": 1606250624257,
            "xdm:createdClientId": "{CLIENT_ID}",
            "xdm:lastModifiedClientId": "{CLIENT_ID}",
            "xdm:createdUserId": "{USER_ID}",
            "xdm:lastModifiedUserId": "{USER_ID}",
            "eTag": "9dadfaf8168af30eae1a745de95eace760680cfc9a69bcc938f68fe3caf57317",
            "meta:globalLibVersion": "1.16.3"
        },
        "meta:containerId": "tenant",
        "meta:sandboxId": "52c8dbe0-ced2-11e9-a524-cd79ba95ea3a",
        "meta:sandboxType": "production",
        "meta:tenantNamespace": "_{TENANT_ID}"
    },
    {
        "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "mixins",
        "version": "1.0",
        "title": "Restaurant",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "type": "object",
                "properties": {
                    "_{TENANT_ID}": {
                        "type": "object",
                        "properties": {
                            "capacity": {
                                "title": "Capacity",
                                "description": "Restaurant capacity",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "kitchen": {
                                "title": "Kitchen Style",
                                "description": "Style of kitchen",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "rating": {
                                "title": "Rating",
                                "description": "",
                                "type": "integer",
                                "isRequired": false,
                                "meta:xdmType": "int"
                            },
                            "property": {
                                "title": "Property",
                                "description": "",
                                "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                                "type": "object",
                                "meta:xdmType": "object"
                            }
                        },
                        "meta:xdmType": "object"
                    }
                },
                "meta:xdmType": "object"
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "refs": [
            "https://ns.adobe.com/{TENANT_ID}/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495"
        ],
        "imsOrg": "{ORG_ID}",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:registryMetadata": {
            "repo:createdDate": 1606250624357,
            "repo:lastModifiedDate": 1606250624357,
            "xdm:createdClientId": "{CLIENT_ID}",
            "xdm:lastModifiedClientId": "{CLIENT_ID}",
            "xdm:createdUserId": "{USER_ID}",
            "xdm:lastModifiedUserId": "{USER_ID}",
            "eTag": "5a5401ba8e6845b2f42d330002331e6e96c031c4e228f860423a3d5cd3598b40",
            "meta:globalLibVersion": "1.16.3"
        },
        "meta:containerId": "tenant",
        "meta:sandboxId": "52c8dbe0-ced2-11e9-a524-cd79ba95ea3a",
        "meta:sandboxType": "production",
        "meta:tenantNamespace": "_{TENANT_ID}"
    }
]
```

