---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mesures disponibles
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 86%

---


# Liste des mesures disponibles

The following tables list all of the metrics that are exposed by Observability Insights, broken down by [!DNL Platform] service. Chaque mesure comprend une description et un paramètre de requête d’identifiant accepté.

## [!DNL Data Ingestion]

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Data Ingestion]. Les mesures en **gras** sont des mesures d’ingestion par flux.

| Mesure d’insights  | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Nombre total de jeux de données créés. | N/A |
| timeseries.ingestion.dataset.size | Taille cumulée de toutes les données ingérées pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| timeseries.ingestion.dataset.dailysize | Taille des données ingérées quotidiennement pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| timeseries.ingestion.dataset.batchfailed.count | Nombre de lots échoués pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| timeseries.ingestion.dataset.batchsuccess.count | Nombre de lots ingérés pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| timeseries.ingestion.dataset.recordsuccess.count | Nombre d’enregistrements ingérés pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| **timeseries.data.collection.validation.total.messages.rate** | Nombre total de messages pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| **timeseries.data.collection.validation.valid.messages.rate** | Nombre total de messages valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| **timeseries.data.collection.validation.invalid.messages.rate** | Nombre total de messages non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| **timeseries.data.collection.validation.category.type.count** | Nombre total de messages « type » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| **timeseries.data.collection.validation.category.range.count** | Nombre total de messages « plage » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| **timeseries.data.collection.validation.category.format.count** | Nombre total de messages « format » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| **timeseries.data.collection.validation.category.pattern.count** | Nombre total de messages « modèle » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| **timeseries.data.collection.validation.category.presence.count** | Nombre total de messages « présence » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| **timeseries.data.collection.validation.category.enum.count** | Nombre total de messages « énumération » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| **timeseries.data.collection.validation.category.unclassified.count** | Nombre total de messages « non classé » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| **timeseries.data.collection.validation.category.unknown.count** | Nombre total de messages « inconnu » non valides pour un jeu de données ou tous les jeux de données. | Identifiant du jeu de données (facultatif) |
| **timeseries.data.collection.inlet.total.messages.received** | Nombre total de messages reçus pour un inlet de données ou tous les inlets de données. | Identifiant d’inlet (facultatif) |
| **timeseries.data.collection.inlet.total.messages.size.received** | Taille totale des données reçues pour un inlet de données ou tous les inlets de données. | Identifiant d’inlet (facultatif) |
| **timeseries.data.collection.inlet.success** | Nombre total d’appels HTTP réussis à un inlet de données ou tous les inlets de données. | Identifiant d’inlet (facultatif) |
| **timeseries.data.collection.inlet.failure** | Nombre total d’appels HTTP échoués à un inlet de données ou tous les inlets de données. | Identifiant d’inlet (facultatif) |

## [!DNL Identity Service]

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Identity Service].

| Mesure d’insights  | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Number of records written to their data source by [!DNL Identity Service], for one dataset or all datasets. | Identifiant du jeu de données (facultatif) |
| timeseries.identity.dataset.recordfailed.count | Number of records failed by [!DNL Identity Service], for one dataset or for all datasets. | Identifiant du jeu de données (facultatif) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Nombre d’enregistrements d’identité correctement ingérés pour un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Nombre d’enregistrements d’identité échoués par un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Nombre d’enregistrements d’identité ignorés par un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identités de votre organisation IMS. | N/A |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identités pour un espace de noms. | Identifiant d’espace de noms (**obligatoire**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Nombre d’identités de graphique uniques stockées dans le graphique d’identités de votre organisation IMS. | N/A |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identités de votre organisation IMS pour une force de graphique spécifique (« inconnu », « faible » ou « fort »). | Force de graphique (**obligatoire**) |

## [!DNL Privacy Service]

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Privacy Service].

| Mesure d’insights  | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Nombre total de tâches créées issues du RGPD. | ENV (**obligatoire**) |
| timeseries.gdpr.jobs.completedjobs.count | Nombre total de tâches terminées issues du RGPD. | ENV (**obligatoire**) |
| timeseries.gdpr.jobs.errorjobs.count | Nombre total de tâches d’erreur issues du RGPD. | ENV (**obligatoire**) |

## [!DNL Query Service]

Le tableau suivant décrit les mesures pour Adobe Experience Platform [!DNL Query Service].

| Mesure d’insights  | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Nombre total de requêtes planifiées non périodiques. | N/A |
| timeseries.queryservice.query.scheduledrecurring.count | Nombre total de requêtes planifiées périodiques. | N/A |
| timeseries.queryservice.query.batchquery.count | Nombre total de requêtes en lot exécutées. | N/A |
| timeseries.queryservice.query.scheduledquery.count | Nombre total de requêtes planifiées exécutées. | N/A |
| timeseries.queryservice.query.interactivequery.count | Nombre total de requêtes interactives exécutées. | N/A |
| timeseries.queryservice.query.batchfrompsqlquery.count | Nombre total de requêtes en lot exécutées à partir de PSQL. | N/A |

## [!DNL Real-time Customer Profile]

The following table outlines metrics for [!DNL Real-time Customer Profile].

| Mesure d’insights  | Description | Paramètre de requête d’identifiant |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Number of records read from the [!DNL Data Lake] by [!DNL Profile], for one dataset or for all datasets. | Identifiant du jeu de données (facultatif) |
| timeseries.profiles.dataset.recordsuccess.count | Number of records written to their data source by [!DNL Profile], for one dataset or for all datasets. | Identifiant du jeu de données (facultatif) |
| timeseries.profiles.dataset.recordfailed.count | Number of records failed by [!DNL Profile], for one dataset or for all datasets. | Identifiant du jeu de données (facultatif) |
| timeseries.profiles.dataset.batchsuccess.count | Number of [!DNL Profile] batches ingested for a dataset or for all datasets. | Identifiant du jeu de données (facultatif) |
| timeseries.profiles.dataset.batchfailed.count | Number of [!DNL Profile] batches failed for one dataset or for all datasets. | Identifiant du jeu de données (facultatif) |
| platform.ups.ingest.streaming.request.m1_rate | Taux de requêtes entrantes. | Organisation IMS |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Taux de réussite d’ingestion. | Organisation IMS |
| platform.ups.ingest.streaming.records.created.m15_rate | Taux de nouveaux enregistrements ingérés pour un jeu de données. | Identifiant du jeu de données |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Taux d’enregistrements horodatés en désordre de requête de création pour un jeu de données. | Identifiant du jeu de données |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Horodatage de la dernière requête d’enregistrement de création pour un jeu de données. | Identifiant du jeu de données |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Taux d’enregistrements horodatés en désordre de requête de mise à jour pour un jeu de données. | Identifiant du jeu de données |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Horodatage de la dernière requête d’enregistrement de mise à jour pour un jeu de données. | Identifiant du jeu de données |
| platform.ups.ingest.streaming.record.size.m1_rate | Taille moyenne des enregistrements. | Organisation IMS |
| platform.ups.ingest.streaming.records.updated.m15_rate | Taux de requêtes de mise à jour pour les enregistrements ingérés pour un jeu de données. | Identifiant du jeu de données |
