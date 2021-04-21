---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour de l’Experience Platform pour le 21 avril 2021.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: f0350be580394516016373b1754a49951b58e846
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 36%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 21 avril 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, de transformer et de valider des données à partir du modèle de données d’expérience (XDM).

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de la modification du mappage pour les flux de données existants | Vous pouvez maintenant mettre à jour les jeux de correspondances d’un flux de données existant. Vous ne pouvez pas mettre à jour les jeux de mappages pour les flux de données planifiés pour une assimilation unique. Cette fonctionnalité n’est pas prise en charge pour les API HTTP, Adobe Analytics, Adobe Audience Manager et [!DNL Marketo Engage]. Pour plus d&#39;informations, consultez le didacticiel sur la [mise à jour des flux de données sources dans l&#39;interface utilisateur](../../sources/tutorials/ui/update-dataflows.md). |
| Prise en charge de l’assimilation en flux continu | Vous pouvez désormais utiliser les fonctions de prép de données lors de la création d’une connexion source de flux continu. Pour plus d’informations, voir le didacticiel sur la [création d’une connexion source de flux continu dans l’interface utilisateur](../../sources/tutorials/ui/create/streaming/http.md). |

Pour plus d’informations, reportez-vous à la [[!DNL Data Prep] présentation des ](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Le modèle de données d’expérience (XDM) est une spécification open source conçue pour améliorer la puissance des expériences numériques. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En respectant les normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

| Fonctionnalité | Description |
| --- | --- |
| Recommandations schémas par secteur | Lors de la sélection de classes et de mixins dans l’interface utilisateur de l’éditeur de Schémas, vous pouvez utiliser un nouveau filtre pour vue des composants standard recommandés en fonction de votre secteur d’activité spécifique. Voir la documentation sur [les modèles de données du secteur](https://www.adobe.com/go/xdm-industry-erds-en) pour plus d&#39;informations sur la façon dont ces composants se connectent les uns aux autres pour différents cas d&#39;utilisation du secteur. |

## [!DNL Intelligent Services] {#intelligent-services}

Intelligent Services permet aux analystes et spécialistes du marketing d’exploiter la puissance de l’intelligence artificielle et de l’apprentissage automatique dans les cas d’utilisation de l’expérience client. Cela permet aux analystes marketing de configurer des prédictions spécifiques aux besoins d’une société en utilisant des configurations de niveau professionnel sans avoir besoin d’une expertise en sciences des données.

### Customer AI

L’IA du client disponible dans la plate-forme de données client en temps réel est utilisée pour générer des scores de propension personnalisés tels que l’évolution et la conversion pour des profils individuels à l’échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème d’apprentissage automatique ou d’avoir recours à un algorithme, à une formation ou à un déploiement.

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge des données Adobe Analytics | Mise à jour de la fonctionnalité de prise en charge des jeux de données Adobe Analytics via le connecteur source Analytics sans avoir à traiter vos données de manière à les rendre conformes au schéma CEE (Consumer Experience Événement). |
| Prise en charge des données Adobe Audience Manager | Mise à jour de la fonctionnalité de prise en charge des jeux de données Adobe Audience Manager via le connecteur de source d’Audience Manager, sans qu’il soit nécessaire d’ETL pour vos données afin de les rendre conformes au schéma CEE (Consumer Experience Événement). |
| Résumé des performances du modèle | L’IA du client dispose désormais d’un [onglet de résumé des performances du modèle](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) dans la page d’informations de l’instance de service. L&#39;onglet de performances du modèle affiche tous les taux de conversion et d&#39;exécution réels. Cela vous permet de déchiffrer et de comprendre ce qui se passe dans chacun de vos groupes de propension. |

Pour plus d&#39;informations sur les jeux de données pris en charge, consultez la [[!DNL Intelligent Services] documentation sur la préparation des données](../../intelligent-services/data-preparation.md).

### Attribution AI

Attribution AI est utilisé pour attribuer des crédits aux points de contact qui génèrent des événements de conversion. Il peut aider les spécialistes du marketing à quantifier l’impact publicitaire de chaque point de contact marketing sur le parcours client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge des données Adobe Analytics | Mise à jour de la fonctionnalité de prise en charge des jeux de données Adobe Analytics via le connecteur source Analytics sans avoir à traiter vos données de manière à les rendre conformes au schéma CEE (Consumer Experience Événement). |

Pour plus d&#39;informations sur les jeux de données pris en charge, consultez la [[!DNL Intelligent Services] documentation sur la préparation des données](../../intelligent-services/data-preparation.md).

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données [!DNL Real-time Customer Profile]. Ces segments sont configurés et conservés de manière centralisée sur Platform, ce qui les rend facilement accessibles depuis n’importe quelle application Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Fonctions d&#39;agrégation supplémentaires | Des fonctions de décompte ont été ajoutées dans le créateur de segments. Les fonctions Compter vous permettent de comptabiliser le nombre de fois où le événement spécifié a été exécuté. Pour plus d&#39;informations sur les fonctions de décompte, consultez la section des fonctions de décompte du [guide du Créateur de segments](../../segmentation/ui/segment-builder.md#count-functions). |

Pour plus d&#39;informations sur [!DNL Segmentation Service], consultez l&#39;[Présentation de la segmentation](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| ------- | ----------- |
| [!DNL Marketo Engage] (bêta) | Vous pouvez désormais créer une connexion source [!DNL Marketo Engage] à l’aide de l’interface utilisateur pour apporter des données B2B à la plate-forme et garder ces données à jour à l’aide d’applications connectées à la plate-forme. Pour plus d&#39;informations, consultez la [[!DNL Marketo Engage] documentation du connecteur source](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Sources bêta passant à GA | Les sources suivantes ont été promues de la version bêta à la version GA : <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
