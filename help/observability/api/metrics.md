---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Point de terminaison de l’API de mesures
topic: guide du développeur
description: Découvrez comment récupérer les mesures d’observabilité dans l’Experience Platform à l’aide de l’API Observability Insights.
translation-type: tm+mt
source-git-commit: 136c75f56c2ba4d61fef7981ff8a7889a0ade3d1
workflow-type: tm+mt
source-wordcount: '2056'
ht-degree: 43%

---


# Point de terminaison des mesures

Les mesures d’observabilité fournissent des informations sur les statistiques d’utilisation, les tendances historiques et les indicateurs de performances pour diverses fonctionnalités de Adobe Experience Platform. Le point de terminaison `/metrics` dans [!DNL Observability Insights API] vous permet de récupérer par programmation les données de mesure pour l&#39;activité de votre organisation dans [!DNL Platform].

## Prise en main

Le point de terminaison API utilisé dans ce guide fait partie de l&#39;[[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API [!DNL Experience Platform].

## Récupération des mesures d’observabilité

Il existe deux méthodes prises en charge pour récupérer les données de mesure à l’aide de l’API :

* [Version 1](#v1) : Spécifiez des mesures à l’aide de paramètres de requête.
* [Version 2](#v2) : Spécifiez et appliquez des filtres aux mesures à l’aide d’une charge utile JSON.

### Version 1 {#v1}

Vous pouvez récupérer des données de mesures en faisant une demande de GET au point de terminaison `/metrics`, en spécifiant des mesures à l’aide de paramètres de requête.

**Format d’API**

Au moins une mesure doit être fournie dans le paramètre `metric`. Les autres paramètres de requête sont facultatifs pour le filtrage des résultats.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Paramètre | Description |
| --- | --- |
| `{METRIC}` | La mesure que vous souhaitez afficher. Lorsque vous combinez plusieurs mesures dans un seul appel, vous devez utiliser une esperluette (`&`) pour les séparer. Par exemple : `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | Identifiant d&#39;une ressource [!DNL Platform] particulière dont vous souhaitez exposer les mesures. Cet identifiant peut être facultatif, obligatoire ou non applicable en fonction des mesures utilisées. Consultez l&#39;[annexe](#available-metrics) pour obtenir la liste des mesures disponibles, y compris les ID pris en charge (obligatoires et facultatifs) pour chaque mesure. |
| `{DATE_RANGE}` | La période des mesures que vous souhaitez afficher, au format ISO 8601 (par exemple, `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d’objets, dont chacun contient une date et heure dans la `dateRange` fournie et les valeurs correspondantes pour les mesures spécifiées dans le chemin de requête. Si l’identifiant `id` d’une ressource de est inclus dans le chemin de requête, les résultats s’appliqueront uniquement à cette ressource particulière. [!DNL Platform] Si l’identifiant `id` est omis, les résultats s’appliqueront à toutes les ressources applicables au sein de votre organisation IMS.

```json
{
  "id": "5cf8ab4ec48aba145214abeb",
  "imsOrgId": "{IMS_ORG}",
  "timeseries": {
    "granularity": "MONTH",
    "items": [
      {
        "timestamp": "2019-06-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1125,
          "timeseries.ingestion.dataset.size": 32320
        }
      },
      {
        "timestamp": "2019-05-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1003,
          "timeseries.ingestion.dataset.size": 31409
        }
      },
      {
        "timestamp": "2019-04-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-03-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-02-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 390,
          "timeseries.ingestion.dataset.size": 16801
        }
      }
    ],
    "_page": null,
    "_links": null
  },
  "stats": {}
}
```

### Version 2 {#v2}

Vous pouvez récupérer des données de mesures en adressant une requête de POST au point de terminaison `/metrics`, en spécifiant les mesures que vous souhaitez récupérer dans la charge utile.

**Format d’API**

```http
POST /metrics
```

**Requête**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          }
        ]
      }'
