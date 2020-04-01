---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Suppression d’un objet
topic: developer guide
translation-type: tm+mt
source-git-commit: 85b497d87fcfb54f390302036ce24c98c6dba6ff

---


# Suppression d’un objet

Vous pouvez supprimer un objet Catalog en indiquant son ID dans le chemin d’une requête DELETE.

>[!WARNING] Soyez très prudent lors de la suppression d’objets, car cette opération ne peut pas être annulée et peut entraîner des modifications de rupture ailleurs dans la plateforme d’expérience.

**Format API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

| Paramètre | Description |
| --- | --- |
| `{OBJECT_TYPE}` | Type d’objet Catalog à supprimer. Les objets valides sont : <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifiant de l’objet spécifique que vous souhaitez mettre à jour. |

**Requête**

La requête suivante supprime un jeu de données dont l’ID est spécifié dans le chemin d’accès à la requête.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 (OK) et un tableau contenant l’ID du jeu de données supprimé. Cet identifiant doit correspondre à celui envoyé dans la requête DELETE. L’exécution d’une requête GET sur l’objet supprimé renvoie l’état HTTP 404 (Introuvable), confirmant que le jeu de données a bien été supprimé.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE] Si aucun objet Catalog ne correspond à l’ID fourni dans votre requête, vous pouvez toujours recevoir un code d’état HTTP 200, mais le tableau de réponses sera vide.
