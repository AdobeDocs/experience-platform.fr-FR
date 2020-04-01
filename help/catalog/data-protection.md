---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Protection des données dans Adobe Experience Platform
topic: data protection
translation-type: tm+mt
source-git-commit: edf7cef0991ceef0465d5c1d750bd1885754f716

---


# Protection des données dans Adobe Experience Platform

Toutes les données ingérées et utilisées par Adobe Experience Platform sont stockées dans Data Lake, une banque de données très granulaire contenant toutes les données gérées par Platform, quel que soit le   ou le format de fichier. Toutes les données conservées dans Data Lake sont chiffrées, stockées et gérées dans un compte de Microsoft Azure Data Lake  isolé qui est unique à votre organisation.

Le diagramme de flux de processus suivant illustre la manière dont les données sont assimilées, traitées, chiffrées et conservées par la plateforme d’expérience :

![](images/data-protection/flow.png)

Pour plus d&#39;informations sur la façon dont les données au repos sont chiffrées dans le Data Lake  , reportez-vous au sur le chiffrement des [données dans le](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)Azure Data Lake. Pour plus d&#39;informations sur la façon dont les données au repos sont chiffrées dans la base de données Cosmos, consultez le  sur le chiffrement [des données dans la base de données](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)Azure Cosmos.