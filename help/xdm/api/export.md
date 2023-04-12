---
title: Exporter le point de terminaison de l’API
description: Le point de terminaison /export de l’API Schema Registry vous permet de partager des ressources XDM entre environnements de test.
exl-id: 1dcbfa59-af98-4db5-b6f4-f848e5bf5e81
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 13%

---

# Exporter le point de fin

Toutes les ressources dans la variable [!DNL Schema Library] sont contenus dans un environnement de test spécifique dans Adobe Experience Platform. Dans certains cas, vous pouvez vouloir partager des ressources de modèle de données d’expérience (XDM) entre des environnements de test et des organisations. Le `/rpc/export` du point de terminaison [!DNL Schema Registry] L’API vous permet de générer une payload d’exportation pour tout schéma, groupe de champs de schéma ou type de données dans la variable [!DNL Schema Library], puis utilisez cette payload pour importer cette ressource (et toutes les ressources dépendantes) dans un environnement de test cible et une organisation via la fonction [`/rpc/import` endpoint](./import.md).

## Prise en main

Le `/rpc/export` Le point de terminaison fait partie de la variable [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

Le `/rpc/export` Le point d’entrée fait partie des appels de procédure distants (RPC) pris en charge par la fonction [!DNL Schema Registry]. Contrairement aux autres points de terminaison dans la variable [!DNL Schema Registry] API, les points de terminaison RPC ne nécessitent pas d’en-têtes supplémentaires comme `Accept` ou `Content-Type`, et n’utilisez pas d’événement `CONTAINER_ID`. Ils doivent plutôt utiliser la variable `/rpc` , comme illustré dans les appels API ci-dessous.

## Génération d’un payload d’exportation pour une ressource {#export}

Pour tout schéma, groupe de champs ou type de données existant dans la variable [!DNL Schema Library], vous pouvez générer une payload d’exportation en envoyant une requête de GET à la variable `/export` point de terminaison , en indiquant l’identifiant de la ressource dans le chemin d’accès.

**Format d’API**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_ID}` | Le `meta:altId` ou encodé URL `$id` de la ressource XDM que vous souhaitez exporter. |

{style="table-layout:auto"}

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

Une réponse réussie renvoie un tableau d’objets, qui représente la ressource XDM cible et toutes ses ressources dépendantes. Dans cet exemple, le premier objet du tableau est un objet créé par le client. `Property` le type de données qui `Restaurant` le groupe de champs utilise, tandis que le second objet est le suivant : `Restaurant` groupe de champs lui-même. Cette payload peut ensuite être utilisée pour [importer la ressource](#import) dans un autre environnement de test ou une autre organisation.

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

## Importer la ressource {#import}

Après avoir généré la payload d’exportation à partir du fichier CSV, vous pouvez envoyer cette payload à la variable `/rpc/import` point d’entrée pour générer le schéma.

Voir [guide de point de fin d’importation](./import.md) pour plus d’informations sur la génération de schémas à partir de payloads d’exportation.
