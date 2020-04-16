---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l’intégration des données d’Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac

---


# Présentation de l&#39;insertion de données

Adobe Experience Platform rassemble des données provenant de plusieurs sources afin d’aider les spécialistes du marketing à mieux comprendre le comportement de leurs clients. Adobe Experience Platform Data Ingestion représente les méthodes multiples par lesquelles Platform imprime des données à partir de ces sources, ainsi que la manière dont ces données sont conservées dans Data Lake pour être utilisées par les services Plateforme en aval.

Ce présente les trois principales manières dont les données sont ingérées dans Platform, avec des liens vers leur documentation d’aperçu respective pour plus d’informations.

## Importation par lot

L’assimilation de lots vous permet d’assimiler des données dans la plateforme d’expérience sous forme de fichiers de commandes. Les lots sont des unités de données composées d’un ou de plusieurs fichiers à assimiler en une seule unité. Une fois assimilés, les lots fournissent des métadonnées qui décrivent le nombre d’enregistrements correctement assimilés, ainsi que les enregistrements ayant échoué et les messages d’erreur associés.

Les fichiers de données téléchargés manuellement, tels que les fichiers CSV aplatis (mappés à des  XDM) et les noms de fichier Parquet, doivent être assimilés à l’aide de cette méthode.

See the [batch ingestion overview](./batch-ingestion/overview.md) for more information.

## Extraction en flux continu

L’assimilation en flux continu vous permet d’envoyer en temps réel des données des périphériques client et serveur vers Experience Platform. La plate-forme prend en charge l’utilisation des entrées de données pour diffuser en continu les données d’expérience entrantes, qui sont conservées dans les jeux de données activés pour la diffusion en continu dans Data Lake. Les entrées de données peuvent être configurées pour authentifier automatiquement les données qu’elles collectent, en veillant à ce que les données proviennent d’une source approuvée.

See the [streaming ingestion overview](./streaming-ingestion/overview.md) for more information.

## Sources

Experience Platform vous permet de configurer des connexions source à différents fournisseurs de données. Ces connexions vous permettent de vous authentifier auprès de vos sources de données externes, de définir les heures d’exécution de l’assimilation et de gérer le débit d’assimilation.

Les connexions source peuvent être configurées pour collecter des données à partir d’autres applications Adobe (telles qu’Adobe Analytics et Adobe   Manager), de sources de de données tierces sur le cloud (telles que Azure Blob, Amazon S3, des serveurs FTP et des serveurs SFTP) et de systèmes de gestion de la relation client tiers (tels que Microsoft Dynamics et Salesforce).

See the [Sources overview](../sources/home.md) for more information.

## Étapes suivantes

Ce présente brièvement les différents aspects de la gestion des données dans la plateforme d’expérience. Veuillez continuer à lire la documentation d&#39;aperçu de chaque méthode d&#39;ingestion pour vous familiariser avec leurs différentes capacités, leurs cas d&#39;utilisation et leurs meilleures pratiques. Pour plus d’informations sur le suivi des métadonnées par Experience Platform pour les enregistrements assimilés, voir la présentation [du service de](../catalog/home.md)catalogue.