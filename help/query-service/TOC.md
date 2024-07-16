---
audience: user
user-guide-title: Aide d’Adobe Experience Platform Query Service
breadcrumb-title: Guide de Query Service
user-guide-description: Utilisez le langage SQL standard pour interroger les données du lac de données dans Experience Platform.
feature: Queries
role: User,Developer
source-git-commit: bb95e0aa8ee92aee5a2f126d85e78308e652a061
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 83%

---


# Adobe Experience Platform Query Service {#query}

- [Présentation de Query Service](home.md)
- [Package Query Service](packaging.md)
- [Mécanismes de sécurisation de Query Service](guardrails.md)
- Prise en main {#get-started}
   - [Conditions préalables](get-started/prerequisites.md)
- Data Distiller {#data-distiller}
   - [Aperçu](data-distiller/overview.md)
   - [Utilisation des licences](data-distiller/license-usage.md)
   - Jeux de données dérivés {#derived-datasets}
      - [Vue d’ensemble](data-distiller/derived-datasets/overview.md)
      - [Création de jeux de données dérivés avec SQL](data-distiller/derived-datasets/create-derived-datasets-with-sql.md)
      - [Création de jeux de données dérivés basés sur des déciles](data-distiller/derived-datasets/decile-based-derived-attributes.md)
   - Informations personnalisables pour la création de rapports d’application étendue {#customizable-insights}
      - [Vue d’ensemble](data-distiller/customizable-insights/overview.md)
      - [Mode de requête pro](data-distiller/customizable-insights/query-pro-mode.md)
      - [Envoi de requêtes accélérées](data-distiller/customizable-insights/send-accelerated-queries.md)
      - [Guide sur le modèle de données d’insights de rapports](data-distiller/customizable-insights/reporting-insights-data-model.md)
   - Pipelines de fonctionnalités AI/ML {#ml-feature-pipelines}
      - [Vue d’ensemble](data-distiller/ml-feature-pipelines/overview.md)
      - [Connexion aux notebooks Jupyter](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [Analyse exploratoire des données](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [Fonctionnalités de conception pour ML](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [Exportation des données dans des environnements ML](data-distiller/ml-feature-pipelines/export-data.md)
      - [Workflow d’enrichissement de pipeline de données AI/ML de bout en bout](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- Cas d’utilisation {#use-cases}
   - [Vue d’ensemble](use-cases/overview.md)
   - [Navigation abandonnée](use-cases/abandoned-browse.md)
   - [Analyse de l’attribution](use-cases/attribution-analysis.md)
   - [Filtrage des robots](use-cases/bot-filtering.md)
   - [Créer un rapport de tendance d’événements](use-cases/trended-report-of-events.md)
   - [Analyse du consentement](use-cases/consent-analysis.md)
   - [Valeur durée de vie client](use-cases/customer-lifetime-value.md)
   - [Jeux de données dérivés basés sur le décile](use-cases/deciles-use-case.md)
   - [Correspondance approximative](use-cases/fuzzy-match.md)
   - [Répertorier les pages vues d’un utilisateur ou d’une utilisatrice](use-cases/list-visitor-sessions.md)
   - [Répertorier les visiteurs et visiteuses selon leurs vues de page](use-cases/visitors-by-number-of-page-views.md)
   - [Score de propension](use-cases/propensity-score.md)
   - [Récupération d’enregistrements similaires avec des fonctions d’ordre supérieur](use-cases/retrieve-similar-records.md)
   - [Renvoyer et utiliser des variables de marchandisage à partir de données d’analyse](use-cases/merchandising-variables.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Afficher le rapport de cumul pour un visiteur ou une visiteuse](use-cases/roll-up-report-of-a-visitor.md)
   - [Informations sur les analyses web et mobiles](use-cases/analytics-insights.md)
- Principaux concepts {#key-concepts}
   - [Utilisation de structures de données imbriquées](key-concepts/nested-data-structures.md)
   - [Aplatir les structures de données imbriquées](key-concepts/flatten-nested-data.md)
   - [Bloc anonyme](key-concepts/anonymous-block.md)
   - [Modèle intégré](key-concepts/inline-templates.md)
   - [Chargement incrémentiel](key-concepts/incremental-load.md)
   - [Dédoublonnage des données](key-concepts/deduplication.md)
   - [Échantillon de jeux de données](key-concepts/dataset-samples.md)
   - [Calcul des statistiques des jeux de données](key-concepts/dataset-statistics.md)
- Connexion des clients à Query Service {#clients}
   - [Présentation de la connexion des clients](clients/overview.md)
   - [Modes SSL](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Notebook Jupyter](clients//jupyter-notebook.md)
   - [Looker](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- UI Query Service {#ui}
   - [Présentation de l’interface utilisateur](ui/overview.md)
   - [Guide d’utilisation de Query Editor](ui/user-guide.md)
   - [Modèles de requête](ui/query-templates.md)
   - [Requêtes paramétrées](ui/parameterized-queries.md)
   - [Plannings de requête](ui/query-schedules.md)
   - [Journaux de requête](ui/query-logs.md)
   - [Surveiller les requêtes planifiées](ui/monitor-queries.md)
   - [Guide sur les informations d’identification](ui/credentials.md)
   - [Générer des jeux de données de sortie à partir des résultats de requête](ui/create-datasets.md)
- Points d’entrée de l’API Query Service {#api}
   - [Prise en main](api/getting-started.md)
   - [Requêtes](api/queries.md)
   - [Paramètres de connexion](api/connection-parameters.md)
   - [Plannings](api/scheduled-queries.md)
   - [Exécutions pour les requêtes planifiées](api/runs-scheduled-queries.md)
   - [Modèles de requête](api/query-templates.md)
   - [Requêtes accélérées](api/accelerated-queries.md)
   - [Abonnements aux alertes](api/alert-subscriptions.md)
- Gouvernance des données {#data-governance}
   - [Aperçu](data-governance/overview.md)
   - [Guide du journal d’audit](data-governance/audit-log-guide.md)
   - [Identités dans les jeux de données à schéma ad hoc](data-governance/ad-hoc-schema-identities.md)
   - [Prise en charge du contrôle d’accès basé sur les attributs pour les schémas ad hoc](./data-governance/ad-hoc-schema-labels.md)
- Bonnes pratiques {#best-practices}
   - [Exécution de la requête](best-practices/writing-queries.md)
   - [Organisation des ressources de données](./best-practices/organize-data-assets.md)
- Référence SQL {#sql}
   - [Présentation de SQL](sql/overview.md)
   - [Syntaxe SQL](sql/syntax.md)
   - [Fonctions définies par Adobe](sql/adobe-defined-functions.md)
   - [Fonctions d’ordre supérieur](sql/higher-order-functions.md)
   - [Fonctions Spark SQL](sql/spark-sql-functions.md)
   - [Commandes de métadonnées](sql/metadata.md)
   - [Instructions préparées](sql/prepared-statements.md)
- [Questions fréquentes](troubleshooting-guide.md)
- [Liste autorisée d’adresses IP](ip-address-allowlist.md)
- [Référence d’API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Notes de mise à jour de Platform](https://experienceleague.adobe.com/fr/docs/experience-platform/release-notes/latest)
