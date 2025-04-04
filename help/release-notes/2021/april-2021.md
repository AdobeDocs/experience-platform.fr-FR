---
title: Notes de mise à jour d’Adobe Experience Platform - Avril 2021
description: Les notes de mise à jour d’avril 2021 pour Adobe Experience Platform.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 89%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 21 avril 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de la modification du mappage pour les flux de données existants | Vous pouvez maintenant mettre à jour les jeux de mappages d’un flux de données existant. Vous ne pouvez pas mettre à jour les jeux de mappages pour les flux de données planifiés pour une ingestion unique. Cette fonctionnalité n’est pas prise en charge pour les API HTTP, Adobe Analytics, Adobe Audience Manager et [!DNL Marketo Engage]. Pour plus d’informations, consultez le tutoriel sur la [mise à jour des flux de données source dans l’interface utilisateur](../../sources/tutorials/ui/update-dataflows.md). |
| Prise en charge de l’ingestion par flux | Vous pouvez désormais utiliser les fonctions de préparation de données lors de la création d’une connexion source par flux. Pour plus d’informations, consultez le tutoriel sur la [création d’une connexion source par flux dans l’interface utilisateur](../../sources/tutorials/ui/create/streaming/http.md). |

Pour plus d’informations, reportez-vous à la [[!DNL Data Prep] présentation](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Le modèle de données d’expérience (XDM) est une spécification open source conçue pour améliorer la puissance des expériences digitales. Il fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

| Fonctionnalité | Description |
| --- | --- |
| Recommandations de schémas par secteur | Lors de la sélection de classes et de groupes de champs de schéma dans l’interface utilisateur de l’éditeur de schémas, vous pouvez utiliser un nouveau filtre pour afficher les composants standard recommandés en fonction de votre secteur d’activité spécifique. Pour plus d’informations sur la manière dont ces composants sont liés les uns aux autres pour différents cas d’utilisation du secteur, consultez la documentation sur les [modèles de données du secteur](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/industries/overview.html?lang=fr). |

## [!DNL Intelligent Services] {#intelligent-services}

Intelligent Services permet aux analystes et spécialistes du marketing d’exploiter la puissance de l’intelligence artificielle et du machine learning dans les cas d’utilisation de l’expérience client. Les analystes marketing peuvent obtenir des prédictions spécifiques aux besoins d’une entreprise en utilisant des configurations au niveau de l’entreprise sans avoir besoin d’expertise en sciences des données.

### Customer AI

L’IA dédiée aux clients disponible dans Real-Time Customer Data Platform est utilisée pour générer des scores de propension personnalisés tels que l’attrition et la conversion pour des profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème de machine learning ou d’avoir recours à un algorithme, à une formation ou à un déploiement.

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge des données Adobe Analytics | Mise à jour de la fonctionnalité afin de prendre en charge les jeux de données Adobe Analytics via le connecteur source Analytics sans avoir à utiliser ETL pour vos données afin de se conformer au schéma d’événement d’expérience client (CEE). |
| Prise en charge des données Adobe Audience Manager | Mise à jour de la fonctionnalité afin de prendre en charge les jeux de données Adobe Audience Manager via le connecteur source Audience Manager sans avoir à utiliser ETL pour vos données afin de se conformer au schéma d’événement d’expérience client (CEE). |
| Résumé des performances du modèle | Customer AI dispose désormais d’un [onglet de résumé des performances du modèle](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) dans la page d’informations de l’instance de service. L’onglet des performances du modèle affiche tous les taux de conversion et d’attrition réels. Vous pouvez ainsi déchiffrer et comprendre ce qui se passe dans chacun de vos compartiments de propension. |

Pour plus d’informations sur les jeux de données pris en charge, consultez la [[!DNL Intelligent Services] documentation sur la préparation des données](../../intelligent-services/data-preparation.md).

### Attribution AI

L’IA dédiée à l’attribution est utilisée pour attribuer des crédits aux points de contact qui génèrent des événements de conversion. Il peut aider les spécialistes du marketing à quantifier l’impact publicitaire de chaque point de contact marketing sur le parcours client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge des données Adobe Analytics | Mise à jour de la fonctionnalité afin de prendre en charge les jeux de données Adobe Analytics via le connecteur source Analytics sans avoir à utiliser ETL pour vos données afin de se conformer au schéma d’événement d’expérience client (CEE). |

Pour plus d’informations sur les jeux de données pris en charge, consultez la [[!DNL Intelligent Services] documentation sur la préparation des données](../../intelligent-services/data-preparation.md).

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service propose une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir des données [!DNL Real-Time Customer Profile]. Ces segments sont configurés et conservés de manière centralisée sur Experience Platform, ce qui les rend facilement accessibles depuis n’importe quelle application Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Fonctions d’agrégation supplémentaires | Des fonctions de comptage ont été ajoutées dans le créateur de segments. Les fonctions de comptage permettent de compter le nombre de fois où l’événement spécifié a été exécuté. Vous trouverez plus d’informations sur les fonctions de comptage dans la section des fonctions de comptage du [guide du créateur de segments](../../segmentation/ui/segment-builder.md#count-functions). |

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| ------- | ----------- |
| [!DNL Marketo Engage] (version bêta) | Vous pouvez désormais créer une connexion source [!DNL Marketo Engage] à l’aide de l’interface utilisateur pour importer les données B2B vers Experience Platform et maintenir ces données à jour à l’aide d’applications connectées à Experience Platform. Pour plus d’informations, voir la [[!DNL Marketo Engage] documentation des connecteurs source](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Sources bêta passant à la version générale | Les sources suivantes ont été promues de la version bêta à la version générale : <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
