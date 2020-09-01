---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriels sur la gouvernance et la confidentialité des données
topic: tutorial
description: Data Usage Labeling and Enforcement (DULE) constitue le mécanisme de base de la gouvernance des données d’Adobe Experience Platform. Les fonctionnalités de DULE vous permettent d’appliquer des libellés d’utilisation des données aux jeux de données et aux champs, en les classant en fonction des stratégies d’utilisation des données associées.
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 65%

---


# [!DNL Data Governance] et [!DNL Privacy] Tutorials

[!DNL Data Usage Labeling and Enforcement] (DULE) est le mécanisme central de Adobe Experience Platform [!DNL Data Governance]. Les fonctionnalités de DULE vous permettent d’appliquer des libellés d’utilisation des données aux jeux de données et aux champs, en les classant en fonction des stratégies d’utilisation des données associées. Avant de commencer avec les libellés, consultez la [présentation de la gouvernance des données](../data-governance/home.md) pour une introduction plus détaillée de la structure DULE dans [!DNL Platform].

Adobe Experience Platform [!DNL Privacy Service] provides a RESTful API and user interface that allow you to coordinate privacy and compliance requests across various solutions. Pour en savoir plus, commencez par lire la [présentation de Privacy Service](../privacy-service/home.md).

## Ajout de libellés d’utilisation des données

Les libellés d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Best practices encourage labeling data as soon as it is ingested into [!DNL Experience Platform], or as soon as data becomes available for use in [!DNL Platform]. Les libellés d’utilisation des données appliqués au niveau du jeu de données sont propagés à tous les champs du jeu de données. Vous pouvez également appliquer les libellés directement sur des champs individuels (en-têtes de colonne) d’un jeu de données, sans propagation. Pour apprendre à appliquer des libellés d’utilisation des données à vos données, consultez la [présentation des libellés d’utilisation des données](../data-governance/labels/overview.md).

## Création de stratégies d’utilisation des données

The DULE [!DNL Policy Service] API allows you to create and manage DULE policies to determine what marketing actions can be taken against data that contains certain DULE labels. Pour commencer, lisez la [présentation des stratégies d’utilisation des données](../data-governance/policies/overview.md).

## Application des stratégies d’utilisation des données

Once you have created Data Usage Labeling and Enforcement (DULE) labels for your data, and have created DULE policies for marketing actions against those labels, you can use the DULE [!DNL Policy Service] API to evaluate whether a marketing action performed on a dataset, or an arbitrary group of DULE labels, constitutes a policy violation. Vous pouvez ensuite configurer vos propres protocoles internes pour gérer les violations de stratégie en fonction de la réponse de l’API. Pour commencer, consultez la [présentation de l’application des stratégies](../data-governance/enforcement/overview.md).

## Application de la conformité de l’utilisation des données pour un segment ciblé

Segments that are enabled for use in [!DNL Real-time Customer Profile] contain a merge policy ID within their segment definition. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui à leur tour contiennent les libellés d’utilisation de données applicables. Pour connaître les étapes spécifiques à l’application de la conformité de l’utilisation des données pour un segment ciblé, suivez le [tutoriel sur l’application de la conformité de l’utilisation des données pour les segments](../segmentation/tutorials/governance.md).

## Get started with [!DNL Privacy Service]

[!DNL Privacy Service] fournit une API RESTful et une interface utilisateur qui vous permettent de gérer les données personnelles de vos titulaires de données (clients) dans les applications Adobe Experience Cloud. [!DNL Privacy Service] fournit aussi un mécanisme central d’audit et de connexion qui vous permet d’accéder à l’état et aux résultats des tâches impliquant des applications [!DNL Experience Cloud] For instructions showing how to create and monitor [!DNL Privacy Service] jobs, follow the steps provided in the [Privacy Service developer guide](../privacy-service/api/getting-started.md) or the [Privacy Service user guide](../privacy-service/ui/overview.md).