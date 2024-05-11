---
title: Informations personnalisables
description: Découvrez les cas d’utilisation, les fonctionnalités essentielles et les étapes requises pour développer un tableau de bord d’informations personnalisables avec Data Distiller. Découvrez comment la fonctionnalité Informations personnalisables de Data Distiller peut améliorer la transparence et obtenir des informations opérationnelles sur différentes dimensions telles que les profils, les audiences, les campagnes, les parcours, les droits et le consentement.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: bb95e0aa8ee92aee5a2f126d85e78308e652a061
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 5%

---

# Informations personnalisables

Créez des modèles de données de rapports personnalisés sur mesure pour extraire des informations plus approfondies, optimiser des stratégies et adapter les analyses pour répondre aux besoins spécifiques de l’entreprise grâce à la fonctionnalité Informations personnalisables de Data Distiller. Utilisez la fonctionnalité Informations personnalisables pour améliorer la transparence et obtenir des informations opérationnelles à partir de vos données Adobe Experience Platform dans des dimensions telles que les profils, les audiences, les campagnes, les parcours, les droits et le consentement. Cette fonctionnalité offre une solution adaptative polyvalente pour adapter les modèles de données de rapport de votre entreprise en fonction de vos besoins spécifiques.

À [visualiser vos statistiques personnalisables](../../../dashboards/data-distiller/overview.md) vous pouvez utiliser [mode query pro](../../../dashboards/data-distiller/customizable-insights/query-pro-mode.md) pour effectuer des analyses complexes avec des requêtes SQL personnalisées et transformer vos données en graphiques facilement interprétables. Utilisez le mode professionnel des requêtes pour créer des insights et des visualisations personnalisés sur vos tableaux de bord et répondre aux audiences techniques et non techniques en téléchargeant vos informations au format CSV.

Ce document couvre les cas d’utilisation, les fonctionnalités essentielles et les étapes requises pour développer un tableau de bord d’insights personnalisables avec Data Distiller.

## Conditions préalables

Ce tutoriel utilise des tableaux de bord définis par l’utilisateur pour visualiser les données de votre modèle de données personnalisé dans l’interface utilisateur de Platform. Voir [documentation des tableaux de bord définis par l’utilisateur](../../../dashboards/user-defined-dashboards.md) pour en savoir plus sur cette fonctionnalité.

## Commencer

