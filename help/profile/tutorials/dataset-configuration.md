---
keywords: Experience Platform ; profil ; profil client en temps réel ; dépannage ; API ; activer le jeu de données
title: Configuration d’un jeu de données pour Profil et Identity Service à l’aide d’API
topic-legacy: tutorial
type: Tutorial
description: Ce didacticiel explique comment activer un jeu de données à utiliser avec le Profil client en temps réel et le service d’identité à l’aide des API Adobe Experience Platform.
exl-id: 142cb7df-072a-4f3a-8a9c-9a78afb35312
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 62%

---

# Configurez un jeu de données pour [!DNL Profile] et [!DNL Identity Service] à l’aide d’API.

Ce didacticiel porte sur le processus d&#39;activation d&#39;un jeu de données à utiliser dans [!DNL Real-time Customer Profile] et [!DNL Identity Service], ventilé en plusieurs étapes :

1. Activez un jeu de données à utiliser dans [!DNL Real-time Customer Profile] en utilisant l&#39;une des deux options suivantes :
   - [Création d’un jeu de données](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configuration d’un jeu de données existant](#configure-an-existing-dataset)
1. [Ingestion de données dans le jeu de données](#ingest-data-into-the-dataset)
1. [Confirmation de l’ingestion des données par Real-time Customer Profile](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmation de l’ingestion des données par Identity Service](#confirm-data-ingest-by-identity-service)

## Prise en main

Ce didacticiel nécessite une bonne compréhension des différents services Adobe Experience Platform impliqués dans la gestion des [!DNL Profile] jeux de données activés. Avant de commencer ce didacticiel, veuillez consulter la documentation relative à ces services [!DNL Platform] connexes :

- [[!DNL Real-time Customer Profile]](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [[!DNL Identity Service]](../../identity-service/home.md): Permet  [!DNL Real-time Customer Profile] de relier des identités provenant de sources de données disparates et qui sont absorbées  [!DNL Platform]par ces identités.
- [[!DNL Catalog Service]](../../catalog/home.md): API RESTful qui vous permet de créer des jeux de données et de les configurer pour  [!DNL Real-time Customer Profile] et  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API Platform.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

Toutes les ressources de [!DNL Experience Platform] sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu. Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../sandboxes/home.md).

- x-sandbox-name: `{SANDBOX_NAME}`

## Créez un jeu de données activé pour [!DNL Profile] et [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

Vous pouvez activer un jeu de données pour [!DNL Real-time Customer Profile] et [!DNL Identity Service] immédiatement au moment de la création ou à tout moment après la création du jeu de données. Si vous souhaitez activer un jeu de données déjà créé, suivez les étapes de [configuration d’un jeu de données existant](#configure-an-existing-dataset) qui se trouvent plus bas dans ce document. Pour créer un jeu de données, vous devez connaître l’identifiant d’un schéma XDM existant et activé pour Real-time Customer Profile. Pour plus d’informations sur la recherche ou la création d’un schéma activé pour Profile, reportez-vous au tutoriel sur la [création d’un schéma à l’aide de l’API Schema Registry](../../xdm/tutorials/create-schema-api.md). L&#39;appel suivant à l&#39;API [!DNL Catalog] active un jeu de données pour [!DNL Profile] et [!DNL Identity Service].

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
| `schemaRef.id` | ID du schéma activé [!DNL Profile] sur lequel le jeu de données sera basé. |
| `{TENANT_ID}` | L&#39;espace de nommage au sein du [!DNL Schema Registry] qui contient des ressources appartenant à votre organisation IMS. Pour plus d&#39;informations, consultez la section [ID_TENANT](../../xdm/api/getting-started.md#know-your-tenant-id) du guide du développeur [!DNL Schema Registry]. |

**Réponse**

Une réponse réussie affiche un tableau contenant l’identifiant du jeu de données nouvellement créé sous la forme d’un `"@/dataSets/{DATASET_ID}"`. Une fois le jeu de données créé et activé, passez à l’étape du [chargement des données](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configuration d’un jeu de données existant {#configure-an-existing-dataset}

Les étapes suivantes décrivent comment activer un jeu de données créé précédemment pour [!DNL Real-time Customer Profile] et [!DNL Identity Service]. Si vous avez déjà créé un jeu de données activé pour Profile, passez à l’étape de l’[ingestion de données](#ingest-data-into-the-dataset).

### Vérifiez si le jeu de données est activé {#check-if-the-dataset-is-enabled}

À l&#39;aide de l&#39;API [!DNL Catalog], vous pouvez examiner un jeu de données existant pour déterminer s&#39;il est activé pour l&#39;utilisation dans [!DNL Real-time Customer Profile] et [!DNL Identity Service]. L’appel suivant récupère les détails d’un jeu de données via son identifiant.

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

Si le jeu de données existant n&#39;a pas été activé pour [!DNL Profile] ou [!DNL Identity Service], vous pouvez l&#39;activer en faisant une demande de PATCH à l&#39;aide de l&#39;ID de jeu de données.

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

[!DNL Real-time Customer Profile] et [!DNL Identity Service] consomment tous les deux des données XDM lors de leur assimilation dans un jeu de données. Pour apprendre à charger des données dans un jeu de données, reportez-vous au tutoriel sur la [création d’un jeu de données à l’aide d’API](../../catalog/datasets/create.md). Lors de la planification des données à envoyer à votre jeu de données [!DNL Profile] activé, tenez compte des bonnes pratiques suivantes :

- Incluez toutes les données à utiliser comme critères de segments ciblés.
- Incluez autant d’identifiants que vous pouvez en valider à partir des données de profil afin d’optimiser le graphique d’identités. Cela permet à [!DNL Identity Service] d&#39;associer plus efficacement les identités entre les jeux de données.

## Confirmer l&#39;assimilation des données par [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Lors du premier chargement de données vers un nouveau jeu de données ou dans le cadre d’un processus impliquant un nouveau ETL ou une nouvelle source de données, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été chargées comme prévu. L&#39;API d&#39;accès [!DNL Real-time Customer Profile] vous permet de récupérer des données de lot lors de leur chargement dans un jeu de données. Si vous ne parvenez pas à récupérer les entités attendues, il se peut que votre jeu de données ne soit pas activé pour [!DNL Real-time Customer Profile]. Une fois que vous avez confirmé que votre jeu de données a été activé, assurez-vous que le format et les identifiants des données sources répondent à vos attentes. Pour obtenir des instructions détaillées sur la façon d&#39;utiliser l&#39;API [!DNL Real-time Customer Profile] pour accéder aux données [!DNL Profile], veuillez suivre le [guide des points de terminaison des entités](../api/entities.md), également appelé &quot;[!DNL Profile Access] API&quot;.

## Confirmation de l’ingestion des données par Identity Service {#confirm-data-ingest-by-identity-service}

Chaque fragment de données ingéré contenant plusieurs identités crée un lien dans votre graphique d’identités privé. Pour plus d’informations sur les graphiques d’identités et sur l’accès aux données d’identité, veuillez commencer par lire la [présentation d’Identity Service](../../identity-service/home.md).
