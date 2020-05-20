---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Remplacer une ressource
topic: developer guide
translation-type: tm+mt
source-git-commit: 67826f838951b3202a6a04321c28daa8ee883d20
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---


# Remplacer une ressource

Le Registre de Schéma vous permet de remplacer une ressource entière par une opération PUT. Cette opération réécrit essentiellement la ressource. Par conséquent, l&#39;organisme de demande doit inclure tous les champs requis lors de la création d&#39;une ressource à l&#39;aide d&#39;une requête POST.

Cette méthode est particulièrement utile si vous souhaitez mettre à jour un grand nombre d&#39;informations dans la ressource en même temps.

>[!NOTE] Si vous souhaitez seulement mettre à jour une partie d&#39;une ressource au lieu de la remplacer entièrement, consultez le document sur la [mise à jour d&#39;une ressource à l&#39;aide d&#39;une opération](update-resource.md)PATCH.

**Format d’API**

Une requête PUT ne peut être exécutée que sur les ressources que vous définissez dans le conteneur client.

```http
PUT /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_TYPE}` | Type de ressource à mettre à jour à partir de la bibliothèque de Schémas. Les types valides sont `datatypes`, `mixins`, `schemas`et `classes`. |
| `{RESOURCE_ID}` | URI codé en URL `$id` ou `meta:altId` de la ressource. |

**Requête**

Cet exemple de demande remplace le type de données Construction de propriétés qui a été créé dans un exemple précédent. Le corps de la requête ressemble à celui de la requête POST utilisée pour créer le type de données, sauf qu’il contient désormais un ensemble de champs mis à jour et que de nouvelles valeurs remplacent ce qui était précédemment défini.

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

Une réponse positive renvoie les détails du type de données, en indiquant les champs et valeurs mis à jour, comme indiqué dans la requête.

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
