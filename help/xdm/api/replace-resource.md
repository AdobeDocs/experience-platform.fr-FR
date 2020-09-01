---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;replace;Replace;put;PUT
solution: Experience Platform
title: Remplacement d’une ressource
description: Le registre des schémas vous permet de remplacer une ressource entière par une opération PUT. Cette opération réécrivant la ressource, le corps de requête doit inclure tous les champs qui seraient requis pour créer une ressource à l’aide d’une requête POST.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 91%

---


# Remplacement d’une ressource

The [!DNL Schema Registry] allows you to replace an entire resource through a PUT operation. Cette opération réécrivant la ressource, le corps de requête doit inclure tous les champs qui seraient requis pour créer une ressource à l’aide d’une requête POST.

Cette méthode est particulièrement utile si vous souhaitez mettre à jour simultanément un grand nombre d’informations dans la ressource.

>[!NOTE]
>
>Si vous ne souhaitez mettre à jour qu’une partie d’une ressource au lieu de la remplacer entièrement, consultez le document sur la [mise à jour d’une ressource à l’aide d’une opération PATCH](update-resource.md).

**Format d’API**

Une requête PUT ne peut être exécutée que sur les ressources définies dans le conteneur client.

```http
PUT /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_TYPE}` | The type of resource to be updated from the [!DNL Schema Library]. Les types valides sont `datatypes`, `mixins`, `schemas` et `classes`. |
| `{RESOURCE_ID}` | URI `$id` encodé par l’URL ou le `meta:altId` de la ressource. |

**Requête**

Cet exemple de requête remplace le type de données Property Construction créé dans un exemple précédent. Le corps de la requête ressemble à la requête POST utilisée pour créer le type de données, sauf qu’il contient désormais un jeu de champs mis à jour avec de nouvelles valeurs remplaçant ce qui a été défini précédemment.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the construction of the property.",
        "type":"object",
        "properties": {
          "dateOpened": {
            "type":"string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "standAlone",
              "highRise",
              "stripMall"
            ],
            "meta:enum": {
              "standAlone": "Stand-Alone Building",
              "highRise": "High Rise Building",
              "stripMall": "Strip Mall"
            }
          },
          "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property."
          },
          "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property."
          }
        } 
      }'
```

**Réponse**

Une réponse réussie renvoie les détails du type de données, en indiquant les champs et les valeurs mis à jour, comme indiqué dans la requête.

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the construction of the property.",
    "type": "object",
    "properties": {
        "dateOpened": {
            "type": "string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened.",
            "meta:xdmType": "date"
        },
        "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "standAlone",
                "highRise",
                "stripMall"
            ],
            "meta:enum": {
                "standAlone": "Stand-Alone Building",
                "highRise": "High Rise Building",
                "stripMall": "Strip Mall"
            },
            "meta:xdmType": "string"
        },
        "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property.",
            "meta:xdmType": "string"
        },
        "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property.",
            "meta:xdmType": "int"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.2",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552090569013,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
