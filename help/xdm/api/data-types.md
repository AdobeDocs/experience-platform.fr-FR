---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;data type registry;Schema Registry;data type;Data type;data types;Data types;create
solution: Experience Platform
title: Création d’un type de données
description: Le point de terminaison /datatypes de l'API Schéma Registry vous permet de gérer par programmation les types de données XDM dans votre application d'expérience.
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 13%

---


# Point de terminaison des types de données

Les types de données sont utilisés comme champs de type référence dans les classes ou les mixins de la même manière que les champs littéraux de base, la différence majeure étant que les types de données peuvent définir plusieurs sous-champs. Bien que semblables aux mixins en ce qu&#39;ils permettent l&#39;utilisation cohérente d&#39;une structure à champs multiples, les types de données sont plus flexibles parce qu&#39;ils peuvent être inclus n&#39;importe où dans la structure de schéma alors que les mixins ne peuvent être ajoutés qu&#39;au niveau racine. Le `/datatypes` point de terminaison de l’ [!DNL Schema Registry] API vous permet de gérer par programmation les types de données dans votre application d’expérience.

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l’ [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mixin-registry.yaml). Avant de continuer, consultez le guide [de](./getting-started.md) prise en main pour obtenir des liens vers la documentation connexe, un guide pour lire les exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API Experience Platform.

## Retrieve a list of data types {#list}

Vous pouvez liste tous les types de données sous le `global` conteneur ou le `tenant` en adressant une demande de GET à `/global/datatypes` ou `/tenant/datatypes`, respectivement.

>[!NOTE]
>
>Lors de la mise en vente de ressources, le Registre des Schémas limite les résultats à 300 éléments. Pour renvoyer des ressources au-delà de cette limite, vous devez utiliser des paramètres de pagination. Il est également recommandé d’utiliser des paramètres de requête supplémentaires pour filtrer les résultats et réduire le nombre de ressources renvoyées. Pour plus d&#39;informations, consultez la section sur les paramètres [de](./appendix.md#query) requête dans le document de l&#39;appendice.

**Format d’API**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur à partir duquel vous souhaitez récupérer les types de données : `global` pour les types de données créés par Adobe ou `tenant` pour les types de données appartenant à votre entreprise. |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs en fonction desquels filtrer les résultats. Pour obtenir une liste des paramètres disponibles, reportez-vous au document [](./appendix.md#query) annexe. |

**Requête**

La requête suivante récupère une liste de types de données du `tenant` conteneur, en utilisant un paramètre `orderby` de requête pour trier les types de données selon leur `title` attribut.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

The response format depends on the `Accept` header sent in the request. Les `Accept` en-têtes suivants sont disponibles pour répertorier les types de données :

| En-tête `Accept` | Description |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Renvoie un bref résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour la liste des ressources. (Limite : 300) |
| `application/vnd.adobe.xed+json` | Returns full JSON data type for each resource, with original `$ref` and `allOf` included. (Limite : 300) |

**Réponse**

The request above used the `application/vnd.adobe.xed-id+json` `Accept` header, therefore the response includes only the `title`, `$id`, `meta:altId`, and `version` attributes for each data type. L’utilisation de l’autre `Accept` en-tête (`application/vnd.adobe.xed+json`) renvoie tous les attributs de chaque type de données. Select the appropriate `Accept` header depending on the information you require in your response.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
      "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
      "version": "1.0",
      "title": "Loyalty"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/4b0329b5573cbb7cb757db667d7fdf66",
      "meta:altId": "_{TENANT_ID}.datatypes.4b0329b5573cbb7cb757db667d7fdf66",
      "version": "1.0",
      "title": "Property Details"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 2
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/datatypes?orderby=title"
    }
  }
}
```

## Rechercher un type de données {#lookup}

Vous pouvez rechercher un type de données spécifique en incluant l’ID du type de données dans le chemin d’une demande de GET.

**Format d’API**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur qui contient le type de données à récupérer : `global` pour un type de données créé par un Adobe ou `tenant` pour un type de données détenu par votre organisation. |
| `{DATA_TYPE_ID}` | Code `meta:altId` ou URL `$id` du type de données à rechercher. |

**Requête**

La requête suivante récupère un type de données en fonction de sa `meta:altId` valeur fournie dans le chemin d’accès.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

The response format depends on the `Accept` header sent in the request. All lookup requests require a `version` be included in the `Accept` header. The following `Accept` headers are available:

| En-tête `Accept` | Description |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Brut avec `$ref` et `allOf`, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolus, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Brut avec `$ref` et `allOf`, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolus, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolus, contient des descripteurs. |

**Réponse**

Une réponse réussie renvoie les détails du type de données. The fields that are returned depend on the `Accept` header sent in the request. Experiment with different `Accept` headers to compare the responses and determine which header is best for your use case.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
  "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty",
  "type": "object",
  "description": "Loyalty object containing loyalty-specific fields.",
  "definitions": {
    "customFields": {
      "properties": {
        "loyaltyId": {
          "title": "Loyalty ID",
          "description": "Unique loyalty program member ID. Should be in the format of an email address.",
          "type": "string",
          "meta:xdmType": "string"
        },
        "memberSince": {
          "title": "Member Since",
          "description": "Date person joined loyalty program.",
          "type": "string",
          "format": "date",
          "meta:xdmType": "date"
        },
        "points": {
          "title": "Points",
          "description": "Accumulated loyalty points",
          "type": "integer",
          "meta:xdmType": "int"
        },
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "The current loyalty program level to which the individual member belongs.",
          "type": "string",
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ],
          "meta:enum": {
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          },
          "meta:xdmType": "string"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1557529442681,
    "repo:lastModifiedDate": 1557529442681,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "50b8008b588e911314f9685240dd4c23a247f37179a6d9ff6ba3877dc11ca504",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Création d’un type de données {#create}

Vous pouvez définir un type de données personnalisé sous le `tenant` conteneur en exécutant une requête de POST.

**Format d’API**

```http
POST /tenant/datatypes
```

**Requête**

La définition d’un type de données ne nécessite aucun champ `meta:extends` ou `meta:intendedToExtend`, et il n’est plus nécessaire d’imbriquer les champs pour éviter les collisions.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the property construction",
        "type":"object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          }
        } 
      }'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) ainsi qu’un payload contenant les détails du type de données nouvellement créé, y compris `$id`, `meta:altId` et `version`. These three values are read-only and are assigned by the [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:altId": "_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    }
  },
  "refs": [],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1604524729435,
    "repo:lastModifiedDate": 1604524729435,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1c838764342756868ca1297869f582a38d15f03ed0acfc97fda7532d22e942c7",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

Performing a GET request to [list all data types](#list) in the tenant container would now include the Property Details data type, or you can [perform a lookup (GET) request](#lookup) using the URL-encoded `$id` URI to view the new data type directly.

## Mise à jour d’un type de données {#put}

Vous pouvez remplacer un type de données entier par le biais d’une opération de PUT, en réécrivant essentiellement la ressource. Lors de la mise à jour d’un type de données par le biais d’une requête de PUT, le corps doit inclure tous les champs requis lors de la [création d’un nouveau type](#create) de données dans une requête de POST.

>[!NOTE]
>
>Si vous souhaitez uniquement mettre à jour une partie d&#39;un type de données au lieu de la remplacer entièrement, reportez-vous à la section relative à la [mise à jour d&#39;une partie d&#39;un type](#patch)de données.

**Format d’API**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATA_TYPE_ID}` | Codée `meta:altId` ou URL `$id` du type de données que vous souhaitez réécrire. |

