---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un type de données
topic: developer guide
translation-type: tm+mt
source-git-commit: b0d8c8ee4df11d601d8feb122c70a9cd5d7d5b77
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Création d’un type de données

Lorsqu’il existe des structures de données communes que votre entreprise souhaite utiliser de plusieurs manières, vous pouvez définir un type de données. Les types de données permettent l&#39;utilisation cohérente de structures à champs multiples, avec plus de flexibilité que les mixins, car ils peuvent être inclus n&#39;importe où dans un schéma en les ajoutant comme `type` d&#39;un champ.

En d’autres termes, les types de données vous permettent de définir une hiérarchie d’objets une seule fois et d’y faire référence dans un champ de la même manière que tout autre type scalaire.

**Format d’API**

```http
POST /tenant/datatypes
```

**Requête**

La définition d’un type de données ne nécessite pas de champs `meta:extends` ou `meta:intendedToExtend` de champs, et les champs ne doivent pas non plus être imbriqués pour éviter les collisions.

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
              "shoppingCentre": "Shopping Center"
            }
          }
        } 
      }'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) et une charge utile contenant les détails du type de données nouvellement créé, y compris le `$id`, `meta:altId`et `version`. Ces trois valeurs sont en lecture seule et sont affectées par le Registre du Schéma.

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the property construction",
    "type": "object",
    "properties": {
        "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed.",
            "meta:xdmType": "int"
        },
        "constructionType": {
            "type": "string",
            "title": "Construction Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "freeStanding",
                "mall",
                "shoppingCenter"
            ],
            "meta:enum": {
                "freeStanding": "Free Standing Building",
                "mall": "Mall Space",
                "shoppingCentre": "Shopping Center"
            },
            "meta:xdmType": "string"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552087079285,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

L’exécution d’une requête GET pour liste de tous les types de données dans le conteneur locataire inclurait désormais le type de données Construction immobilière. Vous pouvez également effectuer une demande de recherche (GET) à l’aide de l’ `$id` URI codée URL pour vue directement le nouveau type de données. Veillez à inclure le `version` paramètre dans l’en-tête Accepter pour une demande de recherche.
