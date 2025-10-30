---
solution: Experience Platform
title: Point d’entrée de l’API des tâches d’exportation de segments
description: Les tâches d’exportation sont des processus asynchrones utilisés pour conserver les membres des segments d’audience dans les jeux de données. Vous pouvez utiliser le point d’entrée /export/jobs dans l’API Adobe Experience Platform Segmentation Service, qui vous permet de récupérer, de créer et d’annuler des traitements d’exportation par programmation.
role: Developer
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 32%

---

# Point d’entrée des tâches d’exportation de segments

Les tâches d’exportation sont des processus asynchrones utilisés pour conserver les membres des segments d’audience dans les jeux de données. Vous pouvez utiliser le point d’entrée `/export/jobs` dans l’API de segmentation Adobe Experience Platform, ce qui vous permet de récupérer, de créer et d’annuler des tâches d’exportation par programmation.

>[!NOTE]
>
>Ce guide traite de l’utilisation des tâches d’exportation dans le [!DNL Segmentation API]. Pour plus d’informations sur la gestion des tâches d’exportation pour les données [!DNL Real-Time Customer Profile], consultez le guide sur les [ tâches d’exportation dans l’API Profile](../../profile/api/export-jobs.md)

## Commencer

Les points d’entrée utilisés dans ce guide font partie de l’API [!DNL Adobe Experience Platform Segmentation Service]. Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, y compris les en-têtes requis et la manière de lire des exemples d’appels API.

## Récupération d’une liste de tâches d’exportation {#retrieve-list}

Vous pouvez récupérer une liste de toutes les tâches d’exportation pour votre organisation en envoyant une requête GET au point d’entrée `/export/jobs`.

**Format d’API**

Le point d’entrée `/export/jobs` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Bien que ces paramètres soient facultatifs, leur utilisation est vivement recommandée pour réduire les frais généraux élevés. Si vous effectuez un appel à ce point d’entrée sans paramètre, toutes les tâches d’exportation disponibles pour votre organisation sont récupérées. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

**Paramètres de requête**

+++ Liste des paramètres de requête disponibles.

| Paramètre | Description | Exemple |
| --------- | ----------- | ------- |
| `limit` | Indique le nombre de tâches d’exportation renvoyées. | `limit=10` |
| `offset` | Indique le décalage des pages de résultats. | `offset=1540974701302_96` |
| `status` | Filtre les résultats selon l’état. Les valeurs prises en charge sont « NEW », « SUCCEEDED » et « FAILED ». | `status=NEW` |

+++

**Requête**

La requête suivante récupérera les deux dernières tâches d’exportation de votre organisation.

+++ Exemple de requête pour récupérer des tâches d’exportation.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

La réponse suivante renvoie le statut HTTP 200 avec une liste des tâches d’exportation terminées avec succès, en fonction du paramètre de requête fourni dans le chemin d’accès de la requête.

+++ Exemple de réponse lors de la récupération de tâches d’exportation.

