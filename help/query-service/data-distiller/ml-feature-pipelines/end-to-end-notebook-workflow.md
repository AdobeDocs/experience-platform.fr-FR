---
title: Workflow d’enrichissement de pipeline de données AI/ML de bout en bout
description: Utilisez des notebooks d’environnement d’apprentissage automatique basés sur le cloud pour créer un modèle de formation et de notation de propension qui prédit les conversions d’abonnement à partir des données Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 2853e7c7-cab8-4e1b-b73f-622c937fbbaf
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

<!-- 
title: Cloud Machine Learning Environment Notebooks
Cloud machine learning environment notebooks
Old title: 
# AI/ML data pipeline enrichment end-to-end workflow
-->

# Workflow d’enrichissement de pipeline de données AI/ML de bout en bout

Utilisez Data Distiller pour enrichir vos pipelines d’apprentissage automatique avec des données d’expérience client à forte valeur ajoutée qui ont été collectées et traitées dans Adobe Experience Platform.

Ce document fournit une série de notebooks d’environnement d’apprentissage automatique basés sur le cloud qui montrent un processus de bout en bout. Le workflow utilise vos outils d’apprentissage automatique préférés pour créer des modèles de données personnalisés qui prennent en charge vos cas d’utilisation marketing avec des données Experience Platform.

Ce workflow nécessite l’utilisation de [!DNL Python] notebooks dans vos environnements d’apprentissage automatique. Les instructions de prise en main de ces [!DNL Python] notebooks sont incluses dans leurs fichiers Lisez-moi respectifs.

Avant de poursuivre avec ce guide, suivez les étapes décrites dans la [présentation des pipelines de fonctionnalités AI/ML](./overview.md) pour activer l’utilisation des notebooks Python d’exemple utilisés dans ce cas d’utilisation de ce pipeline de fonctionnalités AI/ML.

## notebooks d’environnement d’apprentissage automatique cloud {#cmle-notebooks}

Le workflow de bout en bout peut être divisé en trois grandes phases, basées sur les services utilisés pour mettre en oeuvre le workflow.

- L’exploration et la préparation initiales des données de Platform reposent sur les services de Platform.
- La formation et la notation des modèles utilisent des outils dans votre environnement ML basé sur le cloud. Les choix courants pour les plateformes ML sont les suivants : Databricks ML, AWS Sagemaker, DataRobot, etc.
- L’ingestion de scores dans Platform et toute création et activation d’audiences basées sur du code basée sur ces scores dépendrait à nouveau des services Platform.

Cependant, toutes ces phases peuvent être exécutées dans un ou plusieurs notebooks de votre environnement ML sans que l’utilisateur ait besoin de basculer entre Platform et ses outils ML basés sur le cloud.

Les étapes typiques de ce flux de bout en bout ont été divisées en un ensemble de notebooks modulaires qui, pris ensemble, montrent les étapes impliquées dans un projet d’apprentissage automatique type impliquant des données Platform. Il est ainsi plus facile d’utiliser les notebooks comme référence pour la mise en oeuvre d’activités spécifiques, ainsi que de sélectionner et d’adapter le code des notebooks appropriés pour mettre en oeuvre un cas pratique concret. En pratique, un spécialiste des données peut préparer un seul notebook pour mettre en oeuvre le pipeline de bout en bout pour son projet ML. Un spécialiste des données peut également simplement adapter l’exemple de code pour interroger les données de Platform et les rendre disponibles dans son environnement ML avant de poursuivre le projet en utilisant des fonctionnalités basées sur l’interface utilisateur dans sa plateforme ML.

Les exemples de notebooks inclus dans le référentiel lié sont brièvement décrits ci-dessous. La documentation détaillée de chaque notebook est insérée dans le code des notebooks.

<!-- Below is the meat - the how to (but without links or details) -->

### Générer des données synthétiques {#generate-synthetic-data}

Ce notebook fournit du code pour la génération de jeux de données de profils synthétiques et d’événements d’expérience dans votre plateforme qui seront utilisés pour illustrer le workflow CMLE.

### EDA et fonctionnalité avec Query Service {#eda-and-featurization-with-query-service}

Ce notebook comprend des exemples d’analyse exploratoire des jeux de données Platform à l’aide de requêtes interactives via Platform Query Service. Ces exemples sont suivis d’exemples de requêtes de fonctionnalité pour créer un jeu de données de formation pour l’exemple de modèle de propension.

### Exporter les données de formation {#export-training-data}

Ce notebook illustre l’exportation du jeu de données d’entraînement vers l’espace de stockage dans le cloud qui peut être lu par vos outils ML.

### Formation d’un modèle de propension {#train-a-propensity-model}

Ce notebook illustre la formation d’un modèle de propension. Il suppose que Databricks ML soit votre environnement ML, mais il est écrit de manière générique (c’est-à-dire sans utilisation intensive de fonctionnalités/API spécifiques à Databricks) afin qu’il puisse être adapté à d’autres plateformes.

### Notation du modèle de propension

Ce notebook illustre la notation du modèle de propension formé afin de produire un jeu de données de scores de propension pour chaque profil client Platform.

### Ingestion de scores dans AEP

Ce notebook de résumé illustre l’ingestion du jeu de données de scores de propension pour enrichir les profils client dans AEP.

### Création et activation d’audiences à partir du code

Ce notebook explique comment l’utilisateur peut créer des audiences à partir des scores et activer ces audiences par le biais des applications Platform à partir de son code de notebook.
