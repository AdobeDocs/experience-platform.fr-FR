---
title: Présentation de Snowflake
description: Découvrez Snowflake pour le transfert d’événement dans Adobe Experience Platform.
last-substantial-update: 2023-06-21T00:00:00.000Z
exl-id: abddf0c4-3d4c-4f66-a6e0-c10b54ea3430
TQID: https://experienceleague.adobe.com/uPDEUwZFSzJyLEiZDSGwpSzSgJl-2Zv3cwba-1-hJso
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c20d46e7-1c7d-476c-a50e-3961d4dce35fid: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: dc6ebdf7-9a94-43eb-9184-759cfdd0cf1c
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 340
ht-degree: 2%

---

# Vue d’ensemble d’[!DNL Snowflake]

[[!DNL Snowflake]](https://www.snowflake.com/en/) est un entrepôt de données cloud qui peut stocker et analyser tous vos enregistrements de données en un seul endroit. Il peut être utilisé pour l’entreposage de données, les lacs de données, l’ingénierie et la science des données, le développement d’applications de données, ainsi que le partage et la consommation sécurisés de données partagées ou en temps réel.

[!DNL Snowflake] repose sur Amazon Web Services (AWS), Microsoft Azure (Azure) et Google Cloud Platform (GCP).

![Diagramme présentant l’architecture des données [!DNL Snowflake].](../../../images/extensions/server/snowflake/snowflake.png)

## Notre intégration Snowflake

Un compte Snowflake peut être hébergé sur l’une des plateformes cloud suivantes :

- [Amazon Web Services ([!DNL AWS])](https://aws.amazon.com/) - [!DNL AWS] est une plateforme d&#39;informatique en nuage qui offre une grande variété de services tels que l&#39;informatique distribuée, le stockage de bases de données, la diffusion de contenu et les services d&#39;intégration de logiciel en tant que service (SaaS) pour la gestion de la relation client (CRM) et la planification des ressources de l&#39;entreprise (ERP).

Pour plus d’informations sur l’installation de l’extension et la configuration des règles de transfert d’événement](../aws/overview.md) reportez-vous à la [[!DNL AWS]  présentation.

- [Microsoft Azure ([!DNL Azure])](https://azure.microsoft.com/en-us/products/event-hubs/#overview) - [!DNL Azure] est une plateforme de cloud computing et un portail en ligne qui vous permet d’accéder aux services et ressources cloud fournis par Microsoft et de les gérer.

Pour plus d’informations sur l’installation de l’extension et la configuration des règles de transfert d’événement](../azure/overview.md) reportez-vous à la [[!DNL Azure]  présentation.

- [[!DNL Google Cloud Platform]](https://cloud.google.com/) - [!DNL Google Cloud Platform] est une plateforme de cloud computing qui offre une grande variété de services tels que l’informatique distribuée, le stockage de bases de données, la diffusion de contenu et les services d’intégration de logiciel en tant que service (SaaS) pour la gestion de la relation client (CRM) et la planification des ressources d’entreprise (ERP).

Pour plus d’informations sur l’installation de l’extension et la configuration des règles de transfert d’événement](../google-cloud-platform/overview.md) reportez-vous à la [[!DNL Google Cloud Platform]  présentation.

Nos extensions de transfert d’événement natives [[!DNL AWS]](../aws/overview.md), [[!DNL Azure]](../azure/overview.md) et [[!DNL Google Cloud Platform]](../google-cloud-platform/overview.md) permettent aux clients de collecter, d’enrichir et de transférer leurs données d’événement côté serveur en temps réel vers leurs services cloud pour qu’elles soient utilisées par [!DNL Snowflake]. Consultez le tableau ci-dessous :

![Diagramme de création de rapports [!DNL Snowflake] montrant le lien entre [!DNL AWS] et [!DNL Azure].](../../../images/extensions/server/snowflake/snowflake-workflow.png)

## Étapes suivantes

Ce guide présente les [!DNL Snowflake] et l’utilisation des extensions de transfert d’événement [!DNL AWS] et [!DNL Azure].

Pour plus d’informations sur les fonctionnalités de transfert d’événement [!DNL AWS] et [!DNL Azure] dans Experience Platform, reportez-vous aux sections [[!DNL AWS]  présentation de l’extension ](../aws/overview.md) et [[!DNL Azure]  présentation de l’extension](../azure/overview.md).
