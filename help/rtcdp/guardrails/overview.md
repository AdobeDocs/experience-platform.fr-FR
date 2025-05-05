---
title: Mécanismes de sécurisation de Real-Time CDP
description: Découvrez les mécanismes de sécurisation des données dans les différents services et zones de Real-Time CDP.
feature: Guardrails, Data Management, Data Ingestion, Data Export
exl-id: 377499b4-5707-4d50-94e3-02f88ad5bf2c
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 7%

---

# Mécanismes de sécurisation de Real-Time CDP

Les mécanismes de sécurisation sont des seuils qui fournissent des conseils pour l’utilisation des données et du système, l’optimisation des performances et la prévention des erreurs ou des résultats inattendus dans Real-Time CDP. Les mécanismes de sécurisation peuvent faire référence à l’utilisation ou la consommation de données et de traitement par rapport à vos droits de licence.

>[!IMPORTANT]
>
>Vérifiez vos droits de licence dans votre commande client et la [Description du produit](https://helpx.adobe.com/fr/legal/product-descriptions.html) correspondante sur les limites d’utilisation réelles en plus de cette page de mécanismes de sécurisation.

Commencez ici et suivez les liens ci-dessous pour découvrir tous les mécanismes de sécurisation dans les différents services et domaines de Real-Time CDP :

* [Barrières de sécurité pour l’ingestion de données](/help/ingestion/guardrails.md)
* [Mécanismes de sécurisation pour  [!DNL Edge Network API]](https://developer.adobe.com/data-collection-apis/docs/getting-started/guardrails/)
* [Mécanismes de sécurisation pour les  [!DNL Real-Time Customer Profile]  et la segmentation](/help/profile/guardrails.md)
* [Mécanismes de sécurisation pour  [!DNL Identity Service]  données](/help/identity-service/guardrails.md)
* [Mécanismes de sécurisation pour  [!DNL Query Service]](/help/query-service/guardrails.md)
* [Mécanismes de sécurisation pour l’activation des données via les destinations](/help/destinations/guardrails.md)
* [Mécanismes de sécurisation pour Real-Time CDP B2B](/help/rtcdp/b2b-guardrails.md)

>[!TIP]
>
>Consultez également la page [Plans directeurs de l’expérience digitale](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=fr) pour obtenir plus d’informations, telles que [diagrammes de latence de bout en bout](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=fr#end-to-end-latency-diagrams) pour divers services Experience Platform.

## Types de mécanismes de sécurisation {#guardrail-types}

Notez que les deux types de mécanismes de sécurisation dans toutes les zones et tous les services Real-Time CDP sont les suivants :

| Type de mécanisme de sécurisation | Description |
|----------|---------|
| **Mécanisme de sécurisation des performances (limite soft)** | Les mécanismes de sécurisation de performances sont des limites d’utilisation liées à la portée de vos cas d’utilisation. Si vous dépassez les mécanismes de sécurisation des performances, vous pouvez rencontrer une dégradation des performances et une latence. Adobe n’est pas responsable de cette dégradation des performances. Les clients qui dépassent régulièrement un mécanisme de sécurisation des performances peuvent choisir de se procurer une licence pour une capacité supplémentaire afin d’éviter une dégradation des performances. |
| **Mécanismes de sécurisation appliqués par le système (limite Hard)** | Les mécanismes de sécurisation appliqués par le système sont appliqués par l’interface utilisateur ou l’API Real-Time CDP. Il s’agit de limites que vous ne pouvez pas dépasser, car l’interface utilisateur et l’API vous en empêcheront ou renverront une erreur. |

{style="table-layout:auto"}

## Informations de licence et de droit Real-Time CDP {#product-descriptions}

Consultez également les liens de description du produit ci-dessous pour obtenir des informations de licence et de droit en fonction de l’édition et du niveau de Real-Time CDP que vous avez achetés :

* [Toutes les descriptions des produits Adobe](https://helpx.adobe.com/fr/legal/product-descriptions.html)
* [Real-Time Customer Data Platform (B2C Edition - Packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (édition B2P - packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B edition - Packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## Mécanismes de sécurisation pour d’autres applications Experience Platform  {#guardrails-other-aep-apps}

Des mécanismes de sécurisation similaires existent pour d’autres applications Experience Platform. Pour plus d’informations, consultez les liens ci-dessous :

* [Mécanismes de sécurisation de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=fr)
* [Mécanismes de sécurisation de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=fr)

## Étapes suivantes

Après avoir compris les mécanismes de sécurisation qui s’appliquent à divers domaines et services de Real-Time CDP, vous pouvez suivre un [exemple de cas d’utilisation d’une implémentation de Real-Time CDP](/help/rtcdp/get-started.md).
