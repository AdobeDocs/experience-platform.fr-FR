---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 11 décembre 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 67%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 11 décembre 2019**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[ !Service de segmentation DNL]](#segmentation)
* [[ !Service de prise de décision DNL]](#decisioning)
* [[ !Sources DNL]](#sources)
* [[ ! Système de modèle de données d’expérience DNL (XDM)]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service provides a user interface and RESTful API that allows you to build segments and generate audiences from your [!DNL Real-time Customer Profile] data. These segments are centrally configured and maintained on [!DNL Platform], making them readily accessible by any Adobe application.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Onglet Audiences fusionnées dans [!DNL Segment Builder] | The [!UICONTROL _Segments_] and [!UICONTROL _Audiences_] tabs in the [!DNL Segment Builder] have been combined into a single [!UICONTROL _Audiences_] tab. Cet onglet vous permet de parcourir et de rechercher les audiences existantes, que vous pouvez ensuite faire glisser dans le canevas du créateur de règles pour créer une nouvelle définition de segment. En référençant une audience, il est possible d’ajouter l’un des jeux de logiques de règles suivants à la nouvelle définition de segment : l’appartenance à l’audience en tant que règle, le jeu complet de la logique de règle qui a défini l’audience référencée. |
| Nouvel emplacement du sélecteur de stratégie de fusion | The location of the merge policy selector in the [!DNL Segment Builder] has been changed. Pour sélectionner une stratégie de fusion pour une définition de segment, cliquez sur l’icône en forme d’engrenage dans l’onglet [!UICONTROL _Champs_], puis utilisez le menu déroulant _[!UICONTROL Stratégie de fusion]_ pour sélectionner la stratégie de fusion à utiliser. |

**Problèmes connus**

* Aucun

Pour plus d’informations, reportez-vous à la [présentation de Segmentation Service](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] provides the ability to programmatically and intelligently select the &quot;Next Best Experience&quot; from a set of available options for a given individual, deliver them to any channel or application, and perform reporting and analysis.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Fonctions de classement | L’ordre des offres pour les profils est désormais établi au moyen d’une fonction de classement, plutôt que d’un ensemble défini d’offres pour tous les profils. |

**Problèmes connus**

* Aucun.

Consultez la [présentation du service de prise de décision](../../decisioning-service/home.md) pour en apprendre davantage sur ce service.

## [!DNL Sources] {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les solutions Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier auprès de vos services de gestion de la relation client et de vos systèmes de stockage, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ---------- | ------------ |
| Connexion en continu | Streaming ingestion enables you to send data from client- and server-side devices to [!DNL Experience Platform] in real-time. La version comprend une nouvelle interface utilisateur pour la connexion en continu. |
| Prise en charge du connecteur pour [!DNL Google Cloud Store] | Support for collecting data from [!DNL Google Cloud Store]. |

**Problèmes connus**

* Aucun.

Pour plus d’informations sur les sources, consultez la [présentation des sources](../../sources/home.md).

## [!DNL Experience Data Model] Système (XDM) {#xdm}

Standardization and interoperability are key concepts behind [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), piloté par l’Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Amélioration de la validation des schémas | Nouvelles vérifications pour s’assurer que les références renvoient à des champs supplémentaires comme prévu. Ajout de vérifications supplémentaires aux champs définis comme un tableau d’objets pour s’assurer que les objets sont bien définis. Amélioration des messages d’erreur pour aider à identifier et à résoudre les problèmes. |

**Corrections de bogues**

* Maintenance et améliorations relatives au contrôle d’accès et aux environnements de test.
* Prise en charge de l’`eTag` pour le point de terminaison `/descriptors` dans l’API [!DNL Schema Registry]

**Problèmes connus**

* Aucun

To learn more about working with XDM using the [!DNL Schema Registry] API and [!DNL Schema Editor] user interface, please read the [XDM System documentation](../../xdm/home.md).