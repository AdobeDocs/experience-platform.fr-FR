---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;activer un jeu de données
title: Activation d’un jeu de données pour Profile et Identity Service à l’aide d’API
type: Tutorial
description: Ce tutoriel vous explique comment activer un jeu de données à utiliser avec Real-time Customer Profile et Identity Service à l’aide des API Adobe Experience Platform.
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 59%

---

# Activation d’un jeu de données pour [!DNL Profile] et [!DNL Identity Service] utilisation des API

Ce tutoriel décrit le processus d’activation d’un jeu de données à utiliser dans [!DNL Real-time Customer Profile] et [!DNL Identity Service], les étapes sont les suivantes :

1. Activation d’un jeu de données à utiliser dans [!DNL Real-time Customer Profile], à l’aide de l’une des deux options suivantes :
   - [Création d’un nouveau jeu de données](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configuration d’un jeu de données existant](#configure-an-existing-dataset)
1. [Ingestion de données dans le jeu de données](#ingest-data-into-the-dataset)
1. [Confirmation de l’ingestion des données par Real-time Customer Profile](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmation de l’ingestion des données par Identity Service](#confirm-data-ingest-by-identity-service)

## Prise en main

Ce tutoriel nécessite une compréhension pratique de plusieurs services Adobe Experience Platform impliqués dans la gestion des jeux de données activés pour Profile. Avant de commencer ce tutoriel, veuillez consulter la documentation relative à ces [!DNL Platform] services :

- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [[!DNL Identity Service]](../../identity-service/home.md): Active [!DNL Real-time Customer Profile] en rapprochant les identités des sources de données disparates ingérées dans [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Une API RESTful qui vous permet de créer des jeux de données et de les configurer pour [!DNL Real-time Customer Profile] et [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API Platform.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Toutes les requêtes contenant un payload (POST, PUT, PATCH) nécessitent une `Content-Type` en-tête . La valeur correcte de cet en-tête s’affiche dans les exemples de requêtes, le cas échéant.

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées à [!DNL Platform] Les API requièrent une `x-sandbox-name` qui spécifie le nom de l’environnement de test dans lequel l’opération aura lieu. Pour plus d’informations sur les environnements de test dans [!DNL Platform], consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

## Création d’un jeu de données activé pour Profile et Identity Service {#create-a-dataset-enabled-for-profile-and-identity}

Vous pouvez activer un jeu de données pour Real-time Customer Profile et Identity Service dès sa création ou à tout moment après sa création. Si vous souhaitez activer un jeu de données déjà créé, suivez les étapes de [configuration d’un jeu de données existant](#configure-an-existing-dataset) qui se trouvent plus bas dans ce document.

>[!NOTE]
>
>Pour créer un jeu de données activé par Profile, vous devez connaître l’identifiant d’un schéma XDM existant activé pour Profile. Pour plus d’informations sur la recherche ou la création d’un schéma activé pour Profile, reportez-vous au tutoriel sur la [création d’un schéma à l’aide de l’API Schema Registry](../../xdm/tutorials/create-schema-api.md).

Pour créer un jeu de données activé pour Profile, vous pouvez utiliser une requête de POST au `/dataSets` point de terminaison .

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields":[],
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags": {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Propriété | Description |
|---|---|
| `schemaRef.id` | L’identifiant de la variable [!DNL Profile]schéma activé sur lequel le jeu de données sera basé. |
| `{TENANT_ID}` | L’espace de noms dans la variable [!DNL Schema Registry] qui contient des ressources appartenant à votre organisation IMS. Voir [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) de la section [!DNL Schema Registry] guide de développement pour plus d’informations. |

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

En utilisant la variable [!DNL Catalog] API, vous pouvez examiner un jeu de données existant pour déterminer s’il est activé pour une utilisation dans [!DNL Real-time Customer Profile] et [!DNL Identity Service]. L’appel suivant récupère les détails d’un jeu de données via son identifiant.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{ORG_ID}",
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
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] } 
      ]'
```

Le corps de la requête comprend un `path` à deux types de balises, `unifiedProfile` et `unifiedIdentity`. Le `value` de chacun sont des tableaux contenant la chaîne `enabled:true`.

**Réponse**
Une requête PATCH réussie renvoie un état HTTP 200 (OK) et un tableau contenant l’identifiant du jeu de données mis à jour. Cet identifiant doit correspondre à celui envoyé dans la requête PATCH. Les balises `unifiedProfile` et `unifiedIdentity` ont maintenant été ajoutées, et le jeu de données est activé pour une utilisation dans Profile et Identity Service.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Ingestion de données dans le jeu de données {#ingest-data-into-the-dataset}

Les [!DNL Real-time Customer Profile] et [!DNL Identity Service] consommer des données XDM lors de leur ingestion dans un jeu de données ; Pour apprendre à charger des données dans un jeu de données, reportez-vous au tutoriel sur la [création d’un jeu de données à l’aide d’API](../../catalog/datasets/create.md). Lors de la planification des données à envoyer à votre [!DNL Profile]Jeu de données compatible, tenez compte des bonnes pratiques suivantes :

- Incluez les données que vous souhaitez utiliser comme critères de segmentation.
- Incluez autant d’identifiants que vous pouvez en valider à partir des données de profil afin d’optimiser le graphique d’identités. Cela permet [!DNL Identity Service] pour regrouper plus efficacement les identités entre les jeux de données.

## Confirmation de l’ingestion des données par [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Lors du premier chargement de données vers un nouveau jeu de données ou dans le cadre d’un processus impliquant un nouveau ETL ou une nouvelle source de données, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été chargées comme prévu. En utilisant la variable [!DNL Real-time Customer Profile] Accédez à l’API , vous pouvez récupérer les données de lot lors de leur chargement dans un jeu de données. Si vous ne parvenez pas à récupérer les entités attendues, il se peut que votre jeu de données ne soit pas activé pour [!DNL Real-time Customer Profile]. Une fois que vous avez confirmé que votre jeu de données a été activé, assurez-vous que le format et les identifiants des données sources répondent à vos attentes. Pour obtenir des instructions détaillées sur l’utilisation de la variable [!DNL Real-time Customer Profile] API d’accès [!DNL Profile] données, reportez-vous à la section [guide de point d’entrée des entités](../../profile/api/entities.md), également appelé &quot;&quot;[!DNL Profile Access]&quot; API.

## Confirmation de l’ingestion des données par Identity Service {#confirm-data-ingest-by-identity-service}

Chaque fragment de données ingéré contenant plusieurs identités crée un lien dans votre graphique d’identités privé. Pour plus d’informations sur les graphiques d’identités et sur l’accès aux données d’identité, veuillez commencer par lire la [présentation d’Identity Service](../../identity-service/home.md).