```json
{
    "records": [
        {
            "id": 100,
            "jobType": "BATCH",
            "destination": {
                "datasetId": "5b7c86968f7b6501e21ba9df",
                "segmentPerBatch": false,
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
            },
            "fields": "identities.id,personalEmail.address",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "status": "SUCCEEDED",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "ups",
                        "status": [
                            "realized"
                        ]
                    }
                ]
            },
            "mergePolicy": {
                "id": "timestampOrdered-none-mp",
                "version": 1
            },
            "profileInstanceId": "ups",
            "errors": [
                {
                    "code": "0100000003",
                    "msg": "Error in Export Job",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger"
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "profileExportTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "totalExportedProfileCounter": 20,
                "exportedProfileByNamespaceCounter": {
                    "namespace1": 10,
                    "namespace2": 5
                }
            },
            "computeGatewayJobId": {
                "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
            },
            "creationTime": 1538615973895,
            "updateTime": 1538616233239,
            "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
        },
        {
            "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
            "errors": [
                {
                    "code": "0090000009",
                    "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
                },
                {
                    "code": "unknown",
                    "msg": "Job aborted.",
                    "callStack": "org.apache.spark.SparkException: Job aborted."
                }
            ],
            "jobType": "BATCH",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "AAM",
                        "status": ["realized"]
                    }
                ]
            },
            "id": 722,
            "schema": {
                "name": "_xdm.context.profile"
            },
            "mergePolicy": {
                "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
                "version": 1
            },
            "status": "FAILED",
            "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
            "computeGatewayJobId": {
                "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
            },
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1538573416687,
                    "endTimeInMs": 1538573922551,
                    "totalTimeInMs": 505864
                },
                "profileExportTime": {
                    "startTimeInMs": 1538573872211,
                    "endTimeInMs": 1538573918809,
                    "totalTimeInMs": 46598
                }
            },
            "destination": {
                "datasetId": "5bb4c46757920712f924a3eb",
                "segmentPerBatch": false,
                "batchId": "IWEQ6920712f9475762D"
            },
            "updateTime": 1538573922551,
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "creationTime": 1538573416687
        }
    ],
    "page":{
        "sortField": "createdTime",
        "sort": "desc",
        "pageOffset": "1540974701302_96",
        "pageSize": 2
    },
    "link":{
        "next": "/export/jobs/?limit=2&offset=1538573416687_722"
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `destination` | Informations de destination pour les données exportées :<ul><li>`datasetId` : ID du jeu de données dans lequel les données ont été exportées.</li><li>`segmentPerBatch` : valeur booléenne, qui indique si les identifiants de segment sont consolidés ou non. Une valeur « false » signifie que tous les identifiants de segment sont exportés dans un seul identifiant de lot. Une valeur « true » signifie qu’un identifiant de segment est exporté dans un identifiant de lot. **Remarque :** la définition de la valeur sur true peut affecter les performances d’exportation par lots.</li></ul> |
| `fields` | Liste des champs exportés, séparés par des virgules. |
| `schema.name` | Nom du schéma associé au jeu de données dans lequel les données doivent être exportées. |
| `filter.segments` | Segments exportés. Les champs suivants sont inclus :<ul><li>`segmentId` : identifiant du segment vers lequel les profils seront exportés.</li><li>`segmentNs` : espace de noms de segment pour la `segmentID` donnée.</li><li>`status` : tableau de chaînes fournissant un filtre de statut pour la `segmentID`. Par défaut, `status` possède la valeur `["realized"]` qui représente tous les profils appartenant au segment à l’heure actuelle. Les valeurs possibles sont les suivantes : `realized` et `exited`. Une valeur `realized` signifie que le profil est qualifié pour le segment. Une valeur `exiting` signifie que le profil quitte le segment.</li></ul> |
| `mergePolicy` | Informations sur la politique de fusion pour les données exportées. |
| `metrics.totalTime` | Champ indiquant le temps total d’exécution de la tâche d’exportation. |
| `metrics.profileExportTime` | Champ indiquant le temps nécessaire aux profils pour l’exportation. |
| `page` | Informations sur la pagination des traitements d’exportation demandés. |
| `link.next` | Lien vers la page suivante des traitements d’exportation. |

+++

## Création d’une tâche d’exportation {#create}

Vous pouvez créer une tâche d’exportation en effectuant une requête POST sur le point d’entrée `/export/jobs`.

**Format d’API**

```http
POST /export/jobs
```

**Requête**

La requête suivante crée une tâche d’exportation, configurée en fonction des paramètres fournis dans la payload.

+++ Exemple de requête de création d’une tâche d’exportation.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "string",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z",
                "toIngestTimestamp": "2020-01-01T00:00:00Z"
            }
        }
    },
    "destination":{
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false
    },
    "schema":{
        "name": "_xdm.context.profile"
    },
    "evaluationInfo": {
        "segmentation": true
    }
}'
```

