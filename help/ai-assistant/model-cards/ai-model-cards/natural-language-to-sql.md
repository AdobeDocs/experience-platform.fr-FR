---
title: Carte de modèle du langage naturel de l’assistant AI vers SQL
description: Découvrez le modèle IA Assistant Langage naturel pour l’IA en SQL AI .
hide: true
hidefromtoc: true
source-git-commit: 70b705a7c6df24ad9549c46832ff4898253670ac
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Carte du modèle SQL d’informations opérationnelles de l’assistant AI en langage naturel

## Présentation du modèle {#model-overview}

* Le nom officiel du modèle est AI Assistant Operational Insights Natural Language to SQL Model ([!DNL NL2SQL]) et a été publié dans sa dernière version mise à disposition générale en février 2025.
* Le modèle est conçu pour traduire les requêtes en langage naturel des clients sur les informations opérationnelles en requêtes SQL. Ces requêtes SQL sont exécutées à l’aide du graphique de connaissances Adobe Experience Platform, qui contient des métadonnées sur les entités Experience Platform des clients, telles que les schémas, les jeux de données, les audiences, les destinations et les parcours. Les résultats des requêtes SQL sont ensuite utilisés pour générer des réponses aux questions en langage naturel d’origine des clients.
* Les principaux utilisateurs de ce modèle sont les professionnels du marketing, les analystes de données ou les responsables de parcours client qui cherchent à comprendre et à agir sur les informations opérationnelles dans Experience Platform à l’aide du langage naturel. Bien qu’ils ne soient pas des experts en SQL ou en ingénierie de données, ils ont besoin de réponses rapides et précises sur leurs entités Experience Platform pour prendre des décisions éclairées et optimiser les expériences client.
* Ce modèle fait partie de l’assistant AI pour Operational Insights, qui permet aux utilisateurs d’accéder aux métadonnées sur leurs entités Experience Platform telles que les audiences, les parcours, les schémas, les attributs, les jeux de données et les destinations. Les utilisateurs et utilisatrices peuvent poser des questions en langage naturel (par exemple, quelles audiences sont activées ou quelles audiences utilisent un schéma spécifique), et le modèle les traduit en requêtes SQL sur le graphique des connaissances d’Experience Platform. Cela permet aux utilisateurs d’obtenir rapidement une visibilité opérationnelle et de prendre des décisions éclairées sans avoir à explorer ou à interroger manuellement le système.
* Ce modèle résout les principaux problèmes auxquels sont confrontés les utilisateurs professionnels et les analystes qui travaillent avec Experience Platform, tels que la complexité de la navigation dans de grands volumes de métadonnées interconnectées, la nécessité d’écrire manuellement des requêtes SQL pour récupérer des informations opérationnelles et le manque de visibilité sur la façon dont les entités Experience Platform telles que les audiences, les jeux de données et les parcours sont connectés ou performantes. En permettant l’accès en langage naturel aux métadonnées et en automatisant la génération SQL, le modèle réduit la dépendance aux ressources techniques, raccourcit le temps de découverte d’insight et permet aux utilisateurs de prendre des décisions plus rapides et basées sur les données.
* Le modèle ne doit pas être utilisé pour accéder ou déduire des informations d’identification personnelle (PII), telles que les noms de client ou cliente, les adresses e-mail ou les numéros de téléphone, même si de telles données existent dans la plateforme.
* En outre, il ne doit pas être utilisé pour les contrôles de conformité ou de gouvernance, tels que la validation des politiques de conservation des données, des règles de contrôle d’accès ou du statut de consentement. Ces tâches nécessitent des systèmes et des stratégies spécialisés.

## Détails du modèle {#model-details}

* Le type de modèle est Invite LLM avec apprentissage dynamique en contexte.
* Les entrées du modèle sont des requêtes en langage naturel de l’utilisateur.
* Le modèle génère des requêtes SQL en syntaxe [!DNL Snowflake], qui sont exécutées sur le graphique de connaissances Experience Platform.

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

## Modèle de formation {#model-training}

* [!DNL NL2SQL] a utilisé [!DNL OpenAI] modèles basés sur le protocole GPT pour l’apprentissage contextuel.
* La banque de questions [!DNL NL2SQL] contient 428 requêtes provenant de l’équipe [!DNL Operational Insights] et 524 d’équipes externes pour les cas d’utilisation de la version alpha.

## Évaluation de modèles {#model-evaluation}

* Le modèle est évalué avec précision. Par exemple, sur toutes les requêtes [!DNL NL2SQL], le nombre de requêtes qui génèrent les résultats SQL corrects.
* Le processus d’évaluation est une combinaison de correspondance basée sur des règles (normalisation SQL, puis correspondance directe des chaînes SQL), de solveur SQL basé sur LLM et d’évaluation humaine
* Les ensembles ouverts sont utilisés pour les tests de régression et les projets d’annotation hebdomadaires surveillent les performances du modèle par le biais du trafic client réel échantillonné.
* Pour ce qui est de l&#39;évaluation contradictoire, il existe un modèle distinct qui fonctionne comme mécanisme de sécurisation pour les [!DNL NL2SQL].

## Déploiement de modèles {#model-deployment}

* Le modèle LLM est un modèle basé sur le protocole GPT hébergé par des API [!DNL Azure OpenAI].
* Le modèle de base est hébergé par [!DNL Azure].
* Le modèle est mis à jour régulièrement, sur une base hebdomadaire, par le biais de l&#39;expansion de la banque de questions. Le mode est également mis à jour par le biais de nouvelles stratégies et instructions d’invite, si nécessaire.

## Explicabilité {#explainability}

Le modèle utilise un modèle d’explication distinct pour SQL.

## Équité et partialité {#fairness-and-bias}

* Pour s’assurer que le modèle interprète et génère des requêtes de manière cohérente selon les différentes intentions des utilisateurs et les variations linguistiques sans introduire de biais ou renforcer les stéréotypes, Adobe utilise un contrôle rapide, une explicabilité et des mesures de protection contre la génération de résultats biaisés ou contraires à l’éthique.
* La sortie du modèle est affectée par les exemples d’apprentissage contextuel et par ce que le récupérateur sélectionne dans l’invite. Les exemples de banques de questions contiennent des exemples considérés comme représentatifs du point de vue du premier ministre, et nous étendons également les banques de questions en fonction du trafic réel de clients.

## Solidité {#robustness}

Comme la plupart des requêtes qu’elle reçoit ne sont pas couvertes dans la banque de questions, la précision du trafic de production reflète la robustesse du modèle.

## Considérations relatives à la confidentialité et la sécurité {#privacy-and-security-considerations}

Le modèle ne traite ni ne conserve aucune information d’identification personnelle (PII) et ces informations sont masquées pour la génération SQL. Pour la vérification des autorisations de contrôle d’accès basé sur les attributs, le code SQL généré sera traité par l’équipe d’Experience Platform Knowledge Graph afin d’assurer la qualité de la gouvernance.

## Considérations éthiques {#ethical-considerations}

Pour éviter d’exposer des informations d’identification personnelle ou des attributs sensibles, le modèle a été conçu pour prendre en charge la confidentialité, éviter de renforcer les biais de données existants et respecter les limites du contrôle d’accès. Cela inclut le filtrage, le balisage et le contrôle des champs de schéma pour une utilisation responsable.

