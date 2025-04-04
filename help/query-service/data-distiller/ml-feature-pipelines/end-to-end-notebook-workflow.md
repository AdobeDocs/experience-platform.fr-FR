---
title: Workflow de bout en bout d’enrichissement du pipeline de données AI/ML
description: Utilisez des notebooks d’environnement de machine learning basés sur le cloud pour créer une formation et un score de modèle de propension qui prédit les conversions d’abonnements à partir des données Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 2853e7c7-cab8-4e1b-b73f-622c937fbbaf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

<!-- 
title: Cloud Machine Learning Environment Notebooks
Cloud machine learning environment notebooks
Old title: 
# AI/ML data pipeline enrichment end-to-end workflow
-->

# Workflow de bout en bout d’enrichissement du pipeline de données AI/ML

Utilisez Data Distiller pour enrichir vos pipelines de machine learning avec des données d’expérience client à forte valeur ajoutée qui ont été collectées et traitées dans Adobe Experience Platform.

Ce document fournit une série de notebooks d’environnement de machine learning basés sur le cloud qui présentent un workflow de bout en bout. Le workflow utilise vos outils de machine learning préférés pour créer des modèles de données personnalisés qui prennent en charge vos cas d’utilisation marketing avec les données Experience Platform.

Ce workflow nécessite l’utilisation de notebooks [!DNL Python] dans vos environnements de machine learning. Les instructions de prise en main de ces notebooks [!DNL Python] sont incluses dans leurs fichiers lisez-moi respectifs.

Avant de poursuivre avec ce guide, suivez les étapes décrites dans la présentation des pipelines de fonctionnalités [AI/ML](./overview.md) pour permettre l’utilisation des exemples de notebooks Python utilisés dans ce cas d’utilisation de pipeline de fonctionnalités AI/ML.

## Notebooks d’environnement de machine learning dans le cloud {#cmle-notebooks}

Le workflow de bout en bout peut être divisé en trois grandes phases en fonction des services utilisés pour mettre en œuvre le workflow.

- L’exploration et la préparation initiales des données Experience Platform reposent sur les services Experience Platform.
- La formation et la notation des modèles s’appuient sur les outils dans votre environnement ML basé sur le cloud. Les choix courants pour les plateformes de ML incluent : Databricks ML, AWS Sagemaker, DataRobot, etc.
- L’ingestion des scores dans Experience Platform ainsi que la création et l’activation d’audiences basées sur du code et basées sur ces scores reposeraient à nouveau sur les services Experience Platform.

Cependant, toutes ces phases peuvent être exécutées dans un ou plusieurs notebooks à partir de votre environnement ML sans que l’utilisateur ait besoin de basculer entre les contextes Experience Platform et leurs outils ML basés sur le cloud.

Les étapes standard de ce flux de bout en bout ont été divisées en un ensemble de notebooks modulaires qui, pris ensemble, montrent les étapes impliquées dans un projet de machine learning type impliquant des données Experience Platform. Cela facilite l’utilisation des notebooks comme référence pour la mise en œuvre d’activités spécifiques, ainsi que la sélection et l’adaptation du code des notebooks appropriés pour mettre en œuvre un cas d’utilisation réel. En pratique, un spécialiste des données peut préparer un seul notebook pour mettre en œuvre le pipeline de bout en bout pour son projet ML. Un spécialiste des données peut également simplement adapter l’exemple de code pour interroger les données Experience Platform et le rendre disponible dans son environnement ML avant de poursuivre le projet en utilisant les fonctionnalités de l’interface utilisateur dans sa plateforme ML.

Les exemples de notebooks inclus dans le référentiel lié sont brièvement décrits ci-dessous. La documentation détaillée de chaque notebook est intercalée avec le code dans les notebooks eux-mêmes.

<!-- Below is the meat - the how to (but without links or details) -->

### Générer des données synthétiques {#generate-synthetic-data}

Ce notebook fournit du code pour générer des jeux de données de profils synthétiques et d’événements d’expérience dans votre Experience Platform qui seront utilisés pour illustrer le workflow CMLE.

### AED et fonctionnalité avec Query Service {#eda-and-featurization-with-query-service}

Ce notebook comprend des exemples d’analyse exploratoire sur les jeux de données Experience Platform à l’aide de requêtes interactives via Experience Platform Query Service. Elles sont suivies d’exemples de requêtes de fonctionnalités permettant de créer un jeu de données d’entraînement pour l’exemple de modèle de propension.

### Exporter les données de formation {#export-training-data}

Ce notebook illustre l’exportation du jeu de données d’entraînement vers l’espace de stockage cloud qui peut être lu par vos outils ML.

### Entraîner un modèle de propension {#train-a-propensity-model}

Ce notebook illustre l’entraînement d’un modèle de propension. Il suppose que Databricks ML est votre environnement ML, mais il est écrit de manière générique (c’est-à-dire sans utiliser beaucoup de fonctionnalités/API spécifiques à Databricks) afin qu’il puisse être adapté à d’autres plateformes.

### Score du modèle de propension

Ce notebook illustre la notation du modèle de propension formé afin de produire un jeu de données de scores de propension pour chaque profil client Experience Platform.

### Ingérer des scores dans AEP

Ce bref notebook illustre l’ingestion du jeu de données de scores de propension pour enrichir les profils client dans AEP.

### Créer et activer des audiences à partir du code

Ce notebook illustre la manière dont l’utilisateur peut créer des audiences à partir des scores et activer ces audiences par le biais des applications Experience Platform à partir du code de son notebook.
