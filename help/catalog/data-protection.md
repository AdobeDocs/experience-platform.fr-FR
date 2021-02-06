---
keywords: Experience Platform ; accueil ; rubriques populaires ; catalogue ; protection des données ; chiffrement des données ; lac
solution: Experience Platform
title: Protection des données au Adobe Experience Platform
topic: data protection
description: Toutes les données conservées dans le lac de données sont chiffrées, stockées et gérées dans un compte Microsoft Azure Data Lake isolé, propre à votre organisation. Le diagramme de flux de processus suivant illustre comment les données sont ingérées, traitées, chiffrées et conservées par l’Experience Platform.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 32%

---


# Protection des données dans Adobe Experience Platform

Toutes les données ingérées et utilisées par Adobe Experience Platform sont stockées dans [!DNL Data Lake], un magasin de données très granulaire contenant toutes les données gérées par [!DNL Platform], quel que soit l&#39;origine ou le format de fichier. Toutes les données conservées dans [!DNL Data Lake] sont chiffrées, stockées et gérées dans un compte d&#39;Enregistrement [!DNL Microsoft Azure Data Lake] isolé qui est unique à votre organisation.

Le diagramme de flux des processus suivant illustre la manière dont les données sont ingérées, traitées, chiffrées et conservées par [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Pour plus d&#39;informations sur la façon dont les données au repos sont chiffrées dans [!DNL Data Lake Storage], consultez le document [cryptage des données dans l&#39;Enregistrement Azure Data Lake](https://docs.microsoft.com/fr-fr/azure/data-lake-store/data-lake-store-encryption). Pour plus d&#39;informations sur la façon dont les données au repos sont chiffrées dans [!DNL Cosmos DB], consultez le document [cryptage des données dans Azure Cosmos DB](https://docs.microsoft.com/fr-fr/azure/cosmos-db/database-encryption-at-rest).