| Propriété | Description |
| -------- | ----------- |
| `fields` | Une liste des champs exportés, séparés par des virgules. Si rien n’est indiqué, tous les champs seront exportés. |
| `mergePolicy` | Indique la politique de fusion pour gérer les données exportées. Ajoutez ce paramètre lorsque plusieurs segments sont exportés. Si elle n’est pas fournie, l’exportation applique la même politique de fusion que le segment donné. |
| `filter` | Objet spécifiant les segments qui seront inclus dans la tâche d’exportation par identifiant, heure de qualification ou heure d’ingestion, selon les sous-propriétés répertoriées ci-dessous. Si rien n’est indiqué, toutes les données seront exportées. |
| `filter.segments` | Indique les segments à exporter. Si vous omettez cette valeur, toutes les données de l’ensemble des profils seront exportées. Accepte un tableau d’objets de segment, chacun contenant les champs suivants :<ul><li>`segmentId` : **(obligatoire en cas d’utilisation de `segments`)** identifiant du segment pour les profils à exporter.</li><li>`segmentNs` : *(facultatif)* espace de noms du segment pour le `segmentID` donné.</li><li>`status` : *(facultatif)* tableau de chaînes fournissant un filtre d’état pour le `segmentID`. Par défaut, `status` possède la valeur `["realized"]` qui représente tous les profils appartenant au segment à l’heure actuelle. Les valeurs possibles sont les suivantes : `realized` et `exited`.  Une valeur `realized` signifie que le profil est qualifié pour le segment. Une valeur `exiting` signifie que le profil quitte le segment.</li></ul> |
| `filter.segmentQualificationTime` | Filtre basé sur le temps de qualification du segment. L’heure de début et/ou l’heure de fin peuvent être fournies. |
| `filter.segmentQualificationTime.startTime` | Heure de début de qualification du segment pour un identifiant de segment pour un statut donné. Si elle n’est pas fournie, aucun filtre ne sera appliqué à l’heure de début pour une qualification d’identifiant du segment. La date et l’heure doivent être fournies au format [RFC 3339](https://tools.ietf.org/html/rfc3339). |
| `filter.segmentQualificationTime.endTime` | Heure de fin de qualification du segment pour un identifiant de segment pour un statut donné. Si elle n’est pas fournie, aucun filtre ne sera appliqué à l’heure de fin pour une qualification d’identifiant du segment. La date et l’heure doivent être fournies au format [RFC 3339](https://tools.ietf.org/html/rfc3339). |
| `filter.fromIngestTimestamp` | Limite les profils exportés à inclure uniquement ceux qui ont été mis à jour après cet horodatage. La date et l’heure doivent être fournies au format [RFC 3339](https://tools.ietf.org/html/rfc3339). <ul><li>`fromIngestTimestamp` pour les **profils**, le cas échéant : inclut tous les profils fusionnés dans lesquels la date et l’heure mises à jour et fusionnées sont supérieures à la date et l’heure données. Prend en charge l’opérande `greater_than`.</li><li>`fromIngestTimestamp` pour les **événements** : tous les événements ingérés après cette date et cette heure seront exportés en fonction du résultat du profil obtenu. Il ne s’agit pas de l’heure de l’événement, mais de l’heure de l’ingestion des événements.</li> |
| `filter.emptyProfiles` | Valeur booléenne qui indique s’il faut filtrer les profils vides. Les profils peuvent contenir des enregistrements de profil, des enregistrements ExperienceEvent ou les deux. Les profils sans enregistrement de profil et uniquement les enregistrements ExperienceEvent sont appelés « emptyProfiles ». Pour exporter tous les profils de la banque de profils, y compris les « emptyProfiles », définissez la valeur de `emptyProfiles` sur `true`. Si `emptyProfiles` est défini sur `false`, seuls les profils ayant des enregistrements de profil dans le magasin sont exportés. Par défaut, si `emptyProfiles` attribut n’est pas inclus, seuls les profils contenant des enregistrements de profil sont exportés. |
| `additionalFields.eventList` | Contrôle les champs d’événement de série temporelle exportés pour les objets enfants ou associés en fournissant un ou plusieurs des paramètres suivants :<ul><li>`fields` : contrôlent les champs à exporter.</li><li>`filter` : indique les critères qui limitent les résultats inclus dans les objets associés. Attend une valeur minimale requise pour l’exportation, généralement une date.</li><li>`filter.fromIngestTimestamp` : filtre les événements de série temporelle sur ceux qui ont été ingérés après l’horodatage fourni. Il ne s’agit pas de l’heure de l’événement, mais de l’heure de l’ingestion des événements.</li><li>`filter.toIngestTimestamp` : filtre la date et l’heure sur celles qui ont été ingérées avant la date et l’heure fournies. Il ne s’agit pas de l’heure de l’événement, mais de l’heure de l’ingestion des événements.</li></ul> |
| `destination` | **(Obligatoire)** Informations sur les données exportées :<ul><li>`datasetId` : **(obligatoire)** identifiant du jeu de données vers lequel les données doivent être exportées.</li><li>`segmentPerBatch` : *(facultatif)* valeur booléenne qui, si elle n’est pas fournie, est définie par défaut sur « false ». Une valeur « false » exporte tous les identifiants de segment dans un seul identifiant de lot. Une valeur « true » exporte un identifiant de segment dans un identifiant de lot. Notez que la définition de la valeur sur « true » peut affecter les performances d’exportation par lots.</li></ul> |
| `schema.name` | **(Obligatoire)** Le nom du schéma associé au jeu de données vers lequel les données doivent être exportées. |
| `evaluationInfo.segmentation` | *(Facultatif)* Valeur booléenne qui, si elle n’est pas fournie, est définie par défaut sur `false`. Une valeur `true` indique que la segmentation doit être effectuée sur la tâche d’exportation. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la tâche d’exportation que vous venez de créer.

+++ Exemple de réponse lors de la création d’une tâche d’exportation.

```json
{
    "id": 100,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
    "status": "NEW",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "_id, _experience",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z"
            }
        }
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
        }
    },
    "computeGatewayJobId": {
        "exportJob": ""    
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Valeur en lecture seule générée par le système identifiant la tâche d&#39;exportation qui vient d&#39;être créée. |

Si `destination.segmentPerBatch` avait été défini sur `true`, l’objet `destination` ci-dessus aurait un tableau `batches`, comme illustré ci-dessous :

```json
    "destination": {
        "dataSetId": "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches": [
            {
                "segmentId": "segment1",
                "segmentNs": "ups",
                "status": ["realized"],
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
            },
            {
                "segmentId": "segment2",
                "segmentNs": "AdCloud",
                "status": "exited",
                "batchId": "df4gssdfb93a09f7e37fa53ad52"
            }
        ]
    }
```

+++

## Récupération d’une tâche d’exportation spécifique {#get}

Vous pouvez récupérer des informations détaillées sur une tâche d’exportation spécifique en adressant une requête GET au point d’entrée `/export/jobs` et en fournissant l’identifiant de la tâche d’exportation que vous souhaitez récupérer dans le chemin de requête.

**Format d’API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | L’`id` de la tâche d’exportation à laquelle vous souhaitez accéder. |

**Requête**

+++ Exemple de requête pour récupérer une tâche d’exportation.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations détaillées sur la tâche d’exportation spécifiée.

+++ Exemple de réponse lors de la récupération d’une tâche d’exportation.

```json
{
    "id": 11037,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
    "status": "SUCCEEDED",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status":[
                    "realized"
                ]
            }
        ]
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "profileExportTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "totalExportedProfileCounter": 20,
        "exportedProfileByNamespaceCounter": {
            "namespace1": 10,
            "namespace2": 5
        }
    },
    "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Propriété | Description |
