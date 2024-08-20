---
keywords: Experience Platform;accueil;rubriques populaires;ingestion des données;emplacement des données;Emplacement Des Données;Gestion des données;gestion des données;Traçabilité;traçabilité;lot;Lot;données ingérées
solution: Experience Platform
title: Présentation de Data Ingestion
description: Ce document présente les trois principales manières dont les données sont ingérées dans Platform, avec des liens vers leur documentation de présentation respectives pour plus d’informations.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: 15de9351203f6b43653042ab73ede17781486160
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 66%

---

# Présentation de Data Ingestion

Adobe Experience Platform rassemble des données provenant de plusieurs sources afin d’aider les spécialistes marketing à mieux comprendre le comportement de leurs clients. Adobe Experience Platform Data Ingestion représente les multiples méthodes par lesquelles Experience Platform ingère des données à partir de ces sources, ainsi que la manière dont ces données sont conservées dans le lac de données pour être utilisées par les services Experience Platform en aval.

Ce document présente les trois principales manières dont les données sont ingérées dans Experience Platform, avec des liens vers la documentation de présentation correspondante pour plus d’informations.

## Ingestion par lots

Lʼingestion par lots vous permet dʼingérer des données dans [!DNL Experience Platform] sous forme de fichiers de lots. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. Une fois ingérés, les lots fournissent des métadonnées qui décrivent le nombre d’enregistrements correctement ingérés ainsi que les enregistrements ayant échoué et les messages d’erreur associés.

Les fichiers de données chargés manuellement, tels que les fichiers CSV plats (mappés à des schémas XDM) et les cadres de données Parquet, doivent être ingérés à l’aide de cette méthode.

Pour plus d’informations, consultez la [présentation de l’ingestion par lots](./batch-ingestion/overview.md).

>[!TIP]
>
>Utilisez le format JSON à une seule ligne au lieu du format JSON à plusieurs lignes comme entrée pour l’ingestion par lots. Le format JSON à une seule ligne permet de meilleures performances, car le système peut diviser un fichier d’entrée en plusieurs blocs et les traiter en parallèle, tandis que le format JSON à plusieurs lignes ne peut pas être divisé. Cela peut réduire considérablement les coûts de traitement des données et améliorer la latence du traitement par lots.

## Ingestion en flux continu

Lʼingestion par flux vous permet dʼenvoyer en temps réel des données provenant des appareils côté client et serveur vers [!DNL Experience Platform] Experience Platform prend en charge l’utilisation d’entrées de données pour diffuser des données d’expérience entrantes, qui sont conservées dans les jeux de données activés pour la diffusion en continu dans le lac de données. Les entrées de données peuvent être configurées pour authentifier automatiquement les données qu’elles collectent, en veillant à ce que celles-ci proviennent d’une source approuvée.

Pour plus d’informations, consultez la [présentation de l’ingestion par flux](./streaming-ingestion/overview.md).

## Sources

[!DNL Experience Platform] vous permet de configurer des connexions source à différents fournisseurs de données. Ces connexions vous permettent de vous authentifier auprès de vos sources données externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Les connexions source peuvent être configurées pour collecter les données dʼautres applications Adobe (telles quʼAdobe Analytics et Adobe Audience Manager), de sources tierces de stockage dans le cloud (telles quʼ[!DNL Azure Blob], [!DNL Amazon]S3, serveurs FTP et SFTP) et de systèmes de gestion de la relation client tiers (tels que [!DNL Microsoft Dynamics] et [!DNL Salesforce]).

Pour plus d’informations, consultez la [présentation des sources](../sources/home.md).

### Création de schéma assisté ML {#ml-assisted-schema-creation}

Pour intégrer rapidement de nouvelles sources de données, vous pouvez désormais utiliser des algorithmes d’apprentissage automatique afin de générer un schéma à partir de données d’exemple. Cette automatisation simplifie la création de schémas précis, réduit les erreurs et accélère le processus, de la collecte de données à l’analyse et aux informations.

Pour plus d’informations sur ce processus, consultez le [guide de création de schéma assisté par ML](../xdm/ui/ml-assisted-schema-creation.md) .

## Étapes suivantes et ressources supplémentaires

Ce document vous a présenté brièvement les différents aspects de [!DNL Data Ingestion] dans [!DNL Experience Platform]. Poursuivez votre lecture de la documentation de présentation de chaque méthode d’ingestion pour vous familiariser avec leurs différentes capacités, les cas d’utilisation et les bonnes pratiques. Vous pouvez également compléter votre apprentissage en regardant la vidéo de présentation de lʼingestion ci-dessous. Pour en savoir plus sur la manière dont [!DNL Experience Platform] suit les métadonnées pour les enregistrements ingérés, reportez-vous à la [présentation du service de catalogue](../catalog/home.md).

>[!WARNING]
>
>Le terme « Profil unifié » utilisé dans la vidéo suivante est obsolète. Les termes [!DNL "Profile"] ou [!DNL "Real-Time Customer Profile"] sont les termes appropriés utilisés dans la documentation dʼ[!DNL Experience Platform]. Reportez-vous à la documentation pour connaître les dernières fonctionnalités.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
