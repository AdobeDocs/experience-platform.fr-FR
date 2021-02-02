---
keywords: Experience Platform;accueil;rubriques populaires;dataset;Dataset;create dataset;create dataset;create dataset;enable dataset
solution: Experience Platform
title: Création d’un jeu de données
topic: developer guide
description: Ce document explique comment créer un objet de jeu de données dans le catalogue.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 57%

---


# Création d’un jeu de données

Pour créer un jeu de données à l&#39;aide de l&#39;API [!DNL Catalog], vous devez connaître la valeur `$id` du schéma [!DNL Experience Data Model] (XDM) sur lequel le jeu de données sera basé. Une fois que vous disposez de l&#39;ID de schéma, vous pouvez créer un jeu de données en envoyant une requête de POST au point de terminaison `/datasets` de l&#39;API [!DNL Catalog].

>[!NOTE]
>
>Ce document traite uniquement de la création d&#39;un objet de jeu de données dans [!DNL Catalog]. Pour obtenir des instructions complètes sur la création, le remplissage et la surveillance d’un jeu de données, reportez-vous au [tutoriel](../datasets/create.md) suivant.

**Format d’API**

```HTTP
POST /dataSets
```

**Requête**

La requête suivante crée un jeu de données se référant à un schéma précédemment défini.

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
| `schemaRef.id` | La valeur `$id` de l’URI pour le schéma XDM sur lequel sera basé le jeu de données. |

>[!NOTE]
>
>Cet exemple utilise le format de fichier [Apache Parquet](https://parquet.apache.org/documentation/latest/) pour sa propriété `containerFormat`. Vous trouverez un exemple d’utilisation du format de fichier JSON dans le [guide de développement de l’ingestion par lots](../../ingestion/batch-ingestion/api-overview.md).

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Créé) et un objet de réponse constitué d’un tableau contenant l’identifiant du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’identifiant du jeu de données est une chaîne en lecture seule générée par le système et utilisée pour référencer le jeu de données dans les appels API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