| -------- | ----------- |
| `destination` | Informations de destination pour les données exportées :<ul><li>`datasetId` : ID du jeu de données dans lequel les données ont été exportées.</li><li>`segmentPerBatch` : valeur booléenne, qui indique si les identifiants de segment sont consolidés ou non. Une valeur `false` signifie que tous les identifiants de segment étaient regroupés dans un seul identifiant de lot. Une valeur `true` signifie qu’un identifiant de segment est exporté dans un identifiant de lot.</li></ul> |
| `fields` | Liste des champs exportés, séparés par des virgules. |
| `schema.name` | Nom du schéma associé au jeu de données dans lequel les données doivent être exportées. |
| `filter.segments` | Segments exportés. Les champs suivants sont inclus :<ul><li>`segmentId` : identifiant du segment pour les profils à exporter.</li><li>`segmentNs` : espace de noms de segment pour la `segmentID` donnée.</li><li>`status` : tableau de chaînes fournissant un filtre de statut pour la `segmentID`. Par défaut, `status` possède la valeur `["realized"]` qui représente tous les profils appartenant au segment à l’heure actuelle. Les valeurs possibles sont les suivantes : `realized` et `exited`.  Une valeur `realized` signifie que le profil est qualifié pour le segment. Une valeur `exiting` signifie que le profil quitte le segment.</li></ul> |
| `mergePolicy` | Informations sur la politique de fusion pour les données exportées. |
| `metrics.totalTime` | Champ indiquant le temps total d’exécution de la tâche d’exportation. |
| `metrics.profileExportTime` | Champ indiquant le temps nécessaire aux profils pour l’exportation. |
| `totalExportedProfileCounter` | Nombre total de profils exportés dans tous les lots. |

+++

## Annulation ou suppression d’une tâche d’exportation spécifique {#delete}

Vous pouvez demander la suppression de la tâche d’exportation spécifiée en adressant une requête DELETE au point d’entrée `/export/jobs` et en fournissant l’identifiant de la tâche d’exportation que vous souhaitez supprimer du chemin de requête.

**Format d’API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | `id` de la tâche d’exportation à supprimer. |

**Requête**

+++ Exemple de requête de suppression d’une tâche d’exportation.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 204 avec le message suivant.

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux le fonctionnement des tâches d’exportation.
