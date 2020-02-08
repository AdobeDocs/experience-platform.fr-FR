---
title: Présentation de la gouvernance des données
seo-title: Gouvernance des données dans la plateforme de données client en temps réel
description: 'La gouvernance des données vous permet de gérer les données client et de vous assurer de la conformité aux réglementations, restrictions et stratégies applicables à l’utilisation des données. '
seo-description: 'La gouvernance des données vous permet de gérer les données client et de vous assurer de la conformité aux réglementations, restrictions et stratégies applicables à l’utilisation des données. '
translation-type: tm+mt
source-git-commit: c583d0ab89dad61e00ba117f7f2e0ec5ab427745

---


# Gouvernance des données dans le CDP en temps réel

La plate-forme de données clientes en temps réel (CDP en temps réel) rassemble les données de plusieurs systèmes d’entreprise, ce qui permet aux spécialistes du marketing de mieux identifier, comprendre et impliquer leurs clients. Ces données peuvent être soumises à des restrictions d&#39;utilisation définies par votre organisation ou par des réglementations légales. Il est donc important de s’assurer que le CDP en temps réel est conforme aux règles d’utilisation lors de la gestion de vos données.

La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données client et de vous assurer de la conformité aux réglementations, restrictions et stratégies applicables à l’utilisation des données. Il joue un rôle clé dans le CDP en temps réel, ce qui vous permet de définir des stratégies d’utilisation, de classer vos données en fonction de ces stratégies et de rechercher les violations de stratégies lors de l’exécution de certaines actions marketing.

Le CDP en temps réel repose sur Adobe Experience Platform. La plupart des fonctionnalités de gouvernance des données sont donc abordées dans la documentation de la plateforme d’expérience. Ce document est destiné à compléter l’aperçu [de la gouvernance des](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) données pour la plateforme d’expérience et décrit les fonctionnalités de gouvernance disponibles dans le CDP en temps réel. Les sujets suivants sont abordés :

* [Appliquer des libellés d’utilisation à vos données](#apply-usage-labels-to-your-data)
* [Gestion des stratégies d’utilisation des données](#manage-data-usage-policies)
* [Appliquer la conformité d’utilisation des données](#enforce-data-usage-compliance)

## Appliquer des libellés d’utilisation à vos données

La gouvernance des données vous permet d’appliquer des libellés d’utilisation à vos données, soit au niveau du jeu de données, soit au niveau du champ du jeu de données. Les étiquettes d’utilisation des données vous permettent de classer les données en fonction des stratégies d’utilisation qui s’appliquent à ces données.

Pour plus d’informations sur l’utilisation des libellés d’utilisation des données, voir le guide [d’utilisation des libellés d’utilisation des](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/tutorials/dule/dule_working_with_labels.md) données pour Adobe Experience Platform.

<!-- (To be included after destinations support is available -- January 2020)
## Set restrictions on destinations

You can set data usage restrictions on a destination by defining the marketing use cases for that destination. Defining use cases for destinations allows you to check for usage policy violations and ensure that any profiles or segments sent to that destination are compatible with Data Governance rules.

Marketing use cases can be defined during the _Setup_ phase for the _Edit Destination_ workflow. See the destination documentation for more information. 
-->


## Gestion des stratégies d’utilisation des données

Pour que les étiquettes d’utilisation des données prennent en charge efficacement la conformité des données, les stratégies d’utilisation des données doivent être définies et activées. Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé à exécuter, ou dont vous n’êtes pas autorisé à effectuer, sur des données dans le CDP en temps réel. Pour plus d’informations, voir la section &quot;Stratégies d’utilisation des données&quot; dans l’aperçu [de la gouvernance des](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) données de la plateforme d’expérience.

Adobe Experience Platform fournit plusieurs stratégies **** principales pour les cas d’utilisation courants de l’expérience client. Ces stratégies peuvent être consultées en adressant une requête à l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)DULE Policy Service, comme illustré dans la section &quot;Répertorier toutes les stratégies&quot; du guide [du développeur de](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_policy_service_developer_guide.md)Policy Service. Vous pouvez également créer vos propres stratégies **** personnalisées pour modéliser les restrictions d’utilisation personnalisées, comme le montre la section &quot;Créer une stratégie&quot; du guide du développeur.

## Appliquer la conformité d’utilisation des données

Une fois que les données sont étiquetées et que les stratégies d’utilisation sont définies, vous pouvez faire respecter les stratégies d’utilisation des données. Pour plus d’informations, consultez le didacticiel sur l’ [application de la conformité à l’utilisation des données pour les segments](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/dule/data_governance_and_segmentation.md) d’audience.

## Étapes suivantes

Maintenant que vous avez été familiarisé avec les principales fonctionnalités de gouvernance des données sur le CDP en temps réel et la manière dont la plateforme d’expérience les active, reportez-vous à la [documentation relative à la gouvernance des données sur la plateforme](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html)Adobe Experience. La documentation présente des vues d’ensemble des concepts essentiels de gouvernance des données, ainsi que des flux de travail détaillés pour la gestion des étiquettes et des stratégies d’utilisation des données.