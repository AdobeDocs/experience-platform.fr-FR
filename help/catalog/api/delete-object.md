---
keywords: Experience Platform;accueil;rubriques populaires;supprimer un objet;service de catalogue;api
solution: Experience Platform
title: Suppression d’un objet dans l’API
description: Vous pouvez supprimer un objet Catalogue en fournissant son identifiant dans le chemin d’accès d’une requête DELETE.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 56%

---

# Suppression d’un objet dans l’API

Vous pouvez supprimer une [!DNL Catalog] en indiquant son identifiant dans le chemin d’accès d’une requête de DELETE.

>[!WARNING]
>
>Soyez très prudent lorsque vous supprimez des objets, car vous ne pouvez pas revenir en arrière et pouvez produire des modifications avec rupture ailleurs dans [!DNL Experience Platform].

**Format d’API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>Le `DELETE /batches/{ID}` Le point de terminaison a été abandonné. Pour supprimer un lot, vous devez utiliser la variable [API Batch Ingestion](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Le type de [!DNL Catalog] à supprimer. Les objets valides sont : <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique que vous souhaitez mettre à jour. |

**Requête**

La requête suivante supprime un jeu de données dont l’identifiant est précisé dans le chemin d’accès de requête.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>Si non [!DNL Catalog] correspondent à l’identifiant fourni dans votre requête. Vous pouvez toujours recevoir un code d’état HTTP 200, mais le tableau de réponse sera vide.
