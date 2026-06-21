---
keywords: Experience Platform;accueil;rubriques populaires;supprimer un objet;service de catalogue;api
solution: Experience Platform
title: Supprimer un objet dans l’API
description: Vous pouvez supprimer un objet Catalogue en fournissant son identifiant dans le chemin d’accès d’une requête DELETE.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
TQID: https://experienceleague.adobe.com/puy0KU3bsw6Zfn-Q-q7JC0cBZorc7pj9M8PouA9htmI
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 210
ht-degree: 48%

---

# Supprimer un objet dans l’API

Vous pouvez supprimer un objet [!DNL Catalog] en fournissant son identifiant dans le chemin d’accès d’une requête DELETE.

>[!WARNING]
>
>Soyez très prudent lorsque vous supprimez des objets, car vous ne pouvez pas revenir en arrière et pouvez produire des modifications avec rupture ailleurs dans [!DNL Experience Platform].

**Format d’API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>Le point d’entrée `DELETE /batches/{ID}` est obsolète. Pour supprimer un lot, vous devez utiliser l’[API Batch Ingestion](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type de [!DNL Catalog] objet à supprimer. Les objets valides sont : <ul><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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
