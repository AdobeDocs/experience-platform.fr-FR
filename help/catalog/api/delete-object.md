---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Suppression d’un objet
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 3%

---


# Suppression d’un objet

Vous pouvez supprimer un objet Catalog en indiquant son identifiant dans le chemin d’une requête de DELETE.

>[!WARNING]
>
>Soyez très prudent lors de la suppression d’objets, car cette opération ne peut pas être annulée et peut entraîner des modifications irréversibles ailleurs dans l’Experience Platform.

**Format d’API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>Le `DELETE /batches/{ID}` point de terminaison a été abandonné. Pour supprimer un lot, vous devez utiliser l&#39;API [d&#39;importation de](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)lot.

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à supprimer. Les objets valides sont : <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique à mettre à jour. |

**Requête**

La requête suivante supprime un jeu de données dont l&#39;ID est spécifié dans le chemin d&#39;accès à la requête.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l&#39;état HTTP 200 (OK) et un tableau contenant l&#39;ID du jeu de données supprimé. Cet identifiant doit correspondre à celui envoyé dans la demande du DELETE. L’exécution d’une requête GET sur l’objet supprimé renvoie l’état HTTP 404 (Introuvable), confirmant que le jeu de données a bien été supprimé.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Si aucun objet Catalog ne correspond à l’ID fourni dans votre requête, vous pouvez toujours recevoir un code d’état HTTP 200, mais le tableau de réponses sera vide.
