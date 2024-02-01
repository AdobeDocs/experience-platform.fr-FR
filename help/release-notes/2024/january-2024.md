---
title: Notes de mise à jour d’Adobe Experience Platform - Janvier 2024
description: Notes de mise à jour de janvier 2024 pour Adobe Experience Platform.
source-git-commit: a4d6c72cc2c3f5f547a3c66e509d520d3fed29ea
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 41%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : mercredi 30 janvier 2024**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Cas d’utilisation des classeurs](#use-case-playbooks)

Mises à jour des fonctionnalités existantes dans Experience Platform :

- [Tableaux de bord](#dashboards)
- [Préparation des données](#data-prep)
- [Destinations](#destinations)
- [Real-Time Customer Data Platform](#rtcdp)
- [Profil client en temps réel](#profile)
- [Sources](#sources)

## Cas d’utilisation des classeurs {#use-case-playbooks}

La variable [!UICONTROL Cas d’utilisation des classeurs] Cette fonctionnalité est désormais disponible pour tous les clients Real-Time CDP et Adobe Journey Optimizer. [!UICONTROL Cas d’utilisation des classeurs] sont conçues pour aider les utilisateurs à surmonter les défis lorsqu’ils commencent à utiliser Real-time Customer Data Platform ou Adobe Journey Optimizer. Lorsque vous ne savez pas où commencer ou comment créer les ressources appropriées pour les cas d’utilisation souhaités, les classeurs de cas d’utilisation vous inspirent et créent différentes ressources que vous pouvez tester et importer dans des environnements de production lorsque vous êtes prêt.

Pour commencer à utiliser [!UICONTROL Cas d’utilisation des classeurs], lisez les pages de documentation suivantes :

- Lisez la section [page d’aperçu](/help/use-case-playbooks/playbooks/overview.md) pour comprendre l’objectif, les informations de disponibilité et obtenir une démonstration de bout en bout du fonctionnement des playbooks, de la découverte à la création d’instances, en passant par l’importation de ressources générées dans d’autres environnements de test.
- Obtenir une liste de tous les [livres de lecture disponibles](/help/use-case-playbooks/playbooks/playbooks-list.md), regroupés par produit (Real-Time CDP ou Journey Optimizer)
- Obtenez des informations sur toutes les [autorisations requises](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) pour utiliser les playbooks et les ressources générées par les playbooks.
- Comprendre le [fonctionnalité de sensibilisation aux données](/help/use-case-playbooks/playbooks/data-awareness.md) qui vous permet de copier des ressources générées vers d’autres environnements de test.
- Get [conseils de dépannage](/help/use-case-playbooks/playbooks/troubleshooting.md) si vous rencontrez des erreurs ou des difficultés lors de l’utilisation des classeurs de cas d’utilisation.

## Préparation des données {#data-prep}

La préparation des données permet aux personnes travaillant dans l’ingénierie de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles fonctions du mappeur | <ul><li>`object_to_map`: utilisez la variable `object_to_map` pour créer des types de données de mappage. Cette fonction prend en charge plusieurs syntaxes différentes. Pour plus d’informations, consultez le guide sur [fonctions pour les hiérarchies - objets](../../data-prep/functions.md#objects). </li><li>`to_map`: utilisez la variable `to_map` pour créer une map avec des paires nom-valeur de champ données à l’aide d’objets. Pour plus d’informations, consultez le guide sur [fonctions pour les hiérarchies - mappages](../../data-prep/functions.md#map). </li><li>`array_to_map`: utilisez la variable `array_to_map` pour créer une map avec des paires nom-valeur de champ données à l’aide de tableaux d’objets. Pour plus d’informations, consultez le guide sur [fonctions pour les hiérarchies - mappages](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Pour plus d’informations sur la préparation des données, consultez la section [Aperçu de la préparation des données](../../data-prep/home.md).

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit de nombreux tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre organisation, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Afficher SQL | Vous pouvez désormais afficher le code SQL derrière vos profils, audiences, destinations et informations personnalisées, puis exécuter la requête à la demande via l’éditeur de requêtes. Tirer parti du SQL de plus de 40 insights existants pour créer de nouvelles requêtes qui obtiennent des insights uniques à partir des données de Platform en fonction des besoins de votre entreprise. Pour plus d’informations, consultez le guide sur [affichage d’informations SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [Présentation des tableaux de bord](../../dashboards/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations** {#new-destinations}

| Destination | Description |
| ----------- | ----------- |
| [Connexion publique](../../destinations/catalog/advertising/pubmatic.md) | Utilisez cette destination pour envoyer des données d’audience à la variable [!DNL PubMatic Connect] plateforme. |

{style="table-layout:auto"}

Pour obtenir des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Basée sur Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) aide les entreprises à rassembler des données connues et inconnues pour activer les profils des clients et clientes avec une prise de décision intelligente tout au long du parcours client. [!DNL Real-Time CDP] associe plusieurs sources de données d’entreprise pour créer des profils client en temps réel. Les segments créés à partir de ces profils peuvent ensuite être envoyés vers des destinations en aval afin de fournir des expériences personnalisées et individuelles aux clients et clientes sur tous les canaux et appareils.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mises à jour du [Page d’accueil Real-Time CDP](https://experience.adobe.com) | <ul><li>**Widget de profils**: vous pouvez désormais utiliser le widget Profils pour accéder à la page d’aperçu des profils et afficher les mesures de profil de votre entreprise.</li><li>**Carte des mesures de profil**: la carte Mesures des profils du tableau de bord de la page d’accueil affiche désormais le nombre total de profils de votre organisation, en fonction de votre stratégie de fusion respective.</li><li>**Widget de schémas**: vous pouvez désormais utiliser le widget de schémas pour accéder au workflow de création de schémas dans l’interface utilisateur.</li></ul> |

Pour en savoir plus sur Real-Time CDP, lisez le [Présentation de Real-Time CDP](../../rtcdp/overview.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue holistique de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le Profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Améliorations de la localisation des cartes de tableau de bord par défaut de la visionneuse de profils | Les cartes de profil par défaut auront désormais des noms localisés dynamiquement. Les cartes de profil personnalisées peuvent toujours comporter des noms personnalisés qui peuvent être modifiés. |

{style="table-layout:auto"}

Pour en savoir plus sur Real-time Customer Profile, lisez la section [Présentation des profils](../../profile/home.md)

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Version Beta]{type=Informative}[!DNL Oracle NetSuite] sources | Utilisez la variable [!DNL Oracle NetSuite] intégrations dans le catalogue de sources pour importer des données de votre [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) et [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) comptes à Experience Platform. |
| [!BADGE Version bêta]{type=Informative}[!DNL Braze Currents] source | Utilisez la variable [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) intégration dans le catalogue de sources pour importer les données de votre [!DNL Braze] compte à Experience Platform. |
| Prise en charge de l’authentification par paire de clés pour [!DNL Snowflake] source du lot | Vous pouvez désormais utiliser l’authentification par paire de clés lors de la création d’une nouvelle [!DNL Snowflake] pour les données de lot. Pour plus d’informations, consultez le guide sur [création d’un [!DNL Snowflake] compte utilisant l’API](../../sources/tutorials/api/create/databases/snowflake.md) ou le guide sur [création d’un [!DNL Snowflake] compte utilisant l’interface utilisateur](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).