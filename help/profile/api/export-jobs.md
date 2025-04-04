---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Point d’entrée de l’API des tâches d’exportation de profils
type: Documentation
description: Le profil client en temps réel vous permet de créer une vue unique des clients individuels dans Adobe Experience Platform en rassemblant des données provenant de plusieurs sources, y compris des données d’attributs et des données comportementales. Les données de profil peuvent ensuite être exportées vers un jeu de données pour un traitement ultérieur.
role: Developer
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 53%

---

# Point d’entrée des tâches d’exportation de profils

[!DNL Real-Time Customer Profile] vous permet de créer une vue unique des clients individuels en rassemblant des données provenant de plusieurs sources, y compris des données d’attributs et des données comportementales. Les données de profil peuvent ensuite être exportées vers un jeu de données pour un traitement ultérieur. Par exemple, les données [!DNL Profile] peuvent être exportées pour activation en créant des audiences, et les attributs de profil peuvent être exportés pour la création de rapports.

Ce document fournit des instructions détaillées sur la création et la gestion des tâches d’exportation à l’aide de l’[API Profile](https://www.adobe.com/go/profile-apis-en).

>[!NOTE]
>
>Ce guide traite de l’utilisation des tâches d’exportation dans le [!DNL Profile API]. Pour plus d’informations sur la gestion des tâches d’exportation pour Adobe Experience Platform Segmentation Service, consultez le guide sur les [ tâches d’exportation dans l’API Segmentation](../../profile/api/export-jobs.md).

Outre la création d’une tâche d’exportation, vous pouvez également accéder aux données [!DNL Profile] à l’aide du point d’entrée `/entities`, également appelé « [!DNL Profile Access] ». Pour plus d’informations, consultez le [ guide des points d’entrée des entités ](./entities.md). Pour savoir comment accéder aux données [!DNL Profile] à l’aide de l’interface utilisateur, reportez-vous au [guide d’utilisation](../ui/user-guide.md).

## Commencer

Les points d’entrée d’API utilisés dans ce guide font partie de l’API [!DNL Real-Time Customer Profile]. Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Création d’une tâche d’exportation

L’exportation de données [!DNL Profile] nécessite d’abord la création d’un jeu de données dans lequel les données seront exportées, puis le lancement d’une nouvelle tâche d’exportation. Ces deux étapes peuvent être réalisées à l’aide des API Experience Platform, la première utilisant l’API Catalog Service et la seconde utilisant l’API Real-Time Customer Profile. Les sections suivantes contiennent des instructions détaillées sur l’exécution de chaque étape.

### Créer un jeu de données cible

Lors de l’exportation de données [!DNL Profile], un jeu de données cible doit d’abord être créé. Il est important que le jeu de données soit correctement configuré pour garantir la réussite de l’exportation.

Le schéma sur lequel repose le jeu de données est l’une des principales considérations (`schemaRef.id` dans l’exemple de requête API ci-dessous). Pour exporter des données de profil, le jeu de données doit être basé sur le schéma d’union [!DNL XDM Individual Profile] (`https://ns.adobe.com/xdm/context/profile__union`). Un schéma d’union est un schéma généré par le système en lecture seule qui agrège les champs des schémas partageant la même classe. Dans ce cas, il s’agit de la classe [!DNL XDM Individual Profile]. Pour plus d’informations sur les schémas d’affichage d’union, consultez la section [ union dans les principes de base du guide de composition de schémas](../../xdm/schema/composition.md#union).

Les étapes qui suivent ce tutoriel expliquent comment créer un jeu de données qui fait référence au schéma d’union [!DNL XDM Individual Profile] à l’aide de l’API [!DNL Catalog]. Vous pouvez également utiliser l’interface utilisateur [!DNL Experience Platform] pour créer un jeu de données qui fait référence au schéma d’union. Les étapes d’utilisation de l’interface utilisateur sont décrites dans [ce tutoriel sur l’interface utilisateur pour l’exportation d’audiences](../../segmentation/tutorials/create-dataset-export-segment.md) mais sont également applicables ici. Une fois que vous avez terminé, vous pouvez revenir à ce tutoriel pour suivre les étapes de [lancement d’une nouvelle tâche d’exportation](#initiate).

Si vous disposez déjà d’un jeu de données compatible et connaissez son identifiant, vous pouvez passer directement à l’étape de [lancement d’une nouvelle tâche d’exportation](#initiate).

**Format d’API**

```http
POST /dataSets
```

**Requête**

La requête suivante crée un jeu de données et fournit des paramètres de configuration dans le payload.

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        }
      }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Un nom explicite pour le jeu de données. |
| `schemaRef.id` | L’identifiant de la vue d’union (schéma) à laquelle le jeu de données sera associé. |

**Réponse**

Une réponse réussie renvoie un tableau contenant l’ID unique, en lecture seule, généré par le système, du nouveau jeu de données créé. Un identifiant de jeu de données correctement configuré est nécessaire pour exporter des données Profile avec succès.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Lancement d’une tâche d’exportation {#initiate}

Une fois que vous disposez d’un jeu de données persistant dans l’union, vous pouvez créer une tâche d’exportation pour conserver les données de profil dans le jeu de données en envoyant une requête POST au point d’entrée `/export/jobs` de l’API Real-Time Customer Profile et en fournissant les détails des données que vous souhaitez exporter dans le corps de la requête.

**Format d’API**

```http
POST /export/jobs
```

**Requête**

La requête suivante crée une tâche d’exportation et fournit des paramètres de configuration dans le payload.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }' 
```

| Propriété | Description |
| -------- | ----------- |
| `fields` | *(Facultatif)* Limite les champs de données à inclure dans l’exportation à ceux fournis dans ce paramètre. Si vous omettez cette valeur, tous les champs seront inclus dans les données exportées. |
| `mergePolicy` | *(Facultatif)* Spécifie la politique de fusion pour régir les données exportées. Incluez ce paramètre lorsqu’il existe plusieurs audiences en cours d’exportation. |
| `mergePolicy.id` | Identifiant de la politique de fusion. |
| `mergePolicy.version` | La version spécifique de la politique de fusion à utiliser. Si vous omettez cette valeur, la version la plus récente sera utilisée par défaut. |
| `additionalFields.eventList` | *(Facultatif)* Contrôle les champs d’événement de série temporelle exportés pour les objets enfants ou associés en fournissant un ou plusieurs des paramètres suivants :<ul><li>`eventList.fields` : contrôlent les champs à exporter.</li><li>`eventList.filter` : indique les critères qui limitent les résultats inclus dans les objets associés. Attend une valeur minimale requise pour l’exportation, généralement une date.</li><li>`eventList.filter.fromIngestTimestamp` : filtre les événements de série temporelle sur ceux qui ont été ingérés après l’horodatage fourni. Il ne s’agit pas de l’heure de l’événement, mais de l’heure de l’ingestion des événements.</li></ul> |
| `destination` | **(Obligatoire)** Informations de destination pour les données exportées :<ul><li>`destination.datasetId` : **(obligatoire)** identifiant du jeu de données vers lequel les données doivent être exportées.</li><li>`destination.segmentPerBatch` : *(facultatif)* valeur booléenne qui, si elle n’est pas fournie, est définie par défaut sur `false`. Une valeur `false` exporte tous les identifiants de définition de segment dans un seul identifiant de lot. Une valeur `true` exporte un identifiant de définition de segment dans un identifiant de lot. Notez que la définition de la valeur sur `true` peut affecter les performances d’exportation par lots.</li></ul> |
| `schema.name` | **(Obligatoire)** Le nom du schéma associé au jeu de données vers lequel les données doivent être exportées. |

>[!NOTE]
>
>Pour exporter uniquement les données de profil et ne pas inclure les données de série temporelle associées, supprimez l’objet « additionalFields » de la requête.

**Réponse**

Une réponse réussie renvoie un jeu de données contenant les données Profile, comme spécifié dans la requête.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
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
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

## Liste de toutes les tâches d’exportation

Vous pouvez renvoyer une liste de toutes les tâches d’exportation pour une organisation spécifique en exécutant une requête GET sur le point d’entrée `export/jobs`. La requête prend également en charge les paramètres de requête `limit` et `offset`, comme illustré ci-dessous.

**Format d’API**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| Paramètre | Description |
| -------- | ----------- |
| `start` | Décalez la page des résultats renvoyée, selon l’heure de création de la requête. Exemple : `start=4` |
| `limit` | Limitez le nombre de résultats renvoyés. Exemple : `limit=10` |
| `page` | Renvoyez une page de résultats spécifique, selon l’heure de création de la requête. Exemple : `page=2` |
| `sort` | Triez les résultats selon un champ spécifique par ordre croissant ( **`asc`** ) ou décroissant ( **`desc`** ). Le paramètre de tri ne fonctionne pas lors du renvoi de plusieurs pages de résultats. Exemple : `sort=updateTime:asc` |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Réponse**

La réponse inclut un objet `records` contenant les tâches d’exportation créées par votre organisation.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
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
      "imsOrgId": "{ORG_ID}",
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
      "imsOrgId": "{ORG_ID}",
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

## Contrôle de la progression de l’exportation

Pour afficher les détails d’une tâche d’exportation spécifique, ou contrôler son état pendant son traitement, vous pouvez effectuer une requête GET sur le point d’entrée `/export/jobs` et inclure l’`id` de la tâche d’exportation dans le chemin d’accès. La tâche d’exportation est terminée lorsque le champ `status` renvoie la valeur &quot;SUCCEEDED&quot;.

**Format d’API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | L’`id` de la tâche d’exportation à laquelle vous souhaitez accéder. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
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
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

| Propriété | Description |
| -------- | ----------- |
| `batchId` | Identifiant des lots créés à partir d’une exportation réussie, à utiliser à des fins de recherche lors de la lecture des données Profile. |

## Annulation d’une tâche d’exportation

Experience Platform vous permet d’annuler une tâche d’exportation existante, ce qui peut s’avérer utile pour plusieurs raisons, notamment si la tâche d’exportation n’a pas été terminée ou est restée bloquée en cours de traitement. Pour annuler une tâche d’exportation, vous pouvez effectuer une requête DELETE sur le point d’entrée `/export/jobs` et inclure l’`id` de la tâche d’exportation que vous souhaitez annuler dans le chemin de la requête.

**Format d’API**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Paramètre | Description |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | L’`id` de la tâche d’exportation à laquelle vous souhaitez accéder. |

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une requête de suppression réussie renvoie un état HTTP 204 (No Content) et un corps de réponse vide, indiquant que l’opération d’annulation a réussi.

## Étapes suivantes

Une fois l’exportation terminée, vos données sont disponibles dans le lac de données d’Experience Platform. Vous pouvez ensuite utiliser l’[API Data Access](https://www.adobe.io/experience-platform-apis/references/data-access/) pour accéder aux données à l’aide du `batchId` associé à l’exportation. Selon la taille de l’exportation, les données peuvent se présenter sous forme de blocs et le lot peut être constitué de plusieurs fichiers.

Pour obtenir des instructions détaillées sur l’utilisation de l’API Data Access afin d’accéder aux fichiers de lot et les télécharger, suivez le [tutoriel portant sur l’accès aux données](../../data-access/tutorials/dataset-data.md).

Vous pouvez également accéder aux données du profil client en temps réel correctement exportées à l’aide de Adobe Experience Platform Query Service. Grâce à l’interface utilisateur ou à l’API RESTful, Query Service vous permet d’écrire, de valider et d’exécuter des requêtes sur des données du lac de données.

Pour plus d’informations sur la manière d’interroger des données d’audience, consultez la [documentation sur Query Service](../../query-service/home.md).

## Annexe

La section suivante contient des informations supplémentaires concernant les tâches d’exportation dans l’API Profile.

### Exemples de payload d’exportation supplémentaires

L’exemple d’appel API illustré dans la section [Lancement d’une tâche d’exportation](#initiate) crée une tâche contenant à la fois des données de profil (enregistrement) et d’événement (série temporelle). Cette section fournit des exemples de payload de requête supplémentaires pour limiter votre exportation à un type de données ou à l’autre.

La payload suivante crée une tâche d’exportation qui contient uniquement des données de profil (aucun événement) :

```json
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

Pour créer une tâche d’exportation contenant uniquement des données d’événement (aucun attribut de profil), la payload peut ressembler à ce qui suit :

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

### Export d’audiences

Vous pouvez également utiliser le point d’entrée des tâches d’exportation pour exporter des audiences plutôt que des données [!DNL Profile]. Pour plus d’informations, consultez le guide sur les tâches d’exportation [ dans l’API Segmentation](../../segmentation/api/export-jobs.md).
