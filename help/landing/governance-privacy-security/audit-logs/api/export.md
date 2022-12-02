---
title: Point de terminaison de l’API d’exportation des événements d’audit
description: Découvrez comment exporter des événements de contrôle dans Experience Platform à l’aide de l’API de requête d’audit.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# Exportation d’une liste d’événements de contrôle

Vous pouvez récupérer des données d’événements en envoyant une requête de GET à la variable `/audit/export` point de terminaison , en spécifiant les événements que vous souhaitez récupérer dans la payload.

**Format d’API**

```http
GET /audit/export
```

| Paramètre | Description |
| --------- | ----------- |
| `timestamp` | Lors du filtrage par horodatage, il est recommandé d’utiliser une plage à l’aide des opérateurs > et &lt; plutôt qu’une valeur exacte. <br/>Exemple : ?property=timestamp&lt;2020-02-08T02:46:48.610862Z&amp;property=timestamp>2020-01-01T02:46:48.610862Z. |
| `status` | État de l’action. Un état peut être l’un des suivants : </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |
| `action` | Type d’action enregistrée pour l’événement. Une action peut être l’une des suivantes : <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `user` | L’utilisateur qui a exécuté l’événement. |
| `assetType` | Type de ressource Platform sur laquelle l’action a été effectuée. |

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Réponse**

Les résultats sont générés dans un fichier CSV en vue de l’exportation. Une réponse réussie renvoie HTTP 307 sans corps de réponse. Un lien vers le fichier d’exportation est fourni dans la variable `Location` en-tête de la réponse.
