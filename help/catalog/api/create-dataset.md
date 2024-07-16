---
keywords: Experience Platform;accueil;rubriques populaires;jeu de données;jeu de données;créer un jeu de données;créer un jeu de données;activer un jeu de données
solution: Experience Platform
title: Création d’un jeu de données dans l’API
description: Ce document explique comment créer un objet de jeu de données dans l’API Catalog Service.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 53%

---

# Création d’un jeu de données dans l’API

Pour créer un jeu de données à l’aide de l’API [!DNL Catalog], vous devez connaître la valeur `$id` du schéma [!DNL Experience Data Model] (XDM) sur lequel le jeu de données sera basé. Une fois que vous disposez de l’identifiant de schéma, vous pouvez créer un jeu de données en envoyant une requête de POST au point de terminaison `/datasets` dans l’API [!DNL Catalog].

>[!NOTE]
>
>Ce document couvre uniquement la création d’un objet de jeu de données dans [!DNL Catalog]. Pour obtenir des instructions complètes sur la création, le remplissage et la surveillance d’un jeu de données, reportez-vous au [tutoriel](../datasets/create.md) suivant.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom du jeu de données à créer. |
| `schemaRef.id` | La valeur `$id` de l’URI pour le schéma XDM sur lequel sera basé le jeu de données. |
| `schemaRef.contentType` | Indique le format et la version du schéma. Pour plus d’informations, reportez-vous à la section [contrôle de version des schémas](../../xdm/api/getting-started.md#versioning) du guide de l’API XDM. |

>[!NOTE]
>
>Cet exemple utilise le format de fichier [Apache Parquet](https://parquet.apache.org/docs/) pour sa propriété `containerFormat`. Vous trouverez un exemple d’utilisation du format de fichier JSON dans le [guide de développement de l’ingestion par lots](../../ingestion/batch-ingestion/api-overview.md).

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Créé) et un objet de réponse constitué d’un tableau contenant l’identifiant du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’identifiant du jeu de données est une chaîne en lecture seule générée par le système et utilisée pour référencer le jeu de données dans les appels API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
