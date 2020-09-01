---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;delete
solution: Experience Platform
title: Suppression d’une ressource
describe: It may occasionally be necessary to remove resource from the Schema Registry. Only resources that you create in the tenant container may be deleted. This is done by performing a DELETE request using the $id of the resource you wish to delete.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 63%

---


# Suppression d’une ressource

It may occasionally be necessary to remove (DELETE) a resource from the [!DNL Schema Registry]. Seules les ressources créées dans le conteneur de client peuvent être supprimées. Pour ce faire, exécutez une requête DELETE à l’aide du `$id` de la ressource que vous souhaitez supprimer.

**Format d’API**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_TYPE}` | The type of resource to be deleted from the [!DNL Schema Library]. Les types valides sont `datatypes`, `mixins`, `schemas` et `classes`. |
| `{RESOURCE_ID}` | URI `$id` encodé par l’URL ou le `meta:altId` de la ressource. |

**Requête**

Les requêtes DELETE ne nécessitent pas d’en-têtes Accept.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant d’envoyer une requête de recherche (GET) à la ressource. You will need to include an Accept header in the request, but should receive an HTTP status 404 (Not Found) because the resource has been removed from the [!DNL Schema Registry].