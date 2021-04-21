---
keywords: Experience Platform ; accueil ; rubriques populaires ; assimilation des données ; emplacement des données ; emplacement des données ; Data Management ; data Management ; lignage ; lignage ; lot ; lot ; données assimilées
solution: Experience Platform
title: Présentation de l'importation de données
topic-legacy: overview
description: Ce document présente les trois principales manières dont les données sont ingérées dans Platform, avec des liens vers leur documentation de présentation respectives pour plus d’informations.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 51%

---

# Présentation de Data Ingestion

Adobe Experience Platform rassemble des données provenant de plusieurs sources afin d’aider les professionnels du marketing à mieux comprendre le comportement de leurs clients. L&#39;Ingestion des données de Adobe Experience Platform représente les méthodes multiples par lesquelles [!DNL Platform] ingère des données provenant de ces sources, ainsi que la façon dont ces données sont conservées dans le lac Data pour être utilisées par les services [!DNL Platform] en aval.

Ce document présente les trois principaux modes d&#39;assimilation des données dans [!DNL Platform], avec des liens vers leur documentation d&#39;aperçu respective pour plus d&#39;informations.

## Ingestion par lots

L’assimilation de lots permet d’assimiler des données dans [!DNL Experience Platform] sous forme de fichiers de lots. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à ingérer en tant qu’unité unique. Une fois ingérés, les lots fournissent des métadonnées qui décrivent le nombre d’enregistrements correctement ingérés ainsi que les enregistrements ayant échoué et les messages d’erreur associés.

Les fichiers de données chargés manuellement, tels que les fichiers CSV plats (mappés à des schémas XDM) et les cadres de données Parquet, doivent être ingérés à l’aide de cette méthode.

Pour plus d’informations, consultez la [présentation de l’ingestion par lots](./batch-ingestion/overview.md).

## Ingestion par flux

L’assimilation en flux continu vous permet d’envoyer en temps réel des données des périphériques client et serveur à [!DNL Experience Platform]. [!DNL Platform] prend en charge l’utilisation des entrées de données pour diffuser des données d’expérience entrantes, qui sont conservées dans les jeux de données activés dans le flux au sein du lac de données. Les entrées de données peuvent être configurées pour authentifier automatiquement les données qu’elles collectent, en veillant à ce que celles-ci proviennent d’une source approuvée.

Pour plus d’informations, consultez la [présentation de l’ingestion par flux](./streaming-ingestion/overview.md).

## Sources

[!DNL Experience Platform] vous permet de configurer des connexions source à différents fournisseurs de données. Ces connexions vous permettent de vous authentifier auprès de vos sources données externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Les connexions sources peuvent être configurées pour collecter des données à partir d’autres applications d’Adobe (telles que Adobe Analytics et Adobe Audience Manager), de sources d’enregistrement de cloud tierces (telles que [!DNL Azure Blob], [!DNL Amazon] S3, de serveurs FTP et de serveurs SFTP) et de systèmes de gestion de la relation client tiers (tels que [!DNL Microsoft Dynamics] et [!DNL Salesforce]).

Pour plus d’informations, consultez la [présentation des sources](../sources/home.md).

## Étapes suivantes et ressources supplémentaires

Ce document présente brièvement les différents aspects de [!DNL Data Ingestion] dans [!DNL Experience Platform]. Poursuivez votre lecture de la documentation de présentation de chaque méthode d’ingestion pour vous familiariser avec leurs différentes capacités, les cas d’utilisation et les bonnes pratiques. Vous pouvez également compléter votre apprentissage en regardant la vidéo de présentation de l&#39;ingestion ci-dessous. Pour plus d&#39;informations sur la façon dont [!DNL Experience Platform] suit les métadonnées pour les enregistrements assimilés, consultez la [Présentation du service de catalogue](../catalog/home.md).

>[!WARNING]
>
>Le terme &quot;Profil unifié&quot; utilisé dans la vidéo suivante est obsolète. Les termes [!DNL "Profile"] ou [!DNL "Real-time Customer Profile"] sont les termes appropriés utilisés dans la documentation [!DNL Experience Platform]. Reportez-vous à la documentation pour connaître les dernières fonctionnalités.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
