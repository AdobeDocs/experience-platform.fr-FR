---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exportation de données à l’aide d’API
topic: tutorial
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# Exportation de données  à l’aide d’API

Le  Client en temps réel vous permet de créer un seul de clients individuels en rassemblant des données provenant de plusieurs sources, y compris des données d’attributs et des données comportementales. Les données disponibles dans le  du peuvent ensuite être exportées dans un jeu de données pour un traitement ultérieur. Ce didacticiel fournit des instructions étape par étape pour la création et la gestion des tâches d’exportation à l’aide de l’API [de  client en temps](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)réel.

Outre la création d’une tâche d’exportation, vous pouvez également accéder aux données  à l’aide de l’API d’accès aux  et des projections. Pour plus d&#39;informations sur ces autres modèles d&#39;accès, consultez le didacticiel [sur l&#39;API d&#39;accès aux](../../profile/api/entities.md) ou le didacticiel sur la [configuration des destinations et des projections](../../profile/api/edge-projections.md) de périphérie.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans l’utilisation des données  des. Avant de commencer ce didacticiel, veuillez consulter la documentation des services suivants :

- [](../../profile/home.md)du client en temps réel : Fournit un client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [Adobe Experience Platform Segmentation Service](../home.md): Permet de créer  segments  à partir de données de client en temps réel.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plateforme organise les données d’expérience client.
- [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

### En-têtes obligatoires

Ce didacticiel nécessite également que vous ayez suivi le didacticiel [d’](../../tutorials/authentication.md) authentification afin d’effectuer des appels aux API de plateforme. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Les demandes d’API de plateforme nécessitent un en-tête qui spécifie le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes POST, PUT et PATCH nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Création d’une tâche d’exportation

L’exportation de données  nécessite d’abord la création d’un jeu de données dans lequel les données seront exportées, puis le lancement d’une nouvelle tâche d’exportation. Ces deux étapes peuvent être réalisées à l’aide des API de plateformes d’expérience, la première utilisant l’API de service de catalogue et la seconde utilisant l’API de  client en temps réel. Les sections qui suivent contiennent des instructions détaillées sur l&#39;exécution de chaque étape.

- [Création d’un jeu](#create-a-target-dataset) de données de  : créez un jeu de données contenant les données exportées.
- [Lancer une nouvelle tâche](#initiate-export-job) d’exportation : renseignez le jeu de données avec les données de  XDM individuels.

### Création d’un jeu de données de 

Lors de l’exportation de données , un jeu de données  doit d’abord être créé. Il est important que le jeu de données soit correctement configuré pour garantir la réussite de l’exportation.

L’une des considérations clés est le  sur lequel le jeu de données est basé (`schemaRef.id` dans l’exemple de requête d’API ci-dessous). Pour exporter un segment, le jeu de données doit être basé sur le individuel XDM   de (`https://ns.adobe.com/xdm/context/profile__union`). Un   est ungénéré par le système et en lecture seule qui permet de les champs de l’qui partagent la même classe, c’est-à-dire la classe de l’ensemble de l’ensemble de l’espace de travail XDM. Pour plus d&#39;informations sur   [](../../xdm/schema/composition.md#union)de l&#39;, veuillez consulter la section de l&#39;en temps réel du guidedu développeur du registre desclients.

Les étapes qui suivent dans ce didacticiel expliquent comment créer un jeu de données qui référence le XDM individuel    le à l’aide de l’API de catalogue. Vous pouvez également utiliser l’interface utilisateur d’Adobe Experience Platform pour créer un jeu de données qui fait référence au   d’ de. Les étapes d’utilisation de l’interface utilisateur sont décrites dans [ce didacticiel de l’interface utilisateur pour l’exportation de segments](./create-dataset-export-segment.md) , mais elles sont également applicables ici. Une fois terminé, vous pouvez revenir à ce didacticiel pour passer aux étapes nécessaires au [lancement d’une nouvelle tâche](#initiate-export-job)d’exportation.

Si vous disposez déjà d’un jeu de données compatible et que vous connaissez son ID, vous pouvez passer directement à l’étape [de création d’une nouvelle tâche](#initiate-export-job)d’exportation.

**Format API**

```http
POST /dataSets
```

**Requête**

La requête suivante crée un jeu de données, fournissant des paramètres de configuration dans la charge utile.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        },
        "fileDescription": {
          "persisted": true,
          "containerFormat": "parquet",
          "format": "parquet"
        },
        "aspect": "production"
      }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom descriptif du jeu de données. |
| `schemaRef.id` | ID de l’ () auquel le jeu de données sera associé. |
| `fileDescription.persisted` | Valeur booléenne qui, lorsqu’elle est définie sur `true`, permet au jeu de données de persister dans le   de . |

**Réponse**

Une réponse réussie renvoie un tableau contenant l&#39;identifiant unique généré par le système et en lecture seule du jeu de données nouvellement créé. Un ID de jeu de données correctement configuré est nécessaire pour exporter avec succès les données .

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Lancer la tâche d&#39;exportation

Une fois que vous disposez d’un jeu de données   persistant, vous pouvez créer une tâche d’exportation afin de conserver les données du jeu de données. Pour ce faire, vous devez envoyer une requête POST au `/export/jobs` point de terminaison dans l’API du client en temps réel et fournir les détails des données que vous souhaitez exporter dans le corps de la requête.

**Format API**

```http
POST /export/jobs
```

**Requête**

La requête suivante crée une nouvelle tâche d’exportation, fournissant des paramètres de configuration dans la charge utile.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `fields` | *(Facultatif)* Limite les champs de données à inclure dans l’exportation à ceux fournis dans ce paramètre. Le même paramètre est également disponible lors de la création d’un segment. Par conséquent, les champs du segment ont peut-être déjà été filtrés. Si vous omettez cette valeur, tous les champs seront inclus dans les données exportées. |
| `mergePolicy` | *(Facultatif)* Spécifie la stratégie de fusion pour régir les données exportées. Incluez ce paramètre lorsque plusieurs segments sont exportés. Si vous omettez cette valeur, le service d’exportation utilisera la stratégie de fusion fournie par le segment. |
| `mergePolicy.id` | ID de la stratégie de fusion. |
| `mergePolicy.version` | Version spécifique de la stratégie de fusion à utiliser. Si vous omettez cette valeur, la version la plus récente sera utilisée par défaut. |
| `filter` | *(Facultatif)* Indique un ou plusieurs des  de suivants à appliquer au segment avant l’exportation. |
| `filter.segments` | *(Facultatif)* Indique les segments à exporter. Si vous omettez cette valeur, toutes les données de tous les  seront exportées. Accepte un tableau d’objets de segment, chacun contenant les champs suivants :<ul><li>`segmentId`: **(Obligatoire en cas d’utilisation`segments`)** de l’ID de segment pour  à exporter.</li><li>`segmentNs` *(Facultatif)* Segmenter le   pour le groupe `segmentID`donné.</li><li>`status` *(Facultatif)* Tableau de chaînes fournissant un filtre d’état pour le `segmentID`. Par défaut, `status` la valeur `["realized", "existing"]` qui représente tous les  de qui tombent dans le segment à l’heure actuelle. Les valeurs possibles sont les suivantes : `"realized"`, `"existing"`et `"exited"`.</br></br>Pour plus d’informations, reportez-vous au didacticiel [sur la](./create-a-segment.md)création de segments.</li></ul> |
| `filter.segmentQualificationTime` | *(Facultatif)* Filtrage basé sur l’heure de qualification du segment. L’heure  et/ou l’heure de fin du peuvent être fournies. |
| `filter.segmentQualificationTime.startTime` | *(Facultatif)* Le de qualification de segment  la durée d’un ID de segment pour un état donné. Il n’est pas fourni, il n’y aura aucun filtre sur l’heure de  du pour une qualification d’ID de segment. L’horodatage doit être fourni au format [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | *(Facultatif)* Heure de fin de qualification de segment pour un ID de segment pour un état donné. Il n’est pas fourni, il n’y aura aucun filtre à l’heure de fin pour une qualification d’ID de segment. L’horodatage doit être fourni au format [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp ` | *(Facultatif)* Limite les  exportées à celles qui ont été mises à jour après cet horodatage. L’horodatage doit être fourni au format [RFC 3339](https://tools.ietf.org/html/rfc3339) . <ul><li>`fromIngestTimestamp` pour les ****, le cas échéant: Inclut tous les  fusionnés dans lesquels l’horodatage mis à jour fusionné est supérieur à l’horodatage donné. Prend en charge `greater_than` l’opérande.</li><li>`fromTimestamp` pour les  ****: Tous les  ingérés après cet horodatage seront exportés correspondant au résultat de l’ résultant. Ce n&#39;est pas l&#39;heure de  elle-même, mais le temps d&#39;ingestion pour la  de la.</li> |
| `filter.emptyProfiles` | *(Facultatif)* Valeur booléenne. Les  de peuvent contenir des enregistrements de  de, des enregistrements d’ExperienceEvent ou les deux. Les  sans enregistrements de et seuls les enregistrements d’ExperienceEvent sont appelés &quot;profils vides&quot;. Pour exporter tous les  de dans le magasin  de, y compris les &quot;profils vides&quot;, définissez la valeur de `emptyProfiles` sur `true`. Si `emptyProfiles` est défini sur `false`, seuls les avec des enregistrements de dans le magasin sont exportés. Par défaut, si `emptyProfiles` l’attribut n’est pas inclus, seuls les  contenant des enregistrements  de sont exportés. |
| `additionalFields.eventList` | *(Facultatif)* Contrôle les champs  série chronologique exportés pour des objets enfants ou associés en fournissant un ou plusieurs des paramètres suivants :<ul><li>`eventList.fields`: Contrôlez les champs à exporter.</li><li>`eventList.filter`: Indique les critères qui limitent les résultats inclus dans les objets associés. Attend une valeur minimale requise pour l’exportation, généralement une date.</li><li>`eventList.filter.fromIngestTimestamp`:  série chronologique de  s’à celles qui ont été ingérées après l’horodatage fourni. Ce n&#39;est pas l&#39;heure de  elle-même, mais le temps d&#39;ingestion pour la  de la.</li></ul> |
| `destination` | **(Obligatoire)** Informations de destination pour les données exportées :<ul><li>`destination.datasetId`: **(Obligatoire)** Identifiant du jeu de données dans lequel les données doivent être exportées.</li><li>`destination.segmentPerBatch`: *(Facultatif)* Valeur booléenne par défaut `false`, si elle n’est pas fournie. Une valeur de `false` exporte tous les ID de segment dans un seul ID de lot. Une valeur de `true` exporte un ID de segment dans un ID de lot. Notez que la définition de la valeur à `true` définir peut affecter les performances d’exportation par lot.</li></ul> |
| `schema.name` | **(Obligatoire)** Nom du  de associé au jeu de données dans lequel les données doivent être exportées. |

>[!NOTE] Pour exporter uniquement les données  du et ne pas inclure les données ExperienceEvent associées, supprimez l’objet &quot;additionalFields&quot; de la requête.

**Réponse**

Une réponse réussie renvoie un jeu de données rempli avec des données , comme spécifié dans la requête.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Si la requête n’ `destination.segmentPerBatch` avait pas été incluse (si elle n’était pas présente, elle est définie par défaut `false`) ou si la valeur avait été définie sur `false`, l’ `destination` objet de la réponse ci-dessus ne contiendrait pas de `batches` tableau et n’en incluerait qu’un `batchId`, comme illustré ci-dessous. Ce lot unique inclurait tous les ID de segment, alors que la réponse ci-dessus montre un ID de segment unique par ID de lot.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

##  toutes les tâches d’exportation

Vous pouvez renvoyer un  de toutes les tâches d’exportation pour une organisation IMS particulière en exécutant une requête GET vers le `export/jobs` point de fin. La requête prend également en charge les paramètres de  `limit` et `offset`, comme illustré ci-dessous.

**Format API**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Propriété | Description |
| -------- | ----------- |
| `limit` | Spécifiez le nombre d’enregistrements à renvoyer. |
| `offset` | Décale la page des résultats à renvoyer par le nombre fourni. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

La réponse comprend un `records` objet contenant les tâches d’exportation créées par votre organisation IMS.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
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
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
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
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

## Suivi de la progression de l’exportation

Pour  les détails d’une tâche d’exportation spécifique ou surveiller son état au cours de son traitement, vous pouvez envoyer une requête GET au `/export/jobs` point de fin et inclure le `id` chemin d’accès de la tâche d’exportation. La tâche d’exportation est terminée lorsque le `status` champ renvoie la valeur &quot;SUCCEEDED&quot;.

**Format API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | La tâche `id` d’exportation à laquelle vous souhaitez accéder. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Propriété | Description |
| -------- | ----------- |
| `batchId` | Identifiant des lots créés à partir d’une exportation réussie, à utiliser à des fins de recherche lors de la lecture des données  du. |

## Annulation d’une tâche d’exportation

Experience Platform vous permet d’annuler une tâche d’exportation existante, ce qui peut s’avérer utile pour plusieurs raisons, notamment si la tâche d’exportation n’a pas été terminée ou est devenue bloquée au cours de l’étape de traitement. Pour annuler une tâche d’exportation, vous pouvez exécuter une requête DELETE vers le `/export/jobs` point de fin et inclure la tâche `id` d’exportation que vous souhaitez annuler dans le chemin d’accès de la demande.

**Format API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | La tâche `id` d’exportation à laquelle vous souhaitez accéder. |

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une requête de suppression réussie renvoie l’état HTTP 204 (aucun contenu) et un corps de réponse vide, indiquant que l’opération d’annulation a réussi.

## Étapes suivantes

Une fois l’exportation terminée, vos données sont disponibles dans Data Lake dans la plateforme Experience Platform. Vous pouvez ensuite utiliser l’API [d’accès aux](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) données pour accéder aux données à l’aide de la `batchId` variable associée à l’exportation. Selon la taille de l’exportation, les données peuvent être en blocs et le lot peut être constitué de plusieurs fichiers.

Pour obtenir des instructions détaillées sur l’utilisation de l’API d’accès aux données pour accéder aux fichiers de commandes et les télécharger, suivez le didacticiel [Accès aux](../../data-access/tutorials/dataset-data.md)données.

Vous pouvez également accéder aux données de de clients en temps réel exportées avec succès à l’aide du service de Adobe Experience Platform. Grâce à l’interface utilisateur ou à l’API RESTful, le service de  de vous permet d’écrire, de valider et d’exécuter des  sur des données du lac Data.

Pour plus d&#39;informations sur la manière de  de données , veuillez consulter la documentation [du service de](../../query-service/home.md)de.