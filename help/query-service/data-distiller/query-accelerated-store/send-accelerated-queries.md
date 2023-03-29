---
title: Envoi de requêtes accélérées
description: Cette section présente l’API de requêtes accélérées.
source-git-commit: 54a6f508818016df1a4ab2a217bc0765b91df9e9
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 14%

---

# Envoi de requêtes accélérées

Dans le cadre du SKU Data Distiller, l’[API Query Service](https://developer.adobe.com/experience-platform-apis/references/query-service/) vous permet d’effectuer des requêtes sans état vers la boutique accélérée. Le [point de terminaison de requêtes accélérées](https://developer.adobe.com/experience-platform-apis/references/query-service/#tag/Accelerated-Queries) renvoie des résultats basés sur des données agrégées afin de réduire le temps d’attente des résultats et de fournir un échange d’informations plus interactif.

Voir [Point d’entrée de requêtes accélérées](../../api/accelerated-queries.md) documentation pour obtenir des instructions sur la manière d’interroger le magasin accéléré.

Avec le magasin accéléré de requêtes, vous pouvez créer un modèle de données personnalisé et/ou étendre un modèle de données Adobe Real-time Customer Data Platform existant. Pour interagir avec vos informations sur les rapports ou les incorporer dans une structure de création de rapports/visualisation, reportez-vous à la section [guide d’informations sur les rapports de magasin accélérés de requête](./reporting-insights-data-model.md). Vous pouvez également lire la documentation du modèle de données Real-time Customer Data Platform Insights pour savoir comment [personnaliser vos modèles de requête SQL pour créer des rapports Real-Time CDP pour vos cas d’utilisation d’indicateurs de performance clés (IPC) et marketing ;](../../../dashboards/cdp-insights-data-model.md). Vous pouvez utiliser la variable [fonctionnalité de contrôle d’accès basé sur les attributs](../../../access-control/abac/overview.md), pour contrôler le niveau de restriction sur les jeux de données dans le magasin accéléré. Voir [gouvernance des données dans Query Service](../../data-governance/overview.md#create-field-based-access-restrictions-on-accelerated-datasets)
pour plus d’informations.
