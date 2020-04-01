---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’une classe
topic: developer guide
translation-type: tm+mt
source-git-commit: 60911e32fd9235be2a258e60818011a42cd5ceba

---


# Création d’une classe

Le bloc de construction principal d’un  est une classe. La classe contient le jeu minimum de champs à définir pour capturer les données de base d’un  de. Par exemple, si vous conceviez un  pour les voitures et les camions, ils utiliseraient probablement une classe appelée Véhicule qui décrivait les propriétés communes de base de tous les véhicules.

Il existe plusieurs classes standard fournies par Adobe et d’autres partenaires d’Experience Platform, mais vous pouvez également définir vos propres classes et les enregistrer dans le registre des  d’expérience. Vous pouvez ensuite composer un  qui implémente la classe que vous avez créée et définir des mixins compatibles avec votre nouvelle classe.

>[!NOTE] Lors de la composition d’un  basé sur une classe que vous définissez, vous ne pourrez pas utiliser de mixins standard. Chaque mixin définit les classes avec lesquelles il est compatible dans leur `meta:intendedToExtend` attribut. Une fois que vous avez commencé à définir des mixins compatibles avec votre nouvelle classe (en utilisant la `$id` de votre nouvelle classe dans le `meta:intendedToExtend` champ du mixin), vous pourrez réutiliser ces mixins chaque fois que vous définissez un qui met en oeuvre la classe que vous avez définie. Pour plus d’informations, reportez-vous aux sections relatives à la [création de mixins](create-mixin.md) et à la [création de](create-schema.md) de.

**Format API**

```http
POST /tenant/classes
```

**Requête**

La demande de création (POST) d’une classe doit inclure un `allOf` attribut contenant une ou deux valeurs `$ref` : `https://ns.adobe.com/xdm/data/record` ou `https://ns.adobe.com/xdm/data/time-series`. Ces valeurs représentent le comportement sur lequel la classe est basée (enregistrement ou série chronologique, respectivement). Pour plus d’informations sur les différences entre les données d’enregistrement et les données de série chronologique, voir la section sur les types de comportement dans les [bases de la composition](../schema/composition.md)des .

Lorsque vous définissez une classe, vous pouvez également inclure des mixins ou des champs personnalisés dans la définition de classe. Les mixins et les champs ajoutés seraient alors inclus dans tous les  qui implémentent la classe. L’exemple de requête suivant définit une classe appelée &quot;Propriété&quot;, qui capture les informations concernant les différentes propriétés détenues et exploitées par un . Il inclut un `propertyId` champ à inclure chaque fois que la classe est utilisée.

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
| `_{TENANT_ID}` | Le `TENANT_ID` pour votre organisation. Toutes les ressources créées par votre organisation doivent inclure cette propriété pour éviter les collisions avec d&#39;autres ressources dans le Registre des  de. |
| `allOf` | de ressources dont les propriétés doivent être héritées par la nouvelle classe. L’un des `$ref` objets du tableau définit le comportement de la classe. Dans cet exemple, la classe hérite du comportement &quot;record&quot;. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) et une charge utile contenant les détails de la nouvelle classe, y compris la `$id`, `meta:altId`et `version`. Ces trois valeurs sont en lecture seule et sont attribuées par le Registre des  du.

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

L’exécution d’une requête GET pour  toutes les classes de l’locataire  inclurait désormais la classe Property. Vous pouvez également effectuer une requête GET (recherche) à l’aide de l’ `$id` URI codée URL pour direct  la nouvelle classe. Veillez à inclure le `version` paramètre dans l’en-tête Accepter lors de l’exécution d’une requête de recherche.
