---
title: Notes de mise à jour d’Adobe Experience Platform - Juillet 2024
description: Les notes de mise à jour de juillet 2024 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c38f6845a4819b648abacea2c36a576dac61f38f
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 27%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : mercredi 30 juillet 2024**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [!BADGE Disponibilité limitée]{type=Informative}[Composition de l’audience fédérée](#federated-audience-composition)

Mises à jour des fonctionnalités et de la documentation existantes dans Experience Platform :

- [Gestion avancée du cycle de vie des données](#advanced-data-lifecycle-management)
- [Collecte de données](#data-collection)
- [Gouvernance des données](#data-governance)
- [Destinations](#destinations)
- [Segmentation Service](#segmentation)
- [Sources](#sources)
- [Balises unifiées](#unified-tags)

## Composition d’audiences fédérées {#federated-audience-composition}

La composition d’audiences fédérées permet aux entreprises de composer des données pour une meilleure application dans divers cas d’utilisation. Grâce à cette nouvelle approche, en tant qu’utilisateur Adobe Real-Time Customer Data Platform et/ou Adobe Journey Optimizer, vous pouvez fédérer les jeux de données directement à partir de votre entrepôt de données existant pour créer et enrichir les audiences et attributs Adobe Experience Platform dans un seul système.

Pour plus d’informations, consultez la [documentation sur la composition d’audiences fédérées](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/home).

## Gestion avancée du cycle de vie des données {#advanced-data-lifecycle-management}

Experience Platform fournit une suite de fonctionnalités d’hygiène des données qui vous permet de gérer vos données stockées par le biais de suppressions programmatiques des enregistrements de consommateurs et des jeux de données. À l’aide de l’espace de travail du cycle de vie des données dans l’interface utilisateur ou par le biais d’appels à l’API Data Hygiene, vous pouvez gérer efficacement vos entrepôts de données. Utilisez ces fonctionnalités pour vous assurer que les informations sont utilisées comme prévu, qu’elles sont mises à jour lorsque des données incorrectes doivent être corrigées et qu’elles sont supprimées lorsque les politiques d’entreprise le jugent nécessaire.

**Nouvelle documentation**

| Nouvelle documentation | Description |
| --- | --- |
| Référence [!DNL Data Hygiene API] | Utilisez l’API Data Hygiene pour gérer efficacement vos entrepôts de données dans Experience Platform. Grâce à ces fonctionnalités, vous pouvez vous assurer que les informations sont utilisées comme prévu, mises à jour lorsqu’elles sont incorrectes et supprimées lorsque les stratégies d’entreprise le jugent nécessaire.<br><br> Lisez le [document de référence de l’API Data Hygiene](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/) pour obtenir des informations détaillées sur l’utilisation de l’API. Vous pouvez utiliser l’API Data Hygiene pour planifier des dates d’expiration de jeu de données, corriger ou supprimer par programmation les données personnelles client stockées et vérifier vos quotas d’hygiène de données. Le document de référence de l’API comprend les points de terminaison, les paramètres de requête et les formats de réponse disponibles pour vous aider à gérer efficacement les données client stockées.</br></br> |

Pour plus d’informations, consultez la [présentation avancée de la gestion du cycle de vie des données](../../hygiene/home.md).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permet de collecter des données d’expérience client côté client et de les envoyer à l’Edge Network Experience Platform où elles peuvent être enrichies, transformées et distribuées vers des destinations Adobe ou non Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Type | Fonctionnalité | Description |
| --- | --- | --- |
| SDK Web | Suivi automatique des interactions de propositions | Vous pouvez désormais utiliser la propriété `autoTrackPropositionInteractionsEnabled` dans le SDK Web pour déterminer si le SDK Web doit automatiquement collecter les interactions de proposition. Consultez la documentation [`autoTrackPropositionInteractionsEnabled`](../../web-sdk/commands/configure/autotrackpropositioninteractionsenabled.md) pour plus d’informations. |

{style="table-layout:auto"}

**Documentation nouvelle ou mise à jour**

| Documentation nouvelle ou mise à jour | Description |
| --- | --- |
| Nouveaux points de terminaison API documentés pour l’API Reactor | Les points de terminaison des autorisations d’utilisation du package d’extension se trouvent maintenant dans la [documentation de référence de l’API Reactor](https://developer.adobe.com/experience-platform-apis/references/reactor/). Les propriétaires d’extensions peuvent ajouter, supprimer et récupérer des autorisations de package pour un package d’extension à l’aide de ces points de terminaison. |
| Nouveau document de points de fin d’autorisation d’utilisation des packages d’extension | Vous trouverez un aperçu de la manière dont les propriétaires de packages d’extension peuvent autoriser d’autres sociétés à utiliser leurs versions privées des packages dans l’API Reactor dans la documentation [ Points de terminaison des autorisations d’utilisation des packages d’extension](/help/tags/api/endpoints/extension-package-usage-authorizations.md) . |
| Nouveau guide sur les extensions privées de partage | Les procédures de création, d’approbation et de suppression des packages d’extension de l’API Reactor sont décrites dans la documentation [ Partage d’extensions privées](/help/tags/api/guides/extension-packages.md). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation de la collecte de données](../../collection/home.md).

## Gouvernance des données {#data-governance}

Dans Adobe Experience Platform, la gouvernance des données désigne un ensemble de politiques et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle clé dans Experience Platform à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’accès aux données et le contrôle de l’accès aux données pour les actions marketing.

**Nouvelle fonctionnalité**

| Fonctionnalité | Description |
| --- | --- |
| API du service mTLS | L’ [API du service mTLS](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/mtls-api/overview) est conçu pour améliorer la sécurité des exchanges de données. Utilisez cette API pour récupérer en toute sécurité les certificats publics émis par Adobe pour les applications de votre entreprise. Ces certificats garantissent que toutes les communications sont authentifiées et chiffrées, et peuvent être utilisées pour vérifier en externe l’authenticité des certificats. Lisez le [guide de point d’entrée de certificat public](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/mtls-api/public-certificate-endpoint) pour savoir comment récupérer en toute sécurité les certificats publics pour les applications d’Adobe de votre entreprise. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation de la gouvernance des données](../../data-governance/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations** {#new-destinations}

| Destination | Description |
| ----------- | ----------- |
| [(Beta) Merkury Enterprise Connections](/help/destinations/catalog/data-partners/merkury-enterprise-connections.md) | Utilisez la destination [!DNL Merkury Enterprise Connections] pour diffuser en toute sécurité des audiences vers [!DNL Merkury]. [!DNL Merkury] fournit aux marketeurs une mise en correspondance et une diffusion aisées des audiences basées sur la personne vers les connexions télévisées/CTV, d’éditeur et de technologie publicitaire 80+ haut débit de [!DNL Merkury]. [!DNL Merkury] est alimenté par un graphique complet d&#39;identités de consommateurs américains adultes de plus de 268 millions de personnes. |
| [(Beta) Merkury Enterprise Identity](/help/destinations/catalog/data-partners/merkury-enterprise-identity.md) | Utilisez la destination [!DNL Merkury Enterprise Identity] pour créer des profils consommateurs plus précis, complets et pertinents. Grâce à l’amélioration des données de profil, les marketeurs peuvent optimiser les informations, les segments et les modèles, ce qui se traduit par un ciblage et une modélisation prédictive plus précis. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| Surveillance du flux de données au niveau de l’audience | La surveillance de vos flux de données, regroupés par audiences, n’était auparavant disponible que pour les destinations par lot (basées sur des fichiers). À compter de cette version, la surveillance au niveau de l’audience est également disponible pour la [(Beta) Google Customer Match + DV360 streaming destination](/help/destinations/catalog/advertising/google-customer-match-dv360.md). Pour en savoir plus sur la [surveillance au niveau de l’audience](/help/dataflows/ui/monitor-destinations.md#segment-level-view) et contactez votre représentant d’Adobe si vous souhaitez rejoindre le programme bêta pour utiliser la destination Google Customer Match + DV360. |
| Prise en charge des attributs d’enrichissement dans les macros de métadonnées d’audience pour Destination SDK | Vous pouvez désormais accéder aux attributs d’enrichissement dans les [modèles de métadonnées d’audience de Destination SDK](../../destinations/destination-sdk/functionality/audience-metadata-management.md) par le biais de macros dédiées. Les attributs d’enrichissement sont disponibles uniquement pour les [audiences de chargement personnalisées](../../destinations/destination-sdk/functionality/destination-configuration/schema-configuration.md#external-audiences). Consultez le [guide d’activation de l’audience par lot](../../destinations/ui/activate-batch-profile-destinations.md#select-enrichment-attributes) pour voir comment fonctionne la sélection des attributs d’enrichissement. Pour plus d’informations, consultez la [liste des macros](../../destinations/destination-sdk/functionality/audience-metadata-management.md#macros) du modèle d’audience. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des destinations](../../destinations/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] permet de segmenter en audiences les données stockées dans [!DNL Experience Platform] qui se rapportent aux personnes (tels que les clientes et clients, les prospects, les utilisateurs et utilisatrices ou les organisations). Vous pouvez créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur [!DNL Platform] et sont facilement accessibles à partir de n’importe quelle solution Adobe.

**Nouvelle documentation**

| Nouvelle documentation | Description |
| ----------------- | ----------- | 
| [Audience Portal](../../segmentation/ui/audience-portal.md) | Découvrez comment utiliser Audience Portal, qui vous permet d’afficher, de gérer et de créer des audiences dans Adobe Experience Platform dans un hub centralisé. |

{style="table-layout:auto"}

## Sources

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Documentation mise à jour**

| Documentation mise à jour | Description |
| --- | --- |
| Guide d’authentification étendu pour [[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md) | Lisez le guide d&#39;authentification étendu pour [!DNL Snowflake] pour apprendre à récupérer votre [identifiant de compte](../../sources/connectors/databases/snowflake.md#retrieve-your-account-identifier) et votre [clé privée](../../sources/connectors/databases/snowflake.md#retrieve-your-private-key) pour l&#39;authentification. De plus, utilisez le guide d’authentification étendu pour savoir comment [vérifier les configurations de votre entrepôt et de vos rôles](../../sources/connectors/databases/snowflake.md#verify-configurations). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des sources](../../sources/home.md).

## Balises unifiées

Les balises unifiées vous permettent de classer et de gérer vos objets commerciaux dans Adobe Experience Platform. Avec l’API des balises unifiées, vous pouvez créer des dossiers et des balises pour mieux organiser les objets Platform tels que les audiences ou les jeux de données.

**Nouvelle documentation**

| Nouvelle documentation | Description |
| ----------------- | ----------- |
| [Guide de l’API des balises unifiées](../../administrative-tags/api/overview.md) | Lisez le guide de l’API des balises unifiées pour savoir comment créer des dossiers et des balises pour trier vos objets commerciaux. |
| [Référence de l’API de balises unifiées](https://developer.adobe.com/experience-platform-apis/references/unified-tags/) | Utilisez la référence de l’API des balises unifiées pour tester de manière interactive les points de terminaison des balises unifiées. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des balises unifiées](../../administrative-tags/overview.md).
