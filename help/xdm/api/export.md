---
title: Exporter le point de terminaison de l’API
description: Le point de terminaison /export de l’API Schema Registry vous permet de partager des ressources XDM entre environnements de test.
exl-id: 1dcbfa59-af98-4db5-b6f4-f848e5bf5e81
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 12%

---

# Exporter le point de fin

Toutes les ressources de [!DNL Schema Library] sont contenues dans un environnement de test spécifique dans Adobe Experience Platform. Dans certains cas, vous souhaiterez peut-être partager des ressources de modèle de données d’expérience (XDM) entre des environnements de test et des organisations. Le point d’entrée `/rpc/export` de l’API [!DNL Schema Registry] vous permet de générer une payload d’exportation pour tout schéma, groupe de champs de schéma ou type de données dans [!DNL Schema Library], puis d’utiliser cette payload pour importer cette ressource (et toutes les ressources dépendantes) dans un environnement de test cible et une organisation via le point d’entrée [`/rpc/import` &#x200B;](./import.md).

## Commencer

Le point d’entrée `/rpc/export` fait partie de l’ [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

Le point d’entrée `/rpc/export` fait partie des appels de procédure distante (RPC) pris en charge par [!DNL Schema Registry]. Contrairement à d’autres points de terminaison dans l’API [!DNL Schema Registry], les points de terminaison RPC ne nécessitent pas d’en-têtes supplémentaires tels que `Accept` ou `Content-Type` et n’utilisent pas un `CONTAINER_ID`. Au lieu de cela, ils doivent utiliser l’espace de noms `/rpc`, comme illustré dans les appels API ci-dessous.

## Générer un payload d’exportation pour une ressource {#export}

Pour tout schéma, groupe de champs ou type de données existant dans [!DNL Schema Library], vous pouvez générer une payload d’exportation en effectuant une requête de GET sur le point de terminaison `/export`, en fournissant l’identifiant de la ressource dans le chemin d’accès.

**Format d’API**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_ID}` | `meta:altId` ou encodé URL `$id` de la ressource XDM que vous souhaitez exporter. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère une payload d’exportation pour un groupe de champs `Restaurant`.

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

Une réponse réussie renvoie un tableau d’objets, qui représente la ressource XDM cible et toutes ses ressources dépendantes. Dans cet exemple, le premier objet du tableau est un type de données `Property` créé par le client et utilisé par le groupe de champs `Restaurant`, tandis que le second objet est le groupe de champs `Restaurant` lui-même. Ce payload peut ensuite être utilisé pour [importer la ressource](#import) dans un environnement de test ou une organisation différent.

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

Après avoir généré la payload d’exportation à partir du fichier CSV, vous pouvez envoyer cette payload au point de terminaison `/rpc/import` pour générer le schéma.

Pour plus d’informations sur la génération de schémas à partir de payloads d’exportation, reportez-vous au [guide de point d’entrée d’import](./import.md) .
