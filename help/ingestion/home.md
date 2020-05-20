---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l’importation des données d’Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---


# Présentation de l&#39;insertion de données

Adobe Experience Platform rassemble les données provenant de plusieurs sources afin d’aider les spécialistes du marketing à mieux comprendre le comportement de leurs clients. L’importation de données de la plateforme Adobe Experience Platform représente les multiples méthodes par lesquelles la plateforme ingère des données à partir de ces sources, ainsi que la manière dont ces données sont conservées dans Data Lake pour être utilisées par les services Plateforme en aval.

Ce document présente les trois principaux modes d’assimilation des données dans la plate-forme, avec des liens vers leur documentation d’aperçu respective pour des informations plus détaillées.

## Importation par lot

L’assimilation de lots vous permet d’assimiler des données dans la plate-forme d’expérience sous forme de fichiers de commandes. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à assimiler en une seule unité. Une fois ingérés, les lots fournissent des métadonnées qui décrivent le nombre d&#39;enregistrements correctement assimilés, ainsi que les enregistrements ayant échoué et les messages d&#39;erreur associés.

Les fichiers de données téléchargés manuellement, tels que les fichiers CSV aplatis (mappés à des schémas XDM) et les noms de fichiers de données Parquet, doivent être assimilés à l’aide de cette méthode.

See the [batch ingestion overview](./batch-ingestion/overview.md) for more information.

## Extraction en flux continu

L’assimilation en flux continu vous permet d’envoyer en temps réel des données des périphériques client et serveur vers Experience Platform. La plate-forme prend en charge l’utilisation d’entrées de données pour diffuser en continu les données d’expérience entrantes, qui sont conservées dans les jeux de données compatibles avec la diffusion en continu dans Data Lake. Les entrées de données peuvent être configurées pour authentifier automatiquement les données qu’elles collectent, en veillant à ce que les données proviennent d’une source approuvée.

See the [streaming ingestion overview](./streaming-ingestion/overview.md) for more information.

## Sources

Experience Platform vous permet de configurer des connexions source à divers fournisseurs de données. Ces connexions vous permettent de vous authentifier auprès de vos sources de données externes, de définir les heures d&#39;exécution pour l&#39;assimilation et de gérer le débit d&#39;assimilation.

Les connexions source peuvent être configurées pour collecter des données à partir d’autres applications Adobe (telles qu’Adobe Analytics et Adobe Audience Manager), de sources d’enregistrement de cloud tierces (telles que Azure Blob, Amazon S3, des serveurs FTP et des serveurs SFTP) et de systèmes de gestion de la relation client tiers (tels que Microsoft Dynamics et Salesforce).

See the [Sources overview](../sources/home.md) for more information.

## Étapes suivantes

Ce document présente brièvement les différents aspects de la gestion des données dans la plateforme d’expérience. Veuillez continuer à lire la documentation d&#39;aperçu de chaque méthode d&#39;ingestion pour vous familiariser avec leurs différentes capacités, leurs cas d&#39;utilisation et leurs meilleures pratiques. Pour plus d’informations sur la façon dont la plate-forme d’expérience effectue le suivi des métadonnées pour les enregistrements assimilés, voir la présentation [du service de](../catalog/home.md)catalogue.