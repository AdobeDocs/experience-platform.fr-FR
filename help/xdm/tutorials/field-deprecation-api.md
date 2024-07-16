---
title: Rendre obsolète un champ XDM dans l’API
description: Découvrez comment rendre obsolètes les champs de modèle de données d’expérience (XDM) dans l’API Schema Registry.
exl-id: e49517c4-608d-4e05-8466-75724ca984a8
source-git-commit: f9f783b75bff66d1bf3e9c6d1ed1c543bd248302
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 100%

---

# Rendre obsolète un champ XDM dans l’API

Dans le modèle de données d’expérience (XDM), vous pouvez rendre obsolète un champ dans un schéma ou une ressource personnalisée à l’aide de l’[API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). En cas d’obsolescence d’un champ, il est masqué dans les IU en aval, telles que l’espace de travail des [!UICONTROL Profils] et Customer Journey Analytics, mais il s’agit d’une modification sans rupture qui n’a pas d’incidence négative sur les flux de données existants.

Ce document explique comment rendre obsolètes les champs pour différentes ressources XDM. Pour savoir comment rendre obsolète un champ XDM à l’aide de l’éditeur de schémas dans l’IU d’Experience Platform, consultez le tutoriel sur l’[obsolescence d’un champ XDM dans l’IU](./field-deprecation-ui.md).

## Prise en main

Ce tutoriel nécessite d’effectuer des appels à l’API Schema Registry. Consultez le [guide de développement](../api/getting-started.md) pour obtenir des informations importantes que vous devez connaître pour effectuer ces appels API. Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête `Accept` et à ses valeurs possibles).

## Rendre obsolète un champ personnalisé {#custom}

Pour rendre obsolète un champ dans une classe, un groupe de champs ou un type de données personnalisés, mettez à jour la ressource personnalisée par le biais d’une requête PUT ou PATCH et ajoutez l’attribut `meta:status: deprecated` au champ en question.

>[!NOTE]
>
>Pour obtenir des informations générales sur la mise à jour des ressources personnalisées dans XDM, consultez la documentation suivante :
>
>* [Mettre à jour une classe](../api/classes.md#patch)
>* [Mettre à jour un groupe de champs](../api/field-groups.md#patch)
>* [Mettre à jour un type de données](../api/data-types.md#patch)

L’exemple d’appel API ci-dessous rend obsolète un champ dans un type de données personnalisées.

**Format d’API**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**Requête**

La requête suivante rend obsolète le champ `expansionArea` d’un type de données qui décrit une propriété immobilière.

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

Une réponse réussie renvoie les détails de mise à jour de la ressource personnalisée, avec le champ obsolète contenant une valeur `meta:status` de `deprecated`. La réponse ci-dessous a été réduite pour gagner de l’espace.

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

## Rendre obsolète un champ standard dans un schéma {#standard}

Les champs des classes, des groupes de champs et des types de données standard ne peuvent pas être directement rendus obsolètes. À la place, vous pouvez rendre obsolète leur utilisation dans les schémas individuels qui utilisent ces ressources standard à l’aide d’un descripteur.

### Créer un descripteur d’obsolescence de champ {#create-descriptor}

Pour créer un descripteur pour les champs de schéma que vous souhaitez rendre obsolètes, envoyez une requête POST au point d’entrée `/tenant/descriptors`.

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
| `@type` | Le type de descripteur. Pour un descripteur d’obsolescence de champ, cette valeur doit être définie sur `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | L’`$id` de l’URI du schéma auquel vous appliquez le descripteur. |
| `xdm:sourceVersion` | La version du schéma auquel vous appliquez le descripteur. Doit être définie sur `1`. |
| `xdm:sourceProperty` | Le chemin d’accès à la propriété dans le schéma auquel vous appliquez le descripteur. Si vous souhaitez appliquer le descripteur à plusieurs propriétés, vous pouvez fournir une liste de chemins d’accès sous la forme d’un tableau (par exemple, `["/firstName", "/lastName"]`). |

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

### Vérifier le champ obsolète {#verify-deprecation}

Une fois le descripteur appliqué, vous pouvez vérifier si le champ est obsolète en recherchant le schéma en question tout en utilisant l’en-tête `Accept` approprié.

>[!NOTE]
>
>L’affichage de champs obsolètes lors de la liste de schémas n’est actuellement pas pris en charge.

**Format d’API**

```http
GET /tenant/schemas
```

**Requête**

Pour inclure des informations sur les champs obsolètes dans la réponse API, vous devez définir l’en-tête `Accept` sur `application/vnd.adobe.xed-deprecatefield+json; version=1`.

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

Une réponse réussie renvoie les détails du schéma, avec le champ obsolète contenant une valeur `meta:status` de `deprecated`. La réponse ci-dessous a été réduite pour gagner de l’espace.

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

Ce document explique comment rendre obsolètes les champs XDM à l’aide de l’API Schema Registry. Pour plus d’informations sur la configuration des champs pour les ressources personnalisées, consultez le guide sur la [définition des champs XDM dans l’API](./custom-fields-api.md). Pour plus d’informations sur la gestion des descripteurs, consultez le [guide de point d’entrée des descripteurs](../api/descriptors.md).
