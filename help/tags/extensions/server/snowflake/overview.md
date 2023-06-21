---
title: Présentation du Snowflake
description: Découvrez le Snowflake pour le transfert d’événement dans Adobe Experience Platform.
last-substantial-update: 2023-06-21T00:00:00Z
source-git-commit: fe28840fab46fadb82f1a37f972084057a00af44
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Présentation des [!DNL Snowflake]

[[!DNL Snowflake]](https://www.snowflake.com/en/) est un entrepôt de données cloud qui peut stocker et analyser tous vos enregistrements de données au même endroit. Il peut être utilisé pour l’entrepôt de données, les lacs de données, l’ingénierie de données, la science des données, le développement d’applications de données, ainsi que le partage et la consommation sécurisés de données en temps réel ou partagées.

[!DNL Snowflake] repose sur Amazon Web Services (AWS), Microsoft Azure (Azure) et Google Cloud Platform (GCP).

![Diagramme affichant la [!DNL Snowflake] architecture des données.](../../../images/extensions/server/snowflake/snowflake.png)

## Intégration de notre Snowflake

Un compte de Snowflake peut être hébergé sur l’une des plateformes cloud suivantes :

- [Amazon Web Services ([!DNL AWS])](https://aws.amazon.com/) - [!DNL AWS] est une plateforme de cloud computing qui offre un large éventail de services tels que l’informatique distribuée, le stockage de base de données, la diffusion de contenu et les services d’intégration de logiciels en tant que service (SaaS) pour la gestion de la relation client (CRM) et la planification des ressources de l’entreprise (ERP).

Reportez-vous à la section [[!DNL AWS] aperçu](../aws/overview.md) pour plus d’informations sur l’installation de l’extension et la configuration des règles de transfert d’événement.

- [Microsoft Azure ([!DNL Azure])](https://azure.microsoft.com/en-us/products/event-hubs/#overview) - [!DNL Azure] est une plateforme de cloud computing et un portail en ligne qui vous permet d’accéder et de gérer les services et ressources cloud fournis par Microsoft.

Reportez-vous à la section [[!DNL Azure] aperçu](../azure/overview.md) pour plus d’informations sur l’installation de l’extension et la configuration des règles de transfert d’événement.

- [[!DNL Google Cloud Platform]](https://cloud.google.com/) - [!DNL Google Cloud Platform] est une plateforme de cloud computing qui offre un large éventail de services tels que l’informatique distribuée, le stockage de base de données, la diffusion de contenu et les services d’intégration de logiciels en tant que service (SaaS) pour la gestion de la relation client (CRM) et la planification des ressources de l’entreprise (ERP).

Reportez-vous à la section [[!DNL Google Cloud Platform] aperçu](../google-cloud-platform/overview.md) pour plus d’informations sur l’installation de l’extension et la configuration des règles de transfert d’événement.

Notre natif [[!DNL AWS]](../aws/overview.md), [[!DNL Azure]](../azure/overview.md), et [[!DNL Google Cloud Platform]](../google-cloud-platform/overview.md) les extensions de transfert d’événement permettent aux clients de collecter, d’enrichir et de transférer leurs données d’événement côté serveur en temps réel vers leurs services cloud pour les utiliser par [!DNL Snowflake]. Consultez le tableau ci-dessous :

![Le [!DNL Snowflake] diagramme de reporting montrant le lien entre [!DNL AWS] et [!DNL Azure].](../../../images/extensions/server/snowflake/snowflake-workflow.png)

## Étapes suivantes

Ce guide donne un aperçu de la [!DNL Snowflake] et l’utilisation de [!DNL AWS] et [!DNL Azure] extensions de transfert d’événement.

Pour plus d’informations sur la variable [!DNL AWS] et [!DNL Azure] fonctionnalité de transfert d’événement dans Experience Platform, voir [[!DNL AWS] présentation de l’extension](../aws/overview.md) et le [[!DNL Azure] présentation de l’extension](../azure/overview.md).
