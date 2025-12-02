---
title: Notes de mise à jour d’Adobe Experience Platform - Septembre 2022
description: Les notes de mise à jour de septembre 2022 pour Adobe Experience Platform.
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '2723'
ht-degree: 86%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 28 septembre 2022**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Contrôle d’accès basé sur les attributs](#abac)

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Journaux d’audit](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Service d’identités](#identity-service)
- [Service de requête](#query-service)
- [Sources](#sources)

## Contrôle d’accès basé sur les attributs {#abac}

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs est disponible depuis octobre 2022. Si vous souhaitez bénéficier de cette fonctionnalité, contactez votre représentant Adobe.

Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui offre une plus grande flexibilité dans la gestion de l’accès utilisateur. Elle est destinée aux marques veillant à garantir un haut niveau de confidentialité. Les objets individuels tels que les champs de schéma et les segments peuvent être affectés à des rôles d’utilisateur. Cette fonctionnalité vous permet d’accorder ou de révoquer l’accès à des objets individuels pour des utilisateurs Experience Platform spécifiques au sein de votre organisation.

Grâce au contrôle d’accès basé sur les attributs, les administrateurs de votre organisation peuvent contrôler l’accès des utilisateurs aux données personnelles sensibles (SPD), aux informations d’identification personnelle (PII) et à d’autres types de données personnalisées sur l’ensemble des workflows et ressources d’Experience Platform. Les administrateurs peuvent définir des rôles d’utilisateur qui n’ont accès qu’à des champs spécifiques et aux données correspondant à ces champs.

| Fonctionnalité | Description |
| --- | --- |
| Contrôle d’accès basé sur les attributs | Le contrôle d’accès basé sur les attributs vous permet de libeller les segments et champs de schéma de modèle de données d’expérience (XDM) avec des libellés qui définissent les limites d’utilisation de l’organisation ou des données. En parallèle, les administrateurs peuvent utiliser l’interface d’administration des utilisateurs et des rôles pour définir des politiques d’accès relatives aux segments et champs de schéma XDM. Ainsi, ils peuvent mieux gérer l’accès accordé aux utilisateurs ou groupes d’utilisateurs (utilisateurs internes, externes ou tiers). Pour plus d’informations, consultez la [présentation du contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md). |
| Autorisations | La zone dédiée aux autorisations dans Experience Cloud permet aux administrateurs de définir des rôles d’utilisateur et des politiques d’accès. Ils peuvent ainsi gérer les autorisations d’accès aux fonctionnalités et objets dans une application de produit. Grâce aux autorisations, vous pouvez créer et gérer des rôles, attribuer les autorisations de ressources souhaitées pour ces rôles et créer des politiques afin d’exploiter les libellés et définir quels rôles utilisateur ont accès à des ressources Experience Platform spécifiques. Les autorisations vous permettent également de gérer les libellés, les sandbox et les utilisateurs associés à un rôle spécifique. Pour plus d’informations, consultez le [guide de l’interface utilisateur des autorisations](../../access-control/abac/ui/browse.md). |

Pour plus d’informations sur le contrôle d’accès basé sur les attributs, consultez la [présentation du contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md). Pour consulter un guide complet sur le workflow de contrôle d’accès basé sur les attributs, reportez-vous au [guide complet du contrôle d’accès basé sur les attributs](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Les services d’IA/ML permettent aux analystes et spécialistes du marketing d’exploiter la puissance de l’intelligence artificielle et du machine learning dans les cas d’utilisation de l’expérience client. Cela permet aux analystes marketing de configurer des modèles spécifiques aux besoins d’une entreprise en utilisant des configurations au niveau de l’entreprise sans avoir besoin d’une expertise en science des données.

### IA dédiée à l’attribution

L’IA dédiée à l’attribution est utilisée pour attribuer des crédits aux points de contact qui génèrent des événements de conversion. Il peut aider les spécialistes du marketing à quantifier l’impact publicitaire de chaque point de contact marketing sur le parcours client.

| Fonctionnalité | Description |
| --- | --- |
| Enregistrer une instance de brouillon | Cette nouvelle fonctionnalité permet aux analystes marketing d’enregistrer un modèle de configuration en tant qu’instance de brouillon et de continuer à la modifier jusqu’à ce qu’elle soit terminée avant la formation et la notation. Les scénarios où cette fonctionnalité est utile incluent notamment le suivant : lorsqu’un utilisateur dispose de plusieurs champs à définir dans le workflow, mais qu’il ne peut pas les terminer en raison de contraintes de temps. Un autre scénario se produit lorsqu’une ou plusieurs statistiques de jeux de données sont en cours de traitement et ne sont pas encore disponibles. Lisez le [Guide de l’utilisateur de l’IA dédiée à l’attribution](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) pour en savoir plus. |
| Politiques de gouvernance | Une fois que les utilisateurs se sont engagés à créer une instance par le biais du workflow de configuration, le nouveau service d’application des politiques vérifie s’il existe des violations des politiques de l’utilisation des données et affiche les détails dans une fenêtre contextuelle. Il garantit que les opérations de données et les actions marketing sont conformes aux politiques d’utilisation des données configurées sur Adobe Experience Platform. |

Consultez la [présentation de l’IA dédiée à l’attribution](../../intelligent-services/attribution-ai/overview.md) pour plus d’informations. Pour plus d’informations sur les politiques de gouvernance des données, consultez la [présentation des politiques](../../data-governance/policies/overview.md).

### IA dédiée aux clients

L’IA dédiée aux clients disponible dans Real-time Customer Data Platform est utilisée pour générer des scores de propension personnalisés tels que l’attrition et la conversion pour des profils individuels à grande échelle.

| Fonctionnalité | Description |
| --- | --- |
| Enregistrer une instance de brouillon | Cette nouvelle fonctionnalité permet aux analystes marketing d’enregistrer un modèle de configuration en tant qu’instance de brouillon et de continuer à la modifier jusqu’à ce qu’elle soit terminée avant la formation et la notation. Les scénarios où cette fonctionnalité est utile incluent notamment le suivant : lorsqu’un utilisateur dispose de plusieurs champs à définir dans le workflow, mais qu’il ne peut pas les terminer en raison de contraintes de temps. Un autre scénario se produit lorsqu’une ou plusieurs statistiques de jeux de données sont en cours de traitement et ne sont pas encore disponibles. Lisez le [Guide de l’utilisateur de l’IA dédiée aux clients](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) pour en savoir plus. |
| Politiques de gouvernance | Une fois que les utilisateurs se sont engagés à créer une instance par le biais du workflow de configuration, le nouveau service d’application des politiques vérifie s’il existe des violations des politiques de l’utilisation des données et affiche les détails dans une fenêtre contextuelle. Il garantit que les opérations de données et les actions marketing sont conformes aux politiques d’utilisation des données configurées sur Adobe Experience Platform. |

Consultez la [présentation de l’IA dédiée aux clients](../../intelligent-services/customer-ai/overview.md) pour plus d’informations. Pour plus d’informations sur les politiques de gouvernance des données, consultez la [présentation des politiques](../../data-governance/policies/overview.md).

## Journaux d’audit {#audit-logs}

Experience Platform vous permet d’auditer l’activité des utilisateurs pour plusieurs services et fonctionnalités. Les journaux d’audit fournissent des informations sur ce qui a été fait, par qui et à quel moment.

**Fonctionnalités mises à jour**

| Fonctionnalité | Nom | Description |
| --- | --- | --- |
| Ressources ajoutées | <ul><li>Instance IA dédiée à l’attribution</li><li>Instance IA dédiée aux clients</li><li>Train de données</li></ul> | Les ressources du journal d’audit sont automatiquement enregistrées lorsque l’activité se produit. Si la fonctionnalité est activée, vous ne devez pas activer manuellement la collecte des journaux. |

{style="table-layout:auto"}

Pour plus d’informations sur les différents types d’événements spécifiques aux ressources suivis par les journaux d’audit dans Experience Platform, reportez-vous à la [&#x200B; présentation des journaux d’audit &#x200B;](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fournit de nombreux tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre organisation, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

| Fonctionnalité | Description |
| --- | --- |
| Libellé en cours d’utilisation | Lorsqu’il est affiché dans la bibliothèque de widgets, le libellé en cours d’utilisation identifie facilement la présence de widgets existants dans votre tableau de bord. Cela permet d’éviter facilement la duplication, bien que vous puissiez ajouter le même widget plusieurs fois si vous le souhaitez. |
| Tableaux de bord définis par l’utilisateur | Les tableaux de bord définis par l’utilisateur accélérèrent les informations et personnalisent les visualisations en vous permettant de créer et de gérer des tableaux de bord personnalisés. Grâce aux tableaux de bord définis par l’utilisateur, vous pouvez créer, ajouter et modifier des widgets personnalisés pour visualiser les mesures clés pertinentes pour votre organisation. Lisez le [guide des fonctionnalités](../../dashboards/standard-dashboards.md) pour en savoir plus. |
| Modèle de données d’informations Customer Data Platform | La fonctionnalité Modèle de données d’informations Customer Data Platform (CDP) expose les modèles de données et SQL qui alimentent les informations pour divers widgets de profil, de destination et de segmentation. Vous pouvez personnaliser ces modèles de requête SQL pour créer des rapports CDP pour vos cas d’utilisation de marketing et d’indicateurs clés de performance. Ces informations peuvent ensuite être utilisées comme widgets personnalisés pour vos tableaux de bord définis par l’utilisateur. Lisez le [guide de fonctionnalité du modèle de données d’informations CDP](../../dashboards/data-models/cdp-insights-data-model-b2c.md) pour en savoir plus. |
| Widget de rapport de chevauchements d’audience | Ce widget est disponible pour les tableaux de bord [!UICONTROL Profiles] et [!UICONTROL Segments]. Le rapport fournit une liste d’audiences classées selon les pourcentages de chevauchement les plus élevés ou les plus bas pour le segment sélectionné. Dans le tableau de bord [!UICONTROL Profiles], vous pouvez filtrer et afficher le chevauchement de vos audiences par politique de fusion de tous les segments disponibles. Les tableaux de bord [!UICONTROL Segments] vous permettent de filtrer le chevauchement des audiences selon un segment spécifique.<br>Utilisez cette analyse pour créer de nouveaux segments hautement performants et éviter d’envoyer la même audience vers différentes destinations. Le rapport permet également d’identifier les informations masquées afin d’améliorer la segmentation ou de localiser les profils uniques à rechercher. Lisez les guides des widgets [profils](../../dashboards/guides/profiles.md#audience-overlap-report) et [segments](../../dashboards/guides/audiences.md#audience-overlap-report) pour en savoir plus. |

Pour plus d’informations sur Query Service [!DNL Dashboards], consultez la [[!DNL Dashboards] présentation](../../dashboards/home.md) de Query Service.

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Intégration de la navigation de gauche dans l’interface utilisateur d’Experience Platform | Toutes les fonctionnalités qui étaient auparavant exclusives à l’interface utilisateur de la collecte de données (y compris les balises, le transfert d’événement et les flux de données) sont désormais disponibles via la navigation de gauche dans Experience Platform, sous la catégorie **[!UICONTROL Data Collection]**. Il n’est donc pas nécessaire de basculer entre les IU lors de l’utilisation des fonctionnalités de collecte de données dans Experience Platform. |
| Attribution utilisateur dans les balises et le transfert d’événement | Lors de l’énumération des [!UICONTROL Properties] disponibles dans les balises et le transfert d’événement, chaque propriété répertoriée indique désormais à quand remonte sa dernière mise à jour et quel utilisateur l’a effectuée. |
| [[!DNL Snap Conversions API] Extension](https://exchange.adobe.com/apps/ec/108550) Snap Conversions API pour le transfert d’événement | Vous pouvez désormais envoyer des données à [!DNL Snapchat Conversions API] à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations sur l’authentification et l’utilisation de l’API, voir la [[!DNL Snapchat Marketing API] documentation](https://marketingapi.snapchat.com/docs/conversion.html) Snapchat Marketing API dédiée.  |
| [User-Agent Client Hints in Web SDK](/help/collection/use-cases/client-hints.md) | Web SDK prend désormais en charge [User-Agent Client Hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Les conseils clients permettent aux propriétaires de site web d’accéder aux mêmes informations que celles disponibles dans la chaîne [!DNL User-Agent], mais d’une manière plus respectueuse de la vie privée. |
| Migration page par page de Web SDK | Vous pouvez désormais migrer vos propriétés web existantes à partir d’autres bibliothèques Experience Cloud, telles que [!DNL at.js], vers le SDK Web, une page à la fois. Vous pouvez ainsi adopter une approche progressive dans la migration du SDK Web, sans qu’il soit nécessaire de migrer toutes vos pages à la fois. |
| Prise en charge des flux de données d’[[!DNL Adobe Journey Optimizer] &#x200B;](../../datastreams/overview.md#aep) | Le service Adobe Experience Platform pour les flux de données prend désormais en charge [!DNL Adobe Journey Optimizer]. Cette option vous permet d’utiliser des canaux entrants web et basés sur des applications dans [!DNL Adobe Journey Optimizer]. |

{style="table-layout:auto"}

Pour plus d’informations sur la collecte de données dans Experience Platform, consultez la [présentation de la collecte de données](../../collection/home.md).

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ----------- | ----------- |
| Destination SDK | Destination SDK offre désormais une prise en charge complète des partenaires et des clients qui créent des destinations standardisées ou privées par lots (ou basées sur les fichiers). Pour plus d’informations, consultez les pages de documentation suivantes : <ul><li>[Présentation de Destination SDK](../../destinations/destination-sdk/overview.md)</li><li>[Configurer une destination basée sur des fichiers](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[Configurer des options de formatage de fichier pour les destinations basées sur des fichiers](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[Testez vos destinations basées sur des fichiers](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services offre une plateforme pour concevoir des expériences client cross-canal ainsi qu’un environnement pour l’orchestration visuelle de campagnes, la gestion d’interactions en temps réel et l’exécution cross-canal. [Prise en main de Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html?lang=fr). Notez que cette intégration fonctionne avec [Adobe Campaign version 8.4 ou ultérieure](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | La destination [!DNL Salesforce CRM] a été mise à jour afin de prendre en charge à la fois les mises à jour des contacts et des prospects, ainsi que des améliorations des performances pour des mises à jour plus rapides. |

{style="table-layout:auto"}

**Documentation nouvelle ou mise à jour**

| Documentation | Description |
| ----------- | ----------- |
| Documentation de l’API de service de flux Destinations | La [documentation de référence de l’API Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/) a été mise à jour afin d’inclure des conseils sur la manière d’effectuer des opérations sur des destinations basées sur des fichiers. Les opérations pour les destinations de diffusion en continu seront ajoutées ultérieurement. |

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types d’audiences clientes par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de l’interface utilisateur pour les énumérations et les valeurs suggérées | Outre les énumérations qui activent la validation des données, vous pouvez désormais [ajouter ou supprimer des valeurs suggérées](../../xdm/ui/fields/enum.md) pour les champs de chaîne standard ou personnalisés, de sorte que les utilisateurs d’Experience Platform disposent d’une liste conviviale de valeurs à sélectionner lors de la création de segments. |

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Groupe de champs | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Propriétés d’un élément spécifique avec lequel il y a eu interaction, ce qui a provoqué le déclenchement de l’événement de proposition. |
| Groupe de champs | [[!UICONTROL MediaAnalytics Interaction Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Effectue le suivi des interactions avec les médias au fil du temps. |
| Groupe de champs | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Effectue le suivi des informations sur les médias. |
| Groupe de champs | [[!UICONTROL Adobe CJM ExperienceEvent - Surfaces]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Décrit les surfaces des événements d’expérience dans Adobe Journey Optimizer. |

{style="table-layout:auto"}

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Comportement | [[!UICONTROL Time series]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Ajout de valeurs pour `eventType` :<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Valeurs supprimées pour `eventType` :<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Groupe de champs | (Multiple) | [Mise à jour de plusieurs descriptions de champ](https://github.com/adobe/xdm/pull/1628/files) sur les composants de Journey Orchestration. |
| Groupe de champs | (Multiple) | [Mise à jour des titres de plusieurs composants Adobe Workfront](https://github.com/adobe/xdm/pull/1634/files) par souci de cohérence. |
| Groupe de champs | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Mise à jour des espaces de noms de plusieurs champs vers `xdm`. |
| Groupe de champs | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Ajout d’un nouveau champ, `isReadSegmentTriggerStartEvent`. |
| Groupe de champs | [[!UICONTROL Forecasted Weathers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Modification du champ `xdm:uvIndex` en un type entier, puis ajout de l’espace de nommage `xdm` à plusieurs champs dans lesquels il était manquant. |
| Groupe de champs | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` et `xdm:implementationDetails` ont été supprimés du groupe de champs. |
| Type de données | (Multiple) | [Mise à jour de plusieurs noms de propriétés de média](https://github.com/adobe/xdm/pull/1626/files) sur plusieurs types de données par souci de cohérence. |
| Type de données | [[!UICONTROL Implementation details]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Ajout de noms connus pour le Flutter. |
| Type de données | [[!UICONTROL Point of interest details]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Le type de données peut désormais accepter une liste de paires clé-valeur de métadonnées associées au point ciblé. |
| Type de données | [[!UICONTROL Proposition Action]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] a été renommé [!UICONTROL Proposition Action]. |
| Type de données | [[!UICONTROL Proposition Event Type]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] a été renommé [!UICONTROL Proposition Action]. |
| (Multiple) | (Multiple) | Les propriétés expérimentales ont été [stabilisées sur tous les composants B2B](https://github.com/adobe/xdm/pull/1617/files). |
| (Multiple) | (Multiple) | Les entités Adobe Journey Optimizer ont été [stabilisées](https://github.com/adobe/xdm/pull/1625/files). |
| (Multiple) | (Multiple) | Les espaces de noms de certains champs dans plusieurs composants expérimentaux ont été [mis à jour par souci de cohérence](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Experience Platform, consultez la [vue d’ensemble du système XDM](../../xdm/home.md).

## Service d’identités {#identity-service}

Proposer des expériences digitales pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre plusieurs systèmes, chaque client semble donc posséder plusieurs « identités ».

Le Service d’identités d’Adobe Experience Platform vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences digitales personnelles et percutantes en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de la suppression de jeux de données | Identity Service prend désormais en charge la suppression de jeux de données lors de la requête via l’[API Catalog Service](https://developer.adobe.com/experience-platform-apis/references/catalog/), l’interface utilisateur ou l’hygiène des données. Pour plus d’informations, lisez le guide sur la [suppression de jeux de données dans l’interface utilisateur](../../catalog/datasets/user-guide.md#delete-a-dataset). |

Pour en savoir plus sur Identity Service, consultez la [présentation d’Identity Service](../../identity-service/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou pour l’ingestion dans le profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| API d’abonnement aux alertes | Adobe Experience Platform Query Service vous permet de vous abonner à des alertes pour les requêtes ad hoc et planifiées. Les alertes peuvent être reçues par e-mail, dans l’interface utilisateur d’Experience Platform ou les deux. Actuellement, il n’est possible de s’abonner aux alertes de requêtes qu’à l’aide de l’[API Query Service](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| Exemples de jeux de données | Les échantillons de jeux de données Query Service vous permettent de mener des requêtes exploratoires sur les données volumineuses avec un temps de traitement considérablement réduit, mais au prix de la précision des requêtes. Pour en savoir plus, consultez le [guide d’échantillons de jeux de données](../../query-service/key-concepts/dataset-samples.md). |

Pour plus d’informations sur Query Service [!DNL Query Service], consultez la [[!DNL Query Service] présentation](../../query-service/home.md) de Query Service.

Pour en savoir plus, consultez la [documentation sur les alertes de requêtes](../../query-service/api/alert-subscriptions.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Impact de la population de segments d’Audience Manager sur un profil client en temps réel | L’ingestion de populations de segments Audience Manager importantes a un impact direct sur le nombre total de profils lorsque vous envoyez un segment Audience Manager pour la première fois à Experience Platform à l’aide de la source Audience Manager. Cela signifie que la sélection de tous les segments peut potentiellement entraîner un nombre de profils excédant vos droits d’utilisation de licence. Pour plus d’informations, reportez-vous à la [présentation de la source Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Pour plus d’informations sur l’utilisation de votre licence, consultez la documentation sur l’[utilisation du tableau de bord de l’utilisation des licences](../../dashboards/guides/license-usage.md). |
| Prise en charge d’Adobe Campaign Managed Cloud Service | Utilisez la source Adobe Campaign Managed Cloud Service pour importer vos données de logs de diffusion et de tracking Adobe Campaign 8.4 dans Experience Platform. Pour plus d’informations, lisez le guide sur la [création d’une connexion source Adobe Campaign Managed Cloud Service dans l’interface utilisateur](../../sources/tutorials/ui/create/adobe-applications/campaign.md). |
| Prise en charge des API pour l’ingestion à la demande des sources de lots | Utilisez l’ingestion à la demande pour créer des exécutions de flux ad hoc pour un flux de données donné à l’aide de l’API [!DNL Flow Service]. Les exécutions de flux créées doivent être définies sur une ingestion unique. Pour plus d’informations, consultez le guide sur la [création d’une exécution de flux pour l’ingestion à la demande à l’aide de l’API](../../sources/tutorials/api/on-demand-ingestion.md). |
| Prise en charge de l’API pour la reprise des exécutions de flux de données ayant échoué pour les sources de lots | Utilisez l’opération `re-trigger` pour essayer à nouveau de transmettre votre flux de données ayant échoué via l’API. Pour plus d’informations, lisez le guide sur la [reprise des exécutions de flux de données ayant échoué à l’aide de l’API](../../sources/tutorials/api/retry-flows.md). |
| Prise en charge de l’API pour le filtrage des données au niveau des lignes pour les sources [!DNL Google BigQuery] et [!DNL Snowflake] | Utilisez des opérateurs logiques et de comparaison pour filtrer les données au niveau des lignes pour les sources [!DNL Google BigQuery] et [!DNL Snowflake]. Pour plus d’informations, lisez le guide sur le [filtrage des données d’une source à l’aide de l’API](../../sources/tutorials/api/filter.md). |

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).
