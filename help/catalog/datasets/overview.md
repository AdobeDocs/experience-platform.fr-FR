---
keywords: Experience Platform;home;popular topics;data location;Data Location;Data management;data management;Lineage;lineage;data type;data types;Data types;Data type
solution: Experience Platform
title: Présentation des jeux de données
topic: datasets
description: Ce document présente de manière générale les jeux de données dans Experience Platform.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 46%

---


# Présentation des jeux de données

All data that is successfully ingested into Adobe Experience Platform is persisted within the [!DNL Data Lake] as datasets. Un jeu de données est une structure de stockage et de gestion pour la collecte de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées.

Ce document présente de manière générale les jeux de données dans [!DNL Experience Platform].

## Création de jeux de données et suivi des métadonnées

[!DNL Catalog Service] est le système d’enregistrement de l’emplacement et du lignage des données [!DNL Experience Platform]et est utilisé pour créer et gérer des jeux de données. [!DNL Catalog] suit les métadonnées de chaque jeu de données, ce qui inclut une référence au schéma [!DNL Experience Data Model] (XDM) auquel le jeu de données est conforme (expliqué dans la section suivante) et le nombre d&#39;enregistrements assimilés à ce jeu de données.

Pour plus d’informations, consultez la [présentation du service de catalogue](../home.md).

## Application de contraintes aix données des jeux de données

[!DNL Experience Data Model] (XDM) est le cadre normalisé qui [!DNL Platform] organise les données d’expérience client. All data that is ingested into [!DNL Platform] must conform to a pre-defined XDM schema before it can be persisted in the [!DNL Data Lake] as a dataset.

Tous les jeux de données contiennent une référence au schéma XDM qui limite le format et la structure des données qui peuvent être stockées. Toute tentative de chargement de données vers un jeu de données non conforme à son schéma XDM entraînera l’échec de l’ingestion.

Pour plus d’informations sur XDM, consultez la [présentation du système XDM](../../xdm/home.md).

## Ingestion de données par les jeux de données

Adobe Experience Platform Data Ingestion represents the multiple methods by which [!DNL Platform] ingests data from various sources. Quelle que soit la méthode d’ingestion, toutes les données ingérées sont converties en fichiers de lot. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. These batch files are then added to dedicated datasets and persisted within the [!DNL Data Lake].

Pour plus d’informations, consultez la [présentation de Data Ingestion](../../ingestion/home.md).

## Application de libellés d’utilisation aux jeux de données

Adobe Experience Platform [!DNL Data Governance] allows you to manage customer data in order to ensure compliance with regulations, restrictions, and policies applicable to data use. Using Data Usage Labeling and Enforcement (DULE) as its core framework, [!DNL Data Governance] allows you to apply usage labels to categorize data according to the usage policies that apply to that data.

Les libellés d’utilisation des données peuvent être appliqués à des jeux de données entiers ou à des champs de jeu de données individuels. Les libellés ajoutés au niveau du jeu de données sont hérités par tous les champs du jeu de données.

Pour plus d’informations sur ce service, consultez la [présentation de la gouvernance des données](../../data-governance/home.md). Pour savoir comment utiliser les libellés d’utilisation dans [!DNL Platform], consultez les guides suivants :

* [Gestion des libellés dans l’interface utilisateur](../../data-governance/labels/user-guide.md)
* [Gérer les étiquettes de jeux de données dans l’API](../../data-governance/labels/dataset-api.md)

## Datasets in downstream [!DNL Platform] services

Once datasets have been used to store ingested data, those datasets are then used by downstream [!DNL Platform] services to update customer profiles, gain insights through machine learning, and more.

Voici une liste des services en aval qui utilisent des jeux de données pour diverses opérations. Veuillez consulter la documentation de chaque service pour en savoir plus.

* [!DNL Data Access API](../../data-access/home.md): Permet d’accéder au contenu des fichiers stockés dans des jeux de données et de le télécharger.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md) : associe les identités des appareils et des systèmes, en liant les jeux de données en fonction des champs d’identité définis par les schémas XDM auxquels ils se conforment.
* [!DNL Real-time Customer Profile](../../profile/home.md): Exploite [!DNL Identity Service] pour créer des profils client détaillés à partir de vos jeux de données en temps réel. [!DNL Real-time Customer Profile] extrait les données [!DNL Data Lake] et conserve les profils clients dans sa propre banque de données distincte.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md)[!DNL Real-time Customer Profile] : permet de créer des segments et de générer des audiences à partir de vos données These audiences can then be exported to their own datasets within the [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md) : utilise l’apprentissage automatique et l’intelligence artificielle pour découvrir des insights dans les jeux de données volumineux.
* [Service](../../query-service/home.md)de Requête Adobe Experience Platform : Vous permet d&#39;utiliser SQL standard pour requête des données dans [!DNL Experience Platform], de joindre des jeux de données dans les jeux de données [!DNL Data Lake] et de capturer les résultats des requêtes sous la forme d&#39;un nouveau jeu de données à utiliser dans le rapports, [!DNL Data Science Workspace]ou [!DNL Real-time Customer Profile].
* [Service de prise de décision d’Adobe Experience Platform](../../decisioning-service/home.md)[!DNL Real-time Customer Profile] : exploite pour déterminer le choix le plus probable du client à partir d’un ensemble d’options, en fonction des données comportementales que extrait des jeux de données activés.[!DNL Profile]

## Étapes suivantes

By reading this document, you have been introduced to the core uses of datasets in [!DNL Experience Platform], as well as the various [!DNL Platform] services that utilize datasets. For more details on the many ways datasets are used in [!DNL Platform], please review the service documentation linked throughout this overview.

For steps on how to interact with datasets within the [!DNL Experience Platform] UI, see the [datasets user guide](user-guide.md).