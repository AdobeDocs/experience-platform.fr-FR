---
title: Barrières de sécurité Real-Time CDP
description: Découvrez les barrières de sécurité des données dans les différents services et zones de Real-Time CDP.
feature: Guardrails, Data Management, Data Ingestion, Data Export
exl-id: 377499b4-5707-4d50-94e3-02f88ad5bf2c
source-git-commit: c2e308b5e743f07062be9a34e23c4bc700b27463
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 11%

---

# Barrières de sécurité Real-Time CDP

Les barrières de sécurité sont des seuils qui fournissent des conseils pour l’utilisation des données et du système, l’optimisation des performances et la prévention des erreurs ou des résultats inattendus dans Real-Time CDP. Les mécanismes de sécurisation peuvent faire référence à l’utilisation ou la consommation de données et de traitement par rapport à vos droits de licence.

Commencez ici et suivez les liens ci-dessous pour comprendre toutes les barrières de sécurité dans les différents services et zones de Real-Time CDP :

* [Barrières de sécurité pour l’ingestion de données](/help/ingestion/guardrails.md)
* [Barrières de sécurité pour les [!DNL Edge Network Server API]](/help/server-api/guardrails.md)
* [Barrières de sécurité pour [!DNL Real-Time Customer Profile] données et segmentation](/help/profile/guardrails.md)
* [Mécanismes de sécurisation pour les  [!DNL Identity Service] données](/help/identity-service/guardrails.md)
* [Barrières de sécurité pour [!DNL Query Service]](/help/query-service/guardrails.md)
* [Barrières de sécurité pour l’activation des données par le biais des destinations](/help/destinations/guardrails.md)

>[!TIP]
>
>En outre, voir [cette page](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html) pour plus d’informations sur les barrières de sécurité pour d’autres applications Experience Platform, telles que [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=fr) et [Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics.html?lang=fr), et [diagrammes de latence de bout en bout](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) pour divers services Experience Platform.

## Types de protection {#guardrail-types}

Notez que les deux types de barrières de sécurité dans toutes les zones et tous les services Real-Time CDP sont les suivants :

| Type de protection | Description |
|----------|---------|
| **Barrière de sécurité des performances (limite de soft)** | Les barrières de performance sont des limites d’utilisation liées à la portée de vos cas d’utilisation. Lorsque vous dépassez les barrières de performance, vous pouvez rencontrer une dégradation des performances et une latence. Adobe n’est pas responsable d’une telle dégradation des performances. Les clients qui dépassent systématiquement une barrière de performance peuvent choisir d’acquérir une capacité supplémentaire afin d’éviter une dégradation des performances. |
| **Barrières de sécurité appliquées par le système (limite stricte)** | Les barrières de sécurité appliquées par le système sont appliquées par l’interface utilisateur ou l’API de Real-Time CDP. Il s’agit de limites que vous ne pouvez pas dépasser, car l’interface utilisateur et l’API vous empêcheront de le faire ou renverront une erreur. |

{style="table-layout:auto"}

## Informations de licence et de droits Real-Time CDP {#product-descriptions}

En outre, reportez-vous aux liens de description du produit ci-dessous pour obtenir des informations sur les licences et les droits en fonction de l’édition et du niveau Real-Time CDP que vous avez achetés :

* [Toutes les descriptions de produits Adobe](https://helpx.adobe.com/fr/legal/product-descriptions.html)
* [Real-time Customer Data Platform (Édition B2C - Packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (Édition B2P - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (Édition B2B - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## Étapes suivantes

Après avoir compris les barrières de sécurité qui s’appliquent à divers domaines et services de Real-Time CDP, vous pouvez suivre une [exemple de cas d’utilisation d’une mise en oeuvre Real-Time CDP](/help/rtcdp/get-started.md).
