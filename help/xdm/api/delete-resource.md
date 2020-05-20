---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Supprimer une ressource
topic: developer guide
translation-type: tm+mt
source-git-commit: d9ab2b1226b051be43f8fc0dd222bc075caed6f0
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 7%

---


# Supprimer une ressource

Il peut parfois être nécessaire de supprimer (SUPPRIMER) une ressource du registre des Schémas. Seules les ressources que vous créez dans le conteneur client peuvent être supprimées. Pour ce faire, vous devez exécuter une requête DELETE à l&#39;aide `$id` de la ressource que vous souhaitez supprimer.

**Format d’API**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Paramètre | Description |
| --- | --- |
| `{RESOURCE_TYPE}` | Type de ressource à supprimer de la bibliothèque de Schémas. Les types valides sont `datatypes`, `mixins`, `schemas`et `classes`. |
| `{RESOURCE_ID}` | URI codé en URL `$id` ou `meta:altId` de la ressource. |

**Requête**

Les requêtes DELETE ne nécessitent pas d’en-têtes Accepter.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 204 (Aucun contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant d&#39;envoyer une requête GET à la ressource. Vous devez inclure un en-tête Accepter dans la requête, mais vous devez recevoir l&#39;état HTTP 404 (Non trouvé) car la ressource a été supprimée du Registre du Schéma.