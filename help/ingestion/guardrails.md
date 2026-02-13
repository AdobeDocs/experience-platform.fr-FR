---
keywords: Experience Platform;dépannage;mécanismes de sécurisation;conseils;
title: Mécanismes de sécurisation pour l’ingestion des données
description: Découvrez les mécanismes de sécurisation pour l’ingestion de données dans Adobe Experience Platform.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: b5b975308d28ae82ea4d811652681215bc2cfbdb
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 37%

---

# Mécanismes de sécurisation pour l’ingestion des données

>[!IMPORTANT]
>
>Les mécanismes de sécurisation pour l’ingestion par lots et en flux continu sont généralement calculés au niveau de l’organisation et non au niveau du sandbox. Cela signifie que votre utilisation des données par sandbox est liée au droit total d’utilisation de licence qui correspond à l’ensemble de votre organisation. En outre, l’utilisation des données dans les sandbox de développement est limitée à 10 % du total de vos profils. Pour plus d’informations sur les droits d’utilisation de licence, consultez le [guide des bonnes pratiques de gestion des données](../landing/license-usage-and-guardrails/data-management-best-practices.md).

Les mécanismes de sécurisation sont des seuils qui fournissent des conseils pour l’utilisation des données et du système, l’optimisation des performances et la prévention des erreurs ou des résultats inattendus dans Adobe Experience Platform. Les mécanismes de sécurisation peuvent faire référence à l’utilisation ou la consommation de données et de traitement par rapport à vos droits de licence.