```

| Propriété | Description |
| --- | --- |
| `start` | Date/heure la plus ancienne à partir de laquelle récupérer les données de mesure. |
| `end` | Date/heure la plus récente à partir de laquelle récupérer les données de mesure. |
| `granularity` | Champ facultatif qui indique l’intervalle de temps de division des données de mesure par. Par exemple, une valeur `DAY` renvoie des mesures pour chaque jour entre la date `start` et la date `end`, alors qu’une valeur `MONTH` regroupe les résultats des mesures par mois. Lors de l&#39;utilisation de ce champ, une propriété `downsample` correspondante doit également être fournie pour indiquer la fonction d&#39;agrégation par laquelle grouper les données. |
| `metrics` | Tableau d’objets, un pour chaque mesure à récupérer. |
| `name` | Nom d’une mesure reconnue par Observability Insights. Pour obtenir une liste complète des noms de mesure acceptés, consultez l&#39;[annexe](#available-metrics). |
| `filters` | Champ facultatif qui vous permet de filtrer les mesures selon des jeux de données spécifiques. Le champ est un tableau d’objets (un pour chaque filtre), avec chaque objet contenant les propriétés suivantes : <ul><li>`name`: Type d’entité par lequel filtrer les mesures. Actuellement, seul `dataSets` est pris en charge.</li><li>`value`: ID d’un ou de plusieurs jeux de données. Plusieurs ID de jeu de données peuvent être fournis sous la forme d’une seule chaîne, chaque ID étant séparé par des caractères verticaux (`|`).</li><li>`groupBy`: Lorsqu’elle est définie sur true, indique que le résultat correspondant  `value` représente plusieurs jeux de données dont les résultats de mesure doivent être renvoyés séparément. S’il est défini sur false, les résultats des mesures de ces jeux de données sont regroupés.</li></ul> |
| `aggregator` | Spécifie la fonction d&#39;agrégation qui doit être utilisée pour regrouper plusieurs enregistrements de séries chronologiques en résultats uniques. Pour obtenir des informations détaillées sur les agrégateurs disponibles, consultez la [documentation OpenTSDB](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html). |
| `downsample` | Champ facultatif qui vous permet de spécifier une fonction d’agrégation pour réduire le taux d’échantillonnage des données de mesure en triant les champs en intervalles (ou &quot;intervalles&quot;). L’intervalle de sous-échantillonnage est déterminé par la propriété `granularity`. Pour des informations détaillées sur le sous-échantillonnage, consultez la [documentation d’OpenTSDB](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html). |

{style=&quot;table-layout:auto&quot;}

**Réponse**

Une réponse réussie renvoie les points de données résultants pour les mesures et les filtres spécifiés dans la requête.

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| Propriété | Description |
| --- | --- |
| `metricResponses` | Tableau dont les objets représentent chacune des mesures spécifiées dans la requête. Chaque objet contient des informations sur la configuration du filtre et les données de mesure renvoyées. |
| `metric` | Nom de l’une des mesures fournies dans la demande. |
| `filters` | Configuration du filtre pour la mesure spécifiée. |
| `datapoints` | Tableau dont les objets représentent les résultats de la mesure et des filtres spécifiés. Le nombre d’objets dans le tableau dépend des options de filtre fournies dans la requête. Si aucun filtres n&#39;a été fourni, le tableau ne contiendra qu&#39;un seul objet qui représente tous les jeux de données. |
| `groupBy` | Si plusieurs jeux de données ont été spécifiés dans la propriété `filter` pour une mesure et que l&#39;option `groupBy` a été définie sur true dans la requête, cet objet contient l&#39;identifiant du jeu de données auquel s&#39;applique la propriété `dps` correspondante.<br><br>Si cet objet apparaît vide dans la réponse, la  `dps` propriété correspondante s&#39;applique à tous les jeux de données fournis dans le  `filters` tableau (ou à tous les jeux de données  [!DNL Platform] si aucun filtres n&#39;a été fourni). |
| `dps` | Données renvoyées pour la mesure, le filtre et la période donnés. Chaque clé de cet objet représente un horodatage avec une valeur correspondante pour la mesure spécifiée. La période entre chaque point de données dépend de la valeur `granularity` spécifiée dans la requête. |

{style=&quot;table-layout:auto&quot;}

## Annexe

La section suivante contient des informations supplémentaires sur l&#39;utilisation du point de terminaison `/metrics`.

### Mesures disponibles {#available-metrics}

Les tableaux suivants liste toutes les mesures exposées par [!DNL Observability Insights], ventilées par service [!DNL Platform]. Chaque mesure comprend une description et un paramètre de requête d’identifiant accepté.

>[!NOTE]
>
>Tous les paramètres de requête d’ID répertoriés sont facultatifs, sauf indication contraire.

#### [!DNL Data Ingestion] {#ingestion}

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Data Ingestion]. Les mesures en **gras** sont des mesures d’ingestion par flux.

| Mesure d’insights | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Nombre total de jeux de données créés. | N/A |
| timeseries.ingestion.dataset.size | Taille cumulée de toutes les données ingérées pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.ingestion.dataset.dailysize | Taille des données ingérées quotidiennement pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.ingestion.dataset.batchfailed.count | Nombre de lots échoués pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.ingestion.dataset.batchsuccess.count | Nombre de lots ingérés pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.ingestion.dataset.recordsuccess.count | Nombre d’enregistrements ingérés pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.validation.total.messages.rate** | Nombre total de messages pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.validation.valid.messages.rate** | Nombre total de messages valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.validation.invalid.messages.rate** | Nombre total de messages non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.validation.category.type.count** | Nombre total de messages « type » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.validation.category.range.count** | Nombre total de messages « plage » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.validation.category.format.count** | Nombre total de messages « format » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.validation.category.pattern.count** | Nombre total de messages « modèle » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.validation.category.presence.count** | Nombre total de messages « présence » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.validation.category.enum.count** | Nombre total de messages « énumération » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.validation.category.unclassified.count** | Nombre total de messages « non classé » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.validation.category.unknown.count** | Nombre total de messages « inconnu » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| **timeseries.data.collection.inlet.total.messages.received** | Nombre total de messages reçus pour un inlet de données ou tous les inlets de données. | ID d’entrée |
| **timeseries.data.collection.inlet.total.messages.size.received** | Taille totale des données reçues pour un inlet de données ou tous les inlets de données. | ID d’entrée |
| **timeseries.data.collection.inlet.success** | Nombre total d’appels HTTP réussis à un inlet de données ou tous les inlets de données. | ID d’entrée |
| **timeseries.data.collection.inlet.failure** | Nombre total d’appels HTTP échoués à un inlet de données ou tous les inlets de données. | ID d’entrée |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Identity Service] {#identity}

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Identity Service].

| Mesure d’insights | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Nombre d&#39;enregistrements écrits dans leur source de données par [!DNL Identity Service], pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données |
| timeseries.identity.dataset.recordfailed.count | Nombre d&#39;enregistrements ayant échoué par [!DNL Identity Service], pour un jeu de données ou pour tous les jeux de données. | Identifiant du jeu de données |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Nombre d’enregistrements d’identité correctement ingérés pour un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Nombre d’enregistrements d’identité échoués par un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Nombre d’enregistrements d’identité ignorés par un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identités de votre organisation IMS. | S/O |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identités pour un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Nombre d’identités de graphique uniques stockées dans le graphique d’identités de votre organisation IMS. | S/O |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identités de votre organisation IMS pour une force de graphique spécifique (« inconnu », « faible » ou « fort »). | Force de graphique (**obligatoire**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Privacy Service] {#privacy}

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Privacy Service].

| Mesure d’insights | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Nombre total de tâches créées issues du RGPD. | ENV (**obligatoire**) |
| timeseries.gdpr.jobs.completedjobs.count | Nombre total de tâches terminées issues du RGPD. | ENV (**obligatoire**) |
| timeseries.gdpr.jobs.errorjobs.count | Nombre total de tâches d’erreur issues du RGPD. | ENV (**obligatoire**) |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Query Service] {#query}

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Query Service].

| Mesure d’insights | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Nombre total de requêtes planifiées non périodiques. | S/O |
| timeseries.queryservice.query.scheduledrecurring.count | Nombre total de requêtes planifiées périodiques. | S/O |
| timeseries.queryservice.query.batchquery.count | Nombre total de requêtes en lot exécutées. | S/O |
| timeseries.queryservice.query.scheduledquery.count | Nombre total de requêtes planifiées exécutées. | S/O |
| timeseries.queryservice.query.interactivequery.count | Nombre total de requêtes interactives exécutées. | S/O |
| timeseries.queryservice.query.batchfrompsqlquery.count | Nombre total de requêtes en lot exécutées à partir de PSQL. | S/O |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Real-time Customer Profile] {#profile}

Le tableau suivant présente les mesures pour [!DNL Real-time Customer Profile].

| Mesure d’insights | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Nombre d&#39;enregistrements lus de [!DNL Data Lake] par [!DNL Profile], pour un jeu de données ou pour tous les jeux de données. | Identifiant du jeu de données |
| timeseries.profiles.dataset.recordsuccess.count | Nombre d&#39;enregistrements écrits dans leur source de données par [!DNL Profile], pour un jeu de données ou pour tous les jeux de données. | Identifiant du jeu de données |
| timeseries.profiles.dataset.recordfailed.count | Nombre d&#39;enregistrements ayant échoué par [!DNL Profile], pour un jeu de données ou pour tous les jeux de données. | Identifiant du jeu de données |
| timeseries.profiles.dataset.batchsuccess.count | Nombre de lots [!DNL Profile] ingérés pour un jeu de données ou pour tous les jeux de données. | Identifiant du jeu de données |
| timeseries.profiles.dataset.batchfailed.count | Nombre de lots [!DNL Profile] ayant échoué pour un jeu de données ou pour tous les jeux de données. | Identifiant du jeu de données |
| platform.ups.ingest.streaming.request.m1_rate | Taux de requêtes entrantes. | Organisation IMS (**Obligatoire**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Taux de réussite d’ingestion. | Organisation IMS (**Obligatoire**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Taux de nouveaux enregistrements ingérés pour un jeu de données. | Identifiant du jeu de données (**Obligatoire**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Taux d’enregistrements horodatés en désordre de requête de création pour un jeu de données. | Identifiant du jeu de données (**Obligatoire**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Horodatage de la dernière requête d’enregistrement de création pour un jeu de données. | Identifiant du jeu de données (**Obligatoire**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Taux d’enregistrements horodatés en désordre de requête de mise à jour pour un jeu de données. | Identifiant du jeu de données (**Obligatoire**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Horodatage de la dernière requête d’enregistrement de mise à jour pour un jeu de données. | Identifiant du jeu de données (**Obligatoire**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Taille moyenne des enregistrements. | Organisation IMS (**Obligatoire**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Taux de requêtes de mise à jour pour les enregistrements ingérés pour un jeu de données. | Identifiant du jeu de données (**Obligatoire**) |

{style=&quot;table-layout:auto&quot;}

### Messages d’erreur

Les réponses du point de terminaison `/metrics` peuvent renvoyer des messages d&#39;erreur dans certaines conditions. Ces messages d’erreur sont renvoyés au format suivant :

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{IMS_ORG}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| Propriété | Description |
| --- | --- |
| `title` | Chaîne contenant le message d’erreur et la raison potentielle pour laquelle il s’est produit. |
| `report` | Contient des informations contextuelles sur l’erreur, y compris le sandbox et l’organisation IMS utilisées dans l’opération qui l’a déclenchée. |

{style=&quot;table-layout:auto&quot;}

Le tableau suivant liste les différents codes d’erreur qui peuvent être renvoyés par l’API :

| Code erreur | Titre | Description |
| --- | --- | --- |
| `INSGHT-1000-400` | Charge utile de requête incorrecte | Un problème est survenu avec la charge utile de la demande. Assurez-vous de correspondre exactement au formatage de la charge utile tel qu’indiqué [ci-dessus](#v2). L’une des raisons possibles peut déclencher cette erreur :<ul><li>Champs obligatoires manquants, tels que `aggregator`</li><li>Mesures non valides</li><li>La demande contient un agrégateur non valide</li><li>Une date de début a lieu après une date de fin.</li></ul> |
| `INSGHT-1001-400` | Échec de la requête des mesures | Une erreur s&#39;est produite lors de la tentative de requête de la base de données des mesures, en raison d&#39;une demande incorrecte ou de l&#39;impossibilité d&#39;analyser la requête elle-même. Assurez-vous que votre requête est correctement formatée avant de réessayer. |
| `INSGHT-1001-500` | Échec de la requête des mesures | Une erreur s&#39;est produite lors de la tentative de requête de la base de données de mesures, en raison d&#39;une erreur du serveur. Réessayez la demande, et si le problème persiste, contactez l’assistance Adobe. |
| `INSGHT-1002-500` | Erreur de service | La demande n&#39;a pas pu être traitée en raison d&#39;une erreur interne. Réessayez la demande, et si le problème persiste, contactez l’assistance Adobe. |
| `INSGHT-1003-401` | Erreur de validation Sandbox | La demande n&#39;a pas pu être traitée en raison d&#39;une erreur de validation de sandbox. Assurez-vous que le nom de sandbox que vous avez indiqué dans l&#39;en-tête `x-sandbox-name` représente un sandbox valide et activé pour votre organisation IMS avant de réessayer la requête. |

{style=&quot;table-layout:auto&quot;}
