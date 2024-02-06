---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour de janvier 2024 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c6d471d7bb8cb9d5e376cc49c9c89c39e663d7f9
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 60%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 30 janvier 2024**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Cas d’utilisation des classeurs](#use-case-playbooks)

Mises à jour des fonctionnalités existantes dans Experience Platform :

- [Contrôle d’accès basé sur les attributs](#abac)
- [Préparation des données](#data-prep)
- [Tableaux de bord](#dashboards)
- [Destinations](#destinations)
- [Identity Service](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [Profil client en temps réel](#profile)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Cas d’utilisation des classeurs {#use-case-playbooks}

La variable [!UICONTROL Cas d’utilisation des classeurs] Cette fonctionnalité est désormais disponible pour tous les clients Real-Time CDP et Adobe Journey Optimizer. [!UICONTROL Cas d’utilisation des classeurs] sont conçues pour aider les utilisateurs à surmonter les défis lorsqu’ils commencent à utiliser Real-time Customer Data Platform ou Adobe Journey Optimizer. Lorsque vous ne savez pas où commencer ou comment créer les ressources appropriées pour les cas d’utilisation souhaités, les classeurs de cas d’utilisation vous inspirent et créent différentes ressources que vous pouvez tester et importer dans des environnements de production lorsque vous êtes prêt.

Pour commencer à utiliser [!UICONTROL Cas d’utilisation des classeurs], lisez les pages de documentation suivantes :

- Lisez la section [page d’aperçu](/help/use-case-playbooks/playbooks/overview.md) pour comprendre l’objectif, les informations de disponibilité et obtenir une démonstration de bout en bout du fonctionnement des playbooks, de la découverte à la création d’instances, en passant par l’importation de ressources générées dans d’autres environnements de test.
- Obtenir une liste de tous les [livres de lecture disponibles](/help/use-case-playbooks/playbooks/playbooks-list.md), regroupés par produit (Real-Time CDP ou Journey Optimizer)
- Obtenez des informations sur toutes les [autorisations requises](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) pour utiliser les playbooks et les ressources générées par les playbooks.
- Comprendre le [fonctionnalité de sensibilisation aux données](/help/use-case-playbooks/playbooks/data-awareness.md) qui vous permet de copier des ressources générées vers d’autres environnements de test.
- Get [conseils de dépannage](/help/use-case-playbooks/playbooks/troubleshooting.md) si vous rencontrez des erreurs ou des difficultés lors de l’utilisation des classeurs de cas d’utilisation.

## Contrôle d’accès basé sur les attributs {#abac}

Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui offre une plus grande flexibilité dans la gestion de l’accès utilisateur. Elle est destinée aux marques veillant à garantir un haut niveau de confidentialité. Les objets individuels tels que les champs de schéma et les segments peuvent être affectés à des rôles d’utilisateur. Cette fonctionnalité vous permet d’accorder ou de révoquer l’accès à des objets individuels pour des utilisateurs Platform spécifiques au sein de votre organisation.

Grâce au contrôle d’accès basé sur les attributs, les administrateurs de votre organisation peuvent contrôler l’accès des utilisateurs aux données personnelles sensibles (SPD), aux informations d’identification personnelle (PII) et à d’autres types de données personnalisées sur l’ensemble des workflows et ressources de Platform. Les administrateurs et administratrices peuvent définir des rôles d’utilisateur qui n’ont accès qu’à des champs spécifiques et aux données correspondant à ces champs.

**Documentation nouvelle ou mise à jour**

| Mise à jour de la documentation | Description |
| --- | --- |
| Nouveaux points de terminaison API documentés pour le contrôle d’accès basé sur les attributs | La variable [Documentation de référence de l’API Access Control](https://developer.adobe.com/experience-platform-apis/references/access-control/) comprend désormais des rôles d’API de contrôle d’accès basés sur des attributs, des stratégies et des points de terminaison de produit. Ces points de terminaison peuvent être utilisés pour récupérer les rôles, stratégies et produits pertinents pour un utilisateur sur des ressources données dans un environnement de test spécifié. |

{style="table-layout:auto"}

Pour plus d’informations sur le contrôle d’accès basé sur les attributs, consultez la [présentation du contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md). Pour consulter un guide complet sur le workflow de contrôle d’accès basé sur les attributs, reportez-vous au [guide complet du contrôle d’accès basé sur les attributs](../../access-control/abac/end-to-end-guide.md).

## Préparation des données {#data-prep}

La préparation des données permet aux personnes travaillant dans l’ingénierie de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles fonctions du mappeur | <ul><li>`object_to_map` : utilisez la fonction `object_to_map` pour créer des types de données de mappage. Cette fonction prend en charge plusieurs syntaxes différentes. Pour plus d’informations, consultez le guide sur les [fonctions pour les hiérarchies - objets](../../data-prep/functions.md#objects). </li><li>`to_map` : utilisez la fonction `to_map` pour créer un mappage avec des paires nom/valeur de champ données à l’aide d’objets. Pour plus d’informations, consultez le guide sur les [fonctions pour les hiérarchies - mappages](../../data-prep/functions.md#map). </li><li>`array_to_map` : utilisez la fonction `array_to_map` pour créer un mappage avec des paires nom/valeur de champ données à l’aide de tableaux d’objets. Pour plus d’informations, consultez le guide sur les [fonctions pour les hiérarchies - mappages](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Pour plus d’informations sur la préparation des données, consultez la [présentation de la préparation des données](../../data-prep/home.md).

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit de nombreux tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre organisation, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Afficher le SQL | Vous pouvez désormais afficher le code SQL derrière vos profils, audiences, destinations et informations personnalisées à l’aide du bouton bascule Afficher le code SQL , puis exécuter la requête à la demande via l’éditeur de requêtes. L’accès au code SQL qui alimente vos insights Real-time Customer Data Platform vous permet de comprendre la logique derrière l’analyse de votre modèle de données. Grâce à cette transparence, vos données CDP en temps réel Adobe sont plus accessibles, plus compréhensibles et plus pertinentes pour la prise de décision.<br>Tirer parti du SQL de plus de 40 insights existants pour créer de nouvelles requêtes qui obtiennent des insights uniques à partir des données de Platform en fonction des besoins de votre entreprise. Le langage SQL est également disponible pour votre [Profils](../../dashboards/insights/profiles.md), [Audiences](../../dashboards/insights/audiences.md), et [Destinations](../../dashboards/insights/destinations.md) informations dans la documentation de l’Experience League. Ces documents mettent en évidence les cas d’utilisation professionnels auxquels des informations standard peuvent répondre. Pour plus d’informations, consultez le guide sur l’[affichage des insights SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [présentation des tableaux de bord](../../dashboards/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations** {#new-destinations}

| Destination | Description |
| ----------- | ----------- |
| [Connexion Pubmatic](../../destinations/catalog/advertising/pubmatic.md) | Utilisez cette destination pour envoyer des données d’audience à la plateforme [!DNL PubMatic Connect]. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| Nouveau **rôle assumé** type d’authentification pour les destinations Amazon S3 | Utilisez le nouveau type d’authentification de rôle assumé lors de la connexion d’Experience Platform à vos compartiments Amazon S3 si vous ne souhaitez pas partager les clés de compte et les clés secrètes avec Experience Platform. En savoir plus sur la nouvelle méthode d’authentification dans la section [section d&#39;authentification](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) de la documentation d’Amazon S3. |

{style="table-layout:auto"}

Pour obtenir plus d’informations générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Identity Service {#identity-service}

Adobe Experience Platform Identity Service vous offre la possibilité de mieux connaître vos clients et clientes ainsi que leur comportement en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.

**Documentation nouvelle ou mise à jour**

| Mise à jour de la documentation | Description |
| --- | --- |
| Restructuration de la documentation | La documentation d’Identity Service a été restructurée afin d’améliorer la présentation et la clarté des concepts au sein d’Identity Service :<ul><li>Visitez le [Page d’aperçu d’Identity Service](../../identity-service/home.md) pour un guide terminologique étendu, un exemple de cas d’utilisation détaillant un parcours client type, une ventilation de la manière dont Identity Service relie les identités et un résumé du rôle que Identity Service place dans l’écosystème Experience Platform.</li><li>Lisez le guide sur [compréhension de la relation entre Identity Service et Real-time Customer Profile](../../identity-service/identity-and-profile.md) pour un résumé détaillé de la façon dont les deux services fonctionnent ensemble et des différences entre leurs objectifs, leurs processus, leurs entrées et leurs sorties.</li><li>Voir [Guide logique de liaison d’Identity Service](../../identity-service/features/identity-linking-logic.md) pour obtenir des explications et des visualisations sur le comportement du graphique d’identités en fonction de différents scénarios et horodatages.</li></ul> |

{style="table-layout:auto"}

Pour en savoir plus sur le Service d’identités, consultez la [vue d’ensemble du Service d’identités](../../identity-service/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Basée sur Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) aide les entreprises à rassembler des données connues et inconnues pour activer les profils des clients et clientes avec une prise de décision intelligente tout au long du parcours client. [!DNL Real-Time CDP] associe plusieurs sources de données d’entreprise pour créer des profils client en temps réel. Les segments créés à partir de ces profils peuvent ensuite être envoyés vers des destinations en aval afin de fournir des expériences personnalisées et individuelles aux clients et clientes sur tous les canaux et appareils.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mises à jour de la [page d’accueil du profil client en temps réel](https://experience.adobe.com) | <ul><li>**Widget de profils** : vous pouvez désormais utiliser le widget de profils pour accéder à la page de la vue d’ensemble des profils et afficher les mesures de profil de votre organisation.</li><li>**Carte des mesures de profil** : la carte des mesures de profil du tableau de bord de la page d’accueil affiche désormais le nombre total de profils de votre organisation, en fonction de votre politique de fusion respective.</li><li>**Widget de schémas** : vous pouvez désormais utiliser le widget de schémas pour accéder au workflow de création de schémas dans l’interface utilisateur.</li></ul> |

{style="table-layout:auto"}

**Documentation nouvelle ou mise à jour**

| Mise à jour de la documentation | Description |
| --- | --- |
| Nouvelle page d’accueil de la documentation Real-Time CDP | Visitez le [nouvelle page d’accueil de la documentation Real-Time CDP](/help/rtcdp/home.md) pour obtenir des informations en un coup d’oeil sur la prise en main du produit, des barrières de sécurité, des exemples de cas d’utilisation, etc. |
| Exemple de cas d’utilisation Real-Time CDP - Aperçu | Visitez le [nouvelle page d’aperçu des exemples de cas d’utilisation](/help/rtcdp/use-case-guides/overview.md) pour un ensemble d’exemples d’utilisation que votre entreprise peut réaliser avec Real-Time CDP. |

{style="table-layout:auto"}

Pour en savoir plus sur Real-Time CDP, lisez le [Présentation de Real-Time CDP](../../rtcdp/overview.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue holistique de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le Profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Améliorations de la localisation des cartes de tableau de bord par défaut de la visionneuse de profils | Les cartes de profil par défaut auront désormais des noms localisés dynamiquement. Les cartes de profil personnalisées peuvent toujours comporter des noms personnalisés qui peuvent être modifiés. |

{style="table-layout:auto"}

Pour en savoir plus sur le profil client en temps réel, lisez d’abord la [présentation des profils](../../profile/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Chargement d’audience généré en externe | Le nombre maximum de colonnes a été augmenté pour **25**. |
| Estimations du créateur de segments | Les estimations et les profils qualifiés s’affichent désormais dans la section des propriétés de l’audience. Pour plus d’informations sur cette modification, consultez la section [Guide de l’interface utilisateur du créateur de segments](../../segmentation/ui/segment-builder.md). |

{style="table-layout:auto"}

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Version Beta]{type=Informative}Sources [!DNL Oracle NetSuite] | Utilisez les intégrations [!DNL Oracle NetSuite] dans le catalogue de sources pour importer des données depuis vos comptes [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) et [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) dans Experience Platform. |
| [!BADGE Version bêta]{type=Informative}Source [!DNL Braze Currents] | Utilisez l’intégration [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) dans le catalogue de sources pour importer des données depuis votre compte [!DNL Braze] dans Experience Platform. |
| Prise en charge de l’authentification par paire de clés pour la source de lots [!DNL Snowflake] | Vous pouvez désormais utiliser l’authentification par paire de clés lors de la création d’un nouveau compte [!DNL Snowflake] pour les données de lots. Pour plus d’informations, consultez le guide sur la [création d’un compte  [!DNL Snowflake]  à l’aide de l’API](../../sources/tutorials/api/create/databases/snowflake.md) ou le guide sur la [création d’un compte  [!DNL Snowflake]  à l’aide de l’interface utilisateur](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).