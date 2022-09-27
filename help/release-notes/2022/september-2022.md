---
title: Notes de mise à jour de Adobe Experience Platform - Septembre 2022
description: Notes de mise à jour de septembre 2022 pour Adobe Experience Platform.
source-git-commit: 1890bd9dbce6a217951c28fc2fb3fec2634e714d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 38%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 28 septembre 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Service d’identités](#identity-service)
- [Sources](#sources)

## Identity Service {#identity-service}

Proposer des expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre des systèmes disparates, chaque client apparaissant ainsi posséder plusieurs &quot;identités&quot;.

Adobe Experience Platform Identity Service vous permet de mieux connaître vos clients et leurs comportements en rapprochant des identités entre appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de la suppression de jeux de données | Identity Service prend désormais en charge la suppression de jeux de données lors de la demande via [API Catalog Service](https://developer.adobe.com/experience-platform-apis/references/catalog/), l’interface utilisateur ou l’hygiène des données. Lisez le guide sur [suppression de jeux de données dans l’interface utilisateur](../../catalog/datasets/user-guide.md#delete-a-dataset) pour plus d’informations. |

Pour en savoir plus sur Identity Service, lisez le [Présentation d’Identity Service](../../identity-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Impact de la population de segments d’Audience Manager sur Real-time Customer Profile | L’ingestion de populations de segments d’Audience Manager importantes a un impact direct sur le nombre total de profils lorsque vous envoyez un segment d’Audience Manager pour la première fois à Platform à l’aide de la source d’Audience Manager. Cela signifie que la sélection de tous les segments peut potentiellement entraîner un nombre de profils supérieur à vos droits d’utilisation de licence. Pour plus d’informations, reportez-vous à la section [Présentation de la source d’Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Pour plus d’informations sur l’utilisation de votre licence, consultez la documentation sur [utilisation du tableau de bord de l’utilisation des licences](../../dashboards/guides/license-usage.md). |

Pour en savoir plus sur les sources, lisez le [présentation des sources](../../sources/home.md).