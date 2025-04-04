---
audience: user
user-guide-title: Aide d’Adobe Experience Platform Data Ingestion
breadcrumb-title: Guide d’ingestion de données
user-guide-description: Insérez vos données dans Experience Platform par ingestion en lot ou en flux continu.
feature: Data Ingestion
role: Developer
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 95%

---


# Adobe Experience Platform Data Ingestion {#ingestion}

- [Présentation de Data Ingestion](home.md)
- Ingestion par flux {#streaming}
   - [Présentation](streaming-ingestion/overview.md)
   - [Connecteur Kafka](streaming-ingestion/kafka.md)
   - [Dépannage](streaming-ingestion/troubleshooting.md)
- Ingestion par lots {#batch}
   - [Prise en main des API d’ingestion par lots](batch-ingestion/getting-started.md)
   - [Présentation de l’API](batch-ingestion/overview.md)
   - [Guide du développeur d’API](batch-ingestion/api-overview.md)
   - [Ingestion par lots partielle](batch-ingestion/partial.md)
   - [Dépannage](batch-ingestion/troubleshooting.md)
- Tutoriels {#tutorials}
   - Mapper un fichier CSV à un {#map-csv} XDM
      - [Présentation](./tutorials/map-csv/overview.md)
      - [Mapper un fichier CSV à un schéma existant](./tutorials/map-csv/existing-schema.md)
      - [Mapper un fichier CSV à l’aide de recommandations générées par l’IA](./tutorials/map-csv/recommendations.md)
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
- [Barrières de sécurité pour l’ingestion de données](guardrails.md)
- [Connecteurs source](source-connectors.md)
- [Référence de l’API d’ingestion par lots](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [Référence de l’API d’ingestion en flux continu](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Notes de mise à jour d’Experience Platform](https://experienceleague.adobe.com/fr/docs/experience-platform/release-notes/latest)
