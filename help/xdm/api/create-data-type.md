---
keywords: Experience Platform;home;popular topics;data type;data types;Data types;Data type;datatype;Datatype
solution: Experience Platform
title: Création d’un type de données
topic: developer guide
description: 'Lorsque votre organisation souhaite utiliser des structures de données communes de plusieurs manières, vous pouvez définir un type de données. Les types de données permettent l''utilisation cohérente de structures à champs multiples, avec plus de flexibilité que les mixins car ils peuvent être inclus n''importe où dans un schéma en les ajoutant comme "type" d''un champ. '
translation-type: tm+mt
source-git-commit: cc81d590f308c7e2677cec000c27e8aca42437f5
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 83%

---


# Création d’un type de données

Lorsque votre organisation souhaite utiliser des structures de données communes de plusieurs manières, vous pouvez définir un type de données. Les types de données permettent l’utilisation cohérente de structures à champs multiples avec plus de souplesse que les mixins, car ils peuvent être inclus n’importe où dans un schéma en les ajoutant en tant que `type` d’un champ.

En d’autres termes, les types de données vous permettent de définir une hiérarchie d’objets une seule fois et d’y faire référence dans un champ de la même manière que tout autre type scalaire.

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
              "shoppingCentre": "Shopping Center"
            }
          }
        } 
      }'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) ainsi qu’un payload contenant les détails du type de données nouvellement créé, y compris `$id`, `meta:altId` et `version`. These three values are read-only and are assigned by the [!DNL Schema Registry].

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

L’exécution d’une requête GET pour répertorier tous les types de données dans le conteneur client inclurait désormais le type de données Conception de propriétés. Vous pouvez également effectuer une requête de recherche (GET) à l’aide de l’URI `$id` encodé URL afin de visualiser directement le nouveau type de données. Veillez à inclure `version` dans l’en-tête Accept pour une requête de recherche.
