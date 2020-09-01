---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 8 avril 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 60%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 8 avril 2020**

Nouvelles fonctionnalités d’Adobe Experience Platform :
* [[ ! DNL Intelligent Services]](#intelligent)

Mises à jour des fonctionnalités existantes :
* [[ ! Modèle de données d’expérience DNL (XDM)]](#xdm)
* [[ ! Gouvernance des données DNL]](#governance)
* [[ !Destinations DNL]](#destinations)
* [[ ! Privacy Service DNL]](#privacy)
* [[ !Sources DNL]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] permet aux analystes et spécialistes du marketing d’exploiter la puissance de l’intelligence artificielle et de l’apprentissage automatique dans les cas d’utilisation de l’expérience client. Les analystes marketing peuvent obtenir des prédictions spécifiques aux besoins d’une entreprise en utilisant des configurations au niveau de l’entreprise sans avoir besoin d’expertise en sciences des données. De plus, les spécialistes du marketing peuvent activer les prédictions dans Adobe Experience Cloud, Adobe Experience Platform et les applications tierces.

**Fonctionnalités clés**

| Fonctionnalité | Description |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] permet aux professionnels du marketing de générer des prédictions client au niveau individuel avec des explications. With the help of influential factors, [!DNL Customer AI] can tell you what a customer is likely to do and why. Additionally, marketers can benefit from [!DNL Customer AI] predictions and insights to personalize customer experiences by serving the most appropriate offers and messaging. |
| [!DNL Attribution AI] | [!DNL Attribution AI] est un service d’attribution algorithmique à plusieurs canaux qui calcule l’influence et l’impact incrémentiel des interactions des clients par rapport à des résultats spécifiés. With [!DNL Attribution AI], marketers can measure and optimize marketing and advertising spend by understanding the impact of every individual customer interaction across each phase of the customers’ journeys. |

**Problèmes connus**

* Aucun problème connu pour le moment.

For more information on [!DNL Intelligent Services] and what it has to offer, see the [Intelligent Services overview](../../intelligent-services/home.md).

## [!DNL Experience Data Model] Système (XDM) {#xdm}

Standardization and interoperability are key concepts behind [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), piloté par l’Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Informations d’affichage de remplacement automatique | The [!DNL Schema Registry] automatically applies the customized title and description values configured in the `alternateDisplayInfo` descriptor. |
| Restrictions des champs scalaires | The [!DNL Schema Registry] does not allow more than 6000 scalar fields in a single schema. |
| Révision des performances | Le [!DNL Schema Registry] programme a été remanié pour répondre aux exigences d&#39; [!DNL Experience Platform] un meilleur rendement. |

**Corrections de bogues**

* XDM mis à jour converti en XED pour prendre en charge un format XED plus propre pour les champs URI imbriqués dans XDM standard.

**Problèmes connus**

* Connu

## [!DNL Data Governance] {#governance}

Adobe Experience Platform [!DNL Data Governance] is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

La prise en main de la gouvernance des données nécessite une compréhension approfondie des réglementations, des obligations contractuelles et des politiques d’entreprise qui s’appliquent aux données clients. À partir de là, les données peuvent être classifiées en appliquant les libellés d’utilisation des données appropriés, et leur utilisation peut être contrôlée via la définition des stratégies d’utilisation des données.

The [!DNL Data Governance] framework simplifies and streamlines the process of categorizing data and creating data usage policies through the [!DNL Experience Platform] user interface and [!DNL Policy Service] API.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Gestion des stratégies d’utilisation des données dans l’interface utilisateur | Data usage policies can now be managed within the _Policies_ workspace in the [!DNL Experience Platform] UI. Pour plus d’informations, voir le [guide d’utilisation des stratégies](../../data-governance/policies/user-guide.md). |

**Problèmes connus**

* Aucun.

Pour plus d’informations, consultez la section [Présentation de la gouvernance des données](../../data-governance/home.md).


## Destinations {#destinations}

Dans la [plateforme de données clients en temps réel d’Adobe](../../rtcdp/overview.md), les destinations sont des intégrations prédéfinies avec des plateformes de destination qui activent les données vers ces partenaires de manière transparente.

**Nouvelles destinations**

Adobe Real-time CDP now supports data activation to over fifty [!DNL Experience Cloud Launch] extensions, enabling analytics, personalization, and other use cases. Voir ci-dessous pour plus de détails :

| Documentation | Description |
|--- | ---|
| [Types et catégories de destination](/help/rtcdp/destinations/destination-types.md) | Cet article explique la différence entre les connexions et les extensions dans l’interface de la plateforme de données clients en temps réel en temps réel d’Adobe et recommande le moment auquel utiliser chacune de ces destinations. |
| [Extensions d’Experience Platform Launch](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | This page explains what [!DNL Launch] extensions are, lists use cases for using them, and links to documentation for each [!DNL Launch] extension in Adobe Real-time CDP. |

Pour plus d’informations, reportez-vous à la [présentation des destinations](/help/rtcdp/destinations/destinations-overview.md).

## [!DNL Privacy Service] {#privacy}

Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d’accéder à leurs données personnelles et de les supprimer de vos banques de données sur demande. Adobe Experience Platform [!DNL Privacy Service] provides a RESTful API and user interface to help you manage these data requests from your customers. With [!DNL Privacy Service], you can submit requests to access and delete private or personal customer data from Adobe Experience Cloud applications, facilitating automated compliance with legal and organizational privacy regulations.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Respect de la loi PDPA | Désormais, les demandes d’accès à des informations personnelles peuvent être créées et suivies en vertu de la loi sur la protection des données à caractère personnel (PDPA) en Thaïlande. Lors de l’envoi de demandes d’accès à des informations personnelles dans l’API, le tableau `regulation` accepte la valeur « pdpa_tha ». |
| Types d’espaces de noms dans l’interface utilisateur | You can now specify different namespace types in the Request Builder in the [!DNL Privacy Service] UI. Pour plus d’informations, voir le [guide d’utilisation](../../privacy-service/ui/user-guide.md). |
| Abandon de l’ancien point de terminaison | L’ancien point de terminaison de l’API (`data/privacy/gdpr`) a été abandonné. |

Problèmes connus

* Aucun

For more information about [!DNL Privacy Service], please start by reading the [Privacy Service overview](../../privacy-service/home.md).

## Sources {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge des API et de l’interface utilisateur pour les bases de données | Nouveaux connecteurs source pour [!DNL Apache Spark] (sur HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (sur HDInsights) et [!DNL Phoenix]. |
| Prise en charge des API et de l’interface utilisateur pour les applications basées sur les paiements | Nouveaux connecteurs source pour [!DNL PayPal]. |
| Prise en charge des API et de l’interface utilisateur pour les applications basées sur les protocoles | Nouveaux connecteurs source pour [!DNL Generic OData]. |

**Problèmes connus**

* Aucun

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
