---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;lookup;Lookup;get;GET
solution: Experience Platform
title: Recherche d’une ressource
description: Vous pouvez rechercher des ressources spécifiques dans l'API Schéma Registry en faisant une demande de GET qui inclut $id (URI encodé en URL) de la ressource dans le chemin de la demande.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 81%

---


# Recherche d’une ressource

Vous pouvez rechercher une ressource spécifique en effectuant une requête GET qui comprend l’identifiant `$id` (URI encodé URL) de la ressource dans le chemin de la requête.

**Format d’API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Le conteneur où se trouvent les ressources (« global » ou « client »). |
| `{RESOURCE_TYPE}` | The type of resource to retrieve from the [!DNL Schema Library]. Les types valides sont `datatypes`, `mixins`, `schemas` et `classes`. |
| `{RESOURCE_ID}` | URI `$id` encodé par l’URL ou le `meta:altId` de la ressource. |

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/mixins/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile-person-details \
  -H 'Accept: application/vnd.adobe.xed+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Les requêtes de recherche de ressource doivent inclure une `version` dans l’en-tête Accept. Vous pouvez utiliser les en-têtes Accept suivants pour les recherches :

| Accept | Description |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Brut avec `$ref` et `allOf`, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolus, contient des titres et des descriptions. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Brut avec `$ref` et `allOf`, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolus, ne contient aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolus, contient des descripteurs. |

>[!NOTE]
>
> Si vous ne fournissez que la version `major` (par exemple, 1, 2, 3, etc.), le registre renverra automatiquement la dernière version `minor`.

**Réponse**

Une réponse réussie renvoie les détails de la ressource. Les champs renvoyés dépendent de l’en-tête Accept envoyé dans la requête. Testez différents en-têtes Accept pour comparer les réponses et déterminer l’en-tête qui convient le mieux à votre cas d’utilisation.

```JSON
{
    "$id": "https://ns.adobe.com/xdm/context/profile-person-details",
    "title": "Profile Person Details",
    "type": "object",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Profile person details including naming, gender etc.",
    "definitions": {
        "profile-person-details": {
            "properties": {
                "person": {
                    "title": "Person",
                    "$ref": "https://ns.adobe.com/xdm/context/person",
                    "description": "An individual actor, contact, or owner.",
                    "meta:xdmField": "xdm:person"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
        },
        {
            "$ref": "#/definitions/profile-person-details"
        }
    ],
    "meta:xdmId": "https://ns.adobe.com/xdm/context/profile-person-details",
    "meta:altId": "_xdm.context.profile-person-details",
    "meta:xdmType": "object",
    "meta:status": "experimental",
    "version": "1",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551745787442,
        "repo:lastModifiedDate": 1551745787442
    }
}
```
