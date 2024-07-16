---
keywords: Experience Platform;accueil;rubriques populaires;supprimer un objet;service de catalogue;api
solution: Experience Platform
title: Suppression d’un objet dans l’API
description: Vous pouvez supprimer un objet Catalogue en fournissant son identifiant dans le chemin d’accès d’une requête DELETE.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: d88336d314e767a068ef6524161baeb642a58433
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 48%

---

# Suppression d’un objet dans l’API

Vous pouvez supprimer un objet [!DNL Catalog] en fournissant son identifiant dans le chemin d’accès d’une requête de DELETE.

>[!WARNING]
>
>Soyez très prudent lors de la suppression d’objets, car cette opération ne peut pas être annulée et peut produire des modifications avec rupture ailleurs dans [!DNL Experience Platform].

**Format d’API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>Le point d’entrée `DELETE /batches/{ID}` est obsolète. Pour supprimer un lot, vous devez utiliser l’ [API d’ingestion par lots](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Le type d’objet [!DNL Catalog] à supprimer. Les objets valides sont : <ul><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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
>Si aucun objet [!DNL Catalog] ne correspond à l’identifiant fourni dans votre requête, vous pouvez toujours recevoir un code d’état HTTP 200, mais le tableau de réponse sera vide.
