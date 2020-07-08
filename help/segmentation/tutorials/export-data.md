---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exportation de données à l’aide d’API
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 2%

---


# Exportation de données de Profil à l’aide d’API

Le Profil client en temps réel vous permet de créer une vue unique de clients individuels en réunissant des données provenant de plusieurs sources, y compris des données d’attributs et des données comportementales. Les données disponibles dans le Profil peuvent ensuite être exportées vers un jeu de données en vue d’un traitement ultérieur. Ce didacticiel fournit des instructions détaillées pour la création et la gestion des tâches d’exportation à l’aide de l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)Segmentation.

Outre la création d’une tâche d’exportation, vous pouvez également accéder aux données de Profil à l’aide de l’API d’accès au Profil et des projections. Pour plus d&#39;informations sur ces autres modèles d&#39;accès, consultez le didacticiel [sur l&#39;API d&#39;accès aux](../../profile/api/entities.md) Profils ou le didacticiel sur la [configuration de destinations et de projections](../../profile/api/edge-projections.md) de périphérie.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des différents services d&#39;Adobe Experience Platform impliqués dans l&#39;utilisation des données de Profil. Avant de commencer ce didacticiel, consultez la documentation relative aux services suivants :

- [Profil](../../profile/home.md)client en temps réel : Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [Service](../home.md)de segmentation des Adobes Experience Platform : Permet de créer des segments d’audience à partir des données du Profil client en temps réel.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.
- [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance Platform unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

### En-têtes requis

Ce didacticiel nécessite également que vous ayez suivi le didacticiel [d’](../../tutorials/authentication.md) authentification afin de pouvoir invoquer les API Platform. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API Experience Platform, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de l&#39;Experience Platform sont isolées dans des sandbox virtuels spécifiques. Les requêtes aux API Platform nécessitent un en-tête qui spécifie le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes POST, PUT et PATCH nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Création d’une tâche d’exportation

Pour exporter des données de Profil, vous devez d’abord créer un jeu de données dans lequel les données seront exportées, puis lancer une nouvelle tâche d’exportation. Ces deux étapes peuvent être effectuées à l’aide d’API Experience Platform, la première utilisant l’API Catalog Service et la seconde utilisant l’API Profil client en temps réel. Les sections qui suivent contiennent des instructions détaillées sur la façon de réaliser chaque étape.

- [Création d&#39;un jeu de données](#create-a-target-dataset) de cible - Créez un jeu de données contenant les données exportées.
- [Lancer une nouvelle tâche](#initiate-export-job) d&#39;exportation : renseignez le jeu de données avec des données de Profil XDM individuelles.

### Création d’un jeu de données de cible

Lors de l’exportation de données de Profil, un jeu de données de cible doit d’abord être créé. Il est important que le jeu de données soit correctement configuré pour garantir la réussite de l&#39;exportation.

L’une des principales considérations à prendre en compte est le schéma sur lequel repose le jeu de données (`schemaRef.id` dans l’exemple de demande d’API ci-dessous). Pour exporter un segment, le jeu de données doit être basé sur le Schéma d&#39;Union de Profil individuel XDM (`https://ns.adobe.com/xdm/context/profile__union`). Un schéma d’union est un schéma généré par le système et en lecture seule qui agrégat les champs des schémas qui partagent la même classe, dans ce cas la classe de Profil XDM Individuel. Pour plus d&#39;informations sur les schémas des vues d&#39;union, consultez la section Profil client en temps [réel du guide](../../xdm/schema/composition.md#union)de développement du registre des Schémas.

Les étapes suivantes de ce didacticiel expliquent comment créer un jeu de données qui référence le Schéma d&#39;Union d&#39;Profil individuel XDM à l&#39;aide de l&#39;API Catalog. Vous pouvez également utiliser l’interface utilisateur de l’Adobe Experience Platform pour créer un jeu de données qui référence le schéma d’union. Les étapes d’utilisation de l’interface utilisateur sont décrites dans [ce didacticiel d’interface utilisateur pour l’exportation de segments](./create-dataset-export-segment.md) , mais elles sont également applicables ici. Une fois terminé, vous pouvez revenir à ce didacticiel pour passer aux étapes permettant d’ [initier une nouvelle tâche](#initiate-export-job)d’exportation.

Si vous disposez déjà d’un jeu de données compatible et connaissez son ID, vous pouvez passer directement à l’étape [d’](#initiate-export-job)ouverture d’une nouvelle tâched’exportation.

**Format d’API**

```http
POST /dataSets
```

**Requête**

La requête suivante crée un nouveau jeu de données, fournissant des paramètres de configuration dans la charge utile.

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
        }
      }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom descriptif du jeu de données. |
| `schemaRef.id` | ID de la vue d&#39;union (schéma) à laquelle le jeu de données sera associé. |
| `fileDescription.persisted` | Valeur booléenne qui, lorsqu’elle est définie sur `true`, permet au jeu de données de persister dans la vue d’union. |

**Réponse**

Une réponse réussie renvoie un tableau contenant l&#39;identifiant unique, généré par le système et en lecture seule du jeu de données nouvellement créé. Un ID de jeu de données correctement configuré est nécessaire pour exporter avec succès les données de Profil.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Lancer la tâche d&#39;exportation

Une fois que vous disposez d’un jeu de données persistant en union, vous pouvez créer une tâche d’exportation afin de conserver les données du Profil dans le jeu de données en envoyant une requête POST au point de `/export/jobs` terminaison dans l’API Profil client en temps réel et en fournissant les détails des données que vous souhaitez exporter dans le corps de la requête.

**Format d’API**

```http
POST /export/jobs
```

**Requête**

La demande suivante crée une nouvelle tâche d’exportation, fournissant des paramètres de configuration dans la charge utile.

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
    },
    "evaluationInfo": {
        "segmentation": true
    }
  }'
