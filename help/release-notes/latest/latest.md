---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour de l’Experience Platform pour le 30 juin 2021.
doc-type: release notes
last-update: June 30, 2021
author: ens60013
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: fc916f87bf07e5eabf7d1681059406e2fea362e0
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 68%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 30 juin 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Profil client en temps réel](#profile)
- [Sandbox](#sandboxes)
- [Sources](#sources)

## Real-time Customer Profile {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Real-time Customer Profile offre une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le [!DNL Profile] vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Mises à jour du workflow de stratégie de fusion | Lors de la création et de la mise à jour de stratégies de fusion dans lʼinterface utilisateur, les utilisateurs peuvent désormais prévisualiser 20 exemples de profils en fonction du schéma dʼunion. Cela permet aux utilisateurs de prévisualiser lʼaspect des profils client avant lʼenregistrement des configurations des stratégies de fusion. Pour plus dʼinformations, consultez le [guide de lʼinterface utilisateur des stratégies de fusion](../../profile/merge-policies/ui-guide.md). |
| Rapport de chevauchement d’identités | Le rapport de chevauchement d’identités fait partie de l’API Real-time Customer Profile et offre une visibilité sur la composition de la banque de profils. En utilisant le point de terminaison `/previewsamplestatus`, le rapport de chevauchement d’identités expose les identités qui contribuent le plus à l’audience adressable. Pour en savoir plus, consultez le [guide d’aperçu du point de terminaison de l’API d’état](../../profile/api/preview-sample-status.md). |

Pour plus d’informations sur le profil client en temps réel, notamment les bonnes pratiques et les tutoriels relatifs à l’utilisation des données de [!DNL Profile], consultez la [présentation du profil client en temps réel](../../profile/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience numérique à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience numérique en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des environnements de test qui divisent une instance unique de Platform en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

| Fonctionnalité | Description |
| ------- | ----------- |
| Environnement de test de production améliorations de réinitialisation | Vous pouvez désormais réinitialiser les environnements de test de production utilisés pour le partage de segments bidirectionnel avec Adobe Audience Manager ou Audience Core Service. Vous pouvez le faire à partir de l’interface utilisateur ou en utilisant les nouveaux paramètres `validationOnly` et `ignoreWarnings` dans l’API. Pour plus d’informations, consultez les tutoriels sur la [réinitialisation d’un environnement de test dans l’interface utilisateur](../../sandboxes/ui/user-guide.md) et la [réinitialisation d’un environnement de test dans l’API](../../sandboxes/api/sandboxes.md) . |

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| ------- | ----------- |
| [!DNL Veeva CRM] (version bêta) | Vous pouvez désormais connecter [!DNL Veeva CRM] à Experience Platform à l’aide de l’API [!DNL Flow Service] ou de l’interface utilisateur. Pour plus d’informations, consultez la présentation du connecteur [[!DNL Veeva CRM] ](../../sources/connectors/crm/veeva.md). |
| Prise en charge de la surveillance des flux de données en continu | Vous pouvez désormais utiliser l’espace de travail de l’interface utilisateur des sources pour surveiller les activités d’ingestion de données provenant de sources en continu avec les mesures et l’état correspondants. Pour plus d’informations, consultez le tutoriel sur la [surveillance des flux de données en continu](../../sources/tutorials/ui/monitor-streaming.md) . |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
