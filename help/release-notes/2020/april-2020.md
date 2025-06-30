---
title: Notes de mise à jour d’Adobe Experience Platform - Avril 2020
description: Notes de mise à jour d’avril 2020 pour Adobe Experience Platform.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: notes de mise à jour ;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 104db777446b19fa9e3ea7538ae1dda6f51a00b1
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 63%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : jeudi 8 avril 2020**

Nouvelles fonctionnalités d’Adobe Experience Platform :
* [[!DNL Intelligent Services]](#intelligent)

Mises à jour des fonctionnalités existantes :
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Gouvernance des données](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] permet aux analystes et aux spécialistes du marketing d’exploiter la puissance de l’intelligence artificielle et du machine learning dans les cas d’utilisation de l’expérience client. Les analystes marketing peuvent obtenir des prédictions spécifiques aux besoins d’une entreprise en utilisant des configurations au niveau de l’entreprise sans avoir besoin d’expertise en sciences des données. De plus, les spécialistes du marketing peuvent activer les prédictions dans Adobe Experience Cloud, Adobe Experience Platform et les applications tierces.

**Fonctionnalités clés**

| Fonctionnalité | Description |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] permet aux professionnels du marketing de générer des prédictions client au niveau individuel avec des explications. À l’aide de facteurs d’influence, [!DNL Customer AI] pouvez savoir ce qu’un client est susceptible de faire et pourquoi. En outre, les professionnels du marketing peuvent tirer parti des prédictions et des informations [!DNL Customer AI] pour personnaliser les expériences client en diffusant les offres et les messages les plus appropriés. |
| [!DNL Attribution AI] | [!DNL Attribution AI] est un service d’attribution algorithmique à plusieurs canaux qui calcule l’influence et l’impact incrémentiel des interactions des clients par rapport à des résultats spécifiés. Grâce à [!DNL Attribution AI], les professionnels du marketing peuvent mesurer et optimiser les dépenses publicitaires et marketing en comprenant l’impact de chaque interaction client sur chaque phase des parcours des clients. |

**Problèmes connus**

* Aucun problème connu pour le moment.

Pour plus d’informations sur les [!DNL Intelligent Services] et ce qu’ils ont à offrir, reportez-vous à la [ présentation des services intelligents ](../../intelligent-services/home.md).

## Système d’[!DNL Experience Data Model] (XDM) {#xdm}

La normalisation et l’interopérabilité sont des concepts clés pour [!DNL Experience Platform]. Le modèle de données [!DNL Experience Data Model] d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences digitales. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Informations d’affichage de remplacement automatique | Le [!DNL Schema Registry] applique automatiquement les valeurs de titre et de description personnalisées configurées dans le descripteur `alternateDisplayInfo`. |
| Restrictions des champs scalaires | Le [!DNL Schema Registry] n’autorise pas plus de 6 000 champs scalaires dans un seul schéma. |
| Révision des performances | Le [!DNL Schema Registry] a été remanié pour mieux fonctionner et répondre aux exigences des [!DNL Experience Platform]. |

**Corrections de bogues**

* XDM mis à jour converti en XED pour prendre en charge un format XED plus propre pour les champs URI imbriqués dans XDM standard.

**Problèmes connus**

* Connu

## Gouvernance des données {#governance}

Dans Adobe Experience Platform, la gouvernance des données désigne un ensemble de politiques et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle clé dans [!DNL Experience Platform] à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’accès aux données et le contrôle d’accès aux données pour les actions marketing.

La prise en main de la gouvernance des données nécessite une compréhension approfondie des réglementations, des obligations contractuelles et des politiques d’entreprise qui s’appliquent aux données clients. À partir de là, les données peuvent être classifiées en appliquant les libellés d’utilisation des données appropriés, et leur utilisation peut être contrôlée via la définition des politiques d’utilisation des données.

Le cadre de gouvernance des données simplifie et rationalise le processus de catégorisation des données et de création des politiques d’utilisation des données par le biais de l’interface utilisateur [!DNL Experience Platform] et de l’API [!DNL Policy Service].

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Gestion des politiques d’utilisation des données dans l’interface utilisateur | Les politiques d’utilisation des données peuvent désormais être gérées dans l’espace de travail **Politiques** de l’interface utilisateur de [!DNL Experience Platform]. Pour plus d’informations, voir le [guide d’utilisation des politiques](../../data-governance/policies/user-guide.md). |

**Problèmes connus**

* Aucun.

Pour plus d’informations, consultez la section [Présentation de la gouvernance des données](../../data-governance/home.md).


## Destinations {#destinations}

Dans [Real-Time Customer Data Platform](../../rtcdp/overview.md), les destinations sont des intégrations préconfigurées à des plateformes de destination qui activent les données vers ces partenaires de manière transparente.

**Nouvelles destinations**

Real-Time CDP prend désormais en charge l’activation de données pour plus de cinquante extensions [!DNL Experience Cloud Launch], ce qui permet d’utiliser des analyses, de la personnalisation et d’autres cas d’utilisation. Voir ci-dessous pour plus de détails :

| Documentation | Description |
|--- | ---|
| [Types et catégories de destination](../../destinations/destination-types.md) | Cet article explique la différence entre les connexions et les extensions dans l’interface Real-Time CDP et recommande quand utiliser chacune de ces destinations. |
| [Extensions d’Experience Platform Launch](../../destinations/catalog/launch-extensions/overview.md) | Cette page explique ce que sont les extensions [!DNL Launch], répertorie les cas d’utilisation et fournit des liens vers la documentation pour chaque extension [!DNL Launch] dans Real-Time CDP. |

Pour plus d’informations, reportez-vous à la [présentation des destinations](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d’accéder à leurs données personnelles et de les supprimer de vos banques de données sur demande. Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface d’utilisation pour vous aider à gérer ces requêtes de données de votre clientèle. Grâce à [!DNL Privacy Service], vous pouvez envoyer des demandes d’accès et de suppression de données clientèle personnelles depuis les applications Adobe Experience Cloud. Cela facilite l’automatisation de la mise en conformité concernant les réglementations légales et organisationnelles liées à la confidentialité.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Respect de la loi PDPA | Désormais, les demandes d’accès à des informations personnelles peuvent être créées et suivies en vertu de la loi sur la protection des données à caractère personnel (PDPA) en Thaïlande. Lors de l’envoi de demandes d’accès à des informations personnelles dans l’API, le tableau `regulation` accepte la valeur « pdpa_tha ». |
| Types d’espaces de noms dans l’interface utilisateur | Vous pouvez désormais spécifier différents types d’espaces de noms dans le créateur de requêtes de l’interface utilisateur de [!DNL Privacy Service]. Pour plus d’informations, voir le [guide d’utilisation](../../privacy-service/ui/user-guide.md). |
| Abandon de l’ancien point d’entrée | L’ancien point d’entrée de l’API (`data/privacy/gdpr`) a été abandonné. |

Problèmes connus

* Aucun

Pour plus d’informations sur [!DNL Privacy Service], commencez par lire la présentation de Privacy Service [](../../privacy-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Experience Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge des API et de l’interface utilisateur pour les bases de données | Nouveaux connecteurs source pour [!DNL Apache Spark] (sur HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage] et [!DNL Hive]. |
| Prise en charge des API et de l’interface utilisateur pour les applications basées sur les protocoles | Nouveaux connecteurs source pour [!DNL Generic OData]. |

**Problèmes connus**

* Aucun

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
