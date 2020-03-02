---
title: Présentation de la gouvernance des données
seo-title: Gouvernance des données sur la plateforme de données client en temps réel
description: 'La gouvernance des données vous permet de gérer les données client et de garantir la conformité aux réglementations, restrictions et stratégies applicables à l’utilisation des données. '
seo-description: 'La gouvernance des données vous permet de gérer les données client et de garantir la conformité aux réglementations, restrictions et stratégies applicables à l’utilisation des données. '
translation-type: ht
source-git-commit: c583d0ab89dad61e00ba117f7f2e0ec5ab427745

---


# Gouvernance des données sur la plateforme CDP en temps réel

La plateforme de données client (CDP) en temps réel rassemble les données de plusieurs systèmes d’entreprise, ce qui permet aux spécialistes marketing de mieux identifier, comprendre et impliquer leurs clients. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Il est donc important de s’assurer que la plateforme CDP en temps réel est conforme aux stratégies d’utilisation lors de la gestion de vos données.

La gouvernance des données Adobe Experience Platform vous permet de gérer les données client et de garantir la conformité aux réglementations, restrictions et stratégies applicables à l’utilisation des données. Elle joue un rôle essentiel sur la plateforme CDP en temps réel, ce qui vous permet de définir des stratégies d’utilisation, de classer vos données en fonction de ces stratégies et de rechercher les violations de stratégies lors de l’exécution de certaines actions de marketing.

La plateforme CDP en temps réel repose sur Adobe Experience Platform. La plupart des fonctionnalités de gouvernance des données sont donc abordées dans la documentation d’Experience Platform. Ce document est destiné à compléter la [présentation de la gouvernance des données](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) pour Experience Platform et décrit les fonctionnalités de gouvernance disponibles dans la plateforme CDP en temps réel. Les sujets suivants sont abordés :

* [Appliquer des étiquettes d’utilisation sur les données](#apply-usage-labels-to-your-data)
* [Gérer des stratégies d’utilisation des données](#manage-data-usage-policies)
* [Appliquer des stratégies d’utilisation des données](#enforce-data-usage-compliance)

## Appliquer des étiquettes d’utilisation sur les données

La gouvernance des données vous permet d’appliquer des étiquettes d’utilisation sur les données, soit au niveau du jeu de données, soit au niveau du champ du jeu de données. Les étiquettes d’utilisation des données vous permettent de classer les données en fonction des stratégies d’utilisation qui s’appliquent à ces données.

Pour plus d’informations sur l’utilisation des étiquettes d’utilisation des données, consultez le [Guide de l’utilisateur des étiquettes d’utilisation des données](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/tutorials/dule/dule_working_with_labels.md) pour Adobe Experience Platform.

<!-- (To be included after destinations support is available -- January 2020)
## Set restrictions on destinations

You can set data usage restrictions on a destination by defining the marketing use cases for that destination. Defining use cases for destinations allows you to check for usage policy violations and ensure that any profiles or segments sent to that destination are compatible with Data Governance rules.

Marketing use cases can be defined during the _Setup_ phase for the _Edit Destination_ workflow. See the destination documentation for more information. 
-->


## Gérer des stratégies d’utilisation des données

Les stratégies d’utilisation des données doivent être définies et activées pour que les étiquettes d’utilisation des données prennent en charge efficacement la conformité des données. Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions de marketing que vous êtes autorisé, ou non, à effectuer sur des données de la plateforme CDP en temps réel. Pour plus d’informations, consultez la section « Stratégies d’utilisation des données » dans la [présentation de la gouvernance des données](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) d’Experience Platform.

Adobe Experience Platform propose plusieurs **stratégies principales** pour les cas d’utilisation courants de l’expérience client. Ces stratégies peuvent être consultées en adressant une requête à l’[API du service stratégique des étiquettes DULE (Data Usage Labeling and Enforcement)](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml), comme illustré dans la section « Répertorier toutes les stratégies » du [Guide du développeur du service stratégique](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_policy_service_developer_guide.md). Vous pouvez également créer vos propres **stratégies personnalisées** pour modéliser des restrictions d’utilisation personnalisées, comme illustré dans la section « Créer une stratégie » du guide du développeur.

## Appliquer des stratégies d’utilisation des données

Une fois que les données sont étiquetées et que les stratégies d’utilisation sont définies, vous pouvez appliquer les stratégies d’utilisation des données. Pour plus d’informations, consultez le tutoriel sur l’[application des stratégies d’utilisation des données pour les segments d’audience](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/dule/data_governance_and_segmentation.md).

## Étapes suivantes

Maintenant que vous avez découvert les principales fonctionnalités de gouvernance des données sur la plateforme CDP en temps réel et la méthode utilisée par Experience Platform pour les activer, reportez-vous à la [documentation relative à la gouvernance des données sur Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html). La documentation offre des présentations sur les principaux concepts de la gouvernance des données, ainsi que sur les workflows détaillés de gestion des étiquettes et des stratégies d’utilisation des données.