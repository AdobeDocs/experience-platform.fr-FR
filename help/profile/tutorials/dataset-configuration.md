---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;activer un jeu de données
title: Configuration d’un jeu de données pour Profile et Identity Service à l’aide des API
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel vous explique comment activer un jeu de données à utiliser avec Real-time Customer Profile et Identity Service à l’aide des API Adobe Experience Platform.
exl-id: 142cb7df-072a-4f3a-8a9c-9a78afb35312
source-git-commit: bcca4d6212ee3f0d661549eca359ab8c8aaf905c
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 60%

---

# Configurer un jeu de données pour [!DNL Profile] et [!DNL Identity Service] à l’aide d’API

Ce tutoriel décrit le processus d’activation d’un jeu de données à utiliser dans [!DNL Real-time Customer Profile] et [!DNL Identity Service], en les divisant par les étapes suivantes :

1. Activez un jeu de données à utiliser dans [!DNL Real-time Customer Profile] à l’aide de l’une des deux options suivantes :
   - [Création d’un nouveau jeu de données](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configuration d’un jeu de données existant](#configure-an-existing-dataset)
1. [Ingestion de données dans le jeu de données](#ingest-data-into-the-dataset)
1. [Confirmation de l’ingestion des données par Real-time Customer Profile](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmation de l’ingestion des données par Identity Service](#confirm-data-ingest-by-identity-service)

## Prise en main

Ce tutoriel nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans la gestion des jeux de données [!DNL Profile] activés. Avant de commencer ce tutoriel, veuillez consulter la documentation relative à ces services [!DNL Platform] associés :

- [[!DNL Real-time Customer Profile]](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [[!DNL Identity Service]](../../identity-service/home.md): Permet  [!DNL Real-time Customer Profile] en rapprochant des identités de sources de données disparates ingérées dans  [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Une API RESTful qui vous permet de créer des jeux de données et de les configurer pour  [!DNL Real-time Customer Profile] et  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API Platform.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L&#39;exemple JSON renvoyé dans les réponses de l&#39;API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, voir la section concernant la [lecture d&#39;exemples d&#39;appels d&#39;API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d&#39;abord suivre le [tutoriel d&#39;authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Toutes les requêtes contenant un payload (POST, PUT, PATCH) nécessitent un en-tête `Content-Type` supplémentaire. La valeur correcte de cet en-tête s’affiche dans les exemples de requêtes, le cas échéant.

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête `x-sandbox-name` spécifiant le nom de l’environnement de test dans lequel l’opération aura lieu. Pour plus d’informations sur les environnements de test dans [!DNL Platform], consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

## Créez un jeu de données activé pour [!DNL Profile] et [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

Vous pouvez activer un jeu de données pour [!DNL Real-time Customer Profile] et [!DNL Identity Service] immédiatement au moment de la création ou à tout moment après la création du jeu de données. Si vous souhaitez activer un jeu de données déjà créé, suivez les étapes de [configuration d’un jeu de données existant](#configure-an-existing-dataset) qui se trouvent plus bas dans ce document. Pour créer un jeu de données, vous devez connaître l’identifiant d’un schéma XDM existant et activé pour Real-time Customer Profile. Pour plus d’informations sur la recherche ou la création d’un schéma activé pour Profile, reportez-vous au tutoriel sur la [création d’un schéma à l’aide de l’API Schema Registry](../../xdm/tutorials/create-schema-api.md). L’appel suivant à l’API [!DNL Catalog] active un jeu de données pour [!DNL Profile] et [!DNL Identity Service].

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
        "persisted": true
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
| `schemaRef.id` | L’identifiant du schéma activé [!DNL Profile] sur lequel le jeu de données sera basé. |
| `{TENANT_ID}` | Espace de noms dans la balise [!DNL Schema Registry] qui contient les ressources appartenant à votre organisation IMS. Pour plus d’informations, voir la section [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) du guide de développement [!DNL Schema Registry] . |

**Réponse**

Une réponse réussie affiche un tableau contenant l’identifiant du jeu de données nouvellement créé sous la forme d’un `"@/dataSets/{DATASET_ID}"`. Une fois le jeu de données créé et activé, passez à l’étape du [chargement des données](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configuration d’un jeu de données existant {#configure-an-existing-dataset}

Les étapes suivantes expliquent comment activer un jeu de données créé précédemment pour [!DNL Real-time Customer Profile] et [!DNL Identity Service]. Si vous avez déjà créé un jeu de données activé pour Profile, passez à l’étape de l’[ingestion de données](#ingest-data-into-the-dataset).

### Vérifiez si le jeu de données est activé {#check-if-the-dataset-is-enabled}

À l’aide de l’API [!DNL Catalog], vous pouvez examiner un jeu de données existant pour déterminer s’il est activé pour une utilisation dans [!DNL Real-time Customer Profile] et [!DNL Identity Service]. L’appel suivant récupère les détails d’un jeu de données via son identifiant.

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
            "persisted": true
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

Sous la propriété `tags`, vous pouvez voir que `unifiedProfile` et `unifiedIdentity` sont tous les deux présents et affichent la valeur `enabled:true`. Par conséquent, [!DNL Real-time Customer Profile] et [!DNL Identity Service] sont activés pour ce jeu de données, respectivement.

### Activation du jeu de données {#enable-the-dataset}

Si le jeu de données existant n’a pas été activé pour [!DNL Profile] ou [!DNL Identity Service], vous pouvez l’activer en effectuant une requête de PATCH à l’aide de l’identifiant du jeu de données.

**Format d&#39;API**

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
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] }	
      ]'
```

Le corps de la requête comprend `path` à deux types de balises, `unifiedProfile` et `unifiedIdentity`. `value` de chacun sont des tableaux contenant la chaîne `enabled:true`.

**Réponse**
Une requête PATCH réussie renvoie un état HTTP 200 (OK) et un tableau contenant l’identifiant du jeu de données mis à jour. Cet identifiant doit correspondre à celui envoyé dans la requête PATCH. Les balises `unifiedProfile` et `unifiedIdentity` ont maintenant été ajoutées, et le jeu de données est activé pour une utilisation dans Profile et Identity Service.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Ingestion de données dans le jeu de données {#ingest-data-into-the-dataset}

[!DNL Real-time Customer Profile] et [!DNL Identity Service] utilisent tous deux des données XDM lors de leur ingestion dans un jeu de données. Pour apprendre à charger des données dans un jeu de données, reportez-vous au tutoriel sur la [création d’un jeu de données à l’aide d’API](../../catalog/datasets/create.md). Lors de la planification des données à envoyer à votre jeu de données compatible [!DNL Profile], tenez compte des bonnes pratiques suivantes :

- Incluez toutes les données à utiliser comme critères de segments ciblés.
- Incluez autant d’identifiants que vous pouvez en valider à partir des données de profil afin d’optimiser le graphique d’identités. Cela permet à [!DNL Identity Service] de regrouper plus efficacement les identités entre les jeux de données.

## Confirmer l’ingestion des données par [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Lors du premier chargement de données vers un nouveau jeu de données ou dans le cadre d’un processus impliquant un nouveau ETL ou une nouvelle source de données, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été chargées comme prévu. À l’aide de l’API d’accès [!DNL Real-time Customer Profile], vous pouvez récupérer les données de lot lors de leur chargement dans un jeu de données. Si vous ne parvenez pas à récupérer les entités attendues, il se peut que votre jeu de données ne soit pas activé pour [!DNL Real-time Customer Profile]. Une fois que vous avez confirmé que votre jeu de données a été activé, assurez-vous que le format et les identifiants des données sources répondent à vos attentes. Pour obtenir des instructions détaillées sur l’utilisation de l’API [!DNL Real-time Customer Profile] pour accéder aux données [!DNL Profile], consultez le [guide des points d’entrée des entités](../api/entities.md), également appelé API &quot;[!DNL Profile Access]&quot;.

## Confirmation de l’ingestion des données par Identity Service {#confirm-data-ingest-by-identity-service}

Chaque fragment de données ingéré contenant plusieurs identités crée un lien dans votre graphique d’identités privé. Pour plus d’informations sur les graphiques d’identités et sur l’accès aux données d’identité, veuillez commencer par lire la [présentation d’Identity Service](../../identity-service/home.md).
