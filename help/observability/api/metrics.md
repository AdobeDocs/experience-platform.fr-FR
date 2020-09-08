---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mesures disponibles
topic: developer guide
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 77%

---


# Point de terminaison des mesures

Les mesures d’observabilité fournissent des informations sur les statistiques d’utilisation, les tendances historiques et les indicateurs de performances pour diverses fonctionnalités de Adobe Experience Platform. Le `/metrics` point de terminaison de la [!DNL Observability Insights API] permet de récupérer par programmation les données de mesure pour l’activité de votre entreprise dans [!DNL Platform].

## Prise en main

The API endpoint used in this guide is part of the [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Avant de continuer, consultez le guide [de](./getting-started.md) prise en main pour obtenir des liens vers la documentation connexe, un guide pour lire les exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute [!DNL Experience Platform] API.

## Récupération des mesures d’observabilité

Vous pouvez récupérer des mesures d’observabilité en effectuant une requête GET sur le point de terminaison `/metrics` dans l’API [!DNL Observability Insights]

**Format d’API**

Lors de l’utilisation du point de terminaison `/metrics`, au moins un paramètre de requête de mesure doit être fourni. Les autres paramètres de requête sont facultatifs pour le filtrage des résultats.

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
| `{ID}` | The identifier for a particular [!DNL Platform] resource whose metrics you want to expose. Cet identifiant peut être facultatif, obligatoire ou non applicable en fonction des mesures utilisées. Consultez l’ [annexe](#available-metrics) pour obtenir une liste des mesures disponibles, ainsi que les ID pris en charge (obligatoires et facultatifs) pour chaque mesure. |
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

## Annexe

La section suivante contient des informations supplémentaires sur l’utilisation du `/metrics` point de terminaison.

### Mesures disponibles {#available-metrics}

The following tables list all of the metrics that are exposed by [!DNL Observability Insights], broken down by [!DNL Platform] service. Chaque mesure comprend une description et un paramètre de requête d’identifiant accepté.

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

#### [!DNL Identity Service] {#identity}

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Identity Service].

| Mesure d’insights | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Number of records written to their data source by [!DNL Identity Service], for one dataset or all datasets. | Identifiant du jeu de données |
| timeseries.identity.dataset.recordfailed.count | Number of records failed by [!DNL Identity Service], for one dataset or for all datasets. | Identifiant du jeu de données |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Nombre d’enregistrements d’identité correctement ingérés pour un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Nombre d’enregistrements d’identité échoués par un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Nombre d’enregistrements d’identité ignorés par un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identités de votre organisation IMS. | N/A |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identités pour un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Nombre d’identités de graphique uniques stockées dans le graphique d’identités de votre organisation IMS. | N/A |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identités de votre organisation IMS pour une force de graphique spécifique (« inconnu », « faible » ou « fort »). | Force de graphique (**obligatoire**) |

#### [!DNL Privacy Service] {#privacy}

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Privacy Service].

| Mesure d’insights | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Nombre total de tâches créées issues du RGPD. | ENV (**obligatoire**) |
| timeseries.gdpr.jobs.completedjobs.count | Nombre total de tâches terminées issues du RGPD. | ENV (**obligatoire**) |
| timeseries.gdpr.jobs.errorjobs.count | Nombre total de tâches d’erreur issues du RGPD. | ENV (**obligatoire**) |

#### [!DNL Query Service] {#query}

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Query Service].

| Mesure d’insights | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Nombre total de requêtes planifiées non périodiques. | N/A |
| timeseries.queryservice.query.scheduledrecurring.count | Nombre total de requêtes planifiées périodiques. | N/A |
| timeseries.queryservice.query.batchquery.count | Nombre total de requêtes en lot exécutées. | N/A |
| timeseries.queryservice.query.scheduledquery.count | Nombre total de requêtes planifiées exécutées. | N/A |
| timeseries.queryservice.query.interactivequery.count | Nombre total de requêtes interactives exécutées. | N/A |
| timeseries.queryservice.query.batchfrompsqlquery.count | Nombre total de requêtes en lot exécutées à partir de PSQL. | N/A |

#### [!DNL Real-time Customer Profile] {#profile}

The following table outlines metrics for [!DNL Real-time Customer Profile].

| Mesure d’insights | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Number of records read from the [!DNL Data Lake] by [!DNL Profile], for one dataset or for all datasets. | Identifiant du jeu de données |
| timeseries.profiles.dataset.recordsuccess.count | Number of records written to their data source by [!DNL Profile], for one dataset or for all datasets. | Identifiant du jeu de données |
| timeseries.profiles.dataset.recordfailed.count | Number of records failed by [!DNL Profile], for one dataset or for all datasets. | Identifiant du jeu de données |
| timeseries.profiles.dataset.batchsuccess.count | Number of [!DNL Profile] batches ingested for a dataset or for all datasets. | Identifiant du jeu de données |
| timeseries.profiles.dataset.batchfailed.count | Number of [!DNL Profile] batches failed for one dataset or for all datasets. | Identifiant du jeu de données |
| platform.ups.ingest.streaming.request.m1_rate | Taux de requêtes entrantes. | Organisation IMS (**Obligatoire**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Taux de réussite d’ingestion. | Organisation IMS (**Obligatoire**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Taux de nouveaux enregistrements ingérés pour un jeu de données. | Identifiant du jeu de données (**Obligatoire**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Taux d’enregistrements horodatés en désordre de requête de création pour un jeu de données. | Identifiant du jeu de données (**Obligatoire**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Horodatage de la dernière requête d’enregistrement de création pour un jeu de données. | Identifiant du jeu de données (**Obligatoire**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Taux d’enregistrements horodatés en désordre de requête de mise à jour pour un jeu de données. | Identifiant du jeu de données (**Obligatoire**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Horodatage de la dernière requête d’enregistrement de mise à jour pour un jeu de données. | Identifiant du jeu de données (**Obligatoire**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Taille moyenne des enregistrements. | Organisation IMS (**Obligatoire**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Taux de requêtes de mise à jour pour les enregistrements ingérés pour un jeu de données. | Identifiant du jeu de données (**Obligatoire**) |