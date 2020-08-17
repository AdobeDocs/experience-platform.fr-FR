---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;enable dataset
solution: Adobe Experience Platform
title: Configuration d’un jeu de données pour Profile et Identity Service à l’aide d’API
topic: tutorial
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 59%

---


# Configure a dataset for [!DNL Profile] and [!DNL Identity Service] using APIs

This tutorial covers the process of enabling a dataset for use in [!DNL Real-time Customer Profile] and [!DNL Identity Service], broken down into the following steps:

1. Enable a dataset for use in [!DNL Real-time Customer Profile], using one of two options:
   - [Création d’un jeu de données](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configuration d’un jeu de données existant](#configure-an-existing-dataset)
1. [Ingestion de données dans le jeu de données](#ingest-data-into-the-dataset)
1. [Confirmation de l’ingestion des données par Real-time Customer Profile](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmation de l’ingestion des données par Identity Service](#confirm-data-ingest-by-identity-service)

## Prise en main

This tutorial requires a working understanding of the various Adobe Experience Platform services involved in managing [!DNL Profile]-enabled datasets. Before beginning this tutorial, please review the documentation for these related [!DNL Platform] services:

- [!DNL Real-time Customer Profile](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [!DNL Identity Service](../../identity-service/home.md): Permet [!DNL Real-time Customer Profile] de relier des identités provenant de sources de données disparates et qui sont incorporées [!DNL Platform]dans.
- [!DNL Catalog Service](../../catalog/home.md): API RESTful qui vous permet de créer des jeux de données et de les configurer pour [!DNL Real-time Customer Profile] et [!DNL Identity Service].
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API Platform.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in. For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

- x-sandbox-name: `{SANDBOX_NAME}`

## Créez un jeu de données activé pour [!DNL Profile] et [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

You can enable a dataset for [!DNL Real-time Customer Profile] and [!DNL Identity Service] immediately upon creation or at any point after the dataset has been created. Si vous souhaitez activer un jeu de données déjà créé, suivez les étapes de [configuration d’un jeu de données existant](#configure-an-existing-dataset) qui se trouvent plus bas dans ce document. Pour créer un jeu de données, vous devez connaître l’identifiant d’un schéma XDM existant et activé pour Real-time Customer Profile. Pour plus d’informations sur la recherche ou la création d’un schéma activé pour Profile, reportez-vous au tutoriel sur la [création d’un schéma à l’aide de l’API Schema Registry](../../xdm/tutorials/create-schema-api.md). The following call to the [!DNL Catalog] API enables a dataset for [!DNL Profile] and [!DNL Identity Service].

**Format d’API**

```http
POST /dataSets
```

**Requête**

En incluant `unifiedProfile` et `unifiedIdentity` sous `tags` dans le corps de la requête, le jeu de données sera immédiatement activé pour et , respectivement. [!DNL Profile][!DNL Identity Service] Les valeurs de ces balises doivent être un tableau contenant la chaîne `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fileDescription" : {
    "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
    "fields":[],
    "schemaRef" : {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags" : {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Propriété | Description |
|---|---|
| `schemaRef.id` | The ID of the [!DNL Profile]-enabled schema upon which the dataset will be based. |
| `{TENANT_ID}` | The namespace within the [!DNL Schema Registry] which contains resources belonging to your IMS Organization. See the [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) section of the [!DNL Schema Registry] developer guide for more information. |

**Réponse**

Une réponse réussie affiche un tableau contenant l’identifiant du jeu de données nouvellement créé sous la forme d’un `"@/dataSets/{DATASET_ID}"`. Une fois le jeu de données créé et activé, passez à l’étape du [chargement des données](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configuration d’un jeu de données existant {#configure-an-existing-dataset}

The following steps cover how to enable a previously created dataset for [!DNL Real-time Customer Profile] and [!DNL Identity Service]. Si vous avez déjà créé un jeu de données activé pour Profile, passez à l’étape de l’[ingestion de données](#ingest-data-into-the-dataset).

### Vérifiez si le jeu de données est activé {#check-if-the-dataset-is-enabled}

Using the [!DNL Catalog] API, you can inspect an existing dataset to determine whether it is enabled for use in [!DNL Real-time Customer Profile] and [!DNL Identity Service]. L’appel suivant récupère les détails d’un jeu de données via son identifiant.

**Format d’API**

```http
GET /dataSets/{DATASET_ID}
```

| Paramètre | Description |
|---|---|
| `{DATASET_ID}` | Identifiant du jeu de données à examiner. |

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "lastBatchId": "6dcd9128a1c84e6aa5177641165e18e4",
        "lastBatchStatus": "success",
        "dule": {},
        "statsCache": {
            "startDate": null,
            "endDate": null
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Sous la propriété `tags`, vous pouvez voir que `unifiedProfile` et `unifiedIdentity` sont tous les deux présents et affichent la valeur `enabled:true`. Therefore, [!DNL Real-time Customer Profile] and [!DNL Identity Service] are enabled for this dataset, respectively.

### Activation du jeu de données {#enable-the-dataset}

If the existing dataset has not been enabled for [!DNL Profile] or [!DNL Identity Service], you can enable it by making a PATCH request using the dataset ID.

**Format d’API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Paramètre | Description |
|---|---|
| `{DATASET_ID}` | Identifiant du jeu de données à mettre à jour. |

**Requête**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags" : {
        "unifiedProfile": ["enabled:true"],
        "unifiedIdentity": ["enabled:true"]
    }
  }'
```

Le corps de la requête comprend une propriété `tags`, qui contient deux sous-propriétés : `"unifiedProfile"` et `"unifiedIdentity"`. Les valeurs de ces sous-propriétés sont des tableaux contenant la chaîne `"enabled:true"`.

**Réponse**
Une requête PATCH réussie renvoie un état HTTP 200 (OK) et un tableau contenant l’identifiant du jeu de données mis à jour. Cet identifiant doit correspondre à celui envoyé dans la requête PATCH. Les balises `"unifiedProfile"` et `"unifiedIdentity"` ont maintenant été ajoutées, et le jeu de données est activé pour une utilisation dans Profile et Identity Service.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Ingestion de données dans le jeu de données {#ingest-data-into-the-dataset}

Both [!DNL Real-time Customer Profile] and [!DNL Identity Service] consume XDM data as it is being ingested into a dataset. Pour apprendre à charger des données dans un jeu de données, reportez-vous au tutoriel sur la [création d’un jeu de données à l’aide d’API](../../catalog/datasets/create.md). When planning what data to send to your [!DNL Profile]-enabled dataset, consider the following best practices:

- Incluez toutes les données à utiliser comme critères de segments ciblés.
- Incluez autant d’identifiants que vous pouvez en valider à partir des données de profil afin d’optimiser le graphique d’identités. This allows [!DNL Identity Service] to stitch identities across datasets more effectively.

## Confirm data ingest by [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Lors du premier chargement de données vers un nouveau jeu de données ou dans le cadre d’un processus impliquant un nouveau ETL ou une nouvelle source de données, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été chargées comme prévu. Using the [!DNL Real-time Customer Profile] Access API, you can retrieve batch data as it gets loaded into a dataset. Si vous ne parvenez pas à récupérer les entités attendues, il se peut que votre jeu de données ne soit pas activé pour [!DNL Real-time Customer Profile]. Une fois que vous avez confirmé que votre jeu de données a été activé, assurez-vous que le format et les identifiants des données sources répondent à vos attentes. Pour obtenir des instructions détaillées sur l&#39;utilisation de l&#39; [!DNL Real-time Customer Profile] API pour accéder aux [!DNL Profile] données, veuillez suivre le guide [des points de terminaison](../api/entities.md)entités, également appelé &quot;[!DNL Profile Access] API&quot;.

## Confirmation de l’ingestion des données par Identity Service {#confirm-data-ingest-by-identity-service}

Chaque fragment de données ingéré contenant plusieurs identités crée un lien dans votre graphique d’identités privé. Pour plus d’informations sur les graphiques d’identités et sur l’accès aux données d’identité, veuillez commencer par lire la [présentation d’Identity Service](../../identity-service/home.md).