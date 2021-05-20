---
audience: user
user-guide-title: Aide d’Adobe Experience Platform Data Ingestion
breadcrumb-title: Guide d’ingestion de données
user-guide-description: Introduisez vos données dans Platform par lot ou en ingestion continue.
feature: Data Ingestion
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 100%

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
   - [Créer une connexion en continu authentifiée](tutorials/create-authenticated-streaming-connection.md)
   - [Création d’une connexion en continu (API)](tutorials/create-streaming-connection.md)
   - [Création d’une connexion en continu (IU)](tutorials/create-streaming-connection-ui.md)
   - [Diffusion en continu des données d’enregistrement](tutorials/streaming-record-data.md)
   - [Diffusion par flux de données de série temporelle](tutorials/streaming-time-series-data.md)
   - [Diffusion en continu de plusieurs messages](tutorials/streaming-multiple-messages.md)
- Qualité et surveillance des données {#quality}
   - [Présentation](quality/overview.md)
   - [Surveillance de l’ingestion des données](quality/monitor-data-ingestion.md)
   - [Récupération des diagnostics d’erreur](quality/error-diagnostics.md)
   - [Récupération des lots en échec](quality/retrieve-failed-batches.md)
   - [Validation de l’ingestion par flux](quality/streaming-validation.md)
   - [Notifications d’ingestion de données](quality/subscribe-events.md)
- [Connecteurs source](source-connectors.md)
- [Référence d’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [Notes de mise à jour de Platform](https://docs.adobe.com/content/help/fr-FR/experience-platform/release-notes/latest.html)