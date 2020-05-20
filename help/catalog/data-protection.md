---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Protection des données dans Adobe Experience Platform
topic: data protection
translation-type: tm+mt
source-git-commit: edf7cef0991ceef0465d5c1d750bd1885754f716
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Protection des données dans Adobe Experience Platform

Toutes les données ingérées et utilisées par Adobe Experience Platform sont stockées dans Data Lake, un magasin de données très granulaire contenant toutes les données gérées par Platform, quel que soit l’origine ou le format de fichier. Toutes les données conservées dans Data Lake sont chiffrées, stockées et gérées dans un compte d&#39;Enregistrement Microsoft Azure Data Lake isolé qui est unique à votre organisation.

Le diagramme de flux de processus suivant illustre comment les données sont ingérées, traitées, chiffrées et conservées par la plateforme d’expérience :

![](images/data-protection/flow.png)

Pour plus d&#39;informations sur la façon dont les données au repos sont chiffrées dans l&#39;Enregistrement Data Lake, consultez le document sur le chiffrement [des données dans l&#39;Enregistrement](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)Azure Data Lake. Pour plus d&#39;informations sur la façon dont les données au repos sont chiffrées dans la base de données Cosmos, consultez le document sur le chiffrement [des données dans la base de données](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)Azure Cosmos.