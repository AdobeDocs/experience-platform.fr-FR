---
keywords: Experience Platform;accueil;rubriques populaires;catalogue;protection des données;chiffrement du lac de données
solution: Experience Platform
title: Protection des données dans Adobe Experience Platform
topic-legacy: data protection
description: Toutes les données conservées dans le lac de données sont chiffrées, stockées et gérées dans un compte Microsoft Azure Data Lake isolé, propre à votre organisation. Le diagramme de flux des processus suivant illustre la manière dont les données sont ingérées, traitées, chiffrées et conservées par Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: ht
source-wordcount: '187'
ht-degree: 100%

---

# Protection des données dans Adobe Experience Platform

Toutes les données ingérées et utilisées par Adobe Experience Platform sont stockées dans [!DNL Data Lake], une banque de données très granulaire contenant toutes les données gérées par [!DNL Platform], quels quʼen soient lʼorigine ou le format. Toutes les données conservées dans [!DNL Data Lake] sont chiffrées, stockées et gérées dans un compte de stockage [!DNL Microsoft Azure Data Lake] isolé, propre à votre organisation.

Le diagramme de flux des processus suivant illustre la manière dont les données sont ingérées, traitées, chiffrées et conservées par [!DNL Experience Platform] :

![](images/data-protection/flow.png)

Pour plus dʼinformations sur la façon dont les données au repos sont chiffrées dans [!DNL Data Lake Storage], reportez-vous au document sur le [chiffrement des données dans Azure Data Lake Storage](https://docs.microsoft.com/fr-fr/azure/data-lake-store/data-lake-store-encryption). Pour plus dʼinformations sur la façon dont les données au repos sont chiffrées dans [!DNL Cosmos DB], reportez-vous au document sur le [chiffrement des données dans Azure Cosmos DB](https://docs.microsoft.com/fr-fr/azure/cosmos-db/database-encryption-at-rest).
