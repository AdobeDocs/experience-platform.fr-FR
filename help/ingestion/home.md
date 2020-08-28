---
keywords: Experience Platform;home;popular topics;data ingestion;data location;Data Location;Data management;data management;Lineage;lineage;batch;Batch;ingested data
solution: Experience Platform
title: Présentation d’Adobe Experience Platform Data Ingestion
topic: overview
description: Ce document présente les trois principales manières dont les données sont ingérées dans Platform, avec des liens vers leur documentation de présentation respectives pour plus d’informations.
translation-type: tm+mt
source-git-commit: 6e4a3ebe84c82790f58f8ec54e6f72c2aca0b7da
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 55%

---


# Présentation de Data Ingestion

Adobe Experience Platform rassemble des données provenant de plusieurs sources afin d’aider les professionnels du marketing à mieux comprendre le comportement de leurs clients. Adobe Experience Platform Data Ingestion represents the multiple methods by which [!DNL Platform] ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream [!DNL Platform] services.

This document introduces the three main ways in which data is ingested into [!DNL Platform], with links to their respective overview documentation for more detailed information.

## Ingestion par lots

Batch ingestion allows you to ingest data into [!DNL Experience Platform] as batch files. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. Une fois ingérés, les lots fournissent des métadonnées qui décrivent le nombre d’enregistrements correctement ingérés ainsi que les enregistrements ayant échoué et les messages d’erreur associés.

Les fichiers de données chargés manuellement, tels que les fichiers CSV plats (mappés à des schémas XDM) et les cadres de données Parquet, doivent être ingérés à l’aide de cette méthode.

Pour plus d’informations, consultez la [présentation de l’ingestion par lots](./batch-ingestion/overview.md).

## Ingestion par flux

Streaming ingestion allows you to send data from client- and server-side devices to [!DNL Experience Platform] in real-time. [!DNL Platform] prend en charge l’utilisation des entrées de données pour diffuser des données d’expérience entrantes, qui sont conservées dans les jeux de données activés dans le flux au sein du lac de données. Les entrées de données peuvent être configurées pour authentifier automatiquement les données qu’elles collectent, en veillant à ce que celles-ci proviennent d’une source approuvée.

Pour plus d’informations, consultez la [présentation de l’ingestion par flux](./streaming-ingestion/overview.md).

## Sources

[!DNL Experience Platform] vous permet de configurer des connexions source à différents fournisseurs de données. Ces connexions vous permettent de vous authentifier auprès de vos sources données externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Source connections can be configured to gather data from other Adobe applications (such as Adobe Analytics and Adobe Audience Manager), third-party cloud storage sources (such as [!DNL Azure Blob], [!DNL Amazon] S3, FTP servers, and SFTP servers), and third-party CRM systems (such as [!DNL Microsoft Dynamics] and [!DNL Salesforce]).

Pour plus d’informations, consultez la [présentation des sources](../sources/home.md).

## Étapes suivantes et ressources supplémentaires

This document provided a brief introduction to the different aspects of [!DNL Data Ingestion] in [!DNL Experience Platform]. Poursuivez votre lecture de la documentation de présentation de chaque méthode d’ingestion pour vous familiariser avec leurs différentes capacités, les cas d’utilisation et les bonnes pratiques. Vous pouvez également compléter votre apprentissage en regardant la vidéo de présentation de l&#39;ingestion ci-dessous. For information on how [!DNL Experience Platform] tracks the metadata for ingested records, see the [Catalog Service overview](../catalog/home.md).

>[!WARNING]
>
>Le terme &quot;Profil unifié&quot; utilisé dans la vidéo suivante est obsolète. Les termes [!DNL "Profile"] ou [!DNL "Real-time Customer Profile"] sont les termes appropriés utilisés dans la [!DNL Experience Platform] documentation. Reportez-vous à la documentation pour connaître les dernières fonctionnalités.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)