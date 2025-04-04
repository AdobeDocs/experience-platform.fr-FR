---
title: Présentation de Data Distiller
description: Résumé des limites d’utilisation de Data Distiller pour les données Query Service par rapport à vos droits de licence.
exl-id: eb4a184b-f241-4f6f-a250-bbe4605d6b1b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Présentation de Data Distiller

Data Distiller est une offre groupée qui comprend un sous-ensemble des fonctionnalités de Adobe Experience Platform. Avec Data Distiller, vous pouvez effectuer une préparation des données après ingestion (telle que le nettoyage, la mise en forme et la manipulation) pour le profil client en temps réel ou les cas d’utilisation analytiques en exécutant des requêtes par lots dans Query Service. Votre utilisation de Data Distiller dépend de vos droits pour les applications basées sur Experience Platform.

<!-- Commented out references to licence usage dashboard. It is temporarily hidden:
## License usage {#license-usage}


The [Data Distiller license usage dashboard](./license-usage.md) is available once you have purchased Data Distiller compute hours. The license usage dashboard helps you to monitor the consumption of entitled compute hours. See the [Data Distiller license usage document](./license-usage.md) to view important information about your organization's Query Service license usage. 

The Data Distiller license usage dashboard is available once you have purchased Data Distiller compute hours. The license usage dashboard helps you to monitor the consumption of entitled compute hours.
-->

<!-- Update these descriptions post 23.3 release
## Scoping parameters {#scoping-parameters}

Scoping parameters are usage limits that relate to the scoping of your required set up, and are defined by your license capacity. Without add-ons, Data Distiller's scoping parameters are as follows: 

* **Compute Hours**: You can use PSQL or the Query Service API to run batch queries executed in any sandbox (scheduled or otherwise) to scan and write data. This uses your allotted Compute Hours per year as determined in the scoping process of your license agreement. Total Compute Hours is accumulated across all Sandboxes.
* **Data Ingested**: The data ingested into Adobe Experience Platform which can be queried using Data Distiller is subject to the limitations described in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer.
* **Data Lake Storage**: The data lake storage provided in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Data Lake Storage is a shared feature.
* **Query Service Users**: The number of Query Service users detailed in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Query Service Users is a shared feature. 
-->

## Mécanismes de sécurisation

Consultez le document [Mécanismes de sécurisation de Query Service](../guardrails.md) concernant les limites d’utilisation par défaut des données de Query Service par rapport à vos droits de licence.

<!-- Update these descriptions post 23.3 release
## Static limits

A static limit is the usage limit that relates to the functional boundaries of Adobe Experience Platform Activation. [More information on Adobe Experience Platform Activation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) can be found in the Adobe help documents. A summary of Data Distiller static limits are listed below, for more complete information please refer to the Query Service guardrail document.  

* **Batch Queries**: Scheduled batch queries time out after 24 hours.
* **Query Service**: You can use Query Service for the following purposes: 
    * To run SQL queries for data analysis and post ingestion data preparation (cleaning, shaping, and manipulation).
    * To run SQL queries to create roll-up metrics to surface directly into a BI tool.
    * To quickly inspect data within Adobe Experience Platform.
    * To generate meaningful insights from your data.
* **Reporting API Call**: To ensure queries run on aggregated data using the reporting API have enough resources to execute efficiently. This includes queries that enhance existing data models such as those provided by Real-Time Customer Data Platform. The reporting API tracks resource utilization by assigning concurrency slots to each query. A maximum of four reporting API calls are available concurrently. If you access the reporting API through a BI tool and require more concurrency slots, a BI server is required.
-->
