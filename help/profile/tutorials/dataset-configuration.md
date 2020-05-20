---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Configuration d’un jeu de données pour Profile et Identity Service à l’aide des API
topic: tutorial
translation-type: tm+mt
source-git-commit: 409d98818888f2758258441ea2d993ced48caf9a
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 2%

---


# Configuration d’un jeu de données pour Profile et Identity Service à l’aide des API

Ce didacticiel porte sur le processus d’activation d’un jeu de données à utiliser dans le service d’Profil et d’identité client en temps réel, en ventilant les étapes suivantes :

1. Activez un jeu de données à utiliser dans le Profil client en temps réel à l’aide de l’une des deux options suivantes :
   - [Créer un jeu de données](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurer un jeu de données existant](#configure-an-existing-dataset)
1. [Envoi de données dans le jeu de données](#ingest-data-into-the-dataset)
1. [Confirmer l’assimilation des données par Profil client en temps réel](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmer l&#39;assimilation de données par le service d&#39;identité](#confirm-data-ingest-by-identity-service)

## Prise en main

Ce didacticiel nécessite une bonne compréhension des différents services Adobe Experience Platform impliqués dans la gestion de jeux de données activés pour le Profil. Avant de commencer ce didacticiel, veuillez consulter la documentation relative aux services de plateformes connexes :

- [Profil](../home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [Service](../../identity-service/home.md)d&#39;identité : Permet le Profil client en temps réel en rapprochant les identités des sources de données disparates qui sont incorporées dans la plate-forme.
- [Service](../../catalog/home.md)de catalogue : API RESTful qui vous permet de créer des jeux de données et de les configurer pour le service d’Profil client et d’identité en temps réel.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les API de plate-forme.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les demandes aux API de plateforme requièrent un en-tête qui spécifie le nom du sandbox dans lequel l&#39;opération aura lieu. Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

- x-sandbox-name : `{SANDBOX_NAME}`

## Créer un jeu de données activé pour le Profil et l’identité {#create-a-dataset-enabled-for-profile-and-identity}

Vous pouvez activer un jeu de données pour le Profil client et le service d’identité en temps réel dès sa création ou à tout moment après la création du jeu de données. Si vous souhaitez activer un jeu de données qui a déjà été créé, suivez les étapes de [configuration d&#39;un jeu](#configure-an-existing-dataset) de données existant qui se trouvent plus loin dans ce document. Pour créer un nouveau jeu de données, vous devez connaître l’ID d’un schéma XDM existant activé pour le Profil client en temps réel. Pour plus d&#39;informations sur la recherche ou la création d&#39;un schéma compatible avec les Profils, consultez le didacticiel sur la [création d&#39;un schéma à l&#39;aide de l&#39;API](../../xdm/tutorials/create-schema-api.md)de registre des Schémas. L&#39;appel suivant à l&#39;API Catalogue active un jeu de données pour Profil et Identity Service.

**Format d’API**

```http
POST /dataSets
```

**Requête**

En incluant `unifiedProfile` et `unifiedIdentity` sous `tags` dans le corps de la demande, le jeu de données sera immédiatement activé pour le Profil et le service d&#39;identité, respectivement. Les valeurs de ces balises doivent être un tableau contenant la chaîne `"enabled:true"`.

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
| `schemaRef.id` | ID du schéma activé par Profil sur lequel le jeu de données sera basé. |
| `{TENANT_ID}` | espace de nommage du registre des Schémas qui contient des ressources appartenant à votre organisation IMS. Pour plus d&#39;informations, consultez la section [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) du guide du développeur du registre des Schémas. |

**Réponse**

Une réponse réussie montre un tableau contenant l&#39;ID du jeu de données nouvellement créé sous la forme `"@/dataSets/{DATASET_ID}"`de. Une fois que vous avez créé et activé un jeu de données, passez à la procédure de [transfert des données](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurer un jeu de données existant {#configure-an-existing-dataset}

Les étapes suivantes décrivent comment activer un jeu de données créé précédemment pour le service d’Profil et d’identité du client en temps réel. Si vous avez déjà créé un jeu de données compatible avec les Profils, passez à la procédure d&#39; [assimilation des données](#ingest-data-into-the-dataset).

### Vérifier si le jeu de données est activé {#check-if-the-dataset-is-enabled}

A l’aide de l’API Catalogue, vous pouvez inspecter un jeu de données existant afin de déterminer s’il est activé pour une utilisation dans le service de Profil client et d’identité en temps réel. L’appel suivant récupère les détails d’un jeu de données par ID.

**Format d’API**

```http
GET /dataSets/{DATASET_ID}
```

| Paramètre | Description |
|---|---|
| `{DATASET_ID}` | ID d’un jeu de données que vous souhaitez inspecter. |

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

Sous la `tags` propriété, vous pouvez voir que `unifiedProfile` et `unifiedIdentity` sont tous deux présents avec la valeur `enabled:true`. Par conséquent, le Profil client en temps réel et le service d’identité sont activés pour ce jeu de données, respectivement.

### Activer le jeu de données {#enable-the-dataset}

Si le jeu de données existant n&#39;a pas été activé pour le Profil ou le service d&#39;identité, vous pouvez l&#39;activer en faisant une demande PATCH à l&#39;aide de l&#39;ID du jeu de données.

**Format d’API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Paramètre | Description |
|---|---|
| `{DATASET_ID}` | ID d&#39;un jeu de données que vous souhaitez mettre à jour. |

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

Le corps de la requête comprend une `tags` propriété qui contient deux sous-propriétés : `"unifiedProfile"` et `"unifiedIdentity"`. Les valeurs de ces sous-propriétés sont des tableaux contenant la chaîne `"enabled:true"`.

**Réponse** Une requête PATCH réussie renvoie HTTP Status 200 (OK) et un tableau contenant l&#39;ID du jeu de données mis à jour. Cet identifiant doit correspondre à celui envoyé dans la demande PATCH. Les balises `"unifiedProfile"` et `"unifiedIdentity"` ont maintenant été ajoutées et le jeu de données est activé pour être utilisé par les services Profil et Identity.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Envoi de données dans le jeu de données {#ingest-data-into-the-dataset}

Le Profil client en temps réel et le service d’identité utilisent les données XDM lors de leur assimilation dans un jeu de données. Pour savoir comment télécharger des données dans un jeu de données, consultez le didacticiel sur la [création d’un jeu de données à l’aide d’API](../../catalog/datasets/create.md). Lors de la planification des données à envoyer à votre jeu de données compatible avec les Profils, tenez compte des bonnes pratiques suivantes :

- Incluez toutes les données que vous souhaitez utiliser comme critères de segment d’audience.
- Insérez autant d&#39;identifiants que vous pouvez le vérifier à partir des données de votre profil pour optimiser votre graphique d&#39;identité. Cela permet au service d’identité de regrouper les identités entre les jeux de données plus efficacement.

## Confirmer l’assimilation des données par Profil client en temps réel {#confirm-data-ingest-by-real-time-customer-profile}

Lors du premier chargement de données dans un nouveau jeu de données, ou dans le cadre d’un processus impliquant un nouveau ETL ou une nouvelle source de données, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été téléchargées comme prévu. A l’aide de l’API d’accès au Profil client en temps réel, vous pouvez récupérer des données de lot lors de leur chargement dans un jeu de données. Si vous ne parvenez pas à récupérer l’une des entités attendues, il se peut que votre jeu de données ne soit pas activé pour le Profil client en temps réel. Après avoir confirmé que votre jeu de données a été activé, veillez à ce que le format et les identifiants de vos données source répondent à vos attentes. Pour obtenir des instructions détaillées sur l’utilisation de l’API Profil client en temps réel pour accéder aux données de Profil, veuillez suivre le [sous-guide Entités, également appelé &quot;API d’accès au Profil&quot;](../api/entities.md).

## Confirmer l&#39;assimilation de données par le service d&#39;identité {#confirm-data-ingest-by-identity-service}

Chaque fragment de données ingéré qui contient plusieurs identités crée un lien dans votre graphique d&#39;identité privée. Pour plus d&#39;informations sur les graphiques d&#39;identité et les données d&#39;identité d&#39;accès, veuillez commencer par lire la présentation [du service](../../identity-service/home.md)d&#39;identité.