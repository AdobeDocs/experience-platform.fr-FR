---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;class registry;Schema Registry;class;Class;classes;Classes;create
solution: Experience Platform
title: Création d’une classe
description: Le point de terminaison /classes de l'API Schéma Registry vous permet de gérer par programmation les classes XDM dans votre application d'expérience.
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 24%

---


# Point de terminaison des classes

Tous les schémas de modèle de données d’expérience (XDM) doivent être basés sur une classe. Une classe détermine la structure de base des propriétés communes que tous les schémas basés sur cette classe doivent contenir, ainsi que les mixins qui peuvent être utilisés dans ces schémas. En outre, une classe de schéma détermine les aspects comportementaux des données qu&#39;un schéma contiendra, dont il existe deux types :

* **[!UICONTROL Enregistrer]**: Fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **[!UICONTROL Série]** chronologique : Fournit un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet d&#39;enregistrement.

>[!NOTE]
>
>Pour plus d&#39;informations sur les comportements des données en termes d&#39;impact sur la composition des schémas, consultez les [bases de la composition](../schema/composition.md)des schémas.

Le `/classes` point de terminaison de l’ [!DNL Schema Registry] API vous permet de gérer par programmation les classes dans votre application d’expérience.

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l’ [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Avant de continuer, consultez le guide [de](./getting-started.md) prise en main pour obtenir des liens vers la documentation connexe, un guide pour lire les exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API Experience Platform.

## Retrieve a list of classes {#list}

Vous pouvez liste toutes les classes sous le `global` ou le `tenant` conteneur en adressant une demande de GET à `/global/classes` ou `/tenant/classes`, respectivement.

>[!NOTE]
>
>Lors de la mise en vente de ressources, le Registre des Schémas limite les résultats à 300 éléments. Pour renvoyer des ressources au-delà de cette limite, vous devez utiliser des paramètres de pagination. Il est également recommandé d’utiliser des paramètres de requête supplémentaires pour filtrer les résultats et réduire le nombre de ressources renvoyées. Pour plus d&#39;informations, consultez la section sur les paramètres [de](./appendix.md#query) requête dans le document de l&#39;appendice.

**Format d’API**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur à partir duquel vous souhaitez récupérer des classes : `global` pour les classes créées par l’Adobe ou `tenant` pour les classes détenues par votre organisation. |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs en fonction desquels filtrer les résultats. Pour obtenir une liste des paramètres disponibles, reportez-vous au document [](./appendix.md#query) annexe. |

**Requête**

La requête suivante récupère une liste de classes du `tenant` conteneur, en utilisant un paramètre `orderby` de requête pour trier les classes selon leur `title` attribut.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

The response format depends on the `Accept` header sent in the request. The following `Accept` headers are available for listing classes:

| En-tête `Accept` | Description |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Renvoie un bref résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour la liste des ressources. (Limite : 300) |
| `application/vnd.adobe.xed+json` | Returns full JSON class for each resource, with original `$ref` and `allOf` included. (Limite : 300) |

**Réponse**

The request above used the `application/vnd.adobe.xed-id+json` `Accept` header, therefore the response includes only the `title`, `$id`, `meta:altId`, and `version` attributes for each class. L’utilisation de l’autre `Accept` en-tête (`application/vnd.adobe.xed+json`) renvoie tous les attributs de chaque classe. Select the appropriate `Accept` header depending on the information you require in your response.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
      "meta:altId": "_{TENANT_ID}.classes.01b7b1745e8ac4ed1e8784ec91b6afa7",
      "version": "1.0",
      "title": "Hotel"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/d43b86253676af50da3f671ecdd26ff9",
      "meta:altId": "_{TENANT_ID}.classes.d43b86253676af50da3f671ecdd26ff9",
      "version": "1.1",
      "title": "Property"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/366f015dbfea802455fbc46c3b27f771",
      "meta:altId": "_{TENANT_ID}.classes.366f015dbfea802455fbc46c3b27f771",
      "version": "1.0",
      "title": "Subscription"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/classes"
    }
  }
}
```

## Rechercher une classe {#lookup}

Vous pouvez rechercher une classe spécifique en incluant son identifiant dans le chemin d&#39;une demande de GET.

**Format d’API**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Conteneur qui héberge la classe que vous souhaitez récupérer : `global` pour une classe créée par un Adobe ou `tenant` pour une classe appartenant à votre organisation. |
| `{CLASS_ID}` | Le code `meta:altId` ou URL `$id` de la classe que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère une classe par sa `meta:altId` valeur fournie dans le chemin d&#39;accès.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

Une réponse réussie renvoie les détails de la classe. The fields that are returned depend on the `Accept` header sent in the request. Experiment with different `Accept` headers to compare the responses and determine which header is best for your use case.

```json
{
  "$id":"https://ns.adobe.com/{TENANT_ID}/classes/f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:altId":"_{TENANT_ID}.classes.f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:resourceType":"classes",
  "version":"1.1",
  "title":"Hotel",
  "type":"object",
  "description":"Base class for the Hotels schema",
  "definitions":{
    "customFields":{
      "type":"object",
      "properties":{
        "_{TENANT_ID}":{
          "type":"object",
          "properties":{
            "Address":{
              "title":"Address",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/common/address",
              "type":"object",
              "meta:xdmType":"object"
            },
            "phoneNumber":{
              "title":"Phone Number",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/context/phonenumber",
              "type":"object",
              "meta:xdmType":"object"
            },
            "brand":{
              "title":"Brand",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            },
            "hotelId":{
              "title":"Hotel ID",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            }
          },
          "meta:xdmType":"object"
        }
      },
      "meta:xdmType":"object"
    }
  },
  "allOf":[
    {
      "$ref":"https://ns.adobe.com/xdm/data/record",
      "type":"object",
      "meta:xdmType":"object"
    },
    {
      "$ref":"#/definitions/customFields",
      "type":"object",
      "meta:xdmType":"object"
    }
  ],
  "imsOrg":"{IMS_ORG}",
  "meta:extensible":true,
  "meta:abstract":true,
  "meta:extends":[
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:xdmType":"object",
  "meta:registryMetadata":{
    "repo:createdDate":1593643258779,
    "repo:lastModifiedDate":1597246362579,
    "xdm:createdClientId":"{CLIENT_ID}",
    "xdm:lastModifiedClientId":"{CLIENT_ID}",
    "xdm:createdUserId":"{USER_ID}",
    "xdm:lastModifiedUserId":"{USER_ID}",
    "eTag":"502f89ee16b8ab2e6b4ea09ecf0ab1e5614907db755051c1f3c65a273001d725",
    "meta:globalLibVersion":"1.15.4"
  },
  "meta:containerId":"tenant",
  "meta:tenantNamespace":"_{TENANT_ID}"
}
```

## Création d’une classe {#create}

Vous pouvez définir une classe personnalisée sous le `tenant` conteneur en exécutant une requête de POST.

>[!IMPORTANT]
>
>Lors de la composition d’un schéma basé sur une classe personnalisée que vous définissez, vous ne pourrez pas utiliser de mixins standard. Chaque mixin définit les classes avec lesquelles il est compatible dans l’attribut `meta:intendedToExtend`. Lorsque vous commencez à définir des mixins compatibles avec votre nouvelle classe (en utilisant le `$id` de votre nouvelle classe dans le champ `meta:intendedToExtend` du mixin), vous pourrez réutiliser ces mixins chaque fois que vous définissez un schéma qui met en œuvre la classe que vous avez définie. Pour plus d’informations, consultez les sections relatives à la [création de mixins](./mixins.md#create) et de [schémas](./schemas.md#create) dans leurs guides de points de terminaison respectifs.
>
>Si vous prévoyez d’utiliser des schémas basés sur des classes personnalisées dans le Profil client en temps réel, il est également important de garder à l’esprit que les schémas d’union ne sont construits que sur la base de schémas partageant la même classe. Si vous souhaitez inclure un schéma de classe personnalisée dans l&#39;union pour une autre classe telle que [!UICONTROL XDM Individuel Profil] ou [!UICONTROL XDM ExperienceEvent], vous devez établir une relation avec un autre schéma qui emploie cette classe. See the tutorial on [establishing a relationship between two schemas in the API](../tutorials/relationship-api.md) for more information.

**Format d’API**

```http
POST /tenant/classes
```

**Requête**

La requête de création (POST) d’une classe doit inclure un attribut `allOf` contenant un `$ref` d’une de ces deux valeurs : `https://ns.adobe.com/xdm/data/record` ou `https://ns.adobe.com/xdm/data/time-series`. Ces valeurs représentent le comportement sur lequel la classe est basée (enregistrement ou série temporelle, respectivement). Pour plus d’informations sur les différences entre les données d’enregistrement et les données de série temporelle, consultez la section sur les types de comportements dans les [principes de base de la composition des schémas](../schema/composition.md).

Lorsque vous définissez une classe, vous pouvez également inclure des mixins ou des champs personnalisés au sein de la définition de la classe. De cette manière, les mixins et les champs ajoutés seront inclus dans tous les schémas qui mettent en œuvre la classe. L’exemple de requête suivant définit une classe intitulée « Propriété » qui capture les informations concernant différentes propriétés détenues et exploitées par une société. Elle inclut un champ `propertyId` à ajouter chaque fois que la classe est utilisée.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `_{TENANT_ID}` | L’espace de noms `TENANT_ID` pour votre organisation. All resources created by your organization must include this property to avoid collisions with other resources in the [!DNL Schema Registry]. |
| `allOf` | Une liste des ressources dont les propriétés doivent être héritées par la nouvelle classe. L’un des objets `$ref` au sein du tableau définit le comportement de la classe. Dans cet exemple, la classe hérite du comportement « enregistrement ». |

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) et un payload contenant les détails de la classe que vous venez de créer, notamment `$id`, `meta:altId` et `version`. These three values are read-only and are assigned by the [!DNL Schema Registry].

