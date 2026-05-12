---
title: Notes de mise à jour préliminaires d’Experience Platform
description: Aperçu des dernières notes de mise à jour de Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: f09a2a1f05f05e7e90aa73d650506a231acbb5df
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 30%

---

# Notes de mise à jour préliminaires de Adobe Experience Platform

>[!IMPORTANT]
>
>Ce document est conçu comme un **aperçu** des notes de mise à jour du mois en cours. Les éléments de version peuvent faire l’objet de modifications et peuvent être ajoutés ou supprimés dans la version finale.

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/latest)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : mai 2026**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [Attributs calculés](#computed-attributes)
- [Destinations](#destinations)
- [Profil client en temps réel](#profile)
- [Service de segmentation](#segmentation-service)
- [Sources](#sources)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités Experience Platform. Vous pouvez vous abonner à différentes règles d’alerte via l’onglet [!UICONTROL Alerts] de l’interface utilisateur d’Experience Platform et choisir de recevoir des messages d’alerte dans l’interface utilisateur elle-même ou par e-mail de notification.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Historique des alertes : filtrage et capacité de découverte | La page Historique des alertes affiche désormais le nom de l’objet associé, ajoute la recherche par type d’alerte et le filtrage par nom d’objet, et comprend un sélecteur de période amélioré, ce qui facilite la corrélation des alertes et la recherche de ce dont vous avez besoin. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [[!DNL Observability Insights] vue d’ensemble](/help/observability/home.md).

## Attributs calculés {#computed-attributes}

Les attributs calculés permettent de résumer facilement les données d’événement dans les attributs de profil par le biais d’une interface utilisateur intuitive pour une segmentation, une personnalisation et une activation optimisées basées sur le comportement. Grâce à cette fonctionnalité, vous pouvez créer des attributs calculés en libre-service, les gérer et les utiliser dans la segmentation, dans les destinations Real-Time CDP ou dans Adobe Journey Optimizer. En outre, les attributs calculés simplifient la segmentation et les workflows de parcours pour vous aider à diffuser facilement des expériences pertinentes.

| Fonctionnalité | Description |
| --- | --- |
| Fonction de liste dans les attributs calculés | Utilisez la fonction List dans les attributs calculés pour renvoyer un tableau de valeurs à partir d’événements de qualification. Cette fonction est destinée à être utilisée lorsque les événements de qualification proviennent d’un seul jeu de données. Si les événements de qualification s’étendent sur plusieurs jeux de données, les résultats peuvent être incomplets. |

{style="table-layout:auto"}

Pour en savoir plus sur les attributs calculés, veuillez lire la [Vue d’ensemble sur les attributs calculés](../profile/computed-attributes/overview.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| {type=Informative} [Exporter des tableaux pour les attributs d’enrichissement](../destinations/ui/activate-batch-profile-destinations.md#select-enrichment-attributes) | Exportez les champs du tableau en tant qu’attributs d’enrichissement lors de l’activation des audiences vers des destinations d’espace de stockage. Sélectionnez des champs internes individuels dans un tableau et ils sont exportés en tant que colonnes distinctes dans les sorties JSON et Parquet. Cette fonctionnalité est disponible pour un nombre limité de clientes et clients. Pour obtenir l’accès, contactez votre représentant ou représentante Adobe. Pour plus d’informations, consultez la [documentation sur les attributs d’enrichissement](../destinations/ui/activate-batch-profile-destinations.md#select-enrichment-attributes). |
| Prise en charge des audiences externes pour [[!DNL Criteo]](../destinations/catalog/advertising/criteo.md) | Activez les audiences d’origines autres que Segmentation Service vers la destination [Criteo](../destinations/catalog/advertising/criteo.md), y compris les audiences de chargement personnalisées (importées depuis CSV), les audiences semblables, les audiences fédérées et les audiences créées dans d’autres applications Experience Platform telles que [!DNL Adobe Journey Optimizer]. Voir la section [audiences prises en charge](../destinations/catalog/advertising/criteo.md#supported-audiences) pour plus d’informations. |
| Nouvelles destinations prises en charge pour [[!DNL Acxiom Audience Connection]](../destinations/catalog/advertising/acxiom-audience-connection.md) et [[!DNL Acxiom Real ID Audience Connection]](../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | Cinq nouvelles destinations sont désormais prises en charge : [!DNL Roku], [!DNL Samsung Ads], [!DNL The Trade Desk] (1ère partie), [!DNL Warner Bros. Discovery] et [!DNL Yahoo]. Pour plus d’informations, consultez les documents [Acxiom Audience Connection](../destinations/catalog/advertising/acxiom-audience-connection.md) et [Acxiom Real ID Audience Connection](../destinations/catalog/advertising/acxiom-real-id-audience-connection.md). |

{style="table-layout:auto"}

**Correctifs et améliorations**

| Corriger | Description |
| --- | --- |
| Prise en charge des macros [[!DNL Google Cloud Storage]](../destinations/catalog/cloud-storage/google-cloud-storage.md) | Le [`%SEGMENT_NAME%`](../destinations/catalog/cloud-storage/overview.md#use-macros) et d’autres macros de chemin de dossier fonctionnent désormais correctement pour les destinations [!DNL Google Cloud Storage]. Auparavant, les macros n’étaient pas remplacées par le nom de l’audience dans le chemin d’exportation. |
| [[!DNL Federated Audiences]](https://www.adobe.com/go/destinations-federated-audience-composition) exporter le fichier maintenant | L’option **[!UICONTROL Export file now]** est désormais prise en charge pour les destinations [!DNL Federated Audience Composition]. |
| Correctif de l’interface utilisateur de planification [[!DNL Snowflake]](../destinations/catalog/warehouses/snowflake.md) | Correction d’un problème en raison duquel le basculement de la fréquence d’exportation entre quotidienne et unique dans la configuration de destination [!DNL Snowflake] entraînait le blocage de l’interface utilisateur. |
| Comportement du type de clé [[!DNL Google Customer Match]](../destinations/catalog/advertising/google-customer-match.md) | Mise à jour de la documentation pour clarifier la façon dont [!DNL Google] gère les types de clés d’identité dans un flux de données de destination. Vous pouvez mapper plusieurs types de clés dans la même connexion, mais si vous mettez à jour les mappages, toute identité que vous ajoutez doit utiliser le même type de clé que l’identité que vous avez supprimée. La suppression de tous les champs d’un type de clé donné ou le changement de type de clé entre les exécutions d’activation [!DNL Google] entraîne la suppression de la liste d’audiences correspondante. Voir la section [comportement du type de clé](../destinations/catalog/advertising/google-customer-match.md#key-type-behavior) pour plus d’informations. |
| [Affichage des jeux de données dans un flux de données d’exportation de jeu de données](../destinations/api/export-datasets.md#view-datasets-in-dataflow) | Mise à jour de la documentation pour montrer comment récupérer les jeux de données associés à un flux de données d’exportation de jeu de données existant à l’aide de l’API Flow Service. Pour plus d’informations, consultez la [documentation sur l’exportation de jeux de données](../destinations/api/export-datasets.md#view-datasets-in-dataflow) . |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des destinations](../destinations/home.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Progression de l’ingestion des profils par lots | Effectuez le suivi en temps réel des traitements d’ingestion de profils par lots depuis le tableau de bord de surveillance. Affichez le lancement de la tâche, le temps dans la file d’attente et la progression du point de contrôle critique, y compris le moment où les données sont prêtes pour la segmentation et la recherche de profil. Utilisez ces informations pour prédire la disponibilité des données en aval et planifier les lancements de campagne en toute confiance. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble du profil client en temps réel](../profile/home.md).

## Service de segmentation {#segmentation-service}

Utilisez Segmentation Service pour créer des audiences à partir des données de vos clients et gérer leur cycle de vie complet dans Experience Platform.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Améliorations de la composition de l’audience | Tous les clients disposent désormais d’une base de 50 compositions. Les autres améliorations comprennent l’activation chaînée et l’enrichissement de l’audience. |
| Mode express pour les audiences externes | Utilisez le mode express pour activer des audiences externes directement via l’API sans le workflow d’activation complet. |
| Audiences de compte avec événements d’expérience (B2B) | Après la mise à niveau de l’architecture B2B CDP, les audiences de compte avec des événements d’expérience ne sont plus directement prises en charge. Pour créer une audience de compte qui utilise des événements d’expérience, commencez par créer une audience de personnes avec les événements d’expérience, puis référencez cette audience de personnes lors de la création de l’audience de compte. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des audiences](../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Sources nouvelles ou mises à jour**

| Source | Description |
| --- | --- |
| [!DNL Delta Sharing] | Vous pouvez utiliser la source [!DNL Delta Sharing] pour importer des tables Delta dans Experience Platform par le biais d’un protocole de partage de données ouvert et sécurisé. Une fois que vous avez configuré une connexion [!DNL Delta Sharing] et sélectionné les partages et les tableaux à ingérer, Experience Platform importe automatiquement ces données dans vos jeux de données afin que vous puissiez les utiliser pour l’analyse, la segmentation et l’activation. |
| [!DNL LAVA] | Utilisez le connecteur source [!DNL LAVA] pour ingérer des données à partir de [!DNL LAVA] dans Experience Platform à l’aide de schémas et de contrôles de gouvernance normalisés, ce qui réduit l’effort d’intégration personnalisé et améliore le délai de rentabilisation pour l’activation et les informations en aval. |
| [!DNL Meta Ads] (Beta) | Vous pouvez utiliser le connecteur source [!DNL Meta Ads] (Beta) dans l’espace de travail Sources pour vous authentifier auprès de [!DNL Meta], sélectionner vos comptes publicitaires et planifier l’ingestion des données de campagne et de performances [!DNL Meta Ads] dans les jeux de données Experience Platform. |

{style="table-layout:auto"}

**Mises à jour et correctifs**

| Source | Description |
| --- | --- |
| Mise à jour de la place sur la liste autorisée IP de la région NLD2 | Cinq plages d’adresses IP ont été ajoutées à la place sur la liste autorisée de la région NLD2 : `20.105.215.28/30`, `20.105.244.48/29`, `57.153.246.72/29`, `57.153.246.80/28` et `57.153.246.96/30`. Mettez à jour votre liste autorisée réseau si vous utilisez des sources dans la région NLD2. |
| Limites des champs de lot [!DNL Shopify] | Certains champs [!DNL Shopify] ne sont pris en charge qu’en mode Aperçu. Pour ingérer ces champs, utilisez l’API pour créer vos flux de données au lieu du workflow de l’interface utilisateur. Pour obtenir la liste des champs concernés, consultez la documentation sur les sources de [!DNL Shopify] . |
| Désactivation automatique du flux de données | Les flux de données Source qui échouent en continu pendant 30 jours sont automatiquement désactivés. Lorsqu’un flux de données est désactivé, passez en revue la raison de l’échec dans Surveillance, appliquez les mises à jour nécessaires et réactivez le flux de données. Les raisons d’échec courantes incluent les informations d’identification, les autorisations ou les modifications de configuration des schémas et des mappages. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des sources](../sources/home.md).
