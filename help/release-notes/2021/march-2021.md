---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour de l’Experience Platform pour le 31 mars 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 8d4270d9168a570fcf92ba60d70dbc8e9af98136
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 50%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 31 mars 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Les mises à jour suivantes concernant les sources sont incluses dans la version de l’Experience Platform de mars 2021 :

| Fonctionnalité | Description |
| ------- | ----------- |
| Sources bêta passant à GA | Les sources suivantes ont été promues de la version bêta à la version GA : <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Prise en charge des API pour l’assimilation de fichiers compressés | Vous pouvez désormais prévisualisation et assimiler des fichiers JSON compressés ou délimités à l’aide de sources d’enregistrement cloud. Pour plus d&#39;informations, consultez le didacticiel sur la [collecte de données d&#39;enregistrement cloud à l&#39;aide d&#39;API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Prise en charge de l’interface utilisateur pour le téléchargement de fichiers récursif | Vous pouvez désormais ingérer des dossiers entiers de manière récursive lors de l’utilisation d’une source d’enregistrement Cloud. Lors de l’importation d’un dossier entier, vous devez vous assurer que son contenu partage le même schéma. Pour plus d’informations, voir le didacticiel sur la [configuration d’un flux de données pour les connecteurs d’enregistrement cloud dans l’interface utilisateur](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
