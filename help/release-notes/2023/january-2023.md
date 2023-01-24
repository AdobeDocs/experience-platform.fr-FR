---
title: Notes de mise à jour de Adobe Experience Platform, janvier 2023
description: Notes de mise à jour de janvier 2023 pour Adobe Experience Platform.
source-git-commit: 01c220147312108649e036d93288823df5389235
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 41%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 25 janvier 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Sources](#sources)

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes et vous permet de structurer, d’étiqueter et d’améliorer ces données à l’aide des services Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| Autoriser l’accès des utilisateurs aux sous-dossiers des sources de stockage dans le cloud | Vous pouvez désormais définir l’accès à un sous-dossier spécifique de votre source de stockage dans le cloud lors de la création d’un compte. Une fois créés, les utilisateurs ne pourront accéder qu’aux données du sous-dossier autorisé. Cette fonctionnalité est disponible pour les sources de stockage dans le cloud suivantes : [Stockage Azure Blob](../../sources/connectors/cloud-storage/blob.md), [Stockage dans le cloud Google](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), et [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilité bêta de [!DNL SugarCRM] | [!DNL SugarCRM] Les sources sont désormais disponibles en version bêta. Utilisez la variable [!DNL SugarCRM Accounts & Contacts] et le [!DNL SugarCRM Events] sources pour importer des données à partir de vos [!DNL SugarCRM] compte à Experience Platform. Pour plus d’informations, reportez-vous à la section [[!DNL SugarCRM] aperçu](../../sources/connectors/crm/sugarcrm.md). |