**Requête**

La requête suivante réécrit un type de données existant, en ajoutant un nouveau `floorSize` champ.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "floorSize" {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        } 
      }'
```

**Réponse**

Une réponse réussie renvoie les détails du type de données mis à jour.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:altId": "_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "floorSize" {
      "type":  "integer",
      "title":  "Floor Size",
      "description":  "The floor size of the property, in square feet.",
      "meta:xdmType": "int"
    }
  },
  "refs": [],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1604524729435,
    "repo:lastModifiedDate": 1604524729435,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1c838764342756868ca1297869f582a38d15f03ed0acfc97fda7532d22e942c7",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Mise à jour d’une partie d’un type de données {#patch}

Vous pouvez mettre à jour une partie d’un type de données à l’aide d’une requête de PATCH. Il [!DNL Schema Registry] prend en charge toutes les opérations de correctif JSON standard, y compris `add`, `remove`et `replace`. Pour plus d’informations sur le correctif JSON, voir le guide [des fondamentaux de l’](../../landing/api-fundamentals.md#json-patch)API.

>[!NOTE]
>
>If you want to replace an entire resource with new values instead of updating individual fields, see the section on [replacing a data type using a PUT operation](#put).

**Format d’API**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{DATA_TYPE_ID}` | The URL-encoded `$id` URI or `meta:altId` of the data type you want to update. |

**Requête**

L’exemple de requête ci-dessous met à jour le type `description` de données existant et ajoute un nouveau `floorSize` champ.

Le corps de la requête prend la forme d&#39;un tableau, chaque objet répertorié représentant une modification spécifique à un champ individuel. Chaque objet comprend l&#39;opération à exécuter (`op`), le champ sur lequel l&#39;opération doit être exécutée (`path`) et les informations à inclure dans cette opération (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Construction-related information for a company-operated property."
        },
        { 
          "op": "add",
          "path": "/properties/floorSize",
          "value": {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        }
      ]'
```

**Réponse**

La réponse montre que les deux opérations ont été réalisées avec succès. Le `description` a été mis à jour et `floorSize` a été ajouté sous `definitions`.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
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
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
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
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Suppression d’un type de données {#delete}

Il peut parfois être nécessaire de supprimer un type de données du registre des Schémas. Pour ce faire, il effectue une demande de DELETE avec l’ID de type de données fourni dans le chemin d’accès.

**Format d’API**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DATA_TYPE_ID}` | The URL-encoded `$id` URI or `meta:altId` of the data type you want to delete. |

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

You can confirm the deletion by attempting a [lookup (GET) request](#lookup) to the data type. You will need to include an `Accept` header in the request, but should receive an HTTP status 404 (Not Found) because the data type has been removed from the Schema Registry.