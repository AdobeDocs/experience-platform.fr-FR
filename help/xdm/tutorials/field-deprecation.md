---
title: Obsolescence d’un champ XDM
description: Découvrez comment abandonner les champs de modèle de données d’expérience (XDM) dans l’API Schema Registry.
source-git-commit: dc400dce8a77f27347e767230faf7301afc7c1fb
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 11%

---

# Obsolescence d’un champ XDM

Dans le modèle de données d’expérience (XDM), vous pouvez abandonner un champ dans un schéma ou une ressource personnalisée à l’aide de la variable [API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Ce document explique comment abandonner les champs pour différentes ressources XDM.

## Prise en main

Ce tutoriel nécessite des appels à l’API Schema Registry. Veuillez consulter la section [guide de développement](../api/getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer ces appels d’API. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête et à ses valeurs possibles).`Accept`

## Obsolescence d’un champ personnalisé {#custom}

Pour abandonner un champ dans une classe personnalisée, un groupe de champs ou un type de données personnalisé, mettez à jour la ressource personnalisée par le biais d’une requête de PUT ou de PATCH et ajoutez l’attribut . `meta:status: deprecated` sur le champ en question.

>[!NOTE]
>
>Pour obtenir des informations générales sur la mise à jour des ressources personnalisées dans XDM, consultez la documentation suivante :
>
>* [Mettre à jour une classe](../api/classes.md#patch)
>* [Mettre à jour un groupe de champs](../api/field-groups.md#patch)
>* [Mise à jour d’un type de données](../api/data-types.md#patch)


L’exemple d’appel API ci-dessous rend obsolète un champ dans un type de données personnalisé.

**Format d’API**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**Requête**

La requête suivante rend obsolète le `expansionArea` champ d’un type de données qui décrit une propriété de l’emplacement.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/properties/expansionArea/meta:status",
          "value": "deprecated"
        }
      ]'
```

**Réponse**

Une réponse réussie renvoie les détails de mise à jour de la ressource personnalisée, avec le champ obsolète contenant un `meta:status` valeur de `deprecated`. La réponse ci-dessous a été réduite pour gagner de l’espace.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a real-estate property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "expansionArea": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
              "meta:status": "deprecated",
            },
            "propertyName": {
              "title": "Property Name",
              "description": "Name of the property",
              "type": "string"
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
            },
            "squareFeet": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
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

## Obsolescence d’un champ standard dans un schéma {#standard}

Les champs des classes standard, des groupes de champs et des types de données ne peuvent pas être directement obsolètes. À la place, vous pouvez abandonner leur utilisation dans les schémas individuels qui utilisent ces ressources standard à l’aide d’un descripteur.

### Création d’un descripteur d’obsolescence de champ {#create-descriptor}

Pour créer un descripteur pour les champs de schéma que vous souhaitez rendre obsolètes, envoyez une requête de POST au `/tenant/descriptors` point de terminaison .

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:descriptorDeprecated",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/faxPhone"
      }'
```

| Propriété | Description |
| --- | --- |
| `@type` | Type de descripteur. Pour un descripteur d’obsolescence de champ, cette valeur doit être définie sur `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | L’URI `$id` du schéma auquel vous appliquez le descripteur. |
| `xdm:sourceVersion` | Version du schéma auquel vous appliquez le descripteur. Doit être défini sur `1`. |
| `xdm:sourceProperty` | Le chemin d’accès à la propriété dans le schéma auquel vous appliquez le descripteur. Si vous souhaitez appliquer le descripteur à plusieurs propriétés, vous pouvez fournir une liste de chemins sous la forme d’un tableau (par exemple, `["/firstName", "/lastName"]`). |

**Réponse**

```json
{
    "@id": "d882b1202bac0ac71f1e31fbcd9afbcc37f364270186b4b3",
    "@type": "xdm:descriptorDeprecated",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/faxPhone",
    "imsOrg": "{IMS_ORG}",
    "version": "1",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

### Vérification du champ obsolète {#verify-deprecation}

Une fois le descripteur appliqué, vous pouvez vérifier si le champ a été abandonné en recherchant le schéma en question tout en utilisant la variable `Accept` en-tête .

>[!NOTE]
>
>L’affichage de champs obsolètes lors de la liste de schémas n’est actuellement pas pris en charge.

**Format d’API**

```http
GET /tenant/schemas
```

**Requête**

Pour inclure des informations sur les champs obsolètes dans la réponse de l’API, vous devez définir la variable `Accept` en-tête à `application/vnd.adobe.xed-deprecatefield+json; version=1`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-deprecatefield+json; version=1'
```

**Réponse**

Une réponse réussie renvoie les détails du schéma, avec le champ obsolète contenant un `meta:status` valeur de `deprecated`. La réponse ci-dessous a été réduite pour gagner de l’espace.

```json
"faxPhone": {
    "title": "Fax phone",
    "description": "Fax phone number.",
    "type": "object",
    "meta:xdmType": "object",
    "properties": {},
    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
    "meta:xdmField": "xdm:faxPhone",
    "meta:status": "deprecated"
}
```

## Étapes suivantes

Ce document explique comment abandonner les champs XDM à l’aide de l’API Schema Registry. Pour plus d’informations sur la configuration des champs pour les ressources personnalisées, consultez le guide sur [définition des champs XDM dans l’API](./custom-fields-api.md). Pour plus d’informations sur la gestion des descripteurs, voir [guide de point de terminaison des descripteurs](../api/descriptors.md).
