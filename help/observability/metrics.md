---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mesures disponibles
topic: developer guide
translation-type: tm+mt
source-git-commit: 947955403a270914437d9172bca458f9c49ccd8f

---


#  de mesures disponibles

Vous trouverez ci-dessous un de mesures exposées par Observability Insights, chacune avec son service de plateforme associé, sa description et son paramètre de d’ID accepté.

| Mesure d’informations | Service Plateforme | Description | Paramètre  d’ID |
| ---- | ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Ingestion des données | Nombre total de jeux de données créés. | S.O. |
| timeseries.ingestion.dataset.size | Ingestion des données | Taille cumulée de toutes les données ingérées pour un jeu de données pour ou tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.ingestion.dataset.dailysize | Ingestion des données | Taille des données ingérées quotidiennement pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.ingestion.dataset.batchfailed.count | Ingestion des données | Nombre de lots ayant échoué pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.ingestion.dataset.batchsuccess.count | Ingestion des données | Nombre de lots ingérés pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.ingestion.dataset.records.success.count | Ingestion des données | Nombre d’enregistrements ingérés pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.data.collection.validation.total.messages.rate | Ingestion des données (flux continu) | Nombre total de messages pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.data.collection.validation.valid.messages.rate | Ingestion des données (flux continu) | Nombre total de messages valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.data.collection.validation.Invalid.messages.rate | Ingestion des données (flux continu) | Nombre total de messages non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.data.collection.validation..type.count | Ingestion des données (flux continu) | Nombre total de messages &quot;type&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.data.collection.validation...range.count | Ingestion des données (flux continu) | Nombre total de messages &quot;plage&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.data.collection.validation..format.count | Ingestion des données (flux continu) | Nombre total de messages &quot;format&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.data.collection.validation..pattern.count | Ingestion des données (flux continu) | Nombre total de messages &quot;pattern&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.data.collection.validation..presence.count | Ingestion des données (flux continu) | Nombre total de messages de &quot;présence&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.data.collection.validation..enum.count | Ingestion des données (flux continu) | Nombre total de messages &quot;enum&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.data.collection.validation..unclassic.count | Ingestion des données (flux continu) | Nombre total de messages non classifiés non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.data.collection.validation..unknown.count | Ingestion des données (flux continu) | Nombre total de messages &quot;inconnus&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.data.collection.entry.total.messages.receive | Ingestion des données (flux continu) | Nombre total de messages reçus pour une entrée de données ou pour toutes les entrées de données. | ID d’entrée (facultatif) |
| timeseries.data.collection.entry.total.messages.size.receive | Ingestion des données (flux continu) | Taille totale des données reçues pour une entrée de données ou pour toutes les entrées de données. | ID d’entrée (facultatif) |
| timeseries.data.collection.entry.success | Ingestion des données (flux continu) | Nombre total d’appels HTTP réussis à une entrée de données ou à toutes les entrées de données. | ID d’entrée (facultatif) |
| timeseries.data.collection.entry.failure | Ingestion des données (flux continu) | Nombre total d’appels HTTP échoués à une entrée de données ou à toutes les entrées de données. | ID d’entrée (facultatif) |
| timeseries..dataset.records.read.count | Profil client en temps réel | Nombre d&#39;enregistrements lus à partir du lac de données par , pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries..dataset.record.success.count | Profil client en temps réel | Nombre d’enregistrements écrits dans leur source de données par , pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries..dataset.recordFailed.count | Profil client en temps réel | Nombre d’enregistrements ayant échoué par , pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries..dataset.batchsuccess.count | Profil client en temps réel | Nombre de lots  assimilés pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries..dataset.batchfailed.count | Profil client en temps réel | Nombre de lots de  ayant échoué pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.identity.dataset.records.success.count | Identity Service | Nombre d’enregistrements écrits dans leur source de données par Identity Service, pour un jeu de données ou tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.identity.dataset.recordFailed.count | Identity Service | Nombre d&#39;enregistrements ayant échoué par Identity Service, pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.identity.dataset.namespacecode.record.success.count | Identity Service | Nombre d&#39;enregistrements d&#39;identité correctement assimilés pour un  . |  ID  (**obligatoire**) |
| timeseries.identity.dataset.namespacecode.recordFailed.count | Identity Service | Nombre d&#39;enregistrements d&#39;identité ayant échoué par un  . |  ID  (**obligatoire**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Identity Service | Nombre d&#39;enregistrements d&#39;identité ignorés par un  . |  ID  (**obligatoire**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Identity Service | Nombre d&#39;identités uniques stockées dans le graphique d&#39;identité de votre organisation IMS. | S.O. |
| timeseries.identity.graph.imsorg.espacecode.uniqueidentities.count | Identity Service | Nombre d’identités uniques stockées dans le graphique d’identité pour un  . |  ID  (**obligatoire**) |
| timeseries.identity.graph.imsorg.numidgraph.count | Identity Service | Nombre d&#39;identités graphiques uniques stockées dans le graphique d&#39;identité de votre organisation IMS. | S.O. |
| timeseries.identity.graph.imsorg.graphStreng.uniqueidentities.count | Identity Service | Nombre d&#39;identités uniques stockées dans le graphique d&#39;identité de votre organisation IMS pour une force graphique particulière (&quot;inconnu&quot;, &quot;faible&quot; ou &quot;fort&quot;). | Force du graphique (**Obligatoire**) |
| timeseries.gdpr.jobs.totaljobs.count | RGPD | Nombre total d&#39;emplois créés à partir du RMPC. | ENV (**obligatoire**) |
| timeseries.gdpr.jobs.complete.jobs.count | RGPD | Nombre total d&#39;emplois terminés du RPMD. | ENV (**obligatoire**) |
| timeseries.gdpr.jobs.errorjobs.count | RGPD | Nombre total de tâches d’erreur provenant de GDPR. | ENV (**obligatoire**) |
| timeseries.queryservice..schedule.once.count | Service  | Nombre total de  planifiées non périodiques. | S.O. |
| timeseries.queryservice...schedule.dReciring.count | Service  | Nombre total de  planifiées périodiques. | S.O. |
| timeseries.queryservice..batchquery.count | Service  | Nombre total de  par lot exécutés. | S.O. |
| timeseries.queryservice..planiledquery.count | Service  | Nombre total de  planifiées exécutées. | S.O. |
| timeseries.queryservice...interactivequery.count | Service  | Nombre total de  interactives exécutées. | S.O. |
| timeseries.queryservice..batchfrompsqlquery.count | Service  | Nombre total de  par lot exécutés à partir de PSQL. | S.O. |