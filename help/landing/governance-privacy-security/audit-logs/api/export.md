---
title: Point d’entrée de l’API d’exportation des événements d’audit
description: Découvrez comment exporter des événements d’audit dans Experience Platform à l’aide de l’API Audit Query.
role: Developer
feature: Audits, API
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: d6575e44339ea41740fa18af07ce5b893f331488
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 4%

---

# Exporter une liste d’événements d’audit

Vous pouvez récupérer les données d’événement en adressant une requête GET au point d’entrée `/audit/export`, en spécifiant les événements que vous souhaitez récupérer dans la payload.

**Format d’API**

```http
GET /audit/export
```

| Paramètre | Description |
| --------- | ----------- |
| `timestamp` | Lors du filtrage par horodatage, il est recommandé d’utiliser une plage utilisant les opérateurs > et &lt; plutôt qu’une valeur exacte. <br/>Exemple : `?property=timestamp<2020-02-08T02:46:48.610862Z&property=timestamp>2020-01-01T02:46:48.610862Z`. |
| `status` | Statut de l’action. Un statut peut être l’un des suivants : </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul><br/>Exemple : `?property=status==Deny`. |
| `action` | Type d’action qui a été enregistré pour l’événement. Une action peut être l’une des suivantes : <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`Remove` </li><li>`Reset` </li><li>`Segment Activate` </li><li>`Segment remove` </li><li>`Update` </li></ul> Exemple : `?property=action==Create`. |
| `user` | L’utilisateur qui a exécuté l’événement. |
| `assetType` | Type de ressource Experience Platform sur laquelle l’action a été effectuée. <br/>Exemple : `?property=assetType==<an asset type>`. |

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

Les résultats sont générés dans un fichier CSV pour l’exportation, chaque entrée représentant un événement d’audit principal ou amélioré. Une réponse réussie renvoie un HTTP 307 sans corps de réponse. Un lien vers le fichier d’exportation est fourni dans l’en-tête de réponse `Location` .
