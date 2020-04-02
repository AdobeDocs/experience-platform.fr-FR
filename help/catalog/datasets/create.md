---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un jeu de données à l’aide d’API
topic: datasets
translation-type: tm+mt
source-git-commit: a6a1ecd9ce49c0a55e14b0d5479ca7315e332904

---


# Création d’un jeu de données à l’aide d’API

Ce décrit les étapes générales de création d’un jeu de données à l’aide des API d’Adobe Experience Platform et de remplissage du jeu de données à l’aide d’un fichier.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Importation](../../ingestion/batch-ingestion/overview.md)par lot : Experience Platform vous permet d’assimiler des données sous forme de fichiers de commandes.
* [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir effectuer des appels aux API de plateforme.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

* Content-Type : application/json

## Tutoriel

Pour créer un jeu de données, un  de doit d&#39;abord être défini. Un est un ensemble de règles permettant de représenter des données. Outre la description de la structure des données, les  de fournissent des contraintes et des attentes qui peuvent être appliquées et utilisées pour valider les données lorsqu’elles sont déplacées d’un système à l’autre.

Ces définitions standard permettent d’interpréter les données de manière cohérente, quel que soit le  , et éliminent la nécessité d’une traduction entre les applications. Pour plus d&#39;informations sur la composition de  de, consultez le guide sur les [bases de la composition](../../xdm/schema/composition.md)

## Rechercher un de jeux de données 

Ce didacticiel commence à l&#39;endroit où se termine le didacticiel [API](../../xdm/tutorials/create-schema-api.md) de Registre, en utilisant le Membres de fidélité  créé au cours de ce didacticiel.

Si vous n&#39;avez pas terminé le tutoriel sur le Registre des , veuillez vous  là-bas et continuer avec ce tutoriel sur l&#39;ensemble de données seulement une fois que vous avez composé le nécessaire.

L’appel suivant peut être utilisé pour  l’des membres de fidélité que vous avez créé pendant le didacticiel de l’API de registre de l’ del’application :

**Format API**

```HTTP
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Le format de l’objet de réponse dépend de l’en-tête Accepter envoyé dans la requête. Les propriétés individuelles de cette réponse ont été réduites pour l’espace.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": {},
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Création d’un jeu de données

Une fois le  des membres de fidélité en place, vous pouvez désormais créer un jeu de données qui référence le  du.

**Format API**

```HTTP
POST /dataSets
```

**Requête**

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

>[!NOTE] Ce didacticiel utilise le format de fichier [parquet](https://parquet.apache.org/documentation/latest/) pour tous ses exemples. Vous trouverez un exemple d’utilisation du format de fichier JSON dans le guide du développeur d’assimilation de [lot](../../ingestion/batch-ingestion/api-overview.md)

**Réponse**

Une réponse réussie renvoie le statut HTTP 201 (Créé) et un objet de réponse constitué d&#39;un tableau contenant l&#39;ID du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’ID du jeu de données est une chaîne générée par le système en lecture seule qui est utilisée pour référencer le jeu de données dans les appels d’API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Création d’un lot

Pour pouvoir ajouter des données à un jeu de données, vous devez créer un lot lié au jeu de données. Le lot sera ensuite utilisé pour le transfert.

**Format API**

```HTTP
POST /batches
```

**Requête**

Le corps de la requête comprend un champ &quot;datasetId&quot;, dont la valeur est la valeur `{DATASET_ID}` générée à l’étape précédente.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Réponse**

Une réponse réussie renvoie HTTP Status 201 (Créé) et un objet de réponse contenant les détails du lot nouvellement créé, y compris sa chaîne générée par le système `id`, en lecture seule.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```

## Téléchargement de fichiers dans un lot

Après avoir créé un nouveau lot à télécharger, vous pouvez désormais télécharger des fichiers vers le jeu de données spécifique. Il est important de se rappeler que lorsque vous avez défini le jeu de données, vous avez spécifié le format de fichier comme parquet. Par conséquent, les fichiers que vous téléchargez doivent être dans ce format.

>[!NOTE] Le fichier de transfert de données le plus volumineux pris en charge est de 512 Mo. Si votre fichier de données est plus volumineux que celui-ci, il doit être divisé en blocs d’une taille maximale de 512 Mo, afin d’être téléchargé un par un. Vous pouvez télécharger chaque fichier dans le même lot en répétant cette étape pour chaque fichier, à l’aide du même ID de lot. Le nombre de fichiers que vous pouvez télécharger dans le cadre d’un lot n’est pas limité.

**Format API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{BATCH_ID}` | Le `id` lot vers lequel vous téléchargez. |
| `{DATASET_ID}` | Le jeu `id` de données dans lequel le lot est conservé. |
| `{FILE_NAME}` | Nom du fichier que vous téléchargez. |

**Requête**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Réponse**

Un fichier téléchargé avec succès renvoie un corps de réponse vide et un état HTTP 200 (OK).

## Fin du lot de signaux

Après avoir téléchargé tous vos fichiers de données dans le lot, vous pouvez signaler que le lot est terminé. La fin de la signature entraîne la création d’ `DataSetFile` entrées de catalogue pour les fichiers téléchargés et leur association au lot généré précédemment. Le lot du catalogue est marqué comme réussi, ce qui déclenche tout flux en aval qui peut alors fonctionner sur les données désormais disponibles.

**Format API**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Paramètre | Description |
| --- | --- |
| `{BATCH_ID}` | Le lot `id` du lot que vous marquez comme terminé. |

**Requête**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Réponse**

Un lot terminé avec succès renvoie un corps de réponse vide et l’état HTTP 200 (OK).

## Impression d&#39;écran

En fonction de la taille des données, l’assimilation des lots prend plus ou moins de temps. Vous pouvez surveiller l’état d’un lot en ajoutant un paramètre de `batch` requête contenant l’identifiant du lot à une `GET /batches` requête. L’API sonde le jeu de données pour connaître l’état du lot depuis l’assimilation jusqu’à ce que la réponse `status` dans la réponse indique l’achèvement (&quot;succès&quot; ou &quot;échec&quot;).

**Format API**

```HTTP
GET /batches?batch={BATCH_ID}
```

| Paramètre | Description |
| --- | --- |
| `{BATCH_ID}` | Le lot `id` du lot à surveiller. |

**Requête**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Réponse**

Une réponse positive renvoie un objet avec son `status` attribut contenant la valeur de `success`:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{IMS_ORG}",
        "created": 1534142888068,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1534142955152,
        "replay": {},
        "status": "success",
        "errors": [],
        "version": "1.0.3",
        "availableDates": {},
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "metrics": {
            "startTime": 1534142943819,
            "endTime": 1534142951760,
            "recordsRead": 108,
            "recordsWritten": 108
        }
    }
}
```

Une réponse négative renvoie un objet avec la valeur de `"failed"` dans son `"status"` attribut et inclut tous les messages d’erreur pertinents :

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{IMS_ORG}",
        "status": "failed",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "replay": {},
        "availableDates": {},
        "metrics": {
            "startTime": 1536610322329,
            "endTime": 1536610438083,
            "recordsRead": 4004,
            "recordsWritten": 4004,
            "failureReason": "Job aborted due to stage failure: Task 0 in stage 1.0 failed 4 times,:"
        },
        "errors": [
            {
                "code": "0070000017",
                "description": "Unknown error occurred."
            },
            {
                "code": "unknown",
                "description": "Job aborted."
            }
        ],
        "created": 1536609893629,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1536610442814,
        "version": "1.0.5"
    }
}
```

>[!NOTE] Un intervalle d’interrogation recommandé est de deux minutes.

## Lire les données du jeu de données

Avec l’ID de lot, vous pouvez utiliser l’API d’accès aux données pour lire et vérifier tous les fichiers téléchargés dans le lot. La réponse renvoie un tableau contenant un d’ID de fichier, chacun faisant référence à un fichier du lot.

Vous pouvez également utiliser l’API d’accès aux données pour renvoyer le nom, la taille en octets et un lien pour télécharger le fichier ou le dossier.

Vous trouverez des étapes détaillées pour travailler avec l’API d’accès aux données dans le guide [du développeur d’accès aux](../../data-access/home.md)données.

## Mettre à jour le de jeux de données 

Vous pouvez ajouter des champs et assimiler des données supplémentaires dans les jeux de données que vous avez créés. Pour ce faire, vous devez d’abord mettre à jour le  du en ajoutant des propriétés supplémentaires qui définissent les nouvelles données. Vous pouvez effectuer cette opération à l’aide des opérations PATCH et/ou PUT pour mettre à jour le  de existant.

Pour plus d&#39;informations sur la mise à jour des  de, consultez le Guide [du développeur de l&#39;API de Registre de](../../xdm/api/getting-started.md).

Une fois que vous avez mis à jour le  du, vous pouvez suivre de nouveau les étapes de ce didacticiel pour assimiler de nouvelles données conformes au révisé.

Il est important de se rappeler que l&#39;évolution  est purement additive, ce qui signifie que vous ne pouvez pas introduire une modification de rupture à un une fois qu&#39;il a été enregistré dans le registre et utilisé pour l&#39;ingestion de données. Pour en savoir plus sur les meilleures pratiques de composition de  à utiliser avec Adobe Experience Platform, reportez-vous au guide sur les [bases de la composition](../../xdm/schema/composition.md)de .