---
title: Notes de mise à jour d’Adobe Experience Platform - Mars 2021
description: Les notes de mise à jour de mars 2021 pour Adobe Experience Platform.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
TQID: https://experienceleague.adobe.com/0-UPlENYqshMrkvXJGmmD9SKe9rZyfogpSd9yv7PFQU
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2: id: b784da9a-7978-4766-bf1f-5ab2b23d894aid: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342id: d1823595-9241-4128-8a33-e4ac3bf08773id: fe06da76-5b92-43de-9bda-c5c9c01b55e8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 433
ht-degree: 94%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 31 mars 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

| Fonctionnalité | Description |
| ------- | ----------- |
| Fonction `add_to_array` | Mise à jour de la fonctionnalité pour la prise en charge des tableaux en tant que paramètre. |
| Fonction `to_array` | Mise à jour de la fonctionnalité pour la prise en charge des objets en tant que paramètre. |

Pour plus d’informations, reportez-vous à la [[!DNL Data Prep] présentation](../../data-prep/home.md).

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service propose une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir des données [!DNL Real-Time Customer Profile]. Ces segments sont configurés et conservés de manière centralisée sur [!DNL Experience Platform], ce qui les rend facilement accessibles depuis n’importe quelle application Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| (Beta) Segmentation Edge | La segmentation Edge évalue les segments en temps réel, ce qui permet d’utiliser les cas de personnalisation de la même page et de la page suivante. Vous trouverez plus d’informations sur la segmentation Edge dans la [présentation de l’interface utilisateur de segmentation](../../segmentation/ui/overview.md). |
| (Beta) Segmentation incrémentielle | Augmente jusqu’à une heure l’actualisation des définitions de segment existantes évaluées dans la segmentation par lots. |

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| ------- | ----------- |
| Sources Beta passant à la version générale | Les sources suivantes ont été promues de la version Beta à la version générale : <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Prise en charge des API pour l’ingestion de fichiers compressés | Vous pouvez désormais prévisualiser et ingérer des fichiers JSON compressés ou délimités à l’aide de sources de stockage dans le cloud. Pour plus d’informations, consultez le tutoriel sur la [collecte de données de stockage dans le cloud à l’aide d’API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Prise en charge de l’interface utilisateur pour le téléchargement de fichiers récursifs | Vous pouvez désormais ingérer des dossiers entiers de manière récursive lors de l’utilisation d’une source de stockage dans le cloud. Lors de l’ingestion d’un dossier entier, vous devez vous assurer que son contenu partage le même schéma. Pour plus d’informations, consultez le tutoriel sur la [configuration d’un flux de données pour les connecteurs de stockage dans le cloud dans l’interface utilisateur](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
