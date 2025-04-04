---
title: SQL Insights
description: Découvrez les cas pratiques, les fonctionnalités essentielles et les étapes requises pour développer un tableau de bord d’informations SQL avec Data Distiller. Découvrez comment la fonctionnalité SQL Insights de Data Distiller peut améliorer la transparence et obtenir des informations opérationnelles sur différentes dimensions telles que les profils, les audiences, les campagnes, les parcours, les droits et le consentement.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---

# SQL Insights

Créez des modèles de données de rapports personnalisés pour extraire des informations plus précises, optimiser des stratégies et adapter les analyses aux besoins spécifiques de l’entreprise grâce aux informations SQL de Distiller de données. Utilisez la fonctionnalité SQL Insights pour améliorer la transparence et obtenir des informations opérationnelles à partir de vos données Adobe Experience Platform sur plusieurs dimensions telles que les profils, les audiences, les campagnes, les parcours, les droits et le consentement. Cette fonctionnalité fournit une solution polyvalente et adaptative pour adapter les modèles de données de création de rapports de votre entreprise aux besoins spécifiques de votre entreprise.

Pour [visualiser vos informations SQL](../../../dashboards/sql-insights-query-pro-mode/overview.md) vous pouvez utiliser le [mode pro](../../../dashboards/sql-insights-query-pro-mode/overview.md) pour effectuer des analyses complexes avec des requêtes SQL personnalisées et transformer vos données en graphiques faciles à interpréter. Utilisez le mode Query Pro pour créer des informations et des visualisations personnalisées sur vos tableaux de bord et répondre aux besoins des audiences techniques et non techniques en téléchargeant vos informations sous forme de fichiers CSV.

Ce document couvre les cas d’utilisation, les fonctionnalités essentielles et les étapes requises pour développer un tableau de bord d’informations SQL avec Data Distiller.

## Conditions préalables

Ce tutoriel utilise des tableaux de bord définis par l’utilisateur pour visualiser les données de votre modèle de données personnalisé dans l’interface utilisateur d’Experience Platform. Consultez la [documentation des tableaux de bord définis par l’utilisateur](../../../dashboards/standard-dashboards.md) pour en savoir plus sur cette fonctionnalité.

## Commencer

