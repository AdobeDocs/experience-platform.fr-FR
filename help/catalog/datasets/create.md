---
keywords: Experience Platform;accueil;rubriques populaires;jeu de données;Jeu de données;créer un jeu de données;créer un jeu de données
solution: Experience Platform
title: Créer un jeu de données à l’aide d’API
description: Ce document décrit les étapes générales pour créer un jeu de données à l’aide des API d’Adobe Experience Platform et pour renseigner le jeu de données à l’aide d’un fichier.
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 80%

---

# Création d’un jeu de données à l’aide d’API

Ce document décrit les étapes générales pour créer un jeu de données à l’aide des API d’Adobe Experience Platform et pour renseigner le jeu de données à l’aide d’un fichier.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Ingestion par lots](../../ingestion/batch-ingestion/overview.md) : [!DNL Experience Platform] permet d’ingérer des données sous forme de fichiers de lots.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
* [[!DNL Sandboxes]](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin afin de passer avec succès des appels aux API [!DNL Experience Platform].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant une payload (POST, PUT, PATCH) nécessitent un en-tête `Content-Type: application/json` supplémentaire : Pour les requêtes JSON+PATCH, le `Content-Type` doit être `application/json-patch+json`.

## Tutoriel

Pour créer un jeu de données, vous devez d’abord définir un schéma. Un schéma est un ensemble de règles permettant de représenter des données. Outre la description de la structure des données, les schémas fournissent des contraintes et des attentes qui peuvent être appliquées et utilisées pour valider les données lorsqu’elles sont déplacées d’un système à l’autre.

Ces définitions standard permettent d’interpréter les données de manière cohérente, quelle que soit leur origine, et éliminent la nécessité d’une traduction entre les applications. Pour plus d’informations sur la composition de schémas, consultez le guide sur les [principes de base de la composition de schémas](../../xdm/schema/composition.md)

## Recherche d’un schéma du jeu de données

Ce tutoriel commence là où le [tutoriel de l’API Schema Registry](../../xdm/tutorials/create-schema-api.md) se termine, en utilisant le schéma des membres du programme de fidélité créé pendant ce tutoriel.

Si vous n’avez pas terminé le tutoriel [!DNL Schema Registry], commencez là et poursuivez ce tutoriel sur les jeux de données uniquement une fois que vous avez composé le schéma nécessaire.

L’appel suivant peut être utilisé pour afficher le schéma des membres du programme de fidélité que vous avez créé au cours du tutoriel de l’API [!DNL Schema Registry] :

**Format d’API**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Le format de l’objet de réponse dépend de l’en-tête Accept envoyé dans la requête. Les propriétés individuelles de cette réponse ont été réduites pour gagner de l’espace.

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
    "imsOrg": "{ORG_ID}",
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

Une fois le schéma des membres du programme de fidélité en place, vous pouvez désormais créer un jeu de données qui référence le schéma.

**Format d’API**

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
| `schemaRef.id` | La valeur `$id` de l’URI pour le schéma XDM sur lequel sera basé le jeu de données. |
| `schemaRef.contentType` | Indique le format et la version du schéma. Pour plus d’informations, reportez-vous à la section [contrôle de version des schémas](../../xdm/api/getting-started.md#versioning) du guide de l’API XDM. |

>[!NOTE]
>
>Ce tutoriel utilise le format de fichier [Apache Parquet](https://parquet.apache.org/docs/) pour tous ses exemples. Vous trouverez un exemple d’utilisation du format de fichier JSON dans le [guide de développement de l’ingestion par lots](../../ingestion/batch-ingestion/api-overview.md)

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Créé) et un objet de réponse constitué d’un tableau contenant l’identifiant du jeu de données nouvellement créé au format `"@/datasets/{DATASET_ID}"`. L’identifiant du jeu de données est une chaîne en lecture seule générée par le système et utilisée pour référencer le jeu de données dans les appels API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Création d’un lot

Avant d’ajouter des données à un jeu de données, vous devez créer un lot lié au jeu de données. Le lot sert ensuite au chargement.

**Format d’API**

```HTTP
POST /batches
```

**Requête**

Le corps de requête comprend un champ « datasetId », dont la valeur `{DATASET_ID}` est générée à l’étape précédente.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) et un objet de réponse. L’objet de réponse est constitué d’un tableau contenant l’identifiant du lot nouvellement créé au format `"@/batches/{BATCH_ID}"`. L’ID de lot est une chaîne générée par le système en lecture seule qui est utilisée pour référencer le lot dans les appels API.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
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

## Chargement de fichiers dans un lot

Une fois le nouveau lot créé pour le chargement, vous pouvez désormais charger des fichiers dans le jeu de données spécifique. Il est important de se rappeler que lorsque vous avez défini le jeu de données, vous avez spécifié le format de fichier Parquet. Par conséquent, les fichiers que vous chargez doivent être dans ce format.

>[!NOTE]
>
>Le fichier de chargement de données le plus volumineux pris en charge est de 512 Mo. Si votre fichier de données est plus volumineux, il doit être divisé en blocs de 512 Mo maximum afin de les charger un par un. En répétant cette étape, vous pouvez charger chaque fichier dans le même lot, à l’aide du même identifiant de lot. Le nombre de fichiers que vous pouvez charger dans le cadre d’un lot n’est pas limité.

**Format d’API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{BATCH_ID}` | L’`id` du lot dans lequel vous effectuez le chargement. |
| `{DATASET_ID}` | L’`id` du jeu de données dans lequel le lot est conservé. |
| `{FILE_NAME}` | Le nom du fichier que vous chargez. |

**Requête**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Réponse**

Un fichier chargé renvoie un corps de réponse vide et un état HTTP 200 (OK).

## Signalement de la fin du lot

Après avoir chargé tous les fichiers de données dans le lot, vous pouvez signaler que le lot est terminé. La signalisation de fin entraîne la création par le service d&#39;entrées de `DataSetFile` [!DNL Catalog] pour les fichiers chargés et leur association au lot généré précédemment. Le lot de [!DNL Catalog] est marqué comme réussi, ce qui déclenche tous les flux en aval qui peuvent ensuite travailler sur les données désormais disponibles.

**Format d’API**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Paramètre | Description |
| --- | --- |
| `{BATCH_ID}` | L’`id` du lot que vous marquez comme terminé. |

**Requête**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Réponse**

Un lot terminé renvoie un corps de réponse vide et un état HTTP 200 (OK).

## Surveillance de l’ingestion

La durée d’ingestion des lots varie en fonction de la taille des données. Vous pouvez surveiller l’état d’un lot en ajoutant l’identifiant d’un lot à une requête `GET /batches`.

**Format d’API**

```HTTP
GET /batches/{BATCH_ID}
```

| Paramètre | Description |
| --- | --- |
| `{BATCH_ID}` | L’`id` du lot que vous souhaitez surveiller. |

**Requête**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Réponse**

Une réponse positive renvoie un objet avec son attribut `status` contenant la valeur de `success` :

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{ORG_ID}",
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

Une réponse négative renvoie un objet avec la valeur `"failed"` dans son attribut `"status"` et comprend les messages d’erreur pertinents :

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{ORG_ID}",
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

>[!NOTE]
>
>Un intervalle d’interrogation recommandé est de deux minutes.

## Lecture des données du jeu de données

L’identifiant de lot vous permet d’utiliser l’API d’accès aux données pour relire et vérifier tous les fichiers chargés dans le lot. La réponse renvoie un tableau contenant une liste d’identifiants de fichier, chacun référençant un fichier du lot.

Vous pouvez également utiliser l’API d’accès aux données pour renvoyer le nom, la taille en octets et un lien pour télécharger le fichier ou le dossier.

Vous trouverez des étapes détaillées pour utiliser l’API d’accès aux données dans le [guide de développement de l’accès aux données](../../data-access/home.md).

## Mise à jour du schéma du jeu de données

Vous pouvez ajouter des champs et ingérer des données supplémentaires dans les jeux de données que vous avez créés. Pour ce faire, vous devez d’abord mettre à jour le schéma en ajoutant des propriétés supplémentaires qui définissent les nouvelles données. Vous pouvez effectuer cette opération à l’aide des opérations PATCH et/ou PUT pour mettre à jour le schéma existant.

Pour plus d’informations sur la mise à jour des schémas, consultez le [guide de développement de l’API Schema Registry](../../xdm/api/getting-started.md).

Une fois que vous avez mis à jour le schéma, vous pouvez à nouveau suivre les étapes de ce tutoriel pour ingérer de nouvelles données conformes au schéma révisé.

Il est important de se rappeler que l’évolution des schémas est purement additive, ce qui signifie que vous ne pouvez pas apporter de modification critique à un schéma une fois qu’il a été enregistré dans le registre et utilisé pour l’ingestion de données. Pour en savoir plus sur les bonnes pratiques de composition de schéma à utiliser avec Adobe Experience Platform, consultez le guide sur les [principes de base de la composition de schémas](../../xdm/schema/composition.md).