```

| Propriété | Description |
| -------- | ----------- |
| `fields` | *(Facultatif)* Limite les champs de données à inclure dans l’exportation à ceux fournis dans ce paramètre. Le même paramètre est également disponible lors de la création d’un segment. Par conséquent, les champs du segment ont peut-être déjà été filtrés. Si cette valeur est omise, tous les champs seront inclus dans les données exportées. |
| `mergePolicy` | *(Facultatif)* Spécifie la stratégie de fusion pour régir les données exportées. Incluez ce paramètre lorsqu’il existe plusieurs segments exportés. Si cette valeur est omise, le service d’exportation utilisera la stratégie de fusion fournie par le segment. |
| `mergePolicy.id` | ID de la stratégie de fusion. |
| `mergePolicy.version` | Version spécifique de la stratégie de fusion à utiliser. Si vous omettez cette valeur, la version la plus récente sera utilisée par défaut. |
| `filter` | *(Facultatif)* Spécifie un ou plusieurs des filtres suivants à appliquer au segment avant l’exportation. |
| `filter.segments` | *(Facultatif)* Indique les segments à exporter. Si cette valeur est omise, toutes les données de tous les profils seront exportées. Accepte un tableau d’objets de segment, chacun contenant les champs suivants :<ul><li>`segmentId`: **(Obligatoire en cas d’utilisation`segments`)** Identifiant de segment pour les profils à exporter.</li><li>`segmentNs` *(Facultatif)* Segmenter l’espace de nommage pour le segment donné `segmentID`.</li><li>`status` *(Facultatif)* Tableau de chaînes fournissant un filtre d’état pour le `segmentID`. Par défaut, `status` aura la valeur `["realized", "existing"]` qui représente tous les profils qui tombent dans le segment à l’heure actuelle. Les valeurs possibles sont les suivantes : `"realized"`, `"existing"`et `"exited"`.</br></br>Pour plus d’informations, voir le didacticiel [sur la](./create-a-segment.md)création de segments.</li></ul> |
| `filter.segmentQualificationTime` | *(Facultatif)* Filtrer en fonction de l’heure de qualification du segment. L’heure de début et/ou l’heure de fin peuvent être fournies. |
| `filter.segmentQualificationTime.startTime` | *(Facultatif)* Heure de début de qualification des segments pour un ID de segment pour un état donné. Il n’est pas fourni, il n’y aura aucun filtre sur l’heure de début pour une qualification d’ID de segment. L&#39;horodatage doit être fourni au format [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | *(Facultatif)* Heure de fin de qualification de segment pour un ID de segment pour un état donné. Il n’est pas fourni, il n’y aura pas de filtre à l’heure de fin pour une qualification d’ID de segment. L&#39;horodatage doit être fourni au format [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp ` | *(Facultatif)* Limite les profils exportés à inclure uniquement ceux qui ont été mis à jour après cet horodatage. L&#39;horodatage doit être fourni au format [RFC 3339](https://tools.ietf.org/html/rfc3339) . <ul><li>`fromIngestTimestamp` pour **les profils**, le cas échéant : Inclut tous les profils fusionnés où l’horodatage mis à jour fusionné est supérieur à l’horodatage donné. Prend en charge `greater_than` l’opérande.</li><li>`fromTimestamp` pour **événements**: Tous les événements ingérés après cet horodatage seront exportés correspondant au résultat du profil obtenu. Ce n&#39;est pas le temps de événement lui-même, mais le temps d&#39;assimilation des événements.</li> |
| `filter.emptyProfiles` | *(Facultatif)* Valeur booléenne. Les Profils peuvent contenir des enregistrements de Profil, des enregistrements ExperienceEvent ou les deux. Les Profils sans enregistrement de Profil et seuls les enregistrements ExperienceEvent sont appelés &quot;profils vides&quot;. Pour exporter tous les profils de la banque de Profils, y compris les &quot;profils vides&quot;, définissez la valeur de `emptyProfiles` sur `true`. Si `emptyProfiles` est défini sur `false`, seuls les profils contenant des enregistrements de Profil dans la boutique sont exportés. Par défaut, si `emptyProfiles` l’attribut n’est pas inclus, seuls les profils contenant des enregistrements de Profil sont exportés. |
| `additionalFields.eventList` | *(Facultatif)* Contrôle les champs de événement de série chronologique exportés pour des objets enfants ou associés en fournissant un ou plusieurs des paramètres suivants :<ul><li>`eventList.fields`: Contrôlez les champs à exporter.</li><li>`eventList.filter`: Indique les critères qui limitent les résultats inclus dans les objets associés. Attend une valeur minimale requise pour l’exportation, généralement une date.</li><li>`eventList.filter.fromIngestTimestamp`: Filtres les événements de série chronologique à ceux qui ont été ingérés après l’horodatage fourni. Ce n&#39;est pas le temps de événement lui-même, mais le temps d&#39;assimilation des événements.</li></ul> |
| `destination` | **(Obligatoire)** Informations de destination pour les données exportées :<ul><li>`destination.datasetId`: **(Obligatoire)** ID du jeu de données dans lequel les données doivent être exportées.</li><li>`destination.segmentPerBatch`: *(Facultatif)* Valeur booléenne qui, si elle n’est pas fournie, prend par défaut la valeur `false`. Une valeur de `false` exporte tous les ID de segment dans un seul ID de lot. Une valeur de `true` exporte un ID de segment dans un ID de lot. Notez que la définition de la valeur `true` peut affecter les performances d’exportation par lot.</li></ul> |
| `schema.name` | **(Obligatoire)** Nom du schéma associé au jeu de données dans lequel les données doivent être exportées. |
| `evaluationInfo.segmentation` | *(Facultatif)* Valeur booléenne qui, si elle n’est pas fournie, prend par défaut la valeur `false`. Une valeur de `true` indique que la segmentation doit être effectuée sur la tâche d’exportation. |

