---
title: Informations SQL
description: Découvrez les cas d’utilisation, les fonctionnalités essentielles et les étapes requises pour développer un tableau de bord des insights SQL avec Data Distiller. Découvrez comment la fonctionnalité SQL Insights de Data Distiller peut améliorer la transparence et obtenir des informations opérationnelles sur différentes dimensions telles que les profils, les audiences, les campagnes, les parcours, les droits et le consentement.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: 3435ddd4b235c1c66cd29c75b779bcca607a5d4f
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 5%

---

# Informations SQL

Créez des modèles de données de rapports personnalisés pour extraire des informations plus approfondies, optimiser des stratégies et adapter les analyses afin de répondre à des besoins professionnels spécifiques avec Data Distiller SQL Insights. Utilisez la fonctionnalité SQL Insights pour améliorer la transparence et obtenir des informations opérationnelles à partir de vos données Adobe Experience Platform sur des dimensions telles que les profils, les audiences, les campagnes, les parcours, les droits et le consentement. Cette fonctionnalité offre une solution adaptative polyvalente pour adapter les modèles de données de rapport de votre entreprise en fonction de vos besoins spécifiques.

Pour [visualiser vos statistiques SQL](../../../dashboards/data-distiller/overview.md), vous pouvez utiliser le [mode de requête pro](../../../dashboards/data-distiller/query-pro-mode/overview.md) pour effectuer des analyses complexes avec des requêtes SQL personnalisées et transformer vos données en graphiques facilement interprétables. Utilisez le mode professionnel des requêtes pour créer des insights et des visualisations personnalisés sur vos tableaux de bord et répondre aux audiences techniques et non techniques en téléchargeant vos informations au format CSV.

Ce document couvre les cas d’utilisation, les fonctionnalités essentielles et les étapes requises pour développer un tableau de bord d’insights SQL avec Data Distiller.

## Conditions préalables

Ce tutoriel utilise des tableaux de bord définis par l’utilisateur pour visualiser les données de votre modèle de données personnalisé dans l’interface utilisateur de Platform. Pour en savoir plus sur cette fonctionnalité, consultez la [documentation des tableaux de bord définis par l’utilisateur](../../../dashboards/user-defined-dashboards.md) .

## Commencer

