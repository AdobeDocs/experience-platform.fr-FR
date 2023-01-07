---
title: Chiffrement des données dans Adobe Experience Platform
description: Découvrez comment les données sont chiffrées en transit et au repos dans Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 5%

---

# Cryptage des données dans Adobe Experience Platform

Adobe Experience Platform est un système puissant et extensible qui centralise et normalise les données d’expérience client dans les solutions d’entreprise. Toutes les données utilisées par Platform sont chiffrées en transit et au repos pour préserver la sécurité de vos données. Ce document décrit les processus de cryptage de Platform à un niveau élevé.

Le diagramme de flux de processus suivant illustre la manière dont les données sont ingérées, chiffrées et conservées par [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## Données en transit {#in-transit}

Toutes les données en transit entre Platform et tout composant externe sont effectuées sur des connexions sécurisées et cryptées à l’aide de HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

En règle générale, les données sont introduites dans Platform de trois façons :

* [Collecte de données](../../collection/home.md) Les fonctionnalités permettent aux sites web et aux applications mobiles d’envoyer des données à Platform Edge Network pour l’évaluation et la préparation à l’ingestion.
* [Connecteurs source](../../sources/home.md) diffuser des données directement vers Platform à partir d’applications Adobe Experience Cloud et d’autres sources de données d’entreprise ;
* Les outils ETL (extraction, transformation, chargement) non Adobes envoient des données à la variable [API d’ingestion par lots](../../ingestion/batch-ingestion/overview.md) pour la consommation.

Une fois les données introduites dans le système et [encrypted au repos](#at-rest), il peut ensuite être enrichi par les services Platform et sorti du système des manières suivantes :

* [Destinations](../../destinations/home.md) vous permettent d’activer les données pour Adobe des applications et des applications partenaires.
* Applications de plateforme natives telles que [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=fr) et [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=fr) peut également utiliser les données.

## Données au repos {#at-rest}

Les données ingérées et utilisées par Platform sont stockées dans le lac de données, un entrepôt de données hautement granulaire contenant toutes les données gérées par le système, indépendamment de l’origine ou du format de fichier. Toutes les données conservées dans le lac de données sont chiffrées, stockées et gérées dans un environnement isolé. [[!DNL Microsoft Azure Data Lake] Stockage](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) qui est propre à votre organisation.

Pour plus d’informations sur la façon dont les données au repos sont chiffrées dans Azure Data Lake Storage, reportez-vous à la section [documentation Azure officielle](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Étapes suivantes

Ce document fournit un aperçu général de la manière dont les données sont chiffrées dans Platform. Pour plus d’informations sur les procédures de sécurité dans Platform, consultez la présentation de [gouvernance, confidentialité et sécurité](./overview.md) sur l’Experience League ou consultez le [Livre blanc sur la sécurité de Platform](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
