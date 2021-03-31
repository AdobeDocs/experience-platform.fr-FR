---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour de l’Experience Platform pour le 31 mars 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 58382528cc787e8d2005c8c322904266880ad0b9
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 47%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 31 mars 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Sandboxes]](#sandboxes)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, de transformer et de valider des données à partir du modèle de données d’expérience (XDM).

| Fonctionnalité | Description |
| ------- | ----------- |
| `add_to_array` fonction | Mise à jour de la fonctionnalité de prise en charge des tableaux en tant que paramètre. |
| `to_array` fonction | Mise à jour de la fonctionnalité de prise en charge des objets en tant que paramètre. |

Pour plus d’informations, reportez-vous à la [[!DNL Data Prep] présentation des ](../../data-prep/home.md).

## [!DNL Sandboxes] {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience numérique à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience numérique en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

Pour répondre à ce besoin, Experience Platform fournit des environnements de test qui divisent une instance unique de Platform en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

| Fonctionnalité | Description |
| ------- | ----------- |
| (bêta) plusieurs sandbox de production | Vous pouvez désormais créer et gérer plusieurs sandbox de production dans votre organisation IMS et dédier des sandbox de production spécifiques à des secteurs d’activité, des marques, des projets ou des régions distincts. Pour plus d’informations, consultez les didacticiels relatifs à la création d’un sandbox de production [dans l’interface utilisateur](../../sandboxes/ui/user-guide.md) ou [à l’aide de l’API](../../sandboxes/api/create-sandbox.md). |

Pour plus d’informations sur les environnements de test, consultez la [présentation des environnements de test](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données [!DNL Real-time Customer Profile]. Ces segments sont configurés et gérés de manière centralisée sur [!DNL Platform], ce qui les rend facilement accessibles par toute application d&#39;Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| (bêta) Segmentation Edge | La segmentation Edge évalue les segments en temps réel, ce qui permet d’utiliser les mêmes cas de personnalisation de page et de page suivante. Vous trouverez plus d’informations sur la segmentation des arêtes dans le [Présentation de l’interface utilisateur de segmentation](../../segmentation/ui/overview.md). |
| (bêta) Segmentation incrémentielle | Augmente la fraîcheur des définitions de segment existantes évaluées dans la segmentation par lots jusqu’à une heure. |

Pour plus d&#39;informations sur [!DNL Segmentation Service], consultez l&#39;[Présentation de la segmentation](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| ------- | ----------- |
| Sources bêta passant à GA | Les sources suivantes ont été promues de la version bêta à la version GA : <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Prise en charge des API pour l’assimilation de fichiers compressés | Vous pouvez désormais prévisualisation et assimiler des fichiers JSON compressés ou délimités à l’aide de sources d’enregistrement cloud. Pour plus d&#39;informations, consultez le didacticiel sur la [collecte de données d&#39;enregistrement cloud à l&#39;aide d&#39;API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Prise en charge de l’interface utilisateur pour le téléchargement de fichiers récursif | Vous pouvez désormais ingérer des dossiers entiers de manière récursive lors de l’utilisation d’une source d’enregistrement Cloud. Lors de l’importation d’un dossier entier, vous devez vous assurer que son contenu partage le même schéma. Pour plus d’informations, voir le didacticiel sur la [configuration d’un flux de données pour les connecteurs d’enregistrement cloud dans l’interface utilisateur](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
