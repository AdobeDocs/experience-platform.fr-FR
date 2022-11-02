---
keywords: Experience Platform;accueil;rubriques les plus consultées;emplacement des données;emplacement des données;gestion des données;gestion des données;liaison;lignage;type de données;types de données;type de données
solution: Experience Platform
title: Présentation des jeux de données
topic-legacy: datasets
description: Ce document présente de manière générale les jeux de données dans Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 02002c9530074b8b05664ff9eab5bc2fe4b7d5d4
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 45%

---

# Présentation des jeux de données

Toutes les données correctement ingérées dans Adobe Experience Platform sont conservées dans la variable [!DNL Data Lake] comme des jeux de données. Un jeu de données est une structure de stockage et de gestion pour la collecte de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées.

Ce document présente de manière générale les jeux de données dans [!DNL Experience Platform].

## Création de jeux de données et suivi des métadonnées

[!DNL Catalog Service] est le système d’enregistrement de l’emplacement et de la traçabilité des données dans [!DNL Experience Platform], et est utilisé pour créer et gérer des jeux de données. [!DNL Catalog] effectue le suivi des métadonnées de chaque jeu de données, qui incluent une référence à la variable [!DNL Experience Data Model] (XDM) schéma auquel le jeu de données se conforme (expliqué dans la section suivante) et le nombre d’enregistrements ingérés dans ce jeu de données.

Pour plus d’informations, consultez la [présentation du service de catalogue](../home.md).

## Application de contraintes aix données des jeux de données

[!DNL Experience Data Model] (XDM) est le cadre normalisé selon lequel [!DNL Platform] organise les données d’expérience client. Toutes les données ingérées dans [!DNL Platform] doit être conforme à un schéma XDM prédéfini avant de pouvoir être conservé dans la variable [!DNL Data Lake] comme un jeu de données.

Tous les jeux de données contiennent une référence au schéma XDM qui limite le format et la structure des données qui peuvent être stockées. Toute tentative de chargement de données vers un jeu de données non conforme à son schéma XDM entraînera l’échec de l’ingestion.

Pour plus d’informations sur XDM, consultez la [présentation du système XDM](../../xdm/home.md).

## Ingestion de données par les jeux de données

Adobe Experience Platform Data Ingestion représente les différentes méthodes par lesquelles [!DNL Platform] ingère des données provenant de diverses sources. Quelle que soit la méthode d’ingestion, toutes les données ingérées sont converties en fichiers de lot. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. Ces fichiers de lot sont ensuite ajoutés aux jeux de données dédiés et conservés dans les [!DNL Data Lake].

Pour plus d’informations, consultez la [présentation de Data Ingestion](../../ingestion/home.md).

## Application de libellés d’utilisation aux jeux de données

La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Le cadre de gouvernance des données vous permet d’appliquer des libellés d’utilisation pour classer les données en fonction des stratégies d’utilisation qui s’appliquent à ces données.

Les libellés d’utilisation des données peuvent être appliqués à des jeux de données entiers ou à des champs de jeu de données individuels. Les libellés ajoutés au niveau du jeu de données sont hérités par tous les champs du jeu de données.

Pour plus d’informations sur ce service, consultez la [présentation de la gouvernance des données](../../data-governance/home.md). Pour savoir comment utiliser les libellés d’utilisation dans [!DNL Platform], reportez-vous aux guides suivants :

* [Gestion des libellés dans l’interface utilisateur](../../data-governance/labels/user-guide.md)
* [Gestion des libellés de jeux de données dans l’API](../../data-governance/labels/dataset-api.md)

## Jeux de données en aval [!DNL Platform] services

Une fois que les jeux de données ont été utilisés pour stocker les données ingérées, ces jeux de données sont ensuite utilisés par les jeux de données en aval. [!DNL Platform] services permettant de mettre à jour les profils client, d’obtenir des informations grâce à l’apprentissage automatique, etc.

Voici une liste des services en aval qui utilisent des jeux de données pour diverses opérations. Veuillez consulter la documentation de chaque service pour en savoir plus.

* [[!DNL Data Access API]](../../data-access/home.md): Permet d’accéder au contenu des fichiers stockés dans les jeux de données et de le télécharger.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md) : associe les identités des appareils et des systèmes, en liant les jeux de données en fonction des champs d’identité définis par les schémas XDM auxquels ils se conforment.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Exploitation [!DNL Identity Service] pour créer des profils client détaillés à partir de vos jeux de données en temps réel. [!DNL Real-time Customer Profile] extrait les données de la fonction [!DNL Data Lake] et conserve les profils client dans son propre entrepôt de données distinct.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md)[!DNL Real-time Customer Profile] : permet de créer des segments et de générer des audiences à partir de vos données Ces audiences peuvent ensuite être exportées vers leurs propres jeux de données dans la variable [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md) : utilise l’apprentissage automatique et l’intelligence artificielle pour découvrir des insights dans les jeux de données volumineux.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Permet d’utiliser SQL standard pour interroger des données dans [!DNL Experience Platform], en associant n’importe quel jeu de données dans [!DNL Data Lake] et capturer les résultats des requêtes en tant que nouveau jeu de données à utiliser dans les rapports, [!DNL Data Science Workspace]ou [!DNL Real-time Customer Profile].
* [Service de destinations Adobe Experience Platform](../../destinations/home.md): Permet à [exportation de jeux de données](/help/destinations/ui/export-datasets.md) vers les destinations de stockage dans le cloud ou de marketing par e-mail de votre choix, pour les activités de création de rapports ou de science des données.

## Étapes suivantes

En lisant ce document, vous avez découvert les principales utilisations des jeux de données dans [!DNL Experience Platform], ainsi que les [!DNL Platform] services qui utilisent des jeux de données. Pour plus d’informations sur les nombreuses façons dont les jeux de données sont utilisés dans [!DNL Platform], veuillez consulter la documentation du service liée tout au long de cette présentation.

Pour savoir comment interagir avec des jeux de données au sein de [!DNL Experience Platform] Dans l’interface utilisateur, reportez-vous à la section [guide d’utilisation des jeux de données](user-guide.md).
