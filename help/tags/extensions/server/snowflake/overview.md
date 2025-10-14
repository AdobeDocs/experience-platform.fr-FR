---
title: Présentation du Snowflake
description: Découvrez Snowflake pour le transfert d’événement dans Adobe Experience Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: abddf0c4-3d4c-4f66-a6e0-c10b54ea3430
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# Vue d’ensemble d’[!DNL Snowflake]

[[!DNL Snowflake]](https://www.snowflake.com/en/) est un entrepôt de données cloud qui peut stocker et analyser tous vos enregistrements de données à un seul endroit. Il peut être utilisé pour l’entrepôt de données, les lacs de données, l’ingénierie de données, la science des données, le développement d’applications de données, ainsi que le partage et la consommation sécurisés de données en temps réel ou partagées.

[!DNL Snowflake] repose sur Amazon Web Services (AWS), Microsoft Azure (Azure) et Google Cloud Platform (GCP).

![Diagramme présentant l’architecture de données [!DNL Snowflake].](../../../images/extensions/server/snowflake/snowflake.png)

## Intégration de notre Snowflake

Un compte de Snowflake peut être hébergé sur l’une des plateformes cloud suivantes :

- [Amazon Web Services ([!DNL AWS])](https://aws.amazon.com/) - [!DNL AWS] est une plateforme de cloud computing qui offre un large éventail de services tels que l’informatique distribuée, le stockage de base de données, la diffusion de contenu et les services d’intégration de logiciels en tant que service (SaaS) pour la gestion de la relation client (CRM) et la planification des ressources de l’entreprise (ERP).

Pour plus d’informations sur l’installation de l’extension et la configuration des règles de transfert d’événement, reportez-vous à la [[!DNL AWS] présentation](../aws/overview.md) .

- [Microsoft Azure ([!DNL Azure])](https://azure.microsoft.com/en-us/products/event-hubs/#overview) - [!DNL Azure] est une plateforme de cloud computing et un portail en ligne qui vous permet d’accéder et de gérer les services et ressources cloud fournis par Microsoft.

Pour plus d’informations sur l’installation de l’extension et la configuration des règles de transfert d’événement, reportez-vous à la [[!DNL Azure] présentation](../azure/overview.md) .

- [[!DNL Google Cloud Platform]](https://cloud.google.com/) - [!DNL Google Cloud Platform] est une plateforme de cloud computing qui offre un large éventail de services tels que l’informatique distribuée, le stockage de base de données, la diffusion de contenu et les services d’intégration de logiciels en tant que service (SaaS) pour la gestion de la relation client (CRM) et la planification des ressources de l’entreprise (ERP).

Pour plus d’informations sur l’installation de l’extension et la configuration des règles de transfert d’événement, reportez-vous à la [[!DNL Google Cloud Platform] présentation](../google-cloud-platform/overview.md) .

Nos extensions natives de transfert d’événement [[!DNL AWS]](../aws/overview.md), [[!DNL Azure]](../azure/overview.md) et [[!DNL Google Cloud Platform]](../google-cloud-platform/overview.md) permettent aux clients de collecter, d’enrichir et de transférer leurs données d’événement côté serveur en temps réel vers leurs services cloud pour être consommés par [!DNL Snowflake]. Consultez le tableau ci-dessous :

![&#x200B; Diagramme de rapport [!DNL Snowflake] présentant le lien entre [!DNL AWS] et [!DNL Azure].](../../../images/extensions/server/snowflake/snowflake-workflow.png)

## Étapes suivantes

Ce guide fournit un aperçu de [!DNL Snowflake] et de l’utilisation des extensions de transfert d’événement [!DNL AWS] et [!DNL Azure].

Pour plus d’informations sur les fonctionnalités de transfert d’événement [!DNL AWS] et [!DNL Azure] en Experience Platform, reportez-vous à la [[!DNL AWS] présentation de l’extension](../aws/overview.md) et à la [[!DNL Azure] présentation de l’extension](../azure/overview.md).