Le SKU Data Distiller est nécessaire pour créer un modèle de données personnalisé pour vos rapports d’informations et pour étendre les modèles de données Real-time CDP qui contiennent des données Platform enrichies. Consultez la documentation [packaging](../../packaging.md), [guardrails](../../guardrails.md#query-accelerated-store) et [licensing](../../data-distiller/license-usage.md) relative au SKU de Data Distiller. Si vous ne possédez pas le SKU de Data Distiller, contactez votre représentant du service client Adobe pour plus d’informations.

## Cas d’utilisation de SQL Insights {#use-cases}

Vous trouverez ci-dessous des cas d’utilisation courants qui peuvent être efficacement résolus par le biais de SQL Insights dans Data Distiller.

### Transparence de l’utilisation des profils et des audiences {#usage-transparency}

**Défi :** Comment ventiler les indicateurs de performance clés (IPC) en fonction de critères spécifiques tels que les unités opérationnelles, l’état de fidélité ou la valeur de durée de vie client (CLTV).

**Solution SQL Insights :** Data Distiller permet l’extension des modèles de données de rapports dans Adobe Experience Platform, ce qui facilite [l’ajout d’attributs de profil personnalisés tels que CLTV](../../use-cases/customer-lifetime-value.md) ou l’état de fidélité.

### Suivi des anomalies du consentement {#consent-anomaly-tracking}

**Défi :** Comment appliquer des rapports de tendances de chevauchement et de taille d’audience aux attributs de consentement personnalisés pour des canaux tels que les emails, les SMS et les téléphones.

**Solution SQL Insights :** Le modèle de données de rapport peut être étendu pour suivre les modifications des préférences de consentement au fil du temps. Cela implique de créer des tableaux de faits et de dimensions supplémentaires pour suivre les préférences de consentement et planifier l’ [actualisation incrémentielle des données](../../key-concepts/incremental-load.md).

### Optimiser la stratégie de segmentation de l’audience {#optimize-audience-segmentation-strategy}

**Défi :** Comment intégrer des scores de propension générés par le modèle d’apprentissage automatique dans leurs rapports IPC d’audience.

**Solution SQL Insights :** Data Distiller permet d’inclure des [scores de propension des modèles ML personnalisés](../../use-cases/propensity-score.md), ce qui facilite le calcul des scores agrégés au niveau de l’audience. Ces données peuvent ensuite être rapportées avec les IPC standard.

### Extension d’audience {#audience-expansion}

**Défi :** Comment acquérir plus que de simples décomptes de profils dans les rapports de chevauchement d’audiences et obtenir des données démographiques ou des préférences supplémentaires pour orienter les stratégies d’expansion d’audience.

**Solution SQL Insights :** En étendant le modèle de données de rapport, les utilisateurs peuvent incorporer des attributs de profil supplémentaires, ce qui enrichit le rapport de chevauchement d’audience avec les données démographiques et les préférences appropriées.

## Fonctionnalités clés de la génération de SQL Insights {#key-capabilities}

L’illustration ci-dessous présente plusieurs fonctionnalités essentielles pour générer SQL Insights. Ces fonctionnalités incluent :

1. **Visualisations de données :** Inclusion d’éléments visuels tels que des tendances et des graphiques à barres pour une vue complète des tendances de données.
1. **Création de tableaux de bord :** activation de la création de tableaux de bord personnalisés adaptés à des cas d’utilisation spécifiques, offrant une expérience d’analyse plus personnalisée et ciblée.
1. **Modélisation flexible des données SQL :** utilisez une approche de modélisation polyvalente des données SQL qui permet aux utilisateurs de combiner et de manipuler en toute transparence différents jeux de données, ce qui améliore la adaptabilité et la profondeur d’analyse.
1. **Boutique accélérée :** mise en oeuvre d’un mécanisme de stockage accéléré pour fournir efficacement des informations agrégées via SQL, assurant un accès rapide et rationalisé à des informations précieuses.
1. **Connectivité BI :** Faciliter une intégration transparente avec les outils de Business Intelligence populaires (BI), y compris Power BI, Tableau, Looker et Apache Superset. Cette connectivité garantit la compatibilité avec divers environnements de BI, offrant ainsi aux utilisateurs la possibilité d’utiliser leur outil de choix pour une analyse et des rapports détaillés.

![Représentations visuelles des fonctionnalités clés de Data Distiller SQL Insights.](../../images/data-distiller/sql-insights/key-capabilities-of-customizable-insights.png)

## Procédure de création de SQL Insights {#steps-to-create}

Pour développer un tableau de bord SQL Insights dans Data Distiller, suivez les instructions étape par étape ci-dessous.

1. **Exploration des requêtes ad hoc :** commencez par exécuter des requêtes ad hoc `SELECT` pour explorer les données brutes sur le lac de données. Cela permet une analyse des données exploratoires à la volée et valide les données où les résultats des requêtes ne sont pas stockés dans le lac de données.
1. **Utilisation des requêtes par lots :** utilisez des requêtes par lots pour [ créer des tâches planifiées ](../../api/scheduled-queries.md#create-a-new-scheduled-query) afin de générer des tables agrégées d’informations, ce qui garantit une approche systématique et automatisée du traitement des données. Les requêtes par lots exécutent des requêtes `INSERT TABLE AS SELECT` et `CREATE TABLE AS SELECT` pour nettoyer, former, manipuler et enrichir les données. Les résultats de ces requêtes sont stockés sur le lac de données.
1. **Chargement des insights agrégés :** Chargez les insights agrégés générés dans le magasin accéléré et utilisez SQL pour tester les requêtes, et assurer la précision et l’efficacité de la récupération des données. Pour savoir comment [ effectuer des requêtes sans état sur le magasin accéléré ](../../api/accelerated-queries.md), consultez la documentation.
1. **Accès et intégration :** Accédez de manière transparente aux informations stockées dans le magasin accéléré en intégrant les [ tableaux de bord définis par l’utilisateur ](../../../dashboards/user-defined-dashboards.md) de Adobe Experience Platform ou d’autres outils de Business Intelligence préférés (BI). Ces intégrations avec des clients tiers facilitent une expérience cohérente et intuitive pour les utilisateurs.

![Infographie illustrant les quatre étapes de SQL Insights dans Data Distiller.](../../images/data-distiller/sql-insights/steps-to-customizable-insights.png)

## Étapes suivantes

En lisant ce document, vous comprenez mieux les cas d’utilisation, les fonctionnalités essentielles et les étapes nécessaires au développement d’un tableau de bord d’insights SQL avec Data Distiller. Pour continuer à en savoir plus sur la création de modèles de données de rapports personnalisés, consultez le [guide de modèle de données d’informations sur les rapports](./reporting-insights-data-model.md).
