---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Rechercher une ressource
topic: developer guide
translation-type: tm+mt
source-git-commit: 71c73a3899ccdd1c024a811b36c411915a3b14be

---


# Rechercher une ressource

Vous pouvez rechercher des ressources spécifiques en effectuant une requête GET qui inclut l’ `$id` (URI encodé en URL) de la ressource dans le chemin de requête.

**Format API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | où se trouvent les ressources (&quot;global&quot; ou &quot;locataire&quot;). |
| `{RESOURCE_TYPE}` | Type de ressource à récupérer de la bibliothèque de . Les types valides sont `datatypes`, `mixins`, `schemas`et `classes`. |
| `{RESOURCE_ID}` | URI codé en URL `$id` ou `meta:altId` de la ressource. |

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

Les demandes de recherche de ressources doivent `version` être incluses dans l’en-tête Accepter. Les en-têtes Accepter suivants sont disponibles pour les recherches :

| Accepter | Description |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw avec `$ref` et `allOf`, a des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolu, a des titres et des descriptions. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw avec `$ref` et `allOf`, sans titres ni descriptions. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolu, aucun titre ou description. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolu, les descripteurs inclus. |

>[!NOTE] Si vous fournissez la `major` version uniquement (1, 2, 3, etc.), le registre renverra automatiquement la dernière `minor` version (.1, .2, .3, etc.).

**Réponse**

Une réponse réussie renvoie les détails de la ressource. Les champs renvoyés dépendent de l’en-tête Accepter envoyé dans la requête. Testez différents en-têtes Accepter pour comparer les réponses et déterminer l’en-tête qui convient le mieux à votre cas d’utilisation.

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
