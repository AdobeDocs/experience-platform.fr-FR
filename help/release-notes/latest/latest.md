---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 56d43d93be7aca059a38e9428ad5680dd52ad6f9
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 49%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 22 juin 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Science Workspace]](#dsw)
- [Query Service](#query-service)
- [Sources](#sources)

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour exploiter les informations contenues dans vos données. Intégré à Adobe Experience Platform, Data Science Workspace vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de l’ensemble des solutions Adobe. L’utilisation de JupyterLab est l’un des moyens d’y parvenir par Data Science Workspace. JupyterLab est une interface utilisateur web pour <a href="https://jupyter.org/" target="_blank">Project Jupyter</a> et est étroitement intégré à Adobe Experience Platform. Il fournit un environnement de développement interactif pour que les analystes de données puissent travailler avec les notebooks, le code et les données Jupyter.

| Fonctionnalité | Description |
| --- | --- |
| Lanceur JupyterLab | Le lanceur JupyterLab comprend désormais des démarrages pour les notebooks Spark 3.2. Les démarrages de notebook Spark 2.4 sont désormais remplacés par des notebooks Spark 3.2 et feront partie de cette version. |
| Spark 3.2 | Les nouvelles recettes Scala (Spark) et PySpark utilisent désormais Spark 3.2. |
| Noyaux | Les notebooks Scala (Spark) sont désormais créés via le noyau Scala. Les notebooks PySpark sont désormais créés via le noyau Python. Le noyau Spark et PySpark sont obsolètes et doivent être supprimés dans une version ultérieure. |
| Recettes | Les nouvelles recettes PySpark et Spark suivent désormais le processus Docker de la même manière que les recettes Python et R. |

{style=&quot;table-layout:auto&quot;}

Pour obtenir des informations plus générales sur Data Science Workspace, voir [documentation de présentation](../../data-science-workspace/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans Data Science Workspace ou pour l’ingestion dans Real-time Customer Profile.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Étiquetage des schémas ad hoc | Gérez l’accès aux données sensibles en appliquant des étiquettes aux champs de données des schémas ad hoc générés automatiquement par le biais de requêtes CTAS Query Service. Vous pouvez restreindre l’utilisation de certains champs ou jeux de données de schémas ad hoc pour contrôler l’accès à des données personnelles sensibles et à des informations d’identification personnelle. En utilisant la fonctionnalité de contrôle d’accès basé sur les attributs, vous pouvez étiqueter les champs de schéma ad hoc via l’interface utilisateur de Platform. |
| `FLATTEN` paramètre | Lors de la connexion à une base de données par le biais d’outils de BI tiers, la variable `FLATTEN` la définition de aplatit les structures de données imbriquées dans des colonnes distinctes où le nom de l’attribut devient le nom de la colonne qui contient les valeurs de ligne. Cela améliore l’utilisation des schémas ad hoc et réduit la charge de travail nécessaire pour récupérer, analyser, transformer et générer des rapports sur les données dans les outils de BI qui ne prennent pas en charge les structures de données imbriquées. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur Query Services, reportez-vous à la section [Présentation de Query Service](../../query-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| Version bêta de la source [!DNL Mixpanel] | Vous pouvez désormais utiliser la variable [!DNL Mixpanel] source pour ingérer des données d’analyse à partir de votre [!DNL Mixpanel] compte à Experience Platform. Voir [[!DNL Mixpanel] documentation source](../../sources/connectors/analytics/mixpanel.md) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
