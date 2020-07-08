---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un jeu de données
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 2%

---


# Création d’un jeu de données

Pour créer un jeu de données à l’aide de l’API Catalogue, vous devez connaître la `$id` valeur du schéma XDM (Experience Data Model) sur lequel le jeu de données sera basé. Une fois que vous disposez de l’ID de schéma, vous pouvez créer un jeu de données en envoyant une requête POST au point de `/datasets` terminaison dans l’API Catalogue.

>[!NOTE]
>
>Ce document traite uniquement de la création d&#39;un objet de jeu de données dans le catalogue. Pour obtenir des instructions complètes sur la création, le remplissage et le contrôle d&#39;un jeu de données, consultez le [didacticiel](../datasets/create.md)suivant.

**Format d’API**

```HTTP
POST /dataSets
```

**Requête**

La requête suivante crée un jeu de données qui fait référence à un schéma précédemment défini.

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom du jeu de données à créer. |
| `schemaRef.id` | Valeur URI `$id` du schéma XDM sur lequel le jeu de données sera basé. |

>[!NOTE]
>
>Cet exemple utilise le format de fichier [parquet](https://parquet.apache.org/documentation/latest/) pour sa `containerFormat` propriété. Vous trouverez un exemple d’utilisation du format de fichier JSON dans le guide [du développeur d’](../../ingestion/batch-ingestion/api-overview.md)assimilation par lot.

**Réponse**

Une réponse réussie renvoie le statut HTTP 201 (Créé) et un objet de réponse constitué d&#39;un tableau contenant l&#39;ID du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’ID de jeu de données est une chaîne générée par le système en lecture seule qui est utilisée pour référencer le jeu de données dans les appels d’API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