```JSON
{
  "title": "Property",
  "description": "Properties owned and operated by the company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property Identification Number",
                  "type": "string",
                  "description": "Unique Property identification number",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
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
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

Performing a GET request to [list all classes](#list) in the `tenant` container would now include the Property class. You can also [perform a lookup (GET) request](#lookup) using the URL-encoded `$id` to view the new class directly.

## Mettre à jour une classe {#put}

Vous pouvez remplacer une classe entière par le biais d&#39;une opération de PUT, en réécrivant essentiellement la ressource. Lors de la mise à jour d&#39;une classe via une requête de PUT, le corps doit inclure tous les champs requis lors de la [création d&#39;une classe](#create) dans une requête de POST.

>[!NOTE]
>
>If you only want to update part of a class instead of replacing it entirely, see the section on [updating a portion of a class](#patch).

**Format d’API**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | Le code `meta:altId` ou URL `$id` de la classe que vous souhaitez réécrire. |

**Requête**

La requête suivante réécrit une classe existante, en modifiant sa classe `description` et celle `title` de l&#39;un de ses champs.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property",
        "description": "Base class for properties operated by a company.",
        "type": "object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property ID",
                        "type": "string",
                        "description": "Unique Property ID string."
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

**Réponse**

Une réponse réussie renvoie les détails de la classe mise à jour.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
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
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Update a portion of a class {#patch}

Vous pouvez mettre à jour une partie d&#39;une classe à l&#39;aide d&#39;une requête de PATCH. Il [!DNL Schema Registry] prend en charge toutes les opérations de correctif JSON standard, y compris `add`, `remove`et `replace`. Pour plus d’informations sur le correctif JSON, voir le guide [des fondamentaux de l’](../../landing/api-fundamentals.md#json-patch)API.

>[!NOTE]
>
>If you want to replace an entire resource with new values instead of updating individual fields, see the section on [replacing a class using a PUT operation](#put).

**Format d’API**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | The URL-encoded `$id` URI or `meta:altId` of the class you want to update. |

**Requête**

L&#39;exemple de requête ci-dessous met à jour la classe existante et `description` `title` l&#39;un de ses champs.

Le corps de la requête prend la forme d&#39;un tableau, chaque objet répertorié représentant une modification spécifique à un champ individuel. Chaque objet comprend l&#39;opération à exécuter (`op`), le champ sur lequel l&#39;opération doit être exécutée (`path`) et les informations à inclure dans cette opération (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Réponse**

La réponse montre que les deux opérations ont été réalisées avec succès. Le `description` champ a été mis à jour, ainsi que le `title` champ du `propertyId` .

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
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
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Suppression d’une classe {#delete}

Il peut parfois être nécessaire de supprimer une classe du registre des Schémas. Pour ce faire, il effectue une demande de DELETE avec l’ID de classe fourni dans le chemin d’accès.

**Format d’API**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Paramètre | Description |
| --- | --- |
| `{CLASS_ID}` | The URL-encoded `$id` URI or `meta:altId` of the class you want to delete. |

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

You can confirm the deletion by attempting a [lookup (GET) request](#lookup) for the class. You will need to include an `Accept` header in the request, but should receive an HTTP status 404 (Not Found) because the class has been removed from the Schema Registry.