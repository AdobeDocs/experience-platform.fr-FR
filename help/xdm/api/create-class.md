---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;class;Class;classes;Classes;create
solution: Experience Platform
title: Création d’une classe
description: Une classe est le bloc de création principal d’un schéma. La classe contient l’ensemble de champs minimum devant être défini afin de capturer les données principales d’un schéma. Par exemple, si vous concevez un schéma pour des voitures et des camions, il est fort probable que vous utilisiez une classe intitulée Véhicule pour décrire les propriétés courantes de base de tous les véhicules.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 90%

---


# Création d’une classe

Une classe est le bloc de création principal d’un schéma. La classe contient l’ensemble de champs minimum devant être défini afin de capturer les données principales d’un schéma. Par exemple, si vous concevez un schéma pour des voitures et des camions, il est fort probable que vous utilisiez une classe intitulée Véhicule pour décrire les propriétés courantes de base de tous les véhicules.

There are several standard classes provided by Adobe and other [!DNL Experience Platform] partners, but you may also define your own classes and save them to the [!DNL Schema Registry]. Vous pouvez ensuite composer un schéma qui met en œuvre la classe que vous avez créée et définir des mixins compatibles avec la classe que vous venez de définir.

>[!NOTE]
>
>Lorsque vous composez un schéma basé sur une classe que vous avez définie, vous ne pourrez pas utiliser les mixins standard. Chaque mixin définit les classes avec lesquelles il est compatible dans l’attribut `meta:intendedToExtend`. Lorsque vous commencez à définir des mixins compatibles avec votre nouvelle classe (en utilisant le `$id` de votre nouvelle classe dans le champ `meta:intendedToExtend` du mixin), vous pourrez réutiliser ces mixins chaque fois que vous définissez un schéma qui met en œuvre la classe que vous avez définie. Pour plus d’informations, reportez-vous aux sections relatives à la [création de mixins](create-mixin.md) et à la [création de schémas](create-schema.md).

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

L’exécution d’une requête GET pour lister toutes les classes dans le conteneur client inclurait désormais la classe Propriété. Vous pouvez également effectuer une requête de recherche (GET) à l’aide de l’URI `$id` encodé URL afin de visualiser directement la nouvelle classe. Veillez à inclure la clé `version` dans l’en-tête Accept lorsque vous réalisez une requête de recherche.
