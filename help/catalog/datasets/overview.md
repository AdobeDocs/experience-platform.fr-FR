---
keywords: Experience Platform;accueil;rubriques les plus consultées;emplacement des données;emplacement des données;gestion des données;gestion des données;traçabilité;traçabilité;type de données;types de données;type de données
solution: Experience Platform
title: Présentation des jeux de données
description: Ce document présente de manière générale les jeux de données dans Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 100%

---

# Présentation des jeux de données

Toutes les données correctement ingérées par Adobe Experience Platform sont conservées sous forme de jeux de données dans le [!DNL Data Lake]. Un jeu de données est une structure de stockage et de gestion pour la collecte de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées.

Ce document présente de manière générale les jeux de données dans [!DNL Experience Platform].

## Créer des jeux de données et suivre des métadonnées

[!DNL Catalog Service] est le système d’enregistrement pour l’emplacement et la traçabilité des données dans [!DNL Experience Platform]. Il sert à créer et à gérer les jeux de données. [!DNL Catalog] suit les métadonnées de chaque jeu de données, ce qui inclut une référence au schéma [!DNL Experience Data Model] (XDM) auquel le jeu de données se conforme (expliqué dans la section suivante) et le nombre d’enregistrements ingérés par ce jeu de données.

Pour plus d’informations, consultez la [présentation du service de catalogue](../home.md).

## Application de contraintes aix données des jeux de données

[!DNL Experience Data Model] (XDM) constitue le cadre normalisé à partir duquel [!DNL Platform] organise les données d’expérience client. Toutes les données ingérées par [!DNL Platform] doivent être conformes à un schéma XDM prédéfini avant de pouvoir être conservées sous la forme d’un jeu de données dans le [!DNL Data Lake].

Tous les jeux de données contiennent une référence au schéma XDM qui limite le format et la structure des données qui peuvent être stockées. Toute tentative de chargement de données vers un jeu de données non conforme à son schéma XDM entraînera l’échec de l’ingestion.

Pour plus d’informations sur XDM, consultez la [présentation du système XDM](../../xdm/home.md).

## Ingestion de données par les jeux de données

Adobe Experience Platform Data Ingestion représente les différentes méthodes par lesquelles [!DNL Platform] ingère les données de diverses sources. Quelle que soit la méthode d’ingestion, toutes les données ingérées sont converties en fichiers de lot. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. Ces fichiers de lot sont ensuite ajoutés aux jeux de données dédiés et conservés dans le [!DNL Data Lake].

Pour plus d’informations, consultez la [présentation de Data Ingestion](../../ingestion/home.md).

## Application de libellés d’utilisation aux jeux de données

La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Le cadre de gouvernance des données vous permet d’appliquer des étiquettes d’utilisation pour classer les données en fonction des politiques d’utilisation qui s’appliquent à ces données.

>[!IMPORTANT]
>
>L’application de libellés au niveau du jeu de données est uniquement prise en charge pour les cas d’utilisation de la gouvernance des données. Si vous essayez de créer des politiques d’accès pour les données, vous devez [appliquer des libellés au schéma](../../xdm/tutorials/labels.md) sur lequel le jeu de données est basé. Consultez la présentation du [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md) pour plus d’informations.

Les libellés d’utilisation des données peuvent être appliqués à des jeux de données entiers ou à des champs de jeu de données individuels. Les libellés ajoutés au niveau du jeu de données sont hérités par tous les champs du jeu de données.

Pour plus d’informations sur ce service, consultez la [présentation de la gouvernance des données](../../data-governance/home.md). Pour savoir comment utiliser les étiquettes d’utilisation dans [!DNL Platform], reportez-vous aux guides suivants :

* [Gérer les libellés dans l’interface utilisateur](../../data-governance/labels/user-guide.md)
* [Gérer les étiquettes de jeux de données dans l’API](../../data-governance/labels/dataset-api.md)

## Jeux de données dans les services [!DNL Platform] en aval

Une fois que les jeux de données ont été utilisés pour stocker les données ingérées, ils sont utilisés par les services [!DNL Platform] en aval pour mettre à jour les profils clients, obtenir des insights grâce au machine learning, etc.

Voici une liste des services en aval qui utilisent des jeux de données pour diverses opérations. Veuillez consulter la documentation de chaque service pour en savoir plus.

* [[!DNL Data Access API]](../../data-access/home.md) : vous permet d’accéder au contenu des fichiers stockés dans les jeux de données et de le télécharger.
* [Service Adobe Experience Platform Identity](../../identity-service/home.md) : associe les identités des appareils et des systèmes, en liant les jeux de données en fonction des champs d’identité définis par les schémas XDM auxquels ils se conforment.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md) : tire parti de [!DNL Identity Service] pour créer des profils client détaillés à partir de vos jeux de données en temps réel. [!DNL Real-Time Customer Profile] extrait les données du [!DNL Data Lake] et conserve les profils clients dans sa propre banque de données distincte.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) : permet de créer des segments et de générer des audiences à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences peuvent ensuite être exportées vers leurs propres jeux de données dans le [!DNL Data Lake].
* [Espace de travail de science des données d’Adobe Experience Platform](../../data-science-workspace/home.md) : utilise le machine learning et l’intelligence artificielle pour découvrir des insights dans les jeux de données volumineux.
* [Adobe Experience Platform Query Service](../../query-service/home.md) : vous permet d’utiliser une requête SQL standard pour interroger les données dans [!DNL Experience Platform]. Il peut joindre n’importe quel jeu de données dans le [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser pour le reporting, [!DNL Data Science Workspace], ou [!DNL Real-Time Customer Profile].
* [Service de destinations d’Adobe Experience Platform](../../destinations/home.md) : vous permet d’[exporter des jeux de données](/help/destinations/ui/export-datasets.md) vers les destinations de stockage dans le cloud ou de marketing par e-mail de votre choix, pour les activités de création de rapports ou de science des données.

## Étapes suivantes

En lisant ce document, vous avez découvert les principales utilisations des jeux de données dans [!DNL Experience Platform], ainsi que les différents services de [!DNL Platform] qui utilisent les jeux de données. Pour plus d’informations sur les nombreuses façons dont les jeux de données sont utilisés dans [!DNL Platform], consultez les liens vers la documentation des services.

Pour savoir comment interagir avec les jeux de données dans l’interface utilisateur de [!DNL Experience Platform], consultez le [guide d’utilisation des jeux de données](user-guide.md).
