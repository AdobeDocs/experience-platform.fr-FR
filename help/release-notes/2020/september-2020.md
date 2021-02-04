---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 9 septembre 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 29%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 9 septembre 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Governance]](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

Dans Adobe Experience Platform, la gouvernance des données désigne un ensemble de stratégies et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux stratégies applicables à l’utilisation des données. Il joue un rôle clé à l&#39;intérieur de [!DNL Experience Platform] à divers niveaux, notamment le catalogage, la lignée de données, l&#39;étiquetage de l&#39;utilisation des données, les stratégies d&#39;accès aux données et le contrôle d&#39;accès sur les données pour les actions marketing.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations de l’interface utilisateur d’étiquetage des jeux de données | Plusieurs nouvelles commandes de tri et de filtrage ont été ajoutées à l’interface d’étiquetage des jeux de données afin de faciliter l’utilisation des schémas volumineux : <ul><li>Triez les champs par ordre alphabétique en fonction du chemin d’accès complet au schéma.</li><li>Effectuez des recherches partielles sur les noms de chemin d’accès aux champs.</li><li>Filtrez les champs sans libellé, avec une étiquette sélectionnée ou avec une catégorie d’étiquettes.</li></ul> |

Pour plus d’informations sur ce service, consultez la [présentation de la gouvernance des données.](../../data-governance/home.md)

## Destinations {#destinations}

Dans [Plate-forme de données client en temps réel](../../rtcdp/overview.md), les destinations sont des intégrations préétablies avec les plateformes de destination qui activent les données à ces partenaires de manière transparente.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations de l&#39;environnement | Les utilisateurs peuvent accéder aux actions de tableaux intégrés pour accéder plus facilement aux actions Principales, telles que l’ajout de données, la modification de la planification et l’ajout de segments. Pour plus d&#39;informations, consultez le document [Destinations workspace](../../destinations/ui/destinations-workspace.md). |

Pour en savoir plus, consultez la [présentation des destinations](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] vous permet de surveiller les activités sur Adobe Experience Platform à l’aide de mesures statistiques et de notifications de événement.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Notifications Événement Adobe I/O | [!DNL Observability Insights] tire parti des Événements Adobe I/O pour créer des notifications de événement pour plusieurs services Experience Platform. Les charges de notification sont envoyées à un hook Web configuré que vous pouvez ensuite utiliser pour automatiser d’autres processus en aval. Pour plus d&#39;informations, consultez l&#39;[aperçu des notifications](../../observability/notifications/overview.md). |

Pour plus d’informations sur le service, voir [[!DNL Observability Insights] overview](../../observability/home.md).

## [!DNL Privacy Service] {#privacy}

Plusieurs réglementations légales et organisationnelles donnent aux utilisateurs le droit d&#39;accéder à vos données personnelles ou de les supprimer de vos entrepôts de données sur demande. Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface utilisateur pour vous aider à gérer ces requêtes de données de vos clients. Avec [!DNL Privacy Service], vous pouvez envoyer des demandes d&#39;accès et de suppression de données clients privées ou personnelles des applications Adobe Experience Cloud, ce qui vous permet de respecter automatiquement les réglementations légales et de confidentialité de l&#39;entreprise.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de la LGPD (Brésil) | Des emplois dans le domaine de la protection de la vie privée peuvent désormais être créés en vertu de la réglementation brésilienne [!DNL Lei Geral de Proteção de Dados] (LGPD). Ces emplois sont suivis sous le code de réglementation `lgpd_bra`. |

Pour plus d’informations sur le service, consultez la [présentation du Privacy Service](../../privacy-service/home.md).

## Real-time Customer Profile {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. [!DNL Real-time Customer Profile] permet de visualiser une vue holistique de chaque client qui combine des données provenant de plusieurs canaux, y compris des données en ligne, hors ligne, CRM et tierces. [!DNL Profile] vous permet de consolider vos données client disparates en une vue unifiée offrant un compte d’activité horodaté de chaque interaction client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Visionneuse de profils | Le lecteur de profil, dans l’interface utilisateur de la plate-forme, a été mis à jour pour être un tableau de bord entièrement personnalisé. L’utilisateur peut désormais effectuer les tâches suivantes : <ul><li>Mettez à jour les attributs standard et personnalisés sélectionnés dans le widget d&#39;informations de base.</li><li>Créer, modifier et supprimer des widgets personnalisés</li><li>Redimensionner et réorganiser les widgets</li></ul> |

Pour plus d&#39;informations sur [!DNL Real-time Customer Profile], y compris des didacticiels et les meilleures pratiques pour travailler avec les données [!DNL Profile], consultez la [Présentation du Profil client en temps réel](../../profile/home.md).

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données [!DNL Real-time Customer Profile]. Ces segments sont configurés et gérés de manière centralisée sur [!DNL Platform], ce qui les rend facilement accessibles par toute application d&#39;Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Tâches d’exportation | Un indicateur a été ajouté pour permettre l’évaluation des segments dans le cadre d’une tâche d’exportation. En conséquence, les utilisateurs peuvent exécuter la segmentation et les exportations dans une seule tâche. |
| Stratégies de fusion | Plusieurs stratégies de fusion peuvent être incluses dans une seule tâche de segmentation par lot. |

Pour plus d&#39;informations sur [!DNL Segmentation Service], consultez la [Présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mappage automatique | [!DNL Platform] fournit des recommandations intelligentes pour le mappage automatique au cours du processus d’assimilation des données, en fonction d’un schéma de cible ou d’un jeu de données sélectionné par l’utilisateur. Vous pouvez ajuster manuellement des règles de mappage automatique flexibles en fonction de vos cas d’utilisation. |
| Améliorations de l&#39;environnement | Les utilisateurs peuvent accéder aux actions de tableaux intégrés pour accéder plus facilement aux actions Principales, telles que l’ajout de données, la modification de la planification et l’ajout de segments. Pour plus d&#39;informations, consultez le document [surveillance des flux de données](../../sources/tutorials/ui/monitor.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
