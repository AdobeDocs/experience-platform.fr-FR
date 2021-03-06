---
audience: user
user-guide-title: Aide d’Adobe Experience Platform Query Service
breadcrumb-title: Guide de Query Service
user-guide-description: Utilisez SQL standard pour créer des requêtes de données dans le lac de données de Platform.
feature: Queries
source-git-commit: d955473fb9123a6fc2384cde4073c713b921f582
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 73%

---


# Adobe Experience Platform Query Service {#query}

- [Présentation de Query Service](home.md)
- Prise en main {#get-started}
   - [Conditions préalables](get-started/prerequisites.md)
- Cas pratiques {#use-cases}
   - [Navigation abandonnée](use-cases/abandoned-browse.md)
   - [Analyse des activités avec Adobe Target](use-cases/activity-analysis-with-adobe-target.md)
   - [Analyse de l’attribution](use-cases/attribution-analysis.md)
   - [Filtrage des robots](use-cases/bot-filtering.md)
   - [Informations sur les analyses web et mobiles](use-cases/analytics-insights.md)
- API Query Service {#api}
   - [Prise en main](api/getting-started.md)
   - [Requêtes](api/queries.md)
   - [Paramètres de connexion](api/connection-parameters.md)
   - [Requêtes planifiées](api/scheduled-queries.md)
   - [Exécutions pour les requêtes planifiées](api/runs-scheduled-queries.md)
   - [Modèles de requête](api/query-templates.md)
- UI Query Service {#ui}
   - [Présentation de l’interface utilisateur](ui/overview.md)
   - [Guide d’utilisation de Query Editor](ui/user-guide.md)
   - [Modèles de requête](ui/query-templates.md)
   - [Utilisation des informations dʼidentification de Query Service](ui/credentials.md)
   - [Génération des jeux de données à partir de résultats de requête](ui/create-datasets.md)
- Bonnes pratiques {#best-practices}
   - [Directives générales pour l’exécution des requêtes](best-practices/writing-queries.md)
   - [Conseils pour l’organisation des ressources de données](./best-practices/organize-data-assets.md)
   - [Utilisation de structures de données imbriquées](best-practices/nested-data-structures.md)
   - [aplatissement des structures de données imbriquées](best-practices/flatten-nested-data.md)
   - [Bloc anonyme](best-practices/anonymous-block.md)
   - [Chargement incrémentiel](best-practices/incremental-load.md)
   - [Dédoublonnage des données](best-practices/deduplication.md)
- Attributs dérivés {#derived-attributes}
   - [Présentation](derived-attributes/overview.md)
   - [Cas d’utilisation des décimales](derived-attributes/deciles-use-case.md)
- Exemples de requêtes {#sample-queries}
   - [Exemples de requêtes dʼévénements dʼexpérience](sample-queries/experience-event.md)
   - [Exemples de requêtes Adobe Analytics](sample-queries/adobe-analytics.md)
- Référence SQL {#sql}
   - [Présentation de SQL](sql/overview.md)
   - [Syntaxe SQL](sql/syntax.md)
   - [Fonctions définies par Adobe](sql/adobe-defined-functions.md)
   - [Fonctions Spark SQL](sql/spark-sql-functions.md)
   - [Commandes de métadonnées](sql/metadata.md)
   - [Instructions préparées](sql/prepared-statements.md)
- Connexion des clients à Query Service {#clients}
   - [Présentation de la connexion des clients](clients/overview.md)
   - [Modes SSL](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [Visualiseur Db](./clients/dbvisulaizer.md)
   - [Looker](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Gouvernance des données {#data-governance}
   - [Présentation](data-governance/overview.md)
   - [Guide du journal d’audit](data-governance/audit-log-guide.md)
   - [Identités dans les jeux de données de schémas ad hoc](data-governance/ad-hoc-schema-identities.md)
   - [Prise en charge du contrôle d’accès basé sur les attributs pour les schémas ad hoc](./data-governance/ad-hoc-schema-labels.md)
- [Guide de dépannage](troubleshooting-guide.md)
- [Référence d’API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Notes de mise à jour de Platform](https://docs.adobe.com/content/help/fr-FR/experience-platform/release-notes/latest.html)