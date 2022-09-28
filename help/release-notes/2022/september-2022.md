---
title: Notes de mise à jour de Adobe Experience Platform - Septembre 2022
description: Notes de mise à jour de septembre 2022 pour Adobe Experience Platform.
source-git-commit: a3f12b9524d393441923cd11e09ed3e406814691
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 34%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 28 septembre 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Modèle de données d’expérience (XDM)](#xdm)
- [Service d’identités](#identity-service)
- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Sources](#sources)

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de l’interface utilisateur pour les énumérations et les valeurs suggérées | Outre les énumérations qui activent la validation des données, vous pouvez désormais [ajouter ou supprimer des valeurs suggérées](../../xdm/ui/fields/enum.md) pour les champs de chaîne standard ou personnalisés, de sorte que les utilisateurs de Platform disposent d’une liste conviviale de valeurs à sélectionner lors de la création de segments. |

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Groupe de champs | [[!UICONTROL Champs de classification AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Propriétés d’un élément spécifique avec lequel l’événement de proposition a été déclenché. |
| Groupe de champs | [[!UICONTROL Détails de l’interaction MediaAnalytics]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Effectue le suivi des interactions multimédia au fil du temps. |
| Groupe de champs | [[!UICONTROL Informations détaillées sur le média]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Effectue le suivi des informations sur les médias. |
| Groupe de champs | [[!UICONTROL Adobe CJM ExperienceEvent - Surfaces]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Décrit les surfaces des événements d’expérience dans Adobe Journey Optimizer. |

{style=&quot;table-layout:auto&quot;}

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Comportement | [[!UICONTROL Série temporelle]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Ajout de valeurs pour `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Valeurs supprimées pour `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Groupe de champs | (Multiple) | [Mise à jour de plusieurs descriptions de champ](https://github.com/adobe/xdm/pull/1628/files) sur les composants de Journey Orchestration. |
| Groupe de champs | (Multiple) | [Mise à jour des titres de plusieurs composants Adobe Workfront](https://github.com/adobe/xdm/pull/1634/files) pour assurer la cohérence. |
| Groupe de champs | [[!UICONTROL Champs de classification AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Mise à jour des espaces de noms de plusieurs champs vers `xdm`. |
| Groupe de champs | [[!UICONTROL Champs communs des événements d’étape de l’orchestration de parcours]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Ajout d’un nouveau champ, `isReadSegmentTriggerStartEvent`. |
| Groupe de champs | [[!UICONTROL Prévisions météorologiques]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Modification de la variable `xdm:uvIndex` à un type entier, puis ajout de la propriété `xdm` de plusieurs champs dans lesquels était manquant. |
| Groupe de champs | [[!UICONTROL Informations détaillées sur le média]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` et `xdm:implementationDetails` ont été supprimés du groupe de champs. |
| Type de données | (Multiple) | [Mise à jour de plusieurs noms de propriétés de média](https://github.com/adobe/xdm/pull/1626/files) sur plusieurs types de données pour assurer la cohérence. |
| Type de données | [[!UICONTROL Détails d’implémentation]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Ajout de noms connus pour flutter. |
| Type de données | [[!UICONTROL Détails des points ciblés]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Le type de données peut désormais accepter une liste de paires clé-valeur de métadonnées associées au point ciblé. |
| Type de données | [[!UICONTROL Action de proposition]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] a été renommé en [!UICONTROL Action de proposition]. |
| Type de données | [[!UICONTROL Type d’événement de proposition]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] a été renommé en [!UICONTROL Action de proposition]. |
| (Multiple) | (Multiple) | Les propriétés expérimentales ont été [stabilisé sur tous les composants B2B](https://github.com/adobe/xdm/pull/1617/files). |
| (Multiple) | (Multiple) | Les entités Adobe Journey Optimizer ont été [stabilisé](https://github.com/adobe/xdm/pull/1625/files). |
| (Multiple) | (Multiple) | Les espaces de noms de certains champs de plusieurs composants expérimentaux ont été [mise à jour pour assurer la cohérence](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md).

## Identity Service {#identity-service}

Proposer des expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre des systèmes disparates, chaque client apparaissant ainsi posséder plusieurs &quot;identités&quot;.

Adobe Experience Platform Identity Service vous permet de mieux connaître vos clients et leurs comportements en rapprochant des identités entre appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de la suppression de jeux de données | Identity Service prend désormais en charge la suppression de jeux de données lors de la demande via [API Catalog Service](https://developer.adobe.com/experience-platform-apis/references/catalog/), l’interface utilisateur ou l’hygiène des données. Lisez le guide sur [suppression de jeux de données dans l’interface utilisateur](../../catalog/datasets/user-guide.md#delete-a-dataset) pour plus d’informations. |

Pour en savoir plus sur Identity Service, lisez le [Présentation d’Identity Service](../../identity-service/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Les services d’IA/ML permettent aux analystes et spécialistes du marketing d’exploiter la puissance de l’intelligence artificielle et du machine learning dans les cas d’utilisation de l’expérience client. Cela permet aux analystes marketing de configurer des modèles spécifiques aux besoins d’une entreprise en utilisant des configurations au niveau de l’entreprise sans avoir besoin d’une expertise en science des données.

### IA dédiée à l’attribution

L’IA dédiée à l’attribution est utilisée pour attribuer des crédits aux points de contact qui génèrent des événements de conversion. Il peut aider les spécialistes du marketing à quantifier l’impact publicitaire de chaque point de contact marketing sur le parcours client.

| Fonctionnalité | Description |
| --- | --- |
| Enregistrement d’une instance Brouillon | Cette nouvelle fonctionnalité permet aux analystes marketing d’enregistrer la configuration du modèle en tant qu’instance de brouillon pendant les configurations et de continuer à modifier le brouillon jusqu’à la fin de la formation et de la notation. Les scénarios où cette fonctionnalité est utile incluent, sans s’y limiter, les cas où les utilisateurs ont plusieurs champs à définir dans le workflow de configuration qu’ils ne peuvent pas terminer en une seule fois ou lorsqu’une ou plusieurs statistiques de jeux de données (telles que l’exhaustivité des colonnes) prennent du temps à être traitées avant qu’elles ne soient disponibles. Lisez le [Guide d’utilisation d’Attribution AI](../../intelligent-services/attribution-ai/user-guide.md) pour en savoir plus. |
| Stratégies de gouvernance | Une fois que les utilisateurs se sont engagés à créer une instance par le biais du processus de configuration, le nouveau service d’application de la stratégie vérifie s’il existe des violations de stratégie de l’utilisation des données et affiche les détails dans une fenêtre contextuelle. Elle garantit que les opérations de données et les actions marketing sont conformes aux stratégies d’utilisation des données configurées sur Adobe Experience Platform. |

Pour plus d’informations sur Attribution AI, la variable [Présentation d’Attribution AI](../../intelligent-services/attribution-ai/overview.md). Pour plus d’informations sur les politiques de gouvernance des données, consultez la section [présentation des stratégies](../../data-governance/policies/overview.md).

### IA dédiée aux clients

L’IA dédiée aux clients disponible dans Real-time Customer Data Platform est utilisée pour générer des scores de propension personnalisés tels que l’attrition et la conversion pour des profils individuels à grande échelle.

| Fonctionnalité | Description |
| --- | --- |
| Enregistrement d’une instance Brouillon | Cette nouvelle fonctionnalité permet aux analystes marketing d’enregistrer la configuration du modèle en tant qu’instance de brouillon pendant les configurations et de continuer à modifier le brouillon jusqu’à la fin de la formation et de la notation. Les scénarios où cette fonctionnalité est utile incluent, sans s’y limiter, les cas où les utilisateurs ont plusieurs champs à définir dans le workflow de configuration qu’ils ne peuvent pas terminer en une seule fois ou lorsqu’une ou plusieurs statistiques de jeux de données (telles que l’exhaustivité des colonnes) prennent du temps à être traitées avant qu’elles ne soient disponibles. Lisez le [Guide d’utilisation de Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md) pour en savoir plus. |
| Stratégies de gouvernance | Une fois que les utilisateurs se sont engagés à créer une instance par le biais du processus de configuration, le nouveau service d’application de la stratégie vérifie s’il existe des violations de stratégie de l’utilisation des données et affiche les détails dans une fenêtre contextuelle. Elle garantit que les opérations de données et les actions marketing sont conformes aux stratégies d’utilisation des données configurées sur Adobe Experience Platform. |

Pour plus d’informations sur Customer AI, consultez la section [Présentation de Customer AI](../../intelligent-services/customer-ai/overview.md). Pour plus d’informations sur les politiques de gouvernance des données, consultez la section [présentation des stratégies](../../data-governance/policies/overview.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Impact de la population de segments d’Audience Manager sur Real-time Customer Profile | L’ingestion de populations de segments d’Audience Manager importantes a un impact direct sur le nombre total de profils lorsque vous envoyez un segment d’Audience Manager pour la première fois à Platform à l’aide de la source d’Audience Manager. Cela signifie que la sélection de tous les segments peut potentiellement entraîner un nombre de profils supérieur à vos droits d’utilisation de licence. Pour plus d’informations, reportez-vous à la section [Présentation de la source d’Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Pour plus d’informations sur l’utilisation de votre licence, consultez la documentation sur [utilisation du tableau de bord de l’utilisation des licences](../../dashboards/guides/license-usage.md). |

Pour en savoir plus sur les sources, lisez le [présentation des sources](../../sources/home.md).