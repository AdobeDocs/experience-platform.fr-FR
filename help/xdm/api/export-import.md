---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;exportation;import;rpc;
solution: Experience Platform
title: Points de terminaison de l’API d’exportation/importation
description: Les points de terminaison /export et /import de l’API Schema Registry vous permettent de partager des ressources XDM entre les organisations IMS et les environnements de test.
topic-legacy: developer guide
exl-id: 33b62f75-2670-42f4-9aac-fa1540cd7d4a
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 14%

---

# Points de fin d’exportation/importation

Toutes les ressources dans la variable [!DNL Schema Library] sont contenus dans un environnement de test spécifique au sein d’une organisation IMS. Dans certains cas, vous souhaiterez peut-être partager des ressources du modèle de données d’expérience (XDM) entre les environnements de test et les organisations IMS. Le [!DNL Schema Registry] L’API fournit deux points de terminaison qui vous permettent de générer une charge d’exportation pour n’importe quel schéma, groupe de champs de schéma ou type de données dans[!DNL  Schema Library], puis utilisez cette payload pour importer cette ressource (et toutes les ressources dépendantes) dans un environnement de test cible et une organisation IMS.

## Prise en main

Les points d’entrée d’API utilisés dans ce guide font partie de l’[[!DNL Schema Registry] ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

Les points de terminaison export/import font partie des appels de procédure distants (RPC) pris en charge par la fonction [!DNL Schema Registry]. Contrairement aux autres points de terminaison dans la variable [!DNL Schema Registry] API, les points de terminaison RPC ne nécessitent pas d’en-têtes supplémentaires comme `Accept` ou `Content-Type`, et n’utilisez pas d’événement `CONTAINER_ID`. Ils doivent plutôt utiliser la variable `/rpc` , comme illustré dans les appels API ci-dessous.

## Récupération d’une payload d’exportation pour une ressource {#export}

Pour tout schéma, groupe de champs ou type de données existant dans la variable [!DNL Schema Library], vous pouvez générer une payload d’exportation en envoyant une requête de GET à la variable `/export` point de terminaison , en indiquant l’identifiant de la ressource dans le chemin d’accès.

**Format d’API**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_ID}` | Le `meta:altId` ou encodé URL `$id` de la ressource XDM que vous souhaitez exporter. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante récupère un payload d’exportation pour un `Restaurant` groupe de champs.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**Réponse**

Une réponse réussie renvoie un tableau d’objets, qui représente la ressource XDM cible et toutes ses ressources dépendantes. Dans cet exemple, le premier objet du tableau est un objet créé par le client. `Property` le type de données qui `Restaurant` le groupe de champs utilise, tandis que le second objet est le suivant : `Restaurant` groupe de champs lui-même. Cette payload peut ensuite être utilisée pour [importer la ressource](#import) dans un autre environnement de test ou organisation IMS.

Notez que toutes les instances de l’identifiant du client de la ressource sont remplacées par `<XDM_TENANTID_PLACEHOLDER>`. Cela permet au registre des schémas d’appliquer automatiquement l’identifiant client correct aux ressources en fonction de l’emplacement où ils sont envoyés dans l’appel d’importation suivant.

```json
[
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
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    }
]
```

## Importer une ressource {#import}

Une fois que vous avez [génération d’une payload d’exportation](#export) pour une ressource XDM, vous pouvez utiliser cette payload dans une requête de POST à la variable `/import` point de terminaison pour importer cette ressource dans une organisation IMS et un environnement de test cible.

**Format d’API**

```http
POST /rpc/import
```

**Requête**

La requête suivante utilise la charge utile renvoyée dans la précédente [exemple d&#39;export](#export) pour importer la variable `Restaurant` groupe de champs dans une nouvelle organisation IMS et un nouvel environnement de test, tel que déterminé par `x-gw-ims-org-id` et `x-sandbox-name` en-têtes, respectivement.

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

Une réponse réussie renvoie une liste des ressources importées, avec les valeurs d’identifiant du client et d’organisation IMS appropriées appliquées.

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
