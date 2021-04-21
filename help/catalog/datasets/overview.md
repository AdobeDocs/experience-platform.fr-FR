---
keywords: Experience Platform ; accueil ; rubriques populaires ; emplacement des données ; emplacement des données ; Data Management ; data Management ; lignage ; lignée ; type de données ; types de données ; type de données ; type de données
solution: Experience Platform
title: Présentation des jeux de données
topic-legacy: datasets
description: Ce document présente de manière générale les jeux de données dans Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 43%

---

# Présentation des jeux de données

Toutes les données qui sont correctement ingérées dans Adobe Experience Platform sont conservées dans les [!DNL Data Lake] sous forme de jeux de données. Un jeu de données est une structure de stockage et de gestion pour la collecte de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées.

Ce document présente de manière générale les jeux de données dans [!DNL Experience Platform].

## Création de jeux de données et suivi des métadonnées

[!DNL Catalog Service] est le système d’enregistrement de l’emplacement et du lignage des données  [!DNL Experience Platform]et est utilisé pour créer et gérer des jeux de données. [!DNL Catalog] suit les métadonnées de chaque jeu de données, ce qui inclut une référence au schéma  [!DNL Experience Data Model] (XDM) auquel le jeu de données est conforme (expliqué dans la section suivante) et le nombre d&#39;enregistrements assimilés à ce jeu de données.

Pour plus d’informations, consultez la [présentation du service de catalogue](../home.md).

## Application de contraintes aix données des jeux de données

[!DNL Experience Data Model] (XDM) est le cadre normalisé qui  [!DNL Platform] organise les données d’expérience client. Toutes les données ingérées dans [!DNL Platform] doivent se conformer à un schéma XDM prédéfini avant de pouvoir être conservées dans le [!DNL Data Lake] en tant que jeu de données.

Tous les jeux de données contiennent une référence au schéma XDM qui limite le format et la structure des données qui peuvent être stockées. Toute tentative de chargement de données vers un jeu de données non conforme à son schéma XDM entraînera l’échec de l’ingestion.

Pour plus d’informations sur XDM, consultez la [présentation du système XDM](../../xdm/home.md).

## Ingestion de données par les jeux de données

L&#39;Ingestion des données Adobe Experience Platform représente les méthodes multiples par lesquelles [!DNL Platform] ingère des données provenant de diverses sources. Quelle que soit la méthode d’ingestion, toutes les données ingérées sont converties en fichiers de lot. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. Ces fichiers de commandes sont ensuite ajoutés aux jeux de données dédiés et conservés dans [!DNL Data Lake].

Pour plus d’informations, consultez la [présentation de Data Ingestion](../../ingestion/home.md).

## Application de libellés d’utilisation aux jeux de données

Adobe Experience Platform [!DNL Data Governance] vous permet de gérer les données client afin de garantir la conformité aux réglementations, restrictions et stratégies applicables à l’utilisation des données. La structure [!DNL Data Governance] vous permet d&#39;appliquer des étiquettes d&#39;utilisation pour classer les données en fonction des stratégies d&#39;utilisation qui s&#39;appliquent à ces données.

Les libellés d’utilisation des données peuvent être appliqués à des jeux de données entiers ou à des champs de jeu de données individuels. Les libellés ajoutés au niveau du jeu de données sont hérités par tous les champs du jeu de données.

Pour plus d’informations sur ce service, consultez la [présentation de la gouvernance des données](../../data-governance/home.md). Pour savoir comment utiliser les libellés d&#39;utilisation dans [!DNL Platform], consultez les guides suivants :

* [Gestion des libellés dans l’interface utilisateur](../../data-governance/labels/user-guide.md)
* [Gérer les étiquettes de jeux de données dans l’API](../../data-governance/labels/dataset-api.md)

## Jeu de données des services [!DNL Platform] en aval

Une fois que les jeux de données ont été utilisés pour stocker des données imbriquées, ces jeux de données sont ensuite utilisés par les services [!DNL Platform] en aval pour mettre à jour les profils client, obtenir des informations grâce à l&#39;apprentissage automatique, etc.

Voici une liste des services en aval qui utilisent des jeux de données pour diverses opérations. Veuillez consulter la documentation de chaque service pour en savoir plus.

* [[!DNL Data Access API]](../../data-access/home.md): Permet d’accéder au contenu des fichiers stockés dans des jeux de données et de le télécharger.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md) : associe les identités des appareils et des systèmes, en liant les jeux de données en fonction des champs d’identité définis par les schémas XDM auxquels ils se conforment.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Exploite  [!DNL Identity Service] pour créer des profils client détaillés à partir de vos jeux de données en temps réel. [!DNL Real-time Customer Profile] extrait les données de  [!DNL Data Lake] et conserve les profils clients dans sa propre banque de données distincte.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md)[!DNL Real-time Customer Profile] : permet de créer des segments et de générer des audiences à partir de vos données Ces audiences peuvent ensuite être exportées vers leurs propres jeux de données dans le [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md) : utilise l’apprentissage automatique et l’intelligence artificielle pour découvrir des insights dans les jeux de données volumineux.
* [Service](../../query-service/home.md) de Requête Adobe Experience Platform : Vous permet d&#39;utiliser SQL standard pour requête des données dans  [!DNL Experience Platform], de joindre tous les jeux de données dans  [!DNL Data Lake] et de capturer les résultats de la requête sous la forme d&#39;un nouveau jeu de données à utiliser dans le rapports,  [!DNL Data Science Workspace]ou  [!DNL Real-time Customer Profile].

## Étapes suivantes

En lisant ce document, vous avez été initié aux principales utilisations des jeux de données dans [!DNL Experience Platform], ainsi qu&#39;aux divers services [!DNL Platform] qui utilisent les jeux de données. Pour plus d&#39;informations sur les nombreuses façons d&#39;utiliser les jeux de données dans [!DNL Platform], veuillez consulter la documentation du service liée dans cet aperçu.

Pour savoir comment interagir avec des jeux de données dans l&#39;interface utilisateur [!DNL Experience Platform], consultez le [guide d&#39;utilisateur des jeux de données](user-guide.md).