>[!IMPORTANT]
>
>Vérifiez vos droits de licence dans votre commande client et la [Description du produit](https://helpx.adobe.com/fr/legal/product-descriptions.html) correspondante sur les limites d’utilisation réelles en plus de cette page de mécanismes de sécurisation.

Ce document fournit des conseils sur les mécanismes de sécurisation pour l’ingestion de données dans Adobe Experience Platform.

## Mécanismes de sécurisation pour l’ingestion par lots

Le tableau suivant décrit les mécanismes de sécurisation à prendre en compte lors de l’utilisation de l’[API d’ingestion par lots](./batch-ingestion/overview.md) ou de sources :

| Type d’ingestion | Instructions | Notes |
| --- | --- | --- |
| Ingestion du lac de données à l’aide de l’API d’ingestion par lots | <ul><li>Vous pouvez ingérer jusqu’à 20 Go de données par heure dans le lac de données à l’aide de l’API d’ingestion par lots.</li><li>Le nombre maximal de fichiers par lot est de 1 500.</li><li>La taille de lot maximale est de 100 Go.</li><li>Le nombre maximal de propriétés ou de champs par ligne est de 10 000.</li><li>Le nombre maximal de lots par minute, par utilisateur est de 2000.</li></ul> | |
| Ingestion du lac de données à l’aide de sources de lots | <ul><li>Vous pouvez ingérer jusqu’à 200 Go de données par heure dans le lac de données à l’aide de sources d’ingestion par lots, telles que [!DNL Azure Blob], [!DNL Amazon S3] et [!DNL SFTP].</li><li>La taille du lot doit être comprise entre 256 Mo et 100 Go. Cela s’applique à la fois aux données compressées et non compressées. Lorsque des données compressées sont décompressées dans le lac de données, ces restrictions s’appliquent.</li><li>Le nombre maximal de fichiers par lot est de 1 500.</li><li>La taille minimale d’un fichier ou dossier est de 1 octet. Vous ne pouvez pas ingérer de fichiers ou de dossiers de taille 0 octet.</li></ul> | Lisez la [présentation des sources](../sources/home.md) pour un catalogue de sources que vous pouvez utiliser pour l’ingestion de données. |
| Ingestion par lots vers le profil | <ul><li>La taille maximale d’une classe d’enregistrement est de 100 Ko (hard).</li><li>La taille maximale d’une classe ExperienceEvent est de 10 Ko (hard).</li></ul> | |
| Nombre de lots Profile ou ExperienceEvent ingérés par jour | **Le nombre maximal de lots Profile ou ExperienceEvent ingérés par jour est de 90 par sandbox.** Cela signifie que le total combiné des lots Profile et ExperienceEvent ingérés chaque jour ne peut pas dépasser 90. L’ingestion de lots supplémentaires affectera les performances du système. | C’est une limite conditionnelle. Il est possible d’aller au-delà d’une limite conditionnelle. Toutefois, ces limites fournissent une orientation recommandée pour les performances du système. En outre, ce mécanisme de sécurisation est défini **par sandbox** et non par organisation. |
| Ingestion de données chiffrées | La taille maximale prise en charge d’un seul fichier chiffré est de 1 Go. Par exemple, alors que vous pouvez ingérer 2 Go ou plus de données dans une seule exécution de flux de données, aucun fichier individuel dans l’exécution de flux de données ne peut dépasser 1 Go. | Le processus d’ingestion de données chiffrées peut prendre plus de temps que celui d’une ingestion de données normale. Lisez le [&#x200B; Guide de l’API d’ingestion de données chiffrées &#x200B;](../sources/tutorials/api/encrypt-data.md) pour plus d’informations. |
| Ingestion par lots upsert | L’ingestion des lots d’upsert peut être jusqu’à 10 fois plus lente que les lots standard. Par conséquent, vous devez **conserver vos lots d’upsert sous deux millions d’enregistrements** afin d’assurer une exécution efficace et d’éviter de bloquer le traitement d’autres lots dans le sandbox. | Bien que vous puissiez sans aucun doute ingérer des lots qui dépassent deux millions d’enregistrements, le temps de votre ingestion sera considérablement plus long en raison des limites des petits sandbox. |

{style="table-layout:auto"}

## Mécanismes de sécurisation pour l’ingestion en flux continu

Lisez la [présentation de l’ingestion en flux continu](./streaming-ingestion/overview.md) pour plus d’informations sur les mécanismes de sécurisation pour l’ingestion en flux continu.

## Mécanismes de sécurisation pour les sources en flux continu

Le tableau suivant présente les mécanismes de sécurisation à prendre en compte lors de l’utilisation des sources de diffusion en continu :

| Type d’ingestion | Instructions | Notes |
| --- | --- | --- |
| Sources en flux continu | <ul><li>La taille d’enregistrement maximale est de 1 Mo, la taille recommandée étant de 10 Ko.</li><li>Les sources en flux continu prennent en charge entre 4 000 et 5 000 requêtes par seconde lors de l’ingestion dans le lac de données. Cela s’applique aux nouvelles connexions source en plus des connexions source existantes. **Remarque** : il peut s’écouler jusqu’à 60 minutes avant que les données de diffusion en continu ne soient complètement traitées dans le lac de données.</li><li>Les sources en flux continu prennent en charge un maximum de 1 500 requêtes par seconde lors de l’ingestion de données vers le profil ou la segmentation en flux continu.</li></ul> | Les sources en flux continu, telles que [!DNL Kafka], [!DNL Azure Event Hubs] et [!DNL Amazon Kinesis], n’utilisent pas l’itinéraire [!DNL Data Collection Core Service] (DCCS) et peuvent avoir différentes limites de débit. Consultez la [présentation des sources](../sources/home.md) pour un catalogue de sources que vous pouvez utiliser pour l’ingestion de données. |

{style="table-layout:auto"}

## Étapes suivantes

Consultez la documentation suivante pour plus d’informations sur les autres mécanismes de sécurisation des services Experience Platform, sur les informations de latence de bout en bout et les informations de licence dans les documents de description du produit Real-Time CDP :

* [Mécanismes de sécurisation de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammes de latence de bout en bout](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=fr#end-to-end-latency-diagrams) pour divers services Experience Platform.
* [Real-Time Customer Data Platform (B2C Edition - Packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
