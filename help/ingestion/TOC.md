---
product: experience-platform
audience: user
user-guide-title: Aide d’Adobe Experience Platform Data Ingestion
breadcrumb-title: Data Ingestion Guide
user-guide-description: Adobe Experience Platform brings data from multiple sources together in order to help marketers better understand the behavior of their customers. Adobe Experience Platform Data Ingestion represents the multiple methods by which Platform ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream Platform services.
translation-type: tm+mt
source-git-commit: 2a5d6a9462950007d00f321ca9f3a3c457a3243e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 94%

---


# Adobe Experience Platform Data Ingestion {#ingestion}

- [Présentation de Data Ingestion](home.md)
- Ingestion par flux {#streaming}
   - [Présentation](streaming-ingestion/overview.md)
   - [Connecteur Kafka](streaming-ingestion/kafka.md)
   - [Dépannage](streaming-ingestion/troubleshooting.md)
- Ingestion par lots {#batch}
   - [Présentation](batch-ingestion/overview.md)
   - [API d’ingestion par lots](batch-ingestion/api-overview.md)
   - [Ingestion par lots partielle](batch-ingestion/partial.md)
   - [Dépannage](batch-ingestion/troubleshooting.md)
- Tutoriels {#tutorials}
   - [Mappage d’un fichier CSV à XDM](tutorials/map-a-csv-file.md)
   - [Ingestion de données par lots à l’aide de l’interface utilisateur](tutorials/ingest-batch-data.md)
   - [Création d’une connexion en continu authentifiée](tutorials/create-authenticated-streaming-connection.md)
   - [Création d’une connexion en continu (API)](tutorials/create-streaming-connection.md)
   - [Création d’une connexion en continu (IU)](tutorials/create-streaming-connection-ui.md)
   - [Diffusion en continu des données d’enregistrement](tutorials/streaming-record-data.md)
   - [Diffusion en continu des données de séries temporelles](tutorials/streaming-time-series-data.md)
   - [Diffusion en continu de plusieurs messages](tutorials/streaming-multiple-messages.md)
- Qualité et contrôle de l’ingestion des données {#quality}
   - [Présentation](quality/overview.md)
   - [Contrôle des flux de données](quality/monitor-data-flows.md)
   - [Récupérer les diagnostics d&#39;erreur](quality/error-diagnostics.md)
   - [Récupération des lots rejetés](quality/retrieve-failed-batches.md)
   - [Validation de l’ingestion par flux](quality/streaming-validation.md)
   - [Abonnement aux événements d’ingestion de données](quality/subscribe-events.md)
- [Connecteurs source](source-connectors.md)
- [Référence d’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [Notes de mise à jour de la plateforme](https://docs.adobe.com/content/help/fr-FR/experience-platform/release-notes/latest.html)