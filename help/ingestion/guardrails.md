---
keywords: Experience Platform;dépannage;mécanismes de sécurisation;conseils;
title: Mécanismes de sécurisation pour l’ingestion des données
description: Découvrez les barrières de sécurité pour l’ingestion de données dans Adobe Experience Platform.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 583eb70235174825dd542b95463784638bdef235
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 50%

---

# Mécanismes de sécurisation pour l’ingestion des données

>[!IMPORTANT]
>
>Les barrières de sécurité pour l’ingestion par lots et par flux sont calculées au niveau de l’organisation et non au niveau de l’environnement de test. Cela signifie que votre utilisation des données par environnement de test est liée au total des droits d’utilisation des licences qui correspondent à l’ensemble de votre organisation. En outre, l’utilisation des données dans les environnements de test de développement est limitée à 10 % de vos profils totaux. Pour plus d’informations sur les droits d’utilisation des licences, consultez la section [guide des bonnes pratiques relatives à la gestion des données](../landing/license-usage-and-guardrails/data-management-best-practices.md).

Les mécanismes de sécurisation sont des seuils qui fournissent des conseils pour l’utilisation des données et du système, l’optimisation des performances et la prévention des erreurs ou des résultats inattendus dans Adobe Experience Platform. Les mécanismes de sécurisation peuvent faire référence à l’utilisation ou la consommation de données et de traitement par rapport à vos droits de licence.

>[!IMPORTANT]
>
>Vérifiez vos droits de licence dans votre commande commerciale et les [Description du produit](https://helpx.adobe.com/fr/legal/product-descriptions.html) sur les limites d’utilisation réelles en plus de cette page des barrières de sécurité.

Ce document fournit des conseils sur les mécanismes de sécurisation pour l’ingestion de données dans Adobe Experience Platform.

## Mécanismes de sécurisation pour l’ingestion par lots

Le tableau suivant décrit les mécanismes de sécurisation à prendre en compte lors de l’utilisation de l’[API d’ingestion par lots](./batch-ingestion/overview.md) ou de sources :

| Type d’ingestion | Instructions | Notes |
| --- | --- | --- |
| Ingestion du lac de données à l’aide de l’API d’ingestion par lots | <ul><li>Vous pouvez ingérer jusqu’à 20 Go de données par heure dans le lac de données à l’aide de l’API d’ingestion par lots.</li><li>Le nombre maximal de fichiers par lot est de 1 500.</li><li>La taille de lot maximale est de 100 Go.</li><li>Le nombre maximal de propriétés ou de champs par ligne est de 10 000.</li><li>Le nombre maximal de lots par minute, par utilisateur est de 2000.</li></ul> | |
| Ingestion du lac de données à l’aide de sources de lots | <ul><li>Vous pouvez ingérer jusqu’à 200 Go de données par heure dans le lac de données à l’aide de sources d’ingestion par lots, telles que [!DNL Azure Blob], [!DNL Amazon S3] et [!DNL SFTP].</li><li>La taille du lot doit être comprise entre 256 Mo et 100 Go. Cela s’applique aux données non compressées et compressées. Lorsque les données compressées sont décompressées dans le lac de données, ces limites s’appliquent.</li><li>Le nombre maximal de fichiers par lot est de 1 500.</li><li>La taille minimale d’un fichier ou d’un dossier est de 1 octet. Vous ne pouvez pas ingérer de fichiers ou de dossiers de taille 0 octet.</li></ul> | Lisez la section [présentation des sources](../sources/home.md) pour un catalogue de sources que vous pouvez utiliser pour l’ingestion de données. |
| Ingestion par lots vers le profil | <ul><li>La taille maximale d’une classe d’enregistrement est de 100 Ko (en dur).</li><li>La taille maximale d’une classe ExperienceEvent est de 10 Ko (en dur).</li></ul> | |
| Nombre de lots Profile ou ExperienceEvent ingérés par jour | **Le nombre maximal de lots Profile ou ExperienceEvent ingérés par jour est de 90.** Cela signifie que le total combiné des lots Profile et ExperienceEvent ingérés chaque jour ne peut pas dépasser 90. L’ingestion de lots supplémentaires affectera les performances du système. | C’est une limite conditionnelle. Limite conditionnelle : il est possible d’aller au-delà d’une limite conditionnelle. Cependant, ces limites fournissent une orientation recommandée pour les performances du système. |

## Mécanismes de sécurisation pour l’ingestion en flux continu

Lisez la section [présentation de l’ingestion par flux](./streaming-ingestion/overview.md) pour plus d’informations sur les barrières de sécurité pour l’ingestion par flux.

## Barrières de sécurité pour les sources en continu

Le tableau suivant décrit les barrières de sécurité à prendre en compte lors de l’utilisation des sources de diffusion en continu :

| Type d’ingestion | Instructions | Notes |
| --- | --- | --- |
| Sources en flux continu | <ul><li>La taille d’enregistrement maximale est de 1 Mo, la taille recommandée étant de 10 Ko.</li><li>Les sources en flux continu prennent en charge entre 4 000 et 5 000 demandes par seconde lors de l’ingestion dans le lac de données. Cela s’applique aux deux nouvelles connexions source, en plus des connexions source existantes. **Remarque** : il peut s’écouler jusqu’à 30 minutes avant que les données de diffusion en continu ne soient complètement traitées dans le lac de données.</li><li>Les sources en flux continu prennent en charge un maximum de 1 500 requêtes par seconde lors de l’ingestion de données à une segmentation de profil ou de diffusion en continu.</li></ul> | Les sources en flux continu, telles que [!DNL Kafka], [!DNL Azure Event Hubs] et [!DNL Amazon Kinesis], n’utilisent pas l’itinéraire [!DNL Data Collection Core Service] (DCCS) et peuvent avoir différentes limites de débit. Consultez la [présentation des sources](../sources/home.md) pour un catalogue de sources que vous pouvez utiliser pour l’ingestion de données. |

## Étapes suivantes

Pour plus d’informations sur les barrières de sécurité des autres services Experience Platform, sur les informations de latence de bout en bout et les informations de licence des documents Description du produit Real-Time CDP, consultez la documentation suivante :

* [Barrières de sécurité Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammes de latence de bout en bout](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) pour divers services Experience Platform.
* [Real-time Customer Data Platform (Édition B2C - Packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
