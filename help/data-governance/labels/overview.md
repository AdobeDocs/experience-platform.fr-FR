---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation des étiquettes d’utilisation des données
topic: labels
translation-type: tm+mt
source-git-commit: 4b6b9ca5ae7861f8e8b974550be14fbce6efdcf1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Présentation des étiquettes d’utilisation des données

L’étiquetage et l’application de l’utilisation des données (DULE) constituent le mécanisme de base de la gouvernance des données de la plate-forme Adobe Experience. Les fonctions DULE permettent d&#39;appliquer des étiquettes d&#39;utilisation des données aux jeux de données et aux champs, en les classant en fonction des stratégies d&#39;utilisation des données associées.

Ce document fournit un aperçu des étiquettes d’utilisation des données (également appelées étiquettes DULE) dans la plateforme d’expérience. Avant de lire ce guide, veuillez consulter l&#39;aperçu [de la gouvernance des](../home.md) données pour une introduction plus robuste au cadre DULE.

## Présentation des étiquettes d’utilisation des données

Les étiquettes d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Les étiquettes peuvent être appliquées à tout moment, ce qui vous permet de gérer les données avec souplesse. Les meilleures pratiques encouragent l’étiquetage des données dès qu’elles sont incorporées dans la plate-forme d’expérience ou dès que les données deviennent disponibles pour une utilisation dans la plate-forme.

Les étiquettes d’utilisation des données appliquées au niveau du jeu de données sont propagées à tous les champs du jeu de données. Les étiquettes peuvent également être appliquées directement à des champs individuels (en-têtes de colonne) dans un jeu de données, sans propagation.

Pour plus d’informations sur les étiquettes d’utilisation des données disponibles dans la plateforme d’expérience et les stratégies d’utilisation qu’elles représentent, voir le guide sur les étiquettes [d’utilisation des données](reference.md)prises en charge.

## Héritage d’étiquette pour les segments d’audience

Tous les segments d’audience créés par [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) héritent des étiquettes d’utilisation de leurs jeux de données correspondants. Cela permet aux applications créées sur la plateforme d’expérience (telle que la plateforme de données clientes en temps réel) de fournir une application automatique de la stratégie d’utilisation des données lors de l’activation de segments vers des destinations.

Outre l’héritage d’étiquettes au niveau des jeux de données, les segments héritent par défaut de tous les libellés au niveau des champs de leurs jeux de données associés. Selon la manière dont votre application basée sur une plateforme utilise les segments, vous pouvez éventuellement spécifier les champs utilisés, ce qui empêche le segment d’hériter des étiquettes des champs exclus.

Pour plus d&#39;informations sur le fonctionnement de l&#39;application automatique dans le CDP en temps réel, consultez l&#39;aperçu [de la gouvernance des données CDP en temps](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)réel.

## Étapes suivantes

Maintenant que vous avez introduit des libellés d’utilisation des données, vous pouvez continuer à lire le guide [](user-guide.md) d’utilisateur pour savoir comment gérer les libellés dans l’interface utilisateur de la plate-forme d’expérience. Pour connaître les étapes de gestion des étiquettes à l’aide des API, voir la section appropriée du guide [du développeur](../../catalog/api/labels.md)Catalog Service.