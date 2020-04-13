---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mesures disponibles
topic: developer guide
translation-type: tm+mt
source-git-commit: ff299a69a81f00cad3e90a83f7411e4b15d4f850

---


#  de mesures disponibles

Les tableaux suivants  toutes les mesures exposées par Observability Insights, ventilées par service de plateforme. Chaque mesure comprend une description et un paramètre de d’ID accepté.

## Ingestion des données

Le tableau suivant décrit les mesures pour l’administration des données d’Adobe Experience Platform. Les mesures en **gras** sont les mesures d’assimilation en flux continu.

| Mesure d’informations | Description | Paramètre  d’ID |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Nombre total de jeux de données créés. | S.O. |
| timeseries.ingestion.dataset.size | Taille cumulée de toutes les données ingérées pour un jeu de données pour ou tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.ingestion.dataset.dailysize | Taille des données ingérées quotidiennement pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.ingestion.dataset.batchfailed.count | Nombre de lots ayant échoué pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.ingestion.dataset.batchsuccess.count | Nombre de lots ingérés pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.ingestion.dataset.recordsuccess.count | Nombre d’enregistrements ingérés pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.total.messages.rate** | Nombre total de messages pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.valid.messages.rate** | Nombre total de messages valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.Invalid.messages.rate** | Nombre total de messages non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation..type.count** | Nombre total de messages &quot;type&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation...range.count** | Nombre total de messages &quot;plage&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation..format.count** | Nombre total de messages &quot;format&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation..pattern.count** | Nombre total de messages &quot;pattern&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation..presence.count** | Nombre total de messages de &quot;présence&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation..enum.count** | Nombre total de messages &quot;enum&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation..unclassic.count** | Nombre total de messages non classifiés non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation..unknown.count** | Nombre total de messages &quot;inconnus&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.entry.total.messages.receive** | Nombre total de messages reçus pour une entrée de données ou pour toutes les entrées de données. | ID d’entrée (facultatif) |
| **timeseries.data.collection.entry.total.messages.size.receive** | Taille totale des données reçues pour une entrée de données ou pour toutes les entrées de données. | ID d’entrée (facultatif) |
| **timeseries.data.collection.entry.success** | Nombre total d’appels HTTP réussis à une entrée de données ou à toutes les entrées de données. | ID d’entrée (facultatif) |
| **timeseries.data.collection.entry.failure** | Nombre total d’appels HTTP échoués à une entrée de données ou à toutes les entrées de données. | ID d’entrée (facultatif) |

## Identity Service

Le tableau suivant décrit les mesures pour le service d’identité d’Adobe Experience Platform.

| Mesure d’informations | Description | Paramètre  d’ID |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Nombre d’enregistrements écrits dans leur source de données par Identity Service, pour un jeu de données ou tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.identity.dataset.recordfailed.count | Nombre d&#39;enregistrements ayant échoué par Identity Service, pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Nombre d&#39;enregistrements d&#39;identité correctement assimilés pour un  . |  ID  (**obligatoire**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Nombre d&#39;enregistrements d&#39;identité ayant échoué par un  . |  ID  (**obligatoire**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Nombre d&#39;enregistrements d&#39;identité ignorés par un  . |  ID  (**obligatoire**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Nombre d&#39;identités uniques stockées dans le graphique d&#39;identité de votre organisation IMS. | S.O. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Nombre d’identités uniques stockées dans le graphique d’identité pour un  . |  ID  (**obligatoire**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Nombre d&#39;identités graphiques uniques stockées dans le graphique d&#39;identité de votre organisation IMS. | S.O. |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Nombre d&#39;identités uniques stockées dans le graphique d&#39;identité de votre organisation IMS pour une force graphique particulière (&quot;inconnu&quot;, &quot;faible&quot; ou &quot;fort&quot;). | Force du graphique (**Obligatoire**) |

## Service confidentialité

Le tableau suivant décrit les mesures pour le service de confidentialité d’Adobe Experience Platform.

| Mesure d’informations | Description | Paramètre  d’ID |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Nombre total d&#39;emplois créés à partir du RMPC. | ENV (**obligatoire**) |
| timeseries.gdpr.jobs.completedjobs.count | Nombre total d&#39;emplois terminés du RPMD. | ENV (**obligatoire**) |
| timeseries.gdpr.jobs.errorjobs.count | Nombre total de tâches d’erreur provenant de GDPR. | ENV (**obligatoire**) |

## Service 

Le tableau ci-dessous décrit les mesures pour le service  de la plateforme Adobe Experience Platform.

| Mesure d’informations | Description | Paramètre  d’ID |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Nombre total de  planifiées non périodiques. | S.O. |
| timeseries.queryservice.query.scheduledrecurring.count | Nombre total de  planifiées périodiques. | S.O. |
| timeseries.queryservice.query.batchquery.count | Nombre total de  par lot exécutés. | S.O. |
| timeseries.queryservice.query.scheduledquery.count | Nombre total de  planifiées exécutées. | S.O. |
| timeseries.queryservice.query.interactivequery.count | Nombre total de  interactives exécutées. | S.O. |
| timeseries.queryservice.query.batchfrompsqlquery.count | Nombre total de  par lot exécutés à partir de PSQL. | S.O. |

## Profil client en temps réel

Le tableau suivant décrit les mesures pour les  de clients en temps réel.

| Mesure d’informations | Description | Paramètre  d’ID |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Nombre d&#39;enregistrements lus à partir du lac de données par , pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.profiles.dataset.recordsuccess.count | Nombre d’enregistrements écrits dans leur source de données par , pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.profiles.dataset.recordfailed.count | Nombre d’enregistrements ayant échoué par , pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.profiles.dataset.batchsuccess.count | Nombre de lots  assimilés pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.profiles.dataset.batchfailed.count | Nombre de lots de  ayant échoué pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| platform.ups.ingest.streaming.request.m1_rate | Taux de requêtes entrantes. | Organisation IMS |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Taux de réussite de l&#39;assimilation. | Organisation IMS |
| platform.ups.ingest.streaming.records.created.m15_rate | Taux de nouveaux enregistrements assimilés pour un jeu de données. | ID du jeu de données |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Taux d’enregistrements horodatés hors commande pour créer une requête pour un jeu de données. | ID du jeu de données |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Horodatage de la dernière demande d’enregistrement de création d’un jeu de données. | ID du jeu de données |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Taux d’enregistrements horodatés hors commande pour la demande de mise à jour d’un jeu de données. | ID du jeu de données |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Horodatage de la dernière demande d’enregistrement de mise à jour pour un jeu de données. | ID du jeu de données |
| platform.ups.ingest.streaming.record.size.m1_rate | Taille moyenne des enregistrements. | Organisation IMS |
| platform.ups.ingest.streaming.records.updated.m15_rate | Taux de demandes de mise à jour pour les enregistrements assimilés pour un jeu de données. | ID du jeu de données |