Le SKU Data Distiller est nécessaire pour créer un modèle de données personnalisé pour vos rapports d’informations et pour étendre les modèles de données Real-Time CDP qui contiennent des données Experience Platform enrichies. Voir la documentation [packaging](../../packaging.md), [mécanismes de sécurisation](../../guardrails.md#query-accelerated-store) et [licence](../../data-distiller/license-usage.md) relative au SKU de Data Distiller. Si vous ne disposez pas du SKU de Data Distiller, contactez votre représentant du service client Adobe pour plus d’informations.

## Cas pratiques SQL Insights {#use-cases}

Vous trouverez ci-dessous des cas d’utilisation courants qui peuvent être traités efficacement par le biais d’Insights SQL dans la Distiller de données.

### Transparence de l’utilisation des profils et des audiences {#usage-transparency}

**Défi :** comment ventiler les indicateurs clés de performance (KPI) en fonction de critères spécifiques tels que les unités commerciales, le statut de fidélité ou la valeur à vie du client (CLTV).

**Solution SQL Insights :** Data Distiller permet l’extension des modèles de données de rapports dans Adobe Experience Platform, ce qui facilite [l’ajout d’attributs de profil personnalisés tels que la CLTV](../../use-cases/customer-lifetime-value.md) ou le statut de fidélité.

### Suivi des anomalies de consentement {#consent-anomaly-tracking}

**Défi :** comment appliquer les rapports de tendance de chevauchement et de taille d’audience aux attributs de consentement personnalisés pour les canaux tels que les e-mails, les SMS et les téléphones.

**Solution SQL Insights :** le modèle de données de rapport peut être étendu pour suivre les modifications des préférences de consentement au fil du temps. Cela implique la création de tableaux de faits et de dimensions supplémentaires pour déterminer les préférences de consentement et la planification [actualisation incrémentielle des données](../../key-concepts/incremental-load.md).

### Optimisation de la stratégie de segmentation des audiences {#optimize-audience-segmentation-strategy}

**Défi :** comment intégrer des scores de propension générés par le modèle de machine learning (ML) dans leurs rapports sur les KPI de l’audience.

**Solution SQL Insights :** Data Distiller permet d’inclure des [scores de propension issus de modèles ML personnalisés](../../use-cases/propensity-score.md), ce qui facilite le calcul des scores agrégés au niveau de l’audience. Ces données peuvent ensuite être générées avec les indicateurs de performance clés standard.

### Expansion des audiences {#audience-expansion}

**Défi :** comment acquérir plus que simplement le nombre de profils dans les rapports de chevauchement d’audience et obtenir des données démographiques ou des préférences supplémentaires pour guider les stratégies d’expansion d’audience.

**Solution SQL Insights :** en étendant le modèle de données de rapport, les utilisateurs et utilisatrices peuvent incorporer des attributs de profil supplémentaires, ce qui enrichit le rapport de chevauchement des audiences avec des données et des préférences démographiques pertinentes.

## Fonctionnalités clés de génération d’informations SQL {#key-capabilities}

L’illustration ci-dessous met en évidence plusieurs fonctionnalités essentielles pour générer des informations SQL. Ces fonctionnalités incluent :

1. **Visualisations des données :** intégration d’éléments visuels tels que des tendances et des graphiques à barres pour une vue complète des tendances des données.
1. **Création de tableaux de bord :** permet de créer des tableaux de bord personnalisés adaptés à des cas d’utilisation spécifiques, offrant ainsi une expérience d’analyse plus personnalisée et plus ciblée.
1. **Modélisation des données SQL flexible :** utilisez une approche de modélisation des données SQL polyvalente qui permet aux utilisateurs et aux utilisatrices de combiner et de manipuler différents jeux de données en toute transparence, ce qui améliore l’adaptabilité et la profondeur d’analyse.
1. **Stockage accéléré :** mise en œuvre d’un mécanisme de stockage accéléré pour diffuser efficacement des informations agrégées via SQL, en garantissant un accès rationalisé et rapide à des informations précieuses.
1. Connectivité **BI :** facilitant l’intégration transparente aux outils de Business Intelligence (BI) populaires, notamment Power BI, Tableau, Looker et Apache Superset. Cette connectivité garantit la compatibilité avec divers environnements de BI et offre aux utilisateurs la possibilité d’utiliser l’outil de leur choix pour des analyses et des rapports approfondis.

![Représentations visuelles des principales fonctionnalités de Data Distiller dans SQL Insights.](../../images/data-distiller/sql-insights/key-capabilities-of-customizable-insights.png)

## Procédure de création d’informations SQL {#steps-to-create}

Pour développer un tableau de bord SQL Insights dans Data Distiller, suivez les instructions détaillées ci-dessous.

1. **Exploration des requêtes ad hoc :** commencez par exécuter des requêtes `SELECT` ad hoc pour explorer les données brutes sur le lac de données. Cela permet une analyse de données exploratoires à la volée à tester et valide les données pour lesquelles les résultats des requêtes ne sont pas stockés dans le lac de données.
1. **Utilisation des requêtes par lots :** utilisez des requêtes par lots pour [créer des tâches planifiées](../../api/scheduled-queries.md#create-a-new-scheduled-query) afin de générer des tables d’agrégats d’informations et d’assurer une approche systématique et automatisée du traitement des données. Les requêtes par lots exécutent des requêtes `INSERT TABLE AS SELECT` et `CREATE TABLE AS SELECT` pour nettoyer, mettre en forme, manipuler et enrichir les données. Les résultats de ces requêtes sont stockés dans le lac de données.
1. **Chargement des informations agrégées :** chargez les informations agrégées générées dans la boutique accélérée et utilisez le langage SQL pour tester les requêtes et garantir la précision et l’efficacité de la récupération des données. Pour savoir comment [effectuer des requêtes sans état vers la boutique accélérée](../../api/accelerated-queries.md), consultez la documentation.
1. **Accès et intégration :** accédez de manière transparente aux informations stockées dans la boutique accélérée en intégrant Adobe Experience Platform [Tableaux de bord définis par l’utilisateur](../../../dashboards/standard-dashboards.md) ou d’autres outils de Business Intelligence préférés. Ces intégrations à des clients tiers facilitent une expérience cohérente et intuitive pour les utilisateurs et les utilisatrices.

![Infographie illustrant les quatre étapes de la création d’Insights SQL dans Data Distiller.](../../images/data-distiller/sql-insights/steps-to-customizable-insights.png)

## Étapes suivantes

Grâce à la lecture de ce document, vous avez maintenant une meilleure compréhension des cas d’utilisation, des fonctionnalités essentielles et des étapes nécessaires pour développer un tableau de bord d’informations SQL avec Data Distiller. Pour continuer à en savoir plus sur la création de modèles de données de rapports personnalisés, consultez le [guide du modèle de données d’informations sur les rapports](./reporting-insights-data-model.md).
