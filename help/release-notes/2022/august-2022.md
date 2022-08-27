---
title: Notes de mise à jour de Adobe Experience Platform - Août 2022
description: Notes de mise à jour d’août 2022 pour Adobe Experience Platform.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: fb9fdc70aabb62cdc39888b1ff90557d8420c31b
workflow-type: tm+mt
source-wordcount: '2137'
ht-degree: 33%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 24 août 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Profil client en temps réel](#profile)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Les services d’IA/ML permettent aux analystes et spécialistes du marketing d’exploiter la puissance de l’intelligence artificielle et du machine learning dans les cas d’utilisation de l’expérience client. Cela permet aux analystes marketing de configurer des modèles spécifiques aux besoins d’une entreprise à l’aide de configurations au niveau de l’entreprise sans avoir besoin d’expertise en science des données.

### IA dédiée à l’attribution

L’IA dédiée à l’attribution est utilisée pour attribuer des crédits aux points de contact qui génèrent des événements de conversion. Il peut aider les spécialistes du marketing à quantifier l’impact publicitaire de chaque point de contact marketing sur le parcours client.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de la confidentialité | <ul><li> Attribution AI prend désormais en charge la définition des rôles utilisateur et des stratégies d’accès pour gérer les [permissions](../../../help/access-control/abac/ui/permissions.md) pour les fonctions et les objets au sein d’une application de produit. </li><li>Les ressources du journal d’audit sont automatiquement enregistrées lorsque l’activité se produit.</li><li> Via [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md), les administrateurs peuvent contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction de certains attributs, qui peuvent être des métadonnées ajoutées à un objet, comme des libellés. Les administrateurs peuvent également définir des rôles utilisateur ayant accès à des champs et des données spécifiques qui correspondent à ces champs.</li><li>Attribution AI exploite les jeux de données Platform. Pour prendre en charge les demandes de droits des consommateurs qu’une marque peut recevoir, les marques doivent utiliser le Privacy Service Platform pour soumettre les demandes d’accès et de suppression des clients afin de supprimer leurs données dans le lac de données, Identity Service et Real-time Customer Profile.  </li><li>Tous les jeux de données utilisés pour l’entrée/la sortie des modèles suivront les directives de Platform. Le chiffrement des données de plateforme s’applique aux données au repos et en transit. Consultez la documentation pour en savoir plus sur [cryptage des données](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Remarque**: Attribution AI ne sera disponible avec les clients existants de Healthcare Shield ou Privacy Shield avant d’être averti.

Pour plus d’informations sur Attribution AI, reportez-vous à la section [Attribution AI](../../intelligent-services/attribution-ai/overview.md) aperçu.

### IA dédiée aux clients

L’IA dédiée aux clients disponible dans Real-time Customer Data Platform est utilisée pour générer des scores de propension personnalisés tels que l’attrition et la conversion pour des profils individuels à grande échelle.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de la confidentialité | <ul><li> Customer AI prend désormais en charge la définition des rôles utilisateur et des stratégies d’accès pour gérer les [permissions](../../../help/access-control/abac/ui/permissions.md) pour les fonctions et les objets au sein d’une application de produit. </li><li>Les ressources du journal d’audit sont automatiquement enregistrées lorsque l’activité se produit.</li><li> Via [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md), les administrateurs peuvent contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction de certains attributs. Ces attributs peuvent être des métadonnées ajoutées à un objet, comme des libellés. Les administrateurs peuvent également définir des rôles utilisateur ayant accès uniquement à des champs et données spécifiques qui correspondent à ces champs.</li><li>Customer AI exploite des jeux de données Platform. Pour prendre en charge les demandes de droits des consommateurs qu’une marque peut recevoir, les marques doivent utiliser le Privacy Service Platform pour soumettre les demandes d’accès et de suppression des clients afin de supprimer leurs données dans le lac de données, Identity Service et Real-time Customer Profile. </li><li>Tous les jeux de données utilisés pour l’entrée/la sortie des modèles suivront les directives de Platform. Le chiffrement des données de plateforme s’applique aux données au repos et en transit. Consultez la documentation pour en savoir plus sur [cryptage des données](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Remarque**: L’IA dédiée aux clients ne sera disponible avec les clients existants de Healthcare Shield ou de Privacy Shield avant d’être avertie.

Pour plus d’informations sur Customer AI, voir [Customer AI](../../intelligent-services/customer-ai/overview.md) aperçu.

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fournit plusieurs [!DNL dashboards] grâce à laquelle vous pouvez afficher des informations importantes sur les données de votre organisation, telles qu’elles sont capturées lors d’instantanés quotidiens.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Widget d’activations planifiées | Le [!UICONTROL Activations planifiées] Le widget offre une vue tabulée des destinations activées le plus récemment. Pour chaque segment, il inclut le nom, la plateforme de destination et les dates de début et de fin de l’activation. Ce widget vous permet de découvrir en un coup d’oeil où et quand l’audience est activée et rend les activations en double ou inutiles plus transparentes. Ces informations cumulées indiquent également les endroits où les activations ont été laissées de côté. |

Pour plus d’informations sur les [!DNL Dashboards], consultez la [[!DNL Dashboards] présentation](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de l’ingestion d’enregistrements avec des avertissements | La préparation des données localisera désormais les avertissements (erreurs non critiques) dans les champs et permettra d’ingérer le reste de la ligne. Toutes les erreurs de transformation du mappeur sont désormais signalées comme avertissements et les lignes partiellement ingérées sont considérées comme réussies, avec un avertissement.  La surveillance est également prise en charge sur les enregistrements avec des avertissements et des informations de diagnostic. Actuellement, l’ingestion partielle des enregistrements avec avertissements n’est disponible que pour la diffusion en continu des données. Consultez la documentation sur [ingestion d’enregistrements avec des avertissements](../../sources/tutorials/ui/monitor-streaming.md) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

Pour en savoir plus sur [!DNL Data Prep], consultez la présentation de [[!DNL Data Prep] ](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ----------- | ----------- |
| (Version bêta) Prise en charge de la personnalisation basée sur les attributs pour les destinations de personnalisation | Avec la version bêta de la personnalisation basée sur les attributs, vous verrez deux nouvelles cartes dans le [catalogue de destination](../../destinations/catalog/overview.md): <ul><li>**[!UICONTROL Adobe Target V2]**: Ce connecteur est actuellement en version bêta et disponible uniquement pour un nombre restreint de clients. Outre les fonctionnalités de la carte Adobe Target V1, le connecteur Target V2 ajoute une [étape de mappage](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) au workflow d’activation, qui vous permet de mapper les attributs de profil à Adobe Target, en activant la personnalisation de la même page et de la page suivante basée sur les attributs.</li><li>**[!UICONTROL Personnalisation Personnalisée Avec Attributs]**: Ce connecteur est actuellement en version bêta et disponible uniquement pour un nombre restreint de clients. En plus des fonctionnalités fournies par la fonction **[!UICONTROL Personnalisation personnalisée]**, la variable **[!UICONTROL Personnalisation Personnalisée Avec Attributs]** Le connecteur ajoute une valeur facultative [étape de mappage](../../destinations/ui/activate-profile-request-destinations.md#map-attributes) au workflow d’activation, qui vous permet de mapper les attributs de profil à votre destination de personnalisation personnalisée, en activant la personnalisation de même page et de page suivante basée sur les attributs.</li></ul> <br> Les attributs de profil peuvent contenir des données sensibles. Pour protéger ces données, la variable **[!UICONTROL Personnalisation Personnalisée Avec Attributs]** La destination requiert que vous utilisiez la variable [API du serveur réseau Edge](../../server-api/overview.md) pour la collecte de données. De plus, tous les appels de l’API du serveur doivent être effectués dans une [contexte authentifié](../../server-api/authentication.md). |

{style=&quot;table-layout:auto&quot;}

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) est une plateforme d’exécution des ventes qui possède le plus grand nombre de données d’interaction entre vendeurs et acheteurs B2B au monde et qui investit de manière significative dans des technologies d’IA propriétaires afin de traduire les données de vente en informations. [!DNL Outreach] aide les entreprises à automatiser l’engagement commercial et à agir sur la base de l’intelligence du chiffre d’affaires afin d’améliorer leur efficacité, leur prévisibilité et leur croissance. |

{style=&quot;table-layout:auto&quot;}

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Schéma global | [[!UICONTROL Schéma d’entité AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Décrit les entités dénormalisées pour Adobe Journey Optimizer. |
| Classe | [[!UICONTROL Entités d’exécution AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | Décrit les entités d’exécution Adobe Journey Optimizer à utiliser dans la segmentation. |
| Groupe de champs | [[!UICONTROL Objets de travail Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Groupe de champs wrapper qui référence tous les groupes de champs spécifiques à l’objet de niveau inférieur pour Adobe Workfront. |

{style=&quot;table-layout:auto&quot;}

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Groupe de champs | [[!UICONTROL Champs communs des événements d’étape du Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Deux nouvelles propriétés ont été ajoutées : `origTimeStamp` et `experienceID`. |
| Groupe de champs | [[!UICONTROL Détails de l’appartenance à un segment]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | En complément de [!UICONTROL XDM Individual Profile], ce groupe de champs peut désormais être utilisé dans les schémas basés sur la classe XDM Business Account . |
| Groupe de champs | (Multiple) | Plusieurs groupes de champs liés aux activités Marketo B2B ont été mis à jour vers un état stable. Voir ce qui suit : [requête d’extraction](https://github.com/adobe/xdm/pull/1593/files) pour plus d’informations. |
| Groupe de champs | (Multiple) | Plusieurs groupes de champs liés à la météo ont été mis à jour afin de corriger les erreurs qui se produisaient pour `uvIndex` et `sunsetTime`. Voir ce qui suit : [requête d’extraction](https://github.com/adobe/xdm/pull/1602/files) pour plus d’informations. |
| Type de données | [[!UICONTROL Élément de liste de produits]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Une nouvelle propriété `productImageUrl` a été ajouté. |
| Type de données | [[!UICONTROL Informations détaillées sur les données de la QoE]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Une nouvelle propriété `framesPerSecond` a été ajouté. |
| Type de données | [[!UICONTROL Informations détaillées sur la session]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` a été renommé `appVersion`. `meta:enum` et `description` ont également été mises à jour. |
| Types de données et groupes de champs | (Multiple) | Plusieurs types de données et groupes de champs de médias comportent de nouveaux champs et des descriptions mises à jour. Voir ce qui suit : [requête d’extraction](https://github.com/adobe/xdm/pull/1582/files) pour plus d’informations. |
| (Toutes) | (Multiple) | Tous les objets de schéma qui contiennent une propriété `enum` contient désormais également un champ correspondant. `meta:enum` champ pour indiquer les valeurs d’affichage de chaque contrainte. Voir ce qui suit : [requête d’extraction](https://github.com/adobe/xdm/pull/1601/files) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Profil client en temps réel offre une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le Profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Limite des stratégies de fusion | Platform appliquera désormais une limite stricte de **cinq** stratégies de fusion par environnement de test. Si votre environnement de test comporte actuellement plus de cinq stratégies de fusion, vous allez **not** être en mesure de créer de nouvelles stratégies de fusion jusqu’à ce que l’environnement de test comporte moins de cinq stratégies de fusion. |
| Nettoyage des attributs de périphérie du profil orphelins | Pour toutes les organisations, le service de profil supprime désormais quotidiennement les attributs de périphérie restants de la région d’activité des utilisateurs afin d’offrir une représentation plus précise de vos profils dans votre système. Ce nettoyage se produit une fois que tous les fragments de profil d’un profil donné sont supprimés et doit avoir une incidence sur les profils fusionnés à partir des jeux de données où `com_adobe_aep_profile_region_dataset` est marqué comme `true`. Cela peut indiquer une baisse de la mesure &quot;Audience adressable&quot; dans le tableau de bord de l’utilisation des licences et une baisse de la mesure &quot;Nombre de profils&quot; dans le tableau de bord du profil, car ces mesures incluaient des fragments d’attribut de périphérie résiduels avant cette version. |

{style=&quot;table-layout:auto&quot;}

Pour en savoir plus sur le profil client en temps réel, notamment les bonnes pratiques et les tutoriels relatifs à lʼutilisation des données de profil, consultez la [présentation du profil client en temps réel](../../profile/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de 4 000 segments | Toutes les organisations disposant de Platform peuvent désormais prendre en charge jusqu’à 4 000 définitions de segment. Pour plus d’informations sur l’impact de cette modification sur les API de tâche de segmentation, consultez la section [guide de point de fin de tâche de segmentation](../../segmentation/api/segment-jobs.md) |

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité générale des sources en libre-service (SDK par lots) | Développez, testez et intégrez votre source de données basée sur l’API REST pour ingérer des données de lot dans Experience Platform à l’aide de spécifications de source faciles à configurer. Avec le SDK Sources, vous pouvez : <ul><li>Configurez une nouvelle source pour le catalogue Experience Platform.</li><li>Définissez les spécifications de votre source, y compris les informations relatives aux types d’authentification pris en charge, à la planification et à la manière dont les données de ressource sont récupérées.</li><li>Créez une documentation destinée aux utilisateurs pour votre nouvelle source.</li></ul> Pour plus d’informations, consultez la documentation sur [Sources en libre-service (SDK par lots)](../../sources/sources-sdk/overview.md). |
| Disponibilité générale de la source [!DNL Google BigQuery] | Utilisez la variable [!DNL Google BigQuery] source pour ingérer des données à partir de votre [!DNL Google BigQuery] entrepôt de données vers Experience Platform. Pour plus d’informations, consultez la documentation relative à la [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] source (bêta) | Utilisez la variable [!DNL Teradata Vantage] source pour ingérer des données à partir d’environnements multicloud hybrides vers Experience Platform. Pour plus d’informations, consultez la documentation relative à la [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Prise en charge inter-régions de la source Adobe Analytics | Vous pouvez désormais ingérer des suites de rapports à partir de n’importe quelle région (États-Unis, Royaume-Uni ou Singapour). Les suites de rapports doivent être mappées à la même organisation que l’instance Sandbox Experience Platform dans laquelle la connexion source est créée. Pour plus d’informations, consultez le guide sur [création d’une connexion source Adobe Analytics dans l’interface utilisateur](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style=&quot;table-layout:auto&quot;}

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
