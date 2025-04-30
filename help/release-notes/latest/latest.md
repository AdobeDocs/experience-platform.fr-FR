---
title: Notes de mise à jour d’Adobe Experience Platform - Avril 2025
description: Les notes de mise à jour d’avril 2025 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 7772e0b6f512c3854a03fb01580c80cc0cb41ba3
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 29%

---

# Notes de mise à jour d’Adobe Experience Platform

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : mercredi 29 avril 2025**

Mises à jour des fonctionnalités et de la documentation existantes dans Adobe Experience Platform :

- [Experience League](#experience-league)
- [Destinations](#destinations)
- [Modèle de données d’expérience](#xdm)
- [Service d’identités](#identity)
- [Query Service](#query-service)
- [Profil client en temps réel](#profile)
- [Sources](#sources)

## Experience League {#experience-league}

Experience League est une plateforme d’apprentissage complète conçue pour vous aider à améliorer vos compétences avec les produits Adobe. Il offre diverses ressources, notamment : des cours, de la documentation, des pages de la communauté, des événements et l’accès aux certifications.

| Fonctionnalité | Description |
| --- | --- |
| Page d’accueil personnalisée | Accédez à votre page d’accueil personnalisée et personnalisez-la sur [Experience League](https://experienceleague.adobe.com/en/home#). Connectez-vous avec vos informations d’identification Adobe, puis sélectionnez **[!UICONTROL Experience League]** dans le menu supérieur pour commencer à optimiser votre expérience d’apprentissage : <ul><li>**Signets** : utilisez la fonction [!UICONTROL Signets] pour enregistrer et collecter vos ressources préférées à un seul endroit. Vous pouvez enregistrer divers contenus, notamment des listes de lecture, des articles et des tutoriels.</li><li>**Personnaliser votre apprentissage** : améliorez votre expérience d’apprentissage en mettant à jour votre profil Experience League avec les rôles, secteurs d’activité, produits et niveaux d’expérience qui correspondent le mieux à vos besoins.</li><li>**Recommandations** : affichez le contenu d’apprentissage recommandé en fonction de votre activité récente.</li><li>**Récemment consultés** : utilisez la section [!UICONTROL Récemment consultés] pour revenir rapidement au contenu récemment consulté, tel que la documentation et les vidéos.</li><li>**Ressources d’apprentissage** : utilisez le panneau [!UICONTROL Toutes les ressources d’apprentissage] pour accéder aux tutoriels, à la documentation, à la communauté, aux événements et aux certifications.</li><li>**Nouveautés** : consultez la section [!UICONTROL Nouveautés] pour obtenir un flux de contenu le plus récent sur Experience League.</li><li>**Regarder des événements passés à la demande** : regardez des diffusions en direct enregistrées précédemment sur les projecteurs de produit, des cas d’utilisation et des tutoriels avec la section [!UICONTROL Regarder des événements passés à la demande].</li></ul><br> ![Page d’accueil personnalisée sur Experience League.](../2025/assets/april/personalized-home-page.png "Page d’accueil personnalisée sur Experience League."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#new-updated-destinations}

| Destination | Description |
| --- | --- |
| [Marketo Engage Person Sync](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe a mis à jour la destination [!DNL Marketo Engage Person Sync] pour résoudre un problème qui affectait les clients lorsque plusieurs e-mails étaient présents dans le mappage d’identité. |
| [(V2) Connexion à l’audience en temps réel Pega CDH](/help/destinations/catalog/personalization/pega-v2.md) | Utilisez la destination [!DNL (V2) Pega Customer Decision Hub Realtime Audience] dans Adobe Experience Platform pour envoyer les attributs de profil et les données d’audience à Pega Customer Decision Hub pour la prise de décision la plus appropriée, lorsque plusieurs applications Pega Customer Decision Hub sont configurées dans votre compte Pega. |

**Fonctionnalité nouvelle ou mise à jour** {#destinations-new-updated-functionality}

| Fonctionnalité | Description |
| --- | --- |
| Options de planification **hebdomadaire** et **mensuelle** pour les exportations de fichiers complets | Vous pouvez désormais planifier des exportations de fichiers complets pour les personnes et les audiences de prospects sur une base hebdomadaire ou mensuelle lors de l’activation vers des destinations basées sur des fichiers de stockage dans le cloud. [En savoir plus](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) sur les options de planification. |

{style="table-layout:auto"}

**correctifs, améliorations et autres annonces** {#destinations-fixes-and-enhancements}

- **Application des dates de fin d’exportation des jeux de données retardées au 1er septembre 2025**\
  Dans le cadre de la version [septembre 2024](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality), Adobe a défini une date de fin par défaut au 1er mai 2025 pour tout flux de données d’exportation de jeux de données créé *avant cette version*. Adobe prolonge désormais cette date limite d’application au **1er septembre 2025** afin de donner aux clients plus de temps pour mettre à jour leurs planifications. Reportez-vous à la section de planification du tutoriel [exportation de jeux de données](../../destinations/ui/export-datasets.md#schedule-dataset-export) pour plus d’informations sur la modification de la date de fin d’un flux de données d’exportation de jeux de données.

- **Amélioration de la gestion des transferts SFTP ayant échoué pour l’intégration LiveRamp**\
  Adobe a implémenté un correctif pour un problème affectant les exportations de fichiers vers la destination [Intégration LiveRamp](/help/destinations/catalog/advertising/liveramp-onboarding.md) via SFTP. Parfois, les transferts de fichiers échouaient en raison de problèmes transitoires côté serveur et les fichiers temporaires provenant de tentatives infructueuses restaient sur le serveur. Ces fichiers impossibles à supprimer ont bloqué les reprises suivantes, car Adobe ne disposait pas de l’autorisation de les remplacer.\
  Avec le correctif, si une nouvelle tentative ne parvient pas à supprimer le fichier temporaire, Adobe génère un nouveau fichier avec un suffixe ajouté , `attempt2`, pour s’assurer que la nouvelle tentative se termine avec succès.

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Composants XDM mis à jour**

| Fonctionnalité | Description |
| --- | --- |
| Les champs de chaîne reçoivent une valeur minimale d’un | Par défaut, les nouveaux champs de chaîne ont une longueur minimale d’un. Les valeurs nulles pour les champs non obligatoires sont toujours acceptables. Pour plus d’informations sur les bonnes pratiques, consultez le guide sur [les bonnes pratiques pour la modélisation des données](../../xdm/schema/best-practices.md#data-integrity-tips) |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Experience Platform, consultez la [ Présentation du système XDM ](../../xdm/home.md).

## Service d’identités {#identity}

Utilisez le service d’identités d’Adobe Experience Platform pour créer une vue complète de votre clientèle et de ses comportements en reliant les identités entre les appareils et les systèmes, vous permettant ainsi de proposer des expériences numériques personnelles et percutantes en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Disponibilité limitée]{type=Informative} [!DNL Identity Graph Linking Rules] | Les règles de liaison du graphique d’identités sont désormais en disponibilité limitée et sont accessibles à tous les clients dans les sandbox de développement. <ul><li>**Exigences d’activation** : la fonctionnalité reste inactive jusqu’à ce que vous configuriez et enregistriez votre [!DNL Identity Settings]. Sans cette configuration, le système continuera à fonctionner normalement, sans changement de comportement.</li><li>**Remarques importantes** : au cours de cette phase de disponibilité limitée, la segmentation d’Edge peut produire des résultats inattendus en termes d’appartenance à un segment. Cependant, la segmentation par lots et en flux continu fonctionnera comme prévu.</li><li>**Étapes suivantes** : pour plus d’informations sur la manière d’activer cette fonctionnalité dans les sandbox de production, contactez l’équipe de votre compte Adobe.</li></ul> |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [[!DNL Identity Graph Linking Rules]  documentation ](../../identity-service/identity-graph-linking-rules/overview.md).

## Service de requête {#query-service}

Interrogez des données dans le lac de données Adobe Experience Platform à l’aide de SQL standard avec le service de requête. Combinez en toute transparence des jeux de données et générez-en de nouveaux à partir des résultats de vos requêtes pour alimenter les rapports, activer les workflows de science des données ou faciliter l’ingestion dans le profil client en temps réel. Vous pouvez, par exemple, fusionner les données de transaction client avec les données comportementales afin d’identifier les audiences à forte valeur ajoutée pour les campagnes marketing ciblées.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Remplacement de l’audience SQL | Actualisez l’appartenance à une audience en remplaçant les profils existants par les résultats d’une nouvelle requête SQL. Vous pouvez ainsi gérer plus efficacement les audiences dynamiques en supprimant les enregistrements obsolètes et en insérant les enregistrements mis à jour en une seule opération. Pour plus d’informations, consultez le guide [extension d’audience SQL](../../query-service/data-distiller-audiences/overview.md#replace-audience). |
| Télécharger et copier les résultats de la requête | [Téléchargez les résultats de la requête directement à partir du Query Editor](../../query-service/ui/overview.md#download-query-results) sous la forme de fichiers CSV, XLSX ou JSON, ou [copiez les résultats dans le presse-papiers](../../query-service/ui/overview.md#copy-results) sous la forme de valeurs séparées par des virgules (CSV) pour une utilisation rapide dans des tableurs tels qu’Excel. Ces améliorations rationalisent les workflows d’analyse, de création de rapports et de validation des données hors ligne. |
| Affichage des résultats de la requête en plein écran | [La requête de prévisualisation donne lieu à une boîte de dialogue plein écran](../../query-service/ui/overview.md#view-results) qui permet d’améliorer la lisibilité, d’analyser facilement les jeux de données volumineux et de sélectionner des lignes à copier. L’affichage plein écran fournit une disposition de grille redimensionnable, ce qui vous permet d’examiner plus efficacement les tableaux larges et les sorties détaillées. |
| Amélioration de la sélection des colonnes dans la prédiction de modèle | Sélectionnez des colonnes spécifiques et appliquez des alias à l’aide de la syntaxe de `model_predict` étendue. Récupérez les résultats de prédiction intermédiaires tels que les vecteurs de caractéristiques et les scores de probabilité. La sélection améliorée nécessite l’activation d’un indicateur de fonctionnalité. Consultez la [documentation du cycle de vie du modèle](../../query-service/advanced-statistics/models.md#select-specific-output-fields) pour obtenir des exemples de syntaxe et des informations sur les indicateurs de fonctionnalité. |
| Enregistrer les sorties de prédiction de modèle à l’aide de CREATE TABLE et INSERT INTO | [Enregistrez les sorties de prédiction sélectionnées dans de nouveaux tableaux à l’aide de CREATE TABLE AS SELECT ou insérez-les dans les tableaux existants à l’aide de INSERT INTO SELECT](../../query-service/advanced-statistics/models.md#predict). Si la sélection améliorée de colonnes est activée, les résultats intermédiaires tels que les vecteurs de caractéristiques et les probabilités peuvent également être conservés avec les prédictions finales. Pour consulter des exemples d’utilisation, consultez la documentation sur la syntaxe [SQL](../../query-service/sql/syntax.md#create-table-as-select). |

Pour plus d’informations sur Query Service [!DNL Query Service], consultez la [[!DNL Query Service] présentation](../../query-service/home.md) de Query Service.

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue holistique de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le Profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Expiration des données de profils pseudonymes | Gérez l’expiration de vos données de profil pseudonymes dans le tableau de bord Profil . Pour en savoir plus sur cette fonctionnalité et les profils pseudonymes, veuillez lire la section [Guide d’expiration des données de profil pseudonyme](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

Pour en savoir plus sur le profil client en temps réel, lisez d’abord la [présentation des profils](../../profile/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Nouvelles sources**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | La source [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md) est désormais disponible. Utilisez cette source pour importer vos données d’affinités des profils d’utilisateurs [!DNL Algolia] dans Experience Platform. Vous pouvez ensuite utiliser ces données pour améliorer l’interaction client, les taux de conversion et l’expérience client globale en proposant des solutions de recherche hautes performances pour les sites web, les plateformes d’e-commerce et les applications. Pour plus d’informations, consultez le guide sur la [ingestion [!DNL Algolia User Profiles] données dans Experience Platform](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md). |
| Prise en charge de l’API [!BADGE Beta]{type=Informative} pour [!DNL Azure Databricks] | La source [!DNL Azure Databricks] est désormais disponible dans l’API. Utilisez l’API [!DNL Flow Service] pour connecter votre compte [!DNL Databricks] et importer vos données [!DNL Databricks] dans Experience Platform. Pour plus d’informations, consultez la documentation sur [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md). |

{style="table-layout:auto"}

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mise à jour des champs XDM pour l’ingestion de données Streaming Media dans Experience Platform. | Le nouveau groupe de champs XDM, `mediaReporting`, est désormais disponible pour ingérer des données de médias en flux continu via la source Adobe Analytics dans Experience Platform. Ce champ remplace le champ `media.mediaTimed`.</br> <br>Pendant une période de transition de trois mois, l’ingestion des données sur les champs `media.mediaTimed` se poursuivra. Cependant, à la fin du mois de juillet 2025, les champs `media.mediaTimed` seront entièrement obsolètes et ne seront plus visibles dans l’interface utilisateur du schéma Experience Platform, et les données seront envoyées uniquement à l’aide des champs `mediaReporting`.</br><br>Si vous avez implémenté la source Analytics pour collecter des données de médias en flux continu dans Platform avant le 22 avril 2025, vous devez migrer vos configurations existantes pour envoyer des données à l’aide du nouveau groupe de champs. Cette migration doit être terminée d’ici la fin juillet 2025. Contactez l’équipe chargée de votre compte Adobe pour obtenir une assistance sur la migration. |
| Nouveaux types d’authentification pour [!DNL MariaDB] et [!DNL PostgreSQL] | Vous pouvez désormais utiliser l’authentification de base pour authentifier vos sources [!DNL MariaDB] et [!DNL PostgreSQL] sur Experience Platform. Pour plus d’informations, consultez la documentation suivante : <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| Prise en charge du filtrage au niveau des lignes pour les [!DNL Amazon Redshift] | Vous pouvez utiliser les fonctionnalités de filtrage au niveau des lignes pour vos données [!DNL Amazon Redshift] sur Experience Platform. Pour plus d’informations, consultez le guide sur le [filtrage des données au niveau des lignes pour les sources dans l’API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../../sources/home.md).
