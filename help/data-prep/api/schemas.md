---
keywords: Experience Platform;accueil;rubriques les plus consultées;préparation des données;guide de l’api;schémas;
solution: Experience Platform
title: Point d’entrée de l’API Schemas
description: Vous pouvez utiliser le point d’entrée `/schemas` dans l’API Adobe Experience Platform pour récupérer, créer et mettre à jour par programmation les schémas à utiliser avec le mappeur dans Experience Platform.
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 84%

---



# Point d’entrée des schémas

Les schémas peuvent être utilisés avec le mappeur pour vous assurer que les données que vous avez ingérées dans Adobe Experience Platform correspondent à ce que vous souhaitez ingérer. Vous pouvez utiliser le point d’entrée `/schemas` pour créer, répertorier et obtenir par programmation des schémas personnalisés à utiliser avec le mappeur dans Experience Platform.

>[!NOTE]
>
>Les schémas créés à l’aide de ce point d’entrée sont utilisés exclusivement avec le mappeur et les jeux de mappages. Pour créer des schémas accessibles par d’autres services Experience Platform, consultez le guide de développement du [registre des schémas](../../xdm/api/schemas.md).

## Obtention de tous les schémas

Vous pouvez récupérer une liste de tous les schémas du mappeur disponibles pour votre organisation en envoyant une requête GET au point d’entrée `/schemas`.

**Format d’API**

Le point d’entrée `/schemas` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que la plupart de ces paramètres soient facultatifs, leur utilisation est vivement recommandée pour réduire les frais généraux élevés. Cependant, vous devez inclure les paramètres `start` et `limit` dans votre requête. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| Paramètre | Description |
| --------- | ----------- |
| `{LIMIT}` | **Obligatoire**. Indique le nombre de schémas renvoyés. |
| `{START}` | **Obligatoire**. Indique le décalage des pages de résultats. Pour obtenir la première page de résultats, définissez la valeur sur `start=0`. |
| `{NAME}` | Filtre le schéma en fonction du nom. |
| `{ORDER_BY}` | Trie l’ordre des résultats. Les champs `modifiedDate` et `createdDate` sont pris en charge. Vous pouvez ajouter le préfixe `+` ou `-` à la propriété pour la trier par ordre croissant ou décroissant, respectivement. |

**Requête**

La requête suivante récupère les deux derniers schémas créés pour votre organisation.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse suivante renvoie un statut HTTP 200 avec une liste des schémas demandés.

>[!NOTE]
>
>La réponse suivante a été tronquée pour des raisons de place.

```json
{
    "data": [
        {
            "id": "823ac494f35e4e84bcb2f061378fcca6",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
                "contentType": "1.0"
            }
        },
        {
            "id": "0f868d3a1b804fb0abf738306290ae79",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema 2",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0f868d3a1b804fb0abf738306290ae79",
                "contentType": "1.0"
            }
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

## Création d’un schéma

Vous pouvez créer un schéma de validation en effectuant une requête POST sur le point d’entrée `/schemas`. Il existe trois façons de créer un schéma : envoi d’un [schéma JSON](https://json-schema.org/), utilisation de données d’exemple ou référencement d’un schéma XDM existant ;

```http
POST /schemas
```

### Utilisation d’un schéma JSON

**Requête**

La requête suivante vous permet de créer un schéma en envoyant un [schéma JSON](https://json-schema.org/).

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec des informations sur le schéma que vous venez de créer.

```json
{
    "id": "6daffabf14b1425292add3719afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

### Utilisation de données d’exemple

**Requête**

La requête suivante vous permet de créer un schéma à l’aide des données d’exemple que vous avez précédemment chargées.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `sampleId` | L’identifiant des données d’exemple sur lesquelles vous basez le schéma. |

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec des informations sur le schéma que vous venez de créer.

```json
{
    "id": "b2ee78bd55ac45f781a93fb8b90d99b2",
    "version": 0,
    "jsonSchema": {
        "title": "SampleSchema:45439a93d48d47d098d26e0f0840cc02",
        "type": "object",
        "properties": {
            "gender": {
                "title": "gender",
                "type": "string"
            },
            "last_name": {
                "title": "last_name",
                "type": "string"
            },
            "id": {
                "title": "id",
                "type": "string"
            },
            "ip_address": {
                "title": "ip_address",
                "type": "string"
            },
            "first_name": {
                "title": "first_name",
                "type": "string"
            },
            "email": {
                "title": "email",
                "type": "string"
            }
        }
    },
    "sampleId": "45439a93d48d47d098d26e0f0840cc02"
}
```

### Référence à un schéma XDM

**Requête**

La requête suivante vous permet de créer un schéma en référençant un schéma XDM.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "name": "outputSchema1",
     "schemaRef": {
         "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0d555890502224d187b619f23c35c8d1",
         "contentType": "application/vnd.adobe.xed-full+json;version=1"
     }  
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom du schéma que vous souhaitez créer. |
| `schemaRef.id` | Identifiant de du schéma auquel vous faites référence. |
| `schemaRef.contentType` | Détermine le format de réponse du schéma référencé. Vous trouverez plus d’informations sur ce champ dans le [guide de développement du registre des schémas](../../xdm/api/schemas.md#lookup). |

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec des informations sur le schéma que vous venez de créer.

>[!NOTE]
>
>La réponse suivante a été tronquée pour des raisons de place.

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{ORG_ID}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## Création d’un schéma à l’aide du téléchargement de fichier

Vous pouvez créer un schéma en téléchargeant un fichier JSON à partir duquel effectuer la conversion.

**Format d’API**

```http
POST /schemas/upload
```

**Requête**

La requête suivante vous permet de créer un schéma à partir d’un fichier JSON téléchargé.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec des informations sur le schéma que vous venez de créer.

```json
{
    "id": "292add3716daffabf14b14259afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

## Récupération d’un schéma spécifique

Vous pouvez récupérer des informations sur un schéma spécifique en envoyant une requête GET au point d’entrée `/schemas` et en fournissant l’identifiant du schéma que vous souhaitez récupérer dans le chemin de requête.

**Format d’API**

```http
GET /schemas/{SCHEMA_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEMA_ID}` | Identifiant du schéma que vous recherchez. |

**Requête**

La requête suivante récupère des informations sur le schéma spécifié.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec des informations sur le schéma spécifié.

```json
{
    "id": "0f868d3a1b804fb0abf738306290ae79",
    "version": 0,
    "jsonSchema": {
        "title": "Sample schema",
        "description": "Sample description",
        "type": "object",
        "properties": {
            "_id": {
                "title": "Identifier",
                "description": "A unique identifier for the record.",
                "type": "string",
                "format": "uri-reference",
                "meta:xdmField": "@id",
                "meta:xdmType": "string"
            },
            "personalEmail": {
                "title": "Personal Email",
                "description": "A personal email address.",
                "type": "object",
                "properties": {
                    "primary": {
                        "title": "Primary",
                        "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                        "type": "boolean",
                        "meta:xdmField": "xdm:primary",
                        "meta:xdmType": "boolean"
                    },
                    "address": {
                        "title": "Address",
                        "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                        "type": "string",
                        "format": "email",
                        "meta:xdmField": "xdm:address",
                        "meta:xdmType": "string"
                    }
                },
                "meta:xdmField": "xdm:personalEmail",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
                "meta:xdmType": "object"
            }
        },
        "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc"
    },
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
        "contentType": "1.0"
    }
}
```