Le SKU Data Distiller est nécessaire pour créer un modèle de données personnalisé pour vos rapports d’informations et pour étendre les modèles de données Real-time CDP qui contiennent des données Platform enrichies. Voir [packaging](../../packaging.md), [barrières de sécurité](../../guardrails.md#query-accelerated-store), et  [licences](../../data-distiller/license-usage.md) documentation relative au SKU de Data Distiller. Si vous ne possédez pas le SKU de Data Distiller, contactez votre représentant du service client Adobe pour plus d’informations.

## Cas d’utilisation de statistiques personnalisables {#use-cases}

Vous trouverez ci-dessous des cas d’utilisation courants qui peuvent être efficacement résolus par le biais de statistiques personnalisables dans Data Distiller.

### Transparence de l’utilisation des profils et des audiences {#usage-transparency}

**Défi :** Comment ventiler les indicateurs de performance clés (IPC) en fonction de critères spécifiques tels que les unités opérationnelles, l’état de fidélité ou la valeur de durée de vie client (CLTV).

**Solution Informations personnalisables :** Data Distiller permet l’extension des modèles de données de création de rapports dans Adobe Experience Platform, ce qui facilite [Ajout d’attributs de profil personnalisés tels que CLTV](../../use-cases/customer-lifetime-value.md) ou l’état de fidélité.

### Suivi des anomalies du consentement {#consent-anomaly-tracking}

**Défi :** Comment appliquer des rapports de tendances de chevauchement et de taille d’audience à des attributs de consentement personnalisés pour des canaux tels que le courrier électronique, les SMS et le téléphone.

**Solution Informations personnalisables :** Le modèle de données de rapport peut être étendu pour suivre les modifications des préférences de consentement au fil du temps. Cela implique de créer des tableaux de faits et de dimensions supplémentaires afin de suivre les préférences et la planification du consentement. [actualisation incrémentielle des données](../../key-concepts/incremental-load.md).

### Optimiser la stratégie de segmentation de l’audience {#optimize-audience-segmentation-strategy}

**Défi :** Comment intégrer des scores de propension générés par le modèle d’apprentissage automatique dans leurs rapports d’indicateurs de performance clés d’audience.

**Solution Informations personnalisables :** Data Distiller permet l’inclusion de la variable [scores de propension des modèles ML personnalisés](../../use-cases/propensity-score.md), ce qui facilite le calcul des scores agrégés au niveau de l’audience. Ces données peuvent ensuite être rapportées avec les IPC standard.

### Extension d’audience {#audience-expansion}

**Défi :** Comment obtenir plus que de simples comptes de profil dans les rapports de chevauchement d’audience et obtenir des données démographiques ou des préférences supplémentaires pour orienter les stratégies d’expansion d’audience.

**Solution Informations personnalisables :** En étendant le modèle de données de rapport, les utilisateurs peuvent incorporer des attributs de profil supplémentaires, en enrichissant le rapport de chevauchement des audiences avec les données démographiques et les préférences appropriées.

## Fonctionnalités clés de la génération d’informations personnalisables {#key-capabilities}

L’illustration ci-dessous présente plusieurs fonctionnalités essentielles pour générer des informations personnalisables. Ces fonctionnalités incluent :

1. **Visualisations des données :** Intégration d’éléments visuels tels que les tendances et les graphiques à barres pour une vue d’ensemble complète des tendances des données.
1. **Création de tableaux de bord :** Activation de la création de tableaux de bord personnalisés adaptés à des cas d’utilisation spécifiques, offrant ainsi une expérience d’analyse plus personnalisée et ciblée.
1. **Modélisation flexible des données SQL :** Utilisez une approche de modélisation des données SQL polyvalente qui permet aux utilisateurs de combiner et de manipuler en toute transparence différents jeux de données, en améliorant l’adaptabilité et la profondeur d’analyse.
1. **Accelerated Store :** Mise en oeuvre d’un mécanisme de stockage accéléré pour fournir efficacement des informations agrégées via SQL, en assurant un accès rapide et rationalisé à des informations précieuses.
1. **Connectivité BI :** Faciliter une intégration transparente avec les outils de Business Intelligence populaires, notamment Power BI, Tableau, Looker et Apache Superset. Cette connectivité garantit la compatibilité avec divers environnements de BI, offrant ainsi aux utilisateurs la possibilité d’utiliser leur outil de choix pour une analyse et des rapports détaillés.

![Représentations visuelles des principales fonctionnalités de Data Distiller Customizable Insights.](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## Procédure de création d’informations personnalisables {#steps-to-create}

Pour développer un tableau de bord Informations personnalisables dans Data Distiller, suivez les instructions étape par étape ci-dessous.

1. **Exploration des requêtes ad hoc :** Commencer par exécuter ad hoc `SELECT` requêtes pour explorer les données brutes sur le lac de données. Cela permet une analyse des données exploratoires à la volée et valide les données où les résultats des requêtes ne sont pas stockés dans le lac de données.
1. **Utilisation des requêtes par lots :** Utilisation de requêtes par lots pour [création de tâches planifiées](../../api/scheduled-queries.md#create-a-new-scheduled-query) pour générer des tableaux agrégés d’insights, en assurant une approche systématique et automatisée du traitement des données. Exécution de requêtes par lots `INSERT TABLE AS SELECT` et `CREATE TABLE AS SELECT` requêtes pour nettoyer, former, manipuler et enrichir les données. Les résultats de ces requêtes sont stockés sur le lac de données.
1. **Chargement des informations agrégées :** Chargez les insights agrégés générés dans le magasin accéléré et utilisez SQL pour tester les requêtes, et assurer la précision et l’efficacité de la récupération des données. Pour apprendre à [Exécution de requêtes sans état dans le magasin accéléré](../../api/accelerated-queries.md), consultez la documentation .
1. **Accès et intégration :** Accédez de manière transparente aux informations stockées dans la boutique accélérée en intégrant Adobe Experience Platform [Tableaux de bord définis par l’utilisateur](../../../dashboards/user-defined-dashboards.md) ou d’autres outils de Business Intelligence préférés. Ces intégrations avec des clients tiers facilitent une expérience cohérente et intuitive pour les utilisateurs.

![Infographie illustrant les quatre étapes de la personnalisation d’insights dans Data Distiller.](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## Étapes suivantes

En lisant ce document, vous comprenez mieux les cas d’utilisation, les fonctionnalités essentielles et les étapes nécessaires au développement d’un tableau de bord d’insights personnalisable avec Data Distiller. Pour continuer à en savoir plus sur la création de modèles de données de rapports personnalisés, voir [guide du modèle de données des informations sur les rapports](./reporting-insights-data-model.md).
