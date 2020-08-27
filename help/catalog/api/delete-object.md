---
keywords: Experience Platform;home;popular topics;delete an object;catalog service;api
solution: Experience Platform
title: Suppression d’un objet
topic: developer guide
description: Vous pouvez supprimer un objet Catalogue en fournissant son identifiant dans le chemin d’accès d’une requête DELETE.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 64%

---


# Suppression d’un objet

You can delete a [!DNL Catalog] object by providing its ID in the path of a DELETE request.

>[!WARNING]
>
>Soyez très prudent lorsque vous supprimez des objets, car vous ne pouvez pas revenir en arrière et pouvez produire des modifications avec rupture ailleurs dans [!DNL Experience Platform].

**Format d’API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>Le `DELETE /batches/{ID}` point de terminaison a été abandonné. Pour supprimer un lot, vous devez utiliser l&#39;API [d&#39;importation de](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)lot.

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | The type of [!DNL Catalog] object to be deleted. Les objets valides sont : <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique que vous souhaitez mettre à jour. |

**Requête**

La requête suivante supprime un jeu de données dont l’identifiant est précisé dans le chemin d’accès de requête.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 (OK) et un tableau contenant l’identifiant du jeu de données supprimé. Cet identifiant doit correspondre à celui envoyé dans la requête DELETE. Exécuter une requête GET sur l’objet supprimé renvoie un état HTTP 404 (introuvable), confirmant que le jeu de données a été supprimé avec succès.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>If no [!DNL Catalog] objects match the ID provided in your request, you may still receive an HTTP Status Code 200, but the response array will be empty.
