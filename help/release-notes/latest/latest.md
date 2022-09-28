---
title: Notes de mise à jour de Adobe Experience Platform - Septembre 2022
description: Notes de mise à jour de septembre 2022 pour Adobe Experience Platform.
source-git-commit: 65743c1741210a87b1cc64406412dd7e58218321
workflow-type: tm+mt
source-wordcount: '2796'
ht-degree: 30%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 28 septembre 2022**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Contrôle d’accès basé sur les attributs](#abac)
- [Hygiène des données](#data-hygiene)
- [[!UICONTROL Console de confidentialité]](#privacy-console)

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Journaux d’audit](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [Collecte de données](#data-collection)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Service d’identités](#identity-service)
- [Query Service](#query-service)
- [Sources](#sources)

## Contrôle d’accès basé sur les attributs {#abac}

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs sera activé à compter d’octobre 2022. Si vous souhaitez être un des premiers adoptants, contactez votre représentant Adobe.

Le contrôle d’accès basé sur les attributs est une fonctionnalité de Adobe Experience Platform qui offre une plus grande flexibilité aux marques soucieuses de la confidentialité pour gérer l’accès des utilisateurs. Les objets individuels tels que les champs de schéma et les segments peuvent être affectés à des rôles utilisateur. Cette fonctionnalité vous permet d’accorder ou de révoquer l’accès à des objets individuels pour des utilisateurs de Platform spécifiques de votre entreprise.

Grâce au contrôle d’accès basé sur les attributs, les administrateurs de votre organisation peuvent contrôler l’accès des utilisateurs aux données personnelles sensibles (SPD), aux informations d’identification personnelle (PII) et à d’autres types de données personnalisés dans tous les workflows et ressources Platform. Les administrateurs peuvent définir des rôles d’utilisateur qui n’ont accès qu’à des champs spécifiques et aux données correspondant à ces champs.

| Fonctionnalité | Description |
| --- | --- |
| Contrôle d’accès basé sur les attributs | Le contrôle d’accès basé sur les attributs vous permet de libeller les champs de schéma et les segments du modèle de données d’expérience (XDM) avec des libellés qui définissent les portées d’utilisation des données ou de l’organisation. En parallèle, les administrateurs peuvent utiliser l’interface d’administration des utilisateurs et des rôles pour définir des stratégies d’accès couvrant les champs de schéma XDM et les segments afin de mieux gérer l’accès attribué aux utilisateurs ou groupes d’utilisateurs (utilisateurs internes, externes ou tiers). Pour plus d’informations, consultez la [présentation du contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md). |
| Autorisations | La zone dédiée aux autorisations dans Experience Cloud permet aux administrateurs de définir des rôles d’utilisateur et des stratégies d’accès. Ils peuvent ainsi gérer les autorisations d’accès aux fonctionnalités et objets dans une application de produit. Grâce aux autorisations, vous pouvez créer et gérer des rôles, attribuer les autorisations de ressources souhaitées pour ces rôles et créer des stratégies pour exploiter les étiquettes et définir les rôles utilisateur ayant accès à des ressources Platform spécifiques. Les autorisations vous permettent également de gérer les libellés, les sandbox et les utilisateurs associés à un rôle spécifique. Pour plus d’informations, consultez le [guide de l’interface utilisateur des autorisations](../../access-control/abac/ui/browse.md). |

Pour plus d’informations sur le contrôle d’accès basé sur les attributs, consultez la [présentation du contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md). Pour consulter un guide complet sur le workflow de contrôle d’accès basé sur les attributs, reportez-vous à la section [guide de bout en bout du contrôle d’accès basé sur les attributs](../../access-control/abac/end-to-end-guide.md).

## Hygiène des données {#data-hygiene}

Adobe Experience Platform offre un ensemble d’outils fiables pour gérer des opérations de données complexes et volumineuses afin d’orchestrer les expériences client. Les données étant ingérées dans le système au fil du temps, il devient de plus en plus important de gérer les banques de données pour que les données soient utilisées comme prévu, mises à jour lorsque des données incorrectes doivent être corrigées et supprimées lorsque les politiques d’entreprise le jugent nécessaire.

Les fonctionnalités d’hygiène des données de Adobe Experience Platform vous permettent de nettoyer vos données en planifiant l’expiration automatisée des jeux de données et en supprimant par programmation les données des consommateurs par identité.

>[!IMPORTANT]
>
>Les fonctionnalités d’hygiène des données ne sont disponibles que pour les organisations qui ont acheté Adobe Healthcare Shield ou Privacy Shield.

Pour commencer à utiliser l’hygiène des données, reportez-vous à la documentation suivante :

- [Présentation de l’hygiène des données](../../hygiene/home.md): Découvrez les principes de base des fonctionnalités d’hygiène des données de Platform.
- [[!UICONTROL Hygiène des données] Guide de l’interface utilisateur](../../hygiene/ui/overview.md): Découvrez comment planifier l’expiration des jeux de données et les demandes de suppression des consommateurs dans l’interface utilisateur de Platform.
- [Guide de l’API d’hygiène des données](../../hygiene/api/overview.md): Toutes les activités d’hygiène des données que vous pouvez exécuter dans l’interface utilisateur peuvent également être programmées

## [!UICONTROL Console de confidentialité] {#privacy-console}

Le [!UICONTROL Console de confidentialité] dans l’interface utilisateur de l’Experience Platform fournit un tableau de bord des principales informations des fonctionnalités liées à la confidentialité, telles que [Requêtes de sujet de données de Privacy Service](../../privacy-service/home.md), [ordres de travail relatifs à l&#39;hygiène des données](../../hygiene/home.md), et [journaux d’audit](../../landing/governance-privacy-security/audit-logs/overview.md). La console fournit également plusieurs guides de cas d’utilisation intégrés au produit pour vous aider à vous guider dans les processus de confidentialité courants.

Voir [Présentation de Privacy Console](../../landing/governance-privacy-security/privacy-console.md) pour plus d’informations sur la fonctionnalité.

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

## Journaux d’audit {#audit-logs}

Experience Platform vous permet d’auditer l’activité des utilisateurs pour plusieurs services et fonctionnalités. Les journaux d’audit fournissent des informations sur ce qui a été fait, par qui et à quel moment.

**Fonctionnalités mises à jour**

| Fonctionnalité | Nom | Description |
| --- | --- | --- |
| Ressources ajoutées | <ul><li>Instance Attribution AI</li><li>Instance Customer AI</li><li>Datastream</li></ul> | Les ressources du journal d’audit sont automatiquement enregistrées lorsque l’activité se produit. Si la fonctionnalité est activée, vous ne devez pas activer manuellement la collecte des journaux. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur les différents types d’événements spécifiques à la ressource suivis par les journaux d’audit dans Platform, reportez-vous à la section [aperçu des journaux d’audit](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fournit plusieurs tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre entreprise, telles qu’elles sont capturées lors d’instantanés quotidiens.

| Fonctionnalité | Description |
| --- | --- |
| Libellé en cours d’utilisation | Lorsqu’il est affiché dans la bibliothèque de widgets, le libellé en cours d’utilisation identifie facilement la présence de widgets existants dans votre tableau de bord. Cela permet d’éviter facilement la duplication bien que vous puissiez ajouter le même widget plusieurs fois si vous le souhaitez. |
| Tableaux de bord définis par l’utilisateur | Les tableaux de bord définis par l’utilisateur accélèrent les insights et personnalisent les visualisations en vous permettant de créer et de gérer des tableaux de bord personnalisés. Avec les tableaux de bord définis par l’utilisateur, vous pouvez créer, ajouter et modifier des widgets personnalisés pour visualiser les mesures clés pertinentes pour votre entreprise. Lisez le [guide des fonctionnalités](../../dashboards/user-defined-dashboards.md) pour en savoir plus. |
| Modèle de données de statistiques sur la plateforme de données clients | La fonction Modèle de données de statistiques de la plateforme de données clients (CDP) expose les modèles de données et SQL qui alimentent les informations pour divers widgets de profil, de destination et de segmentation. Vous pouvez personnaliser ces modèles de requête SQL pour créer des rapports CDP pour vos cas d’utilisation d’indicateurs de performance clés et marketing. Ces informations peuvent ensuite être utilisées comme widgets personnalisés pour vos tableaux de bord définis par l’utilisateur. Lisez le [Guide de fonctionnalité du modèle de données de statistiques CDP](../../dashboards/cdp-insights-data-model.md) pour en savoir plus. |
| Widget de rapport sur le chevauchement des audiences | Ce widget est disponible pour les deux [!UICONTROL Profils] et [!UICONTROL Segments] tableaux de bord. Le rapport fournit une liste ordonnée des audiences classées selon les pourcentages de chevauchement les plus élevés ou les plus bas pour le segment sélectionné. Dans la [!UICONTROL Profils] tableau de bord, vous pouvez filtrer et afficher le chevauchement de vos audiences par stratégie de fusion de tous les segments disponibles. Le [!UICONTROL Segments] Les tableaux de bord vous permettent de filtrer le chevauchement des audiences selon un segment spécifique.<br>Utilisez cette analyse pour créer de nouveaux segments hautement performants et éviter d’envoyer la même audience vers différentes destinations. Le rapport permet également d’identifier les informations masquées afin d’améliorer la segmentation ou de localiser les profils uniques à rechercher. |

Pour plus d’informations sur les [!DNL Dashboards], consultez la [[!DNL Dashboards] présentation](../../dashboards/home.md).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Intégration de la navigation de gauche dans l’interface utilisateur de Platform | Toutes les fonctionnalités qui étaient auparavant exclusives à l’interface utilisateur de collecte de données (y compris les balises, le transfert d’événement et les flux de données) sont désormais disponibles via la navigation de gauche dans Experience Platform, sous la catégorie **[!UICONTROL Collecte de données]**. Cela évite de basculer entre les interfaces utilisateur lors de l’utilisation des fonctionnalités de collecte de données dans Platform. |
| Attribution utilisateur dans les balises et le transfert d’événement | Lorsque la liste est disponible [!UICONTROL Propriétés] dans les balises et le transfert d’événement, chaque propriété répertoriée indique désormais à quel moment elle a été mise à jour pour la dernière fois et quel utilisateur a effectué la mise à jour. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur la collecte de données dans Platform, consultez la [Présentation de la collecte de données](../../collection/home.md).

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

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans Data Science Workspace ou pour l’ingestion dans Profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| API d’abonnement aux alertes | Adobe Experience Platform Query Service vous permet de vous abonner à des alertes pour les requêtes ad hoc et planifiées. Les alertes peuvent être reçues par courrier électronique, dans l’interface utilisateur de Platform ou les deux. Actuellement, les alertes de requête ne peuvent être abonnées qu’à l’aide de la variable [API Query Service](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| Exemples de jeux de données | Les exemples de jeux de données Query Service vous permettent de mener des requêtes exploratoires sur les données volumineuses avec un temps de traitement considérablement réduit, au prix de la précision des requêtes. |

Pour plus d’informations sur les [!DNL Query Service], consultez la [[!DNL Query Service] présentation](../../query-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Impact de la population de segments d’Audience Manager sur Real-time Customer Profile | L’ingestion de populations de segments d’Audience Manager importantes a un impact direct sur le nombre total de profils lorsque vous envoyez un segment d’Audience Manager pour la première fois à Platform à l’aide de la source d’Audience Manager. Cela signifie que la sélection de tous les segments peut potentiellement entraîner un nombre de profils supérieur à vos droits d’utilisation de licence. Pour plus d’informations, reportez-vous à la section [Présentation de la source d’Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Pour plus d’informations sur l’utilisation de votre licence, consultez la documentation sur [utilisation du tableau de bord de l’utilisation des licences](../../dashboards/guides/license-usage.md). |
| Prise en charge d’Adobe Campaign Managed Cloud Service | Utilisez la source du Cloud Service géré Adobe Campaign pour importer vos données de logs de diffusion et de suivi Adobe Campaign v8.4 à l’Experience Platform. Lisez le guide sur [création d’une connexion source Adobe Campaign Managed Cloud Service dans l’interface utilisateur](../../sources/tutorials/ui/create/adobe-applications/campaign.md) pour plus d’informations. |
| Prise en charge des API pour l’ingestion à la demande pour les sources par lots | Utilisez l’ingestion à la demande pour créer des exécutions de flux ad hoc pour un flux de données donné avec la variable [!DNL Flow Service] API. Les exécutions de flux créées doivent être définies sur une ingestion unique. Pour plus d’informations, consultez le guide sur [création d’une exécution de flux pour l’ingestion à la demande à l’aide de l’API](../../sources/tutorials/api/on-demand-ingestion.md) pour plus d’informations. |
| Prise en charge de l’API pour la nouvelle tentative d’exécutions de flux de données ayant échoué pour les sources par lots | Utilisez la variable `re-trigger` pour essayer de relancer votre flux de données ayant échoué via l’API. Lisez le guide sur [reprise des exécutions de flux de données ayant échoué à l’aide de l’API](../../sources/tutorials/api/retry-flows.md) pour plus d’informations. |
| Prise en charge de l’API pour le filtrage des données au niveau des lignes pour le [!DNL Google BigQuery] et [!DNL Snowflake] sources | Utilisez des opérateurs logiques et de comparaison pour filtrer les données au niveau de la ligne pour le [!DNL Google BigQuery] et [!DNL Snowflake] sources. Lisez le guide sur [filtrage des données pour une source à l’aide de l’API](../../sources/tutorials/api/filter.md) pour plus d’informations. |

Pour en savoir plus sur les sources, lisez le [présentation des sources](../../sources/home.md).