>[!NOTE]
>
>Pour exporter uniquement les données de Profil et ne pas inclure les données ExperienceEvent associées, supprimez l’objet &quot;additionalFields&quot; de la requête.

**Réponse**

Une réponse réussie renvoie un jeu de données rempli avec des données de Profil comme spécifié dans la requête.

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

Si `destination.segmentPerBatch` la requête n’avait pas été incluse (si elle n’était pas présente, elle est définie par défaut `false`) ou si la valeur avait été définie sur `false`, l’objet `destination` de la réponse ci-dessus ne contiendrait pas de tableau et inclurait à la place un seul `batches` `batchId`tableau, comme illustré ci-dessous. Ce lot unique inclurait tous les ID de segment, alors que la réponse ci-dessus montre un identifiant de segment unique par ID de lot.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

## Liste de toutes les tâches d’exportation

Vous pouvez renvoyer une liste de toutes les tâches d’exportation pour une organisation IMS particulière en exécutant une demande GET au point de `export/jobs` terminaison. La demande prend également en charge les paramètres de requête `limit` et `offset`, comme indiqué ci-dessous.

**Format d’API**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Propriété | Description |
| -------- | ----------- |
| `limit` | Spécifiez le nombre d&#39;enregistrements à renvoyer. |
| `offset` | Décale la page de résultats à renvoyer par le nombre fourni. |

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

## Suivi de la progression de l&#39;exportation

Pour vue des détails d’une tâche d’exportation spécifique ou pour contrôler son état au fur et à mesure de son traitement, vous pouvez envoyer une requête GET au point de `/export/jobs` terminaison et inclure la tâche `id` d’exportation dans le chemin d’accès. La tâche d’exportation est terminée une fois que le `status` champ renvoie la valeur &quot;SUCCEEDED&quot;.

**Format d’API**

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
| `batchId` | Identifiant des lots créés à partir d&#39;une exportation réussie, à utiliser à des fins de recherche lors de la lecture des données de Profil. |

## Annuler une tâche d’exportation

L’Experience Platform vous permet d’annuler une tâche d’exportation existante, ce qui peut s’avérer utile pour plusieurs raisons, notamment si la tâche d’exportation n’a pas été terminée ou s’est retrouvée bloquée à l’étape de traitement. Pour annuler une tâche d’exportation, vous pouvez exécuter une demande de DELETE sur le point de `/export/jobs` terminaison et inclure la tâche `id` d’exportation que vous souhaitez annuler dans le chemin d’accès de la demande.

**Format d’API**

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

Une fois l’exportation terminée, vos données sont disponibles dans Data Lake en Experience Platform. Vous pouvez ensuite utiliser l’API [d’accès aux](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) données pour accéder aux données à l’aide de l’API `batchId` associée à l’exportation. En fonction de la taille de l’exportation, les données peuvent se trouver en blocs et le lot peut se composer de plusieurs fichiers.

Pour obtenir des instructions détaillées sur l’utilisation de l’API d’accès aux données pour accéder aux fichiers de commandes et les télécharger, suivez le didacticiel [Accès aux](../../data-access/tutorials/dataset-data.md)données.

Vous pouvez également accéder aux données de Profil client en temps réel exportées avec succès à l’aide d’Adobe Experience Platform Requête Service. Grâce à l’interface utilisateur ou à l’API RESTful, Requête Service vous permet d’écrire, de valider et d’exécuter des requêtes sur des données du lac Data.

Pour plus d&#39;informations sur la manière de requête des données d&#39;audience, consultez la documentation [de](../../query-service/home.md)Requête Service.