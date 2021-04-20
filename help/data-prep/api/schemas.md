---
keywords: Experience Platform ; accueil ; rubriques populaires ; prép. de données ; api guide ; schémas ;
solution: Experience Platform
title: Point de terminaison de l'API schémas
topic: schemas
description: 'Vous pouvez utiliser le point de terminaison `/schémas’ dans l’API Adobe Experience Platform pour récupérer, créer et mettre à jour des schémas par programmation en vue de les utiliser avec Mapper dans la plate-forme. '
translation-type: tm+mt
source-git-commit: 435d27f7187074c78209948c0e57b610b63d2055
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 9%

---



# Point de terminaison des schémas

Les schémas peuvent être utilisés avec Mapper pour vous assurer que les données que vous avez ingérées dans Adobe Experience Platform correspondent à ce que vous voulez ingérer. Vous pouvez utiliser le point de terminaison `/schemas` pour créer, liste et obtenir par programmation des schémas personnalisés à utiliser avec Mapper dans la plate-forme.

>[!NOTE]
>
>Les schémas créés à l’aide de ce point de terminaison sont utilisés exclusivement avec Mapper et les jeux de mappages. Pour créer des schémas accessibles par d&#39;autres services de plateforme, veuillez lire le [Guide de développeur du registre des Schémas](../../xdm/api/schemas.md).

## Obtenir tous les schémas

Vous pouvez récupérer une liste de tous les schémas Mapper disponibles pour votre organisation IMS en adressant une demande de GET au point de terminaison `/schemas`.

**Format d’API**

Le point de terminaison `/schemas` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que la plupart de ces paramètres soient facultatifs, leur utilisation est fortement recommandée pour réduire les frais généraux élevés. Cependant, vous devez inclure les paramètres `start` et `limit` dans votre requête. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| Paramètre | Description |
| --------- | ----------- |
| `{LIMIT}` | **Obligatoire**. Indique le nombre de schémas renvoyés. |
| `{START}` | **Obligatoire**. Indique le décalage des pages de résultats. Pour obtenir la première page de résultats, définissez la valeur sur `start=0`. |
| `{NAME}` | Filtres le schéma en fonction du nom. |
| `{ORDER_BY}` | Trie l’ordre des résultats. Les champs `modifiedDate` et `createdDate` sont pris en charge. Vous pouvez ajouter la propriété en préfixe `+` ou `-` pour la trier par ordre croissant ou décroissant, respectivement. |

**Requête**

La requête suivante récupère les deux derniers schémas créés pour votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse suivante renvoie l’état HTTP 200 avec une liste des schémas demandés.

>[!NOTE]
>
>La réponse suivante a été tronquée pour l’espace.

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

Vous pouvez créer un schéma pour lequel effectuer la validation en adressant une requête de POST au point de terminaison `/schemas`. Il existe trois façons de créer un schéma : envoi d’un [Schéma JSON](https://json-schema.org/), à l’aide de données d’exemple ou en référençant un schéma XDM existant.

```http
POST /schemas
```

### Utilisation d’un schéma JSON

**Requête**

La requête suivante vous permet de créer un schéma en envoyant un Schéma [JSON](https://json-schema.org/).

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Une réponse réussie renvoie l’état HTTP 200 avec des informations sur votre schéma nouvellement créé.

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

### Utilisation des données d’exemple

**Requête**

La requête suivante vous permet de créer un schéma en utilisant des données d’exemple que vous avez précédemment téléchargées.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| Propriété | Description |
| -------- | ----------- |
| `sampleId` | ID des données d’exemple sur lesquelles vous basez le schéma. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations sur votre schéma nouvellement créé.

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

### Reportez-vous à un schéma XDM

**Requête**

La requête suivante vous permet de créer un schéma en référençant un schéma XDM existant.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Nom du schéma à créer. |
| `schemaRef.id` | ID du schéma référencé. |
| `schemaRef.contentType` | Détermine le format de réponse du schéma référencé. Pour plus d&#39;informations sur ce champ, consultez le [schéma registry developer guide](../../xdm/api/schemas.md#lookup) |

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations sur votre schéma nouvellement créé.

>[!NOTE]
>
>La réponse suivante a été tronquée pour l’espace.

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{IMS_ORG}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## Création d’un schéma à l’aide du téléchargement de fichiers

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations sur votre schéma nouvellement créé.

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

Vous pouvez récupérer des informations sur un schéma spécifique en adressant une demande de GET au point de terminaison `/schemas` et en indiquant l’identifiant du schéma que vous souhaitez récupérer dans le chemin de requête.

**Format d’API**

```http
GET /schemas/{SCHEMA_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{SCHEMA_ID}` | L&#39;identifiant du schéma que vous cherchez. |

**Requête**

La requête suivante récupère des informations sur le schéma spécifié.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations sur le schéma spécifié.

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
