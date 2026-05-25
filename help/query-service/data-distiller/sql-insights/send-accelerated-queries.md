---
title: Envoi de requêtes accélérées
description: Présentation de l’API de requêtes accélérées.
exl-id: c6cd1182-d3a9-457f-81d5-18027e47c3f9
TQID: https://experienceleague.adobe.com/azW144gC6Z6W2IFZi7yu-ENR69q5zuFBAfvr6bWpWFA
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
subfeature_v2:
  - id: f6ac78a3-5b59-40f5-a37d-45df5303d3a3
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 210
ht-degree: 15%

---

# Envoi de requêtes accélérées

Dans le cadre du SKU Data Distiller, l’[API Query Service](https://developer.adobe.com/experience-platform-apis/references/query-service/) vous permet d’effectuer des requêtes sans état vers la boutique accélérée. Le point d’entrée [requêtes accélérées](https://developer.adobe.com/experience-platform-apis/references/query-service/#tag/Accelerated-Queries) renvoie des résultats en fonction de données agrégées afin de réduire le temps d’attente des résultats et de fournir un échange d’informations plus interactif.

Consultez la documentation [&#x200B; Point d’entrée de requêtes accélérées &#x200B;](../../api/accelerated-queries.md) pour obtenir des instructions sur la manière d’interroger la boutique accélérée.

Avec le magasin d’accélération des requêtes, vous pouvez créer un modèle de données personnalisé et/ou étendre un modèle de données Adobe Real-Time Customer Data Platform existant. Pour utiliser ou incorporer vos informations de rapports dans un framework de création de rapports/visualisation, consultez le guide [Guide d’informations sur les rapports du magasin accéléré de requêtes](./reporting-insights-data-model.md). Vous pouvez également lire la documentation du modèle de données d’informations Real-Time Customer Data Platform pour savoir comment [personnaliser vos modèles de requête SQL pour créer des rapports Real-Time CDP pour vos cas d’utilisation de marketing et d’indicateurs clés de performance (KPI)](../../../dashboards/data-models/cdp-insights-data-model-b2c.md). Vous pouvez utiliser la [fonctionnalité de contrôle d’accès basé sur les attributs](../../../access-control/abac/overview.md) pour contrôler le niveau de restriction des jeux de données dans la boutique accélérée. Consultez la section [&#x200B; gouvernance des données dans Query Service](../../data-governance/overview.md#create-field-based-access-restrictions-on-accelerated-datasets)
pour plus d’informations.
