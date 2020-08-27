---
keywords: Experience Platform;home;popular topics;catalog;data protection;encryption data lake
solution: Experience Platform
title: Protection des données dans Adobe Experience Platform
topic: data protection
description: Toutes les données conservées dans le lac de données sont chiffrées, stockées et gérées dans un compte Microsoft Azure Data Lake isolé, propre à votre organisation. Le diagramme de flux de processus suivant illustre comment les données sont ingérées, traitées, chiffrées et conservées par l’Experience Platform.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 37%

---


# Protection des données dans Adobe Experience Platform

All data that is ingested and used by Adobe Experience Platform is stored in the [!DNL Data Lake], a highly granular data store containing all data managed by [!DNL Platform], regardless of origin or file format. All data persisted in the [!DNL Data Lake] is encrypted, stored, and managed in an isolated [!DNL Microsoft Azure Data Lake] Storage account that is unique to your organization.

Le diagramme de flux des processus suivant illustre la manière dont les données sont ingérées, traitées, chiffrées et conservées par [!DNL Experience Platform]:

![](images/data-protection/flow.png)

For details on how data at rest is encrypted in [!DNL Data Lake Storage], see the document on [data encryption in Azure Data Lake Storage](https://docs.microsoft.com/fr-fr/azure/data-lake-store/data-lake-store-encryption). For information on how data at rest is encrypted in [!DNL Cosmos DB], see the document on [data encryption in Azure Cosmos DB](https://docs.microsoft.com/fr-fr/azure/cosmos-db/database-encryption-at-rest).