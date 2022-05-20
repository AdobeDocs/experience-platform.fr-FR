---
title: Notes de mise à jour de Adobe Experience Platform - Septembre 2020
description: Notes de mise à jour de septembre 2020 pour Adobe Experience Platform.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 34%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 9 septembre 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Gouvernance des données](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## Gouvernance des données {#governance}

Dans Adobe Experience Platform, la gouvernance des données désigne un ensemble de stratégies et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux stratégies applicables à l’utilisation des données. Elle joue un rôle clé dans la [!DNL Experience Platform] à différents niveaux, notamment le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les stratégies d’accès aux données et le contrôle d’accès aux données pour les actions marketing.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations de l’interface utilisateur de l’étiquetage des jeux de données | Plusieurs nouveaux contrôles de tri et de filtrage ont été ajoutés à l’interface utilisateur d’étiquetage des jeux de données afin de faciliter l’utilisation des schémas volumineux : <ul><li>Triez les champs par ordre alphabétique en fonction du chemin d’accès au schéma complet.</li><li>Effectuez des recherches partielles sur les noms de chemin de champ.</li><li>Filtrez les champs sans libellé, avec un libellé sélectionné ou avec une catégorie de libellé.</li></ul> |

Pour plus d’informations sur ce service, consultez la [présentation de la gouvernance des données.](../../data-governance/home.md)

## Destinations {#destinations}

Dans [Real-time Customer Data Platform](../../rtcdp/overview.md), les destinations sont des intégrations prédéfinies avec des plateformes de destination qui activent les données vers ces partenaires de manière transparente.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations de l’expérience utilisateur | Les utilisateurs peuvent accéder aux actions de tableau intégrées pour accéder plus facilement à des actions Principales, telles que l’ajout de données, la modification de la planification et l’ajout de segments. Voir [espace de travail des destinations](../../destinations/ui/destinations-workspace.md) pour plus d’informations. |

Pour en savoir plus, consultez la [présentation des destinations](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] vous permet de surveiller les activités sur Adobe Experience Platform à l’aide de mesures statistiques et de notifications d’événement.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Notifications d’événement d’Adobe I/O | [!DNL Observability Insights] tire parti des événements d’Adobe I/O pour créer des notifications d’événement pour plusieurs services d’Experience Platform. Les payloads de notification sont envoyés à un webhook configuré que vous pouvez ensuite utiliser pour automatiser d’autres processus en aval. |

Voir [[!DNL Observability Insights] aperçu](../../observability/home.md) pour plus d’informations sur le service.

## [!DNL Privacy Service] {#privacy}

Plusieurs réglementations juridiques et organisationnelles donnent aux utilisateurs le droit d’accéder à leurs données personnelles ou de les supprimer de vos entrepôts de données sur demande. Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface utilisateur pour vous aider à gérer ces requêtes de données de vos clients. Avec [!DNL Privacy Service], vous pouvez soumettre des demandes d’accès et de suppression de données clients privées ou personnelles des applications Adobe Experience Cloud, ce qui facilite la conformité automatisée aux réglementations de confidentialité légales et organisationnelles.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de LGPD (Brésil) | Des emplois dans le domaine de la vie privée peuvent maintenant être créés sous l&#39;égide du Brésil [!DNL Lei Geral de Proteção de Dados] (LGPD). Ces tâches sont suivies sous le code de réglementation. `lgpd_bra`. |

Voir [Présentation du Privacy Service](../../privacy-service/home.md) pour plus d’informations sur le service.

## Real-time Customer Profile {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Avec [!DNL Real-time Customer Profile], vous pouvez obtenir une vue d’ensemble de chaque client qui combine des données provenant de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. [!DNL Profile] vous permet de consolider vos données client disparates en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Visionneuse de profils | La visionneuse de profils, dans l’interface utilisateur de Platform, a été mise à jour pour être un tableau de bord avec une personnalisation complète. L’utilisateur a désormais la possibilité d’effectuer les tâches suivantes : <ul><li>Mettez à jour les attributs standard et personnalisés sélectionnés dans le widget d’informations de base.</li><li>Création, modification et suppression de widgets personnalisés</li><li>Redimensionnement et réorganisation des widgets</li></ul> |

Pour plus d’informations sur [!DNL Real-time Customer Profile], y compris des tutoriels et des bonnes pratiques pour travailler avec [!DNL Profile] data, veuillez lire la [Présentation de Real-time Customer Profile](../../profile/home.md).

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service propose une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir des données [!DNL Real-time Customer Profile]. Ces segments sont configurés et conservés de manière centralisée sur [!DNL Platform], ce qui les rend facilement accessibles depuis n’importe quelle application Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Tâches d’exportation | Un indicateur a été ajouté pour permettre l’évaluation des segments dans le cadre d’une tâche d’exportation. Par conséquent, les utilisateurs peuvent exécuter la segmentation et exporter dans une seule tâche. |
| Stratégies de fusion | Plusieurs stratégies de fusion peuvent être incluses dans une seule tâche de segmentation par lots. |

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md)

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide de [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mappage automatique | [!DNL Platform] fournit des recommandations intelligentes pour le mappage automatique lors du processus d’ingestion des données, en fonction d’un schéma ou d’un jeu de données cible sélectionné par l’utilisateur. Vous pouvez ajuster manuellement des règles de mappage automatique flexibles en fonction de vos cas d’utilisation. |
| Améliorations de l’expérience utilisateur | Les utilisateurs peuvent accéder aux actions de tableau intégrées pour accéder plus facilement à des actions Principales, telles que l’ajout de données, la modification de la planification et l’ajout de segments. Voir [suivi des flux de données](../../sources/tutorials/ui/monitor.md) pour plus d’informations. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
