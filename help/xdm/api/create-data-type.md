---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un type de données
topic: developer guide
translation-type: tm+mt
source-git-commit: b0d8c8ee4df11d601d8feb122c70a9cd5d7d5b77

---


# Création d’un type de données

Lorsqu’il existe des structures de données communes que votre entreprise souhaite utiliser de plusieurs manières, vous pouvez définir un type de données. Les types de données permettent l’utilisation cohérente de structures à champs multiples, avec plus de souplesse que les mixins, car ils peuvent être inclus n’importe où dans un  en les ajoutant comme champ `type` de saisie.

En d’autres termes, les types de données vous permettent de définir une hiérarchie d’objets une seule fois et d’y faire référence dans un champ de la même manière que tout autre type scalaire.

**Format API**

```http
POST /tenant/datatypes
```

**Requête**

La définition d’un type de données ne nécessite pas de champs `meta:extends` ou `meta:intendedToExtend` , pas plus que les champs ne doivent être imbriqués pour éviter les collisions.

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

Une réponse réussie renvoie l’état HTTP 201 (Créé) et une charge utile contenant les détails du type de données nouvellement créé, y compris le `$id`, `meta:altId`et `version`. Ces trois valeurs sont en lecture seule et sont attribuées par le Registre des  du.

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

L’exécution d’une requête GET pour  tous les types de données dans le locataire  inclurait désormais le type de données Construction de propriété. Vous pouvez également effectuer une requête GET (recherche) à l’aide de l’ `$id` URI codée URL afin de directement le nouveau type de données. Veillez à inclure le paramètre `version` dans l’en-tête Accepter pour une demande de recherche.
