---
title: Détails de l’assistant AI en langage naturel du modèle SQL
description: Découvrez le modèle IA Assistant Langage naturel pour l’IA en SQL AI .
exl-id: ca157945-5f74-45d0-9d40-c65d09a8e80d
source-git-commit: 26d05e9519491ef2e8f239cba6a2cde43cff941c
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Informations opérationnelles de l’assistant AI en langage naturel pour les détails du modèle SQL

>[!IMPORTANT]
>
>Adobe publie actuellement d’autres détails sur le modèle. Une documentation supplémentaire sera ajoutée à Experience League dès que celle-ci sera disponible.

## Présentation du modèle {#model-overview}

* **Nom et version du modèle** : Adobe Experience Platform AI Assistant Operational Insights Natural Language to SQL Model ([!DNL NL2SQL]).
* **Date de publication du modèle** : février 2025
* **Objectif du modèle** : le modèle est conçu pour traduire les requêtes en langage naturel des clients sur les informations opérationnelles en requêtes SQL. Ces requêtes SQL sont exécutées à l’aide du graphique de connaissances Adobe Experience Platform, qui contient des métadonnées sur les entités Experience Platform des clients, telles que les schémas, les jeux de données, les audiences, les destinations et les parcours. Les résultats des requêtes SQL sont ensuite utilisés pour générer des réponses aux questions en langage naturel d’origine des clients.
* **Utilisateurs prévus** : les principaux utilisateurs de ce modèle sont les professionnels du marketing, les analystes de données ou les responsables de parcours client qui cherchent à comprendre et à agir sur les informations opérationnelles dans Experience Platform à l’aide du langage naturel. Bien qu’ils ne soient pas des experts en SQL ou en ingénierie de données, ils ont besoin de réponses rapides et précises sur leurs entités Experience Platform pour prendre des décisions éclairées et optimiser les expériences client.
* **Cas d’utilisation** : ce modèle permet aux utilisateurs d’accéder aux métadonnées sur leurs entités Experience Platform telles que les audiences, les parcours, les schémas, les attributs, les jeux de données et les destinations. Les utilisateurs et utilisatrices peuvent poser des questions en langage naturel (par exemple, quelles audiences sont activées ou quelles audiences utilisent un schéma spécifique), et le modèle les traduit en requêtes SQL sur le graphique des connaissances d’Experience Platform. Cela permet aux utilisateurs d’obtenir rapidement une visibilité opérationnelle et de prendre des décisions éclairées sans avoir à explorer ou à interroger manuellement le système.
* **Problèmes** : ce modèle résout les principaux problèmes rencontrés par les utilisateurs et les analystes professionnels travaillant avec Experience Platform, tels que la complexité de la navigation dans de grands volumes de métadonnées interconnectées, la nécessité d’écrire manuellement des requêtes SQL pour récupérer des informations opérationnelles et le manque de visibilité sur la manière dont les entités Experience Platform telles que les audiences, les jeux de données et les parcours sont connectées ou performantes. En permettant l’accès en langage naturel aux métadonnées et en automatisant la génération SQL, le modèle réduit la dépendance aux ressources techniques, raccourcit le temps de découverte d’insight et permet aux utilisateurs de prendre des décisions plus rapides et basées sur les données.

## Détails du modèle {#model-details}

* **Type de modèle** : invite LLM avec apprentissage dynamique en contexte
* **Input** : requêtes en langage naturel de l’utilisateur.
* **Output** : le modèle génère des requêtes SQL en syntaxe [!DNL Snowflake], qui seront exécutées dans le graphique de connaissances Experience Platform.

**Exemple d’entrée**

```console
How many datasets were created within the last 10 days?
```

**Exemple de sortie**

```SQL
SELECT
    COUNT(*) AS datasetCount 
FROM hkg_dim_dataset 
WHERE
    createdTime >= DATEADD(day, -10, CURRENT_DATE);
```

## Évaluation de modèles {#model-evaluation}

* **Mesures et procédures d’évaluation** : le modèle est évalué en examinant les requêtes [!DNL NL2SQL] et en évaluant le nombre de requêtes qui produisent les résultats SQL corrects. Le processus d’évaluation est une combinaison de correspondance basée sur des règles (normalisation SQL, puis correspondance directe des chaînes SQL), de solveur SQL basé sur LLM et d’évaluation humaine.
* **Données d’évaluation et prétraitement** : nous utilisons des jeux ouverts pour le test de régression et nous avons également des projets d’annotation hebdomadaires pour surveiller les performances du modèle par le biais du trafic client réel échantillonné.

## Déploiement de modèles {#model-deployment}

* **Surveillance des modèles** : le modèle de base est hébergé par [!DNL Azure].
* **Mise à jour du modèle** : le langage naturel du modèle SQL de l’assistant Adobe Experience Platform AI Operational Insights est mis à jour régulièrement (chaque semaine) par le biais de l’extension de la banque de questions. Le modèle est également mis à jour par le biais de nouvelles stratégies et instructions d’invite, si nécessaire.

## Équité et partialité {#fairness-and-bias}

* **Équité du modèle** : pour s’assurer que le modèle interprète et génère des requêtes de manière cohérente selon les différentes intentions des utilisateurs et les variations linguistiques sans introduire de biais ou renforcer les stéréotypes, Adobe utilise un contrôle rapide, une explicabilité et des mesures de protection contre la génération de résultats biaisés ou contraires à l’éthique.
* **Biais de données** : la sortie du modèle est affectée par les exemples d’apprentissage contextuel et par ce que le récupérateur sélectionne dans l’invite. Les exemples de la banque de questions contiennent des exemples considérés comme représentatifs du point de vue de la gestion des produits. Selon le cas d’utilisation, les clients doivent examiner la manière dont les biais potentiels dans les sorties du modèle peuvent s’aligner sur leur application prévue ou avoir une incidence sur celle-ci.

## Considérations éthiques {#ethical-considerations}

**Considérations éthiques associées au modèle** : pour éviter d’exposer les informations d’identification personnelles ou des attributs sensibles, le modèle a été conçu pour éviter de renforcer les biais de données existants et respecter les limites du contrôle d’accès. Cela inclut le filtrage, le balisage et le contrôle des champs de schéma pour une utilisation responsable.
