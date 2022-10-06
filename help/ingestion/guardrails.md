---
keywords: Experience Platform;dépannage;barrières de sécurité;conseils;
title: Barrières de sécurité pour l’ingestion des données
description: Ce document fournit des conseils sur les barrières de sécurité pour l’ingestion de données dans Adobe Experience Platform.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: fa0ddc4c0053018d013c14c568ebb2fd231f4bd2
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 81%

---

# Barrières de sécurité pour l’ingestion des données

Les barrières de sécurité sont des seuils qui fournissent des conseils pour l’utilisation des données et du système, l’optimisation des performances et la prévention des erreurs ou des résultats inattendus dans Adobe Experience Platform. Les barrières de sécurité peuvent faire référence à l’utilisation ou la consommation de données et de traitement par rapport à vos droits de licence.

Ce document fournit des conseils sur les barrières de sécurité pour l’ingestion de données dans Adobe Experience Platform.

## Barrières de sécurité pour l’ingestion par lots

Le tableau suivant décrit les barrières de sécurité à prendre en compte lors de l’utilisation de l’[API d’ingestion par lots](./batch-ingestion/overview.md) ou de sources :

| Type d’ingestion | Instructions | Notes |
| --- | --- | --- |
| Ingestion du lac de données à l’aide de l’API d’ingestion par lots | <ul><li>Vous pouvez ingérer jusqu’à 20 Go de données par heure dans le lac de données à l’aide de l’API d’ingestion par lots.</li><li>Le nombre maximal de fichiers par lot est de 1 500.</li><li>La taille de lot maximale est de 100 Go.</li><li>Le nombre maximal de propriétés ou de champs par ligne est de 10 000.</li><li>Le nombre maximal de lots par minute, par utilisateur est de 138.</li></ul> |
| Ingestion du lac de données à l’aide de sources de lots | <ul><li>Vous pouvez ingérer jusqu’à 200 Go de données par heure dans le lac de données à l’aide de sources d’ingestion par lots, telles que [!DNL Azure Blob], [!DNL Amazon S3] et [!DNL SFTP].</li><li>La taille du lot doit être comprise entre 256 Mo et 100 Go.</li><li>Le nombre maximal de fichiers par lot est de 1 500.</li></ul> | Consultez la [présentation des sources](../sources/home.md) pour un catalogue de sources que vous pouvez utiliser pour l’ingestion de données. |
| Ingestion par lots vers le profil | <ul><li>Vous pouvez ingérer jusqu’à 120 Go de données par heure.</li><li>La taille maximale d’une classe d’enregistrement est de 100 Ko (soft).</li><li>La taille maximale d’une classe ExperienceEvent est de 10 Ko (soft).</li><li>La taille maximale d’un seul enregistrement est de 1 Mo.</li></ul> |
| Nombre de lots Profile ou ExperienceEvent ingérés par jour | **Le nombre maximal de lots Profile ou ExperienceEvent ingérés par jour est de 90.** Cela signifie que le total combiné des lots Profile et ExperienceEvent ingérés chaque jour ne peut pas dépasser 90. L’ingestion de lots supplémentaires affectera les performances du système. | C&#39;est une limite douce. Il est possible d’aller au-delà d’une limite de type &quot;soft&quot;. Toutefois, les limites de type &quot;soft&quot; fournissent une ligne directrice recommandée pour les performances du système. |

## Barrières de sécurité pour l’ingestion en flux continu

Le tableau suivant décrit les barrières de sécurité à prendre en compte lors de l’utilisation de l’[API d’ingestion en flux continu](./streaming-ingestion/overview.md) ou sources en flux continu :

| Type d’ingestion | Instructions | Remarques |
| --- | --- | --- |
| Ingestion en flux continu | <ul><li>La taille d’enregistrement maximale est de 1 Mo, la taille recommandée étant de 10 Ko.</li><li>Vous pouvez traiter 20 000 requêtes par seconde vers le profil en moins d’une minute.</li><li>Vous pouvez traiter jusqu’à 20 000 requêtes par seconde vers le lac de données en moins de 15 minutes.</li></ul> | Utilisez l’API d’ingestion par lots si vous avez besoin d’un débit de données plus élevé. |
| Sources en flux continu | <ul><li>La taille d’enregistrement maximale est de 1 Mo, la taille recommandée étant de 10 Ko.</li><li>Les sources en flux continu prennent en charge entre 4 000 et 5 000 requêtes par seconde lors de la création d’une connexion source. **Remarque**: Il peut s’écouler jusqu’à 30 minutes avant que les données en flux continu ne soient complètement traitées dans le lac de données.</li><li>Vous pouvez traiter entre 4 000 et 5 000 requêtes par seconde vers un lac de données. **Remarque**: Il peut s’écouler jusqu’à 30 minutes avant que les données en flux continu ne soient complètement traitées dans le lac de données.</li></ul> | Les sources en flux continu, telles que [!DNL Kafka], [!DNL Azure Event Hubs] et [!DNL Amazon Kinesis], n’utilisent pas l’itinéraire [!DNL Data Collection Core Service] (DCCS) et peuvent avoir différentes limites de débit. Consultez la [présentation des sources](../sources/home.md) pour un catalogue de sources que vous pouvez utiliser pour l’ingestion de données. |

## Étapes suivantes

Pour plus d’informations sur les barrières de sécurité des données et du traitement dans Experience Platform, consultez la documentation suivante :

* [Barrières de sécurité pour les données Real-time Customer Profile](../profile/guardrails.md)
* [Barrières de sécurité pour les données Identity Service](../identity-service/guardrails.md)
