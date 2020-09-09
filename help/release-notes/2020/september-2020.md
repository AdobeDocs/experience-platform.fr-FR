---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 9 septembre 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 64b6b59923d549cdcbf35d2e375529aec8cf81b8
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 45%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 9 septembre 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[ ! Gouvernance des données DNL]](#governance)
* [[ !Destinations DNL]](#destinations)
* [[ !Sources DNL]](#sources)

## [!DNL Data Governance] {#governance}

Dans Adobe Experience Platform, la gouvernance des données désigne un ensemble de stratégies et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux stratégies applicables à l’utilisation des données. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Améliorations de l’interface utilisateur d’étiquetage des jeux de données | Plusieurs nouvelles commandes de tri et de filtrage ont été ajoutées à l’interface d’étiquetage des jeux de données afin de faciliter l’utilisation des schémas volumineux : <ul><li>Triez les champs par ordre alphabétique en fonction du chemin d’accès complet au schéma.</li><li>Effectuez des recherches partielles sur les noms de chemin d’accès aux champs.</li><li>Filtrez les champs sans libellé, avec une étiquette sélectionnée ou avec une catégorie d’étiquettes.</li></ul> |

Pour plus d’informations sur ce service, consultez la [présentation de la gouvernance des données.](../../data-governance/home.md)

## Destinations {#destinations}

Dans la [plateforme de données clients en temps réel d’Adobe](../../rtcdp/overview.md), les destinations sont des intégrations prédéfinies avec des plateformes de destination qui activent les données vers ces partenaires de manière transparente.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations de l&#39;environnement | Les utilisateurs peuvent accéder aux actions de tableaux intégrés pour accéder plus facilement aux actions Principales, telles que l’ajout de données, la modification de la planification et l’ajout de segments. See the [destinations workspace](../../rtcdp/destinations/destinations-workspace.md) document for more information. |

Pour en savoir plus, consultez la [présentation des destinations](../../rtcdp/destinations/destinations-overview.md)

## Sources {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mappage automatique | [!DNL Platform] fournit des recommandations intelligentes pour le mappage automatique au cours du processus d’assimilation des données, en fonction d’un schéma de cible ou d’un jeu de données sélectionné par l’utilisateur. Vous pouvez ajuster manuellement des règles de mappage automatique flexibles en fonction de vos cas d’utilisation. |
| Améliorations de l&#39;environnement | Les utilisateurs peuvent accéder aux actions de tableaux intégrés pour accéder plus facilement aux actions Principales, telles que l’ajout de données, la modification de la planification et l’ajout de segments. Pour plus d&#39;informations, consultez le document des flux [de données de](../../sources/tutorials/ui/monitor.md) surveillance. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).