---
keywords: Experience Platform;dépannage;garde-fous;conseils ;
title: Barrières de sécurité pour l’ingestion des données
description: Ce document fournit des conseils sur les barrières de sécurité pour l’ingestion de données dans Adobe Experience Platform
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 4fd26078017ae13e22ebb02f98335094c8e0581b
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Barrières de sécurité pour l’ingestion des données

Les barrières de sécurité sont des seuils qui fournissent des conseils pour l’utilisation des données et du système, l’optimisation des performances et la prévention des erreurs ou des résultats inattendus dans Adobe Experience Platform. Les barrières de sécurité peuvent faire référence à l’utilisation ou la consommation de données et de traitement par rapport à vos droits de licence.

Ce document fournit des conseils sur les barrières de sécurité pour l’ingestion de données dans Adobe Experience Platform.

## Barrières de sécurité pour l’ingestion par lots

Le tableau suivant décrit les barrières de sécurité à prendre en compte lors de l’utilisation de la variable [API d’ingestion par lots](./batch-ingestion/overview.md) ou sources :

| Type d’ingestion | Instructions | Notes |
| --- | --- | --- |
| Ingestion du lac de données à l’aide de l’API d’ingestion par lots | <ul><li>Vous pouvez ingérer jusqu’à 20 Go de données par heure dans le lac de données à l’aide de l’API d’ingestion par lots.</li><li>Le nombre maximal de fichiers par lot est de 1 500.</li><li>La taille de lot maximale est de 100 Go.</li><li>Le nombre maximal de propriétés ou de champs par ligne est de 10 000.</li><li>Le nombre maximal de lots par minute, par utilisateur, est de 138.</li></ul> |
| Ingestion du lac de données à l’aide de sources par lots | <ul><li>Vous pouvez ingérer jusqu’à 200 Go de données par heure dans le lac de données à l’aide de sources d’ingestion par lots, telles que [!DNL Azure Blob], [!DNL Amazon S3], et [!DNL SFTP].</li><li>La taille du lot doit être comprise entre 256 Mo et 100 Go.</li><li>Le nombre maximal de fichiers par lot est de 1 500.</li></ul> | Voir [présentation des sources](../sources/home.md) pour un catalogue de sources que vous pouvez utiliser pour l’ingestion de données. |
| Ingestion par lots dans Profile | <ul><li>Vous pouvez ingérer jusqu’à 120 Go de données par heure.</li><li>La taille maximale d’une classe d’enregistrement est de 100 Ko (soft).</li><li>La taille maximale d’une classe ExperienceEvent est de 10 Ko (soft).</li><li>La taille maximale d’un seul enregistrement est de 1 Mo.</li></ul> |

## Barrières de sécurité pour l’ingestion par flux

Le tableau suivant décrit les barrières de sécurité à prendre en compte lors de l’utilisation de la variable [API d’ingestion par flux](./streaming-ingestion/overview.md) ou sources de diffusion en continu :

| Type d’ingestion | Instructions | Remarques |
| --- | --- | --- |
| Ingestion par flux | <ul><li>La taille d’enregistrement maximale est de 1 Mo, la taille recommandée étant de 10 Ko.</li><li>Vous pouvez traiter 2 000 requêtes par seconde dans Profile en moins d’une minute.</li><li>Vous pouvez traiter jusqu’à 2 000 demandes par seconde pour le lac de données en moins de 15 minutes.</li></ul> | Utilisez l’API d’ingestion par lots si vous avez besoin d’un débit de données plus élevé. |
| Sources de diffusion en continu | <ul><li>La taille d’enregistrement maximale est de 1 Mo, la taille recommandée étant de 10 Ko.</li><li>Les sources en flux continu prennent en charge entre 4 000 et 5 000 requêtes par seconde lors de la création d’une nouvelle connexion source. **Remarque**: Il peut s’écouler jusqu’à 30 minutes avant que les données en flux continu ne soient complètement traitées dans le lac de données.</li><li>Vous pouvez traiter entre 4 000 et 5 000 demandes par seconde dans un lac de données. **Remarque**: Il peut s’écouler jusqu’à 30 minutes avant que les données en flux continu ne soient complètement traitées dans le lac de données.</li></ul> | Sources de diffusion en continu, telles que [!DNL Kafka], [!DNL Azure Event Hubs], et [!DNL Amazon Kinesis] n’utilisez pas la variable [!DNL Data Collection Core Service] itinéraire (DCCS) et peut avoir différentes limites de débit. Voir [présentation des sources](../sources/home.md) pour un catalogue de sources que vous pouvez utiliser pour l’ingestion de données. |

## Étapes suivantes

Pour plus d’informations sur les barrières de sécurité des données et du traitement dans Experience Platform, consultez la documentation suivante :

* [Barrières de sécurité pour les données Real-time Customer Profile](../profile/guardrails.md)
* [Barrières de sécurité pour les données Identity Service](../identity-service/guardrails.md)
