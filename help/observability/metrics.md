---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mesures disponibles
topic: developer guide
translation-type: tm+mt
source-git-commit: ff299a69a81f00cad3e90a83f7411e4b15d4f850
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 3%

---


# Liste des mesures disponibles

Les tableaux suivants liste toutes les mesures exposées par Observability Insights, ventilées par service de plateforme. Chaque mesure comprend une description et un paramètre de requête d’ID accepté.

## Incorporation de données

Le tableau suivant présente les mesures pour l’importation des données de la plate-forme Adobe Experience. Les mesures en **gras** sont les mesures d’assimilation en flux continu.

| Mesure Statistiques  | Description | Paramètre de requête d’ID |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Nombre total de jeux de données créés. | S.O. |
| timeseries.ingestion.dataset.size | Taille cumulée de toutes les données ingérées pour un jeu de données pour ou tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.ingestion.dataset.dailysize | Taille des données ingérées quotidiennement pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.ingestion.dataset.batchfailed.count | Nombre de lots ayant échoué pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.ingestion.dataset.batchsuccess.count | Nombre de lots ingérés pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.ingestion.dataset.recordsuccess.count | Nombre d&#39;enregistrements ingérés pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.total.messages.rate** | Nombre total de messages pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.valid.messages.rate** | Nombre total de messages valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.Invalid.messages.rate** | Nombre total de messages non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.catégorie.type.count** | Nombre total de messages &quot;type&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.catégorie.range.count** | Nombre total de messages &quot;plage&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.catégorie.format.count** | Nombre total de messages &quot;format&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.catégorie.pattern.count** | Nombre total de messages &quot;pattern&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.catégorie.presence.count** | Nombre total de messages de &quot;présence&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.catégorie.enum.count** | Nombre total de messages &quot;enum&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.catégorie.unclassifié.count** | Nombre total de messages non classifiés non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.validation.catégorie.unknown.count** | Nombre total de messages &quot;inconnus&quot; non valides pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| **timeseries.data.collection.inlet.total.messages.receive** | Nombre total de messages reçus pour une entrée de données ou pour toutes les entrées de données. | ID d’entrée (facultatif) |
| **timeseries.data.collection.inlet.total.messages.size.receive** | Taille totale des données reçues pour une entrée de données ou pour toutes les entrées de données. | ID d’entrée (facultatif) |
| **timeseries.data.collection.inlet.success** | Nombre total d&#39;appels HTTP réussis à une entrée de données ou à toutes les entrées de données. | ID d’entrée (facultatif) |
| **timeseries.data.collection.inlet.failure** | Nombre total d&#39;appels HTTP ayant échoué à une entrée de données ou à toutes les entrées de données. | ID d’entrée (facultatif) |

## Identity Service

Le tableau suivant présente les mesures pour Adobe Experience Platform Identity Service.

| Mesure Statistiques  | Description | Paramètre de requête d’ID |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Nombre d&#39;enregistrements écrits dans leur source de données par Identity Service, pour un jeu de données ou tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.identity.dataset.recordfailed.count | Nombre d&#39;enregistrements ayant échoué par Identity Service, pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Nombre d&#39;enregistrements d&#39;identité correctement assimilés pour un espace de nommage. | ID d’Espace de nommage (**obligatoire**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Nombre d&#39;enregistrements d&#39;identité ayant échoué par un espace de nommage. | ID d’Espace de nommage (**obligatoire**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Nombre d&#39;enregistrements d&#39;identité ignorés par un espace de nommage. | ID d’Espace de nommage (**obligatoire**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Nombre d&#39;identités uniques stockées sur le graphique d&#39;identité de votre organisation IMS. | S.O. |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Nombre d&#39;identités uniques stockées dans le graphique d&#39;identité d&#39;un espace de nommage. | ID d’Espace de nommage (**obligatoire**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Nombre d&#39;identités graphiques uniques stockées dans le graphique d&#39;identité de votre organisation IMS. | S.O. |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Nombre d&#39;identités uniques stockées sur le graphique d&#39;identité de votre organisation IMS pour une force graphique particulière (&quot;inconnu&quot;, &quot;faible&quot; ou &quot;fort&quot;). | Force du graphique (**Obligatoire**) |

## Service confidentialité

Le tableau suivant présente les mesures pour Adobe Experience Platform Privacy Service.

| Mesure Statistiques  | Description | Paramètre de requête d’ID |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Nombre total d&#39;emplois créés à partir du RGMD. | ENV (**obligatoire**) |
| timeseries.gdpr.jobs.completedjobs.count | Nombre total d&#39;emplois terminés du RGMD. | ENV (**obligatoire**) |
| timeseries.gdpr.jobs.errorjobs.count | Nombre total de tâches d’erreur provenant de GDPR. | ENV (**obligatoire**) |

## Requête Service

Le tableau suivant présente les mesures pour Adobe Experience Platform Requête Service.

| Mesure Statistiques  | Description | Paramètre de requête d’ID |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Nombre total de requêtes planifiées non périodiques. | S.O. |
| timeseries.queryservice.query.scheduledrecurring.count | Nombre total de requêtes planifiées récurrentes. | S.O. |
| timeseries.queryservice.query.batchquery.count | Nombre total de requêtes par lot exécutées. | S.O. |
| timeseries.queryservice.query.scheduledquery.count | Nombre total de requêtes planifiées exécutées. | S.O. |
| timeseries.queryservice.query.interactivequery.count | Nombre total de requêtes interactives exécutées. | S.O. |
| timeseries.queryservice.query.batchfrompsqlquery.count | Nombre total de requêtes par lot exécutées à partir de PSQL. | S.O. |

## Profil client en temps réel

Le tableau suivant présente les mesures du Profil client en temps réel.

| Mesure Statistiques  | Description | Paramètre de requête d’ID |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Nombre d&#39;enregistrements lus à partir du lac de données par Profil, pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.profiles.dataset.recordsuccess.count | Nombre d’enregistrements écrits dans leur source de données par Profil, pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.profiles.dataset.recordfailed.count | Nombre d&#39;enregistrements ayant échoué par Profil, pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.profiles.dataset.batchsuccess.count | Nombre de lots de Profils ingérés pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| timeseries.profiles.dataset.batchfailed.count | Nombre de lots de Profils ayant échoué pour un jeu de données ou pour tous les jeux de données. | ID du jeu de données (facultatif) |
| platform.ups.ingest.streaming.request.m1_rate | Taux de demande entrant. | Entreprise IMS |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Taux de réussite des embouteillages. | Entreprise IMS |
| platform.ups.ingest.streaming.records.created.m15_rate | Taux de nouveaux enregistrements ingérés pour un jeu de données. | ID de jeu de données |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Taux d’enregistrements horodatés hors commande pour créer une demande de jeu de données. | ID de jeu de données |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Horodatage de la dernière demande d&#39;enregistrement de création d&#39;un jeu de données. | ID de jeu de données |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Taux d’enregistrements horodatés hors commande pour la demande de mise à jour d’un jeu de données. | ID de jeu de données |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Horodatage de la dernière demande d’enregistrement de mise à jour pour un jeu de données. | ID de jeu de données |
| platform.ups.ingest.streaming.record.size.m1_rate | Taille moyenne des enregistrements. | Entreprise IMS |
| platform.ups.ingest.streaming.records.updated.m15_rate | Taux de demandes de mise à jour pour les enregistrements ingérés pour un jeu de données. | ID de jeu de données |
