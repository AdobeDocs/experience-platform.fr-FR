---
title: Envoi de requêtes accélérées
description: Cette section présente l’API de requêtes accélérées.
exl-id: c6cd1182-d3a9-457f-81d5-18027e47c3f9
source-git-commit: 0970fd8fbea86115d92dc78cdba753da69cc2ee6
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 13%

---

# Envoi de requêtes accélérées

Dans le cadre du SKU Data Distiller, l’[API Query Service](https://developer.adobe.com/experience-platform-apis/references/query-service/) vous permet d’effectuer des requêtes sans état vers la boutique accélérée. Le [point d’entrée de requêtes accélérées](https://developer.adobe.com/experience-platform-apis/references/query-service/#tag/Accelerated-Queries) renvoie des résultats basés sur des données agrégées afin de réduire le temps d’attente des résultats et de fournir un exchange d’informations plus interactif.

Pour obtenir des instructions sur la manière d’interroger le magasin accéléré, reportez-vous à la documentation [Accelerated Queries endpoint](../../api/accelerated-queries.md) .

Avec le magasin accéléré de requêtes, vous pouvez créer un modèle de données personnalisé et/ou étendre un modèle de données Adobe Real-Time Customer Data Platform existant. Pour interagir avec vos informations de création de rapports ou les incorporer dans une structure de création de rapports/visualisation, consultez le [guide d’informations de création de rapports de magasin accéléré avec les requêtes](./reporting-insights-data-model.md). Vous pouvez également lire la documentation du modèle de données de Real-Time Customer Data Platform Insights pour savoir comment [personnaliser vos modèles de requête SQL pour créer des rapports Real-Time CDP pour vos cas d’utilisation d’indicateurs de performance clés et marketing](../../../dashboards/data-models/cdp-insights-data-model-b2c.md). Vous pouvez utiliser la [fonctionnalité de contrôle d’accès basé sur les attributs](../../../access-control/abac/overview.md) pour contrôler le niveau de restriction des jeux de données dans le magasin accéléré. Voir la [gouvernance des données dans Query Service](../../data-governance/overview.md#create-field-based-access-restrictions-on-accelerated-datasets)
pour plus d’informations.
