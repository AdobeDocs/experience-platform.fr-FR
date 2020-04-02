---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exportation de tâches
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7

---


# Exportation de tâches

intro

- Récupération d’un  de tâches d’exportation
- Création d’une tâche d’exportation
- Récupération d’une tâche d’exportation spécifique
- Annuler ou supprimer une tâche d’exportation spécifique

## Prise en main

Les points de fin d’API utilisés dans ce guide font partie de l’API de segmentation. Avant de poursuivre, consultez le guide [du développeur de](./getting-started.md)segmentation.

En particulier, la section [de](./getting-started.md#getting-started) prise en main du guide du développeur de segmentation comprend des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans le  du et des informations importantes concernant les en-têtes requis nécessaires pour effectuer des appels à une API de plateforme d’expérience.

## Récupération d’un  de tâches d’exportation

Vous pouvez récupérer un  de toutes les tâches d’exportation pour votre organisation IMS en envoyant une requête GET au point de `/export/jobs` fin.

**Format API**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Facultatif*) Paramètres ajoutés au chemin de requête qui configurent les résultats renvoyés dans la réponse. Plusieurs paramètres peuvent être inclus, séparés par des esperluettes (`&`). Les paramètres disponibles sont répertoriés ci-dessous.

**Paramètres**

Vous trouverez ci-dessous un des paramètres de disponibles pour répertorier les tâches d’exportation. Tous ces paramètres sont facultatifs. Un appel à ce point de fin sans paramètre récupérera toutes les tâches d’exportation disponibles pour votre entreprise.

| Paramètre | Description |
| --------- | ----------- |
| `limit` | Indique le nombre de tâches d’exportation renvoyées. |
| `offset` | Indique le décalage des pages de résultats. |
| `status` |  les résultats selon l’état. Les valeurs prises en charge sont `NEW`, `SUCCEEDED`et `FAILED`. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec un de tâches d’exportation pour l’organisation IMS spécifiée comme JSON. La réponse suivante renvoie un  de toutes les tâches d’exportation réussies pour l’organisation IMS.

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
        "batches": {
          "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
          "segmentNs": "ups",
          "status": [
            "realized"
          ],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        }
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
            "fromIngestTimestamp": "2018-01-01T00:00:00Z"
          }
        }
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
        "aCPDatasetWriteTime": {
          "startTimeInMs": 123456789000,
          "endTimeInMs": 123456799000,
          "totalTimeInMs": 10000
        }
      },
      "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
        "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "creationTime": 1538615973895,
      "updateTime": 1538616233239,
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
    }
  ],
  "page": {
    "sortField": "createdTime",
    "sort": "desc",
    "pageOffset": "1540974701302_96",
    "pageSize": 10
  },
  "link": {
    "next": "string"
  }
}
```

## Création d’une tâche d’exportation

Vous pouvez créer une tâche d’exportation en envoyant une requête POST au point de `/export/jobs` fin.

**Format API**

```http
POST /export/jobs
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
  },
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df"
  },
  "schema": {
    "name": "_xdm.context.profile"
  }
 }'
```

| Paramètre | Description |
| --------- | ----------- |
| `fields` | Facultatif. des champs exportés, séparés par des virgules. Si rien n’est indiqué, tous les champs seront exportés. |
| `mergePolicy` | Facultatif. Si elle n’est pas fournie, l’exportation applique la même stratégie de fusion que le segment donné. |
| `filter` | Facultatif. Si rien n’est indiqué, toutes les données seront exportées. |
| `filter.segments` | Facultatif. de segments pour la tâche d’exportation. |
| `filter.segmentQualificationTime` | Facultatif. Filtre pour l’heure de qualification du segment. Le  et/ou l’heure de fin peuvent être fournis. |
| `filter.fromIngestTimestamp` | Facultatif. Horodatage au format RFC-3339. |
| `destination.datasetId` | Obligatoire. Valeur `id` du jeu de données vers lequel les données sont exportées. |
| `segments.segmentId` | Obligatoire. Valeur `id` du segment en cours d’exportation. |
| `segments.sgementNs` | Facultatif. Le `namespace` segment donné. |



**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les détails de votre tâche d’exportation nouvellement créée.

```json
{
  "id": 100,
  "jobType": "BATCH",
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
    "batches": {
      "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
      "segmentNs": "ups",
      "status": [
        "realized"
      ],
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    }
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
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
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
    "aCPDatasetWriteTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    }
  },
  "computeGatewayJobId": {
    "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
    "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
  },
  "creationTime": 1538615973895,
  "updateTime": 1538616233239,
  "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

## Récupération d’une tâche d’exportation spécifique

Vous pouvez récupérer des informations détaillées sur une tâche d’exportation spécifique en faisant une requête GET au point de `/export/jobs` fin et en indiquant la `id` valeur de la tâche d’exportation dans le chemin d’accès de la requête.

**Format API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

- `{EXPORT_JOB_ID}`: Valeur `id` de la tâche d’exportation que vous souhaitez récupérer.

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations détaillées sur la tâche d’exportation spécifiée.

```json
{
  "id": 100,
  "jobType": "BATCH",
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
    "batches": {
      "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
      "segmentNs": "ups",
      "status": [
        "realized"
      ],
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    }
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
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
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
    "aCPDatasetWriteTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    }
  },
  "computeGatewayJobId": {
    "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
    "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
  },
  "creationTime": 1538615973895,
  "updateTime": 1538616233239,
  "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

## Annuler ou supprimer une tâche d’exportation spécifique

Vous pouvez demander de supprimer une tâche d’exportation spécifiée en effectuant une requête DELETE au point de `/export/jobs` fin et en indiquant la `id` valeur de la tâche d’exportation dans le chemin d’accès de la requête.

**Format API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

- `{EXPORT_JOB_ID}`: Valeur `id` de la tâche d’exportation à supprimer.

**Requête**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec le message suivant :

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Étapes suivantes
