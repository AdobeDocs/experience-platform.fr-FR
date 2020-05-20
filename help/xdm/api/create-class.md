---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Créer une classe
topic: developer guide
translation-type: tm+mt
source-git-commit: 60911e32fd9235be2a258e60818011a42cd5ceba
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---


# Créer une classe

Le bloc de construction principal d&#39;un schéma est une classe. La classe contient le jeu minimum de champs à définir pour capturer les données de base d&#39;un schéma. Par exemple, si vous concevez un schéma pour les voitures et les camions, ils utiliseraient très probablement une classe appelée Véhicule qui décrivait les propriétés communes de base de tous les véhicules.

Il existe plusieurs classes standard fournies par Adobe et d’autres partenaires Experience Platform, mais vous pouvez également définir vos propres classes et les enregistrer dans le registre des Schémas. Vous pouvez ensuite composer un schéma qui implémente la classe que vous avez créée et définir des mixins compatibles avec votre nouvelle classe définie.

>[!NOTE] Lors de la composition d&#39;un schéma basé sur une classe que vous définissez, vous ne pourrez pas utiliser de mixins standard. Chaque mixin définit les classes avec lesquelles ils sont compatibles dans leur `meta:intendedToExtend` attribut. Une fois que vous commencez à définir des mixins compatibles avec votre nouvelle classe (en utilisant la `$id` de votre nouvelle classe dans le `meta:intendedToExtend` champ du mixin), vous pourrez réutiliser ces mixins chaque fois que vous définissez un schéma qui implémente la classe que vous avez définie. Pour plus d’informations, consultez les sections sur la [création de mixins](create-mixin.md) et la [création de schémas](create-schema.md) .

**Format d’API**

```http
POST /tenant/classes
```

**Requête**

La demande de création (POST) d&#39;une classe doit inclure un `allOf` attribut contenant une ou deux valeurs `$ref` : `https://ns.adobe.com/xdm/data/record` ou `https://ns.adobe.com/xdm/data/time-series`. Ces valeurs représentent le comportement sur lequel la classe est basée (enregistrement ou série chronologique, respectivement). Pour plus d&#39;informations sur les différences entre les données d&#39;enregistrement et les données de série chronologique, consultez la section sur les types de comportement dans les [bases de la composition](../schema/composition.md)du schéma.

Lorsque vous définissez une classe, vous pouvez également inclure des mixins ou des champs personnalisés dans la définition de classe. Les mixins et champs ajoutés seraient alors inclus dans tous les schémas qui implémentent la classe. L’exemple de demande suivant définit une classe appelée &quot;Propriété&quot;, qui capture des informations concernant les différentes propriétés détenues et exploitées par une société. Il inclut un `propertyId` champ à inclure chaque fois que la classe est utilisée.

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
| `_{TENANT_ID}` | L’ `TENANT_ID` espace de nommage de votre organisation. Toutes les ressources créées par votre organisation doivent inclure cette propriété pour éviter les collisions avec d&#39;autres ressources dans le registre des Schémas. |
| `allOf` | liste de ressources dont les propriétés doivent être héritées par la nouvelle classe. L&#39;un des `$ref` objets du tableau définit le comportement de la classe. Dans cet exemple, la classe hérite du comportement &quot;record&quot;. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) et une charge utile contenant les détails de la nouvelle classe, y compris la classe `$id`, `meta:altId`et `version`. Ces trois valeurs sont en lecture seule et sont affectées par le Registre du Schéma.

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

L’exécution d’une demande GET pour liste à toutes les classes du conteneur locataire inclurait désormais la classe Property. Vous pouvez également effectuer une requête de recherche (GET) à l’aide de l’ `$id` URI codée URL pour vue directement la nouvelle classe. Veillez à inclure le `version` dans l’en-tête Accepter lors de l’exécution d’une demande de recherche.
