---
title: Notes de mise à jour d’Adobe Experience Platform - Mai 2025
description: Notes de mise à jour de mai 2025 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: ad9ec9c3177c25e2207b67b4c939c3f6fa97883f
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 51%

---

# Notes de mise à jour d’Adobe Experience Platform

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/latest)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de mise à jour : mercredi 20 mai 2025**

Mises à jour des fonctionnalités et de la documentation existantes dans Adobe Experience Platform :

- [Catalog Service](#catalog-service)
- [Préparation des données](#data-prep)
- [Destinations](#destinations)
- [Service d’identités](#identity)
- [Service de requête](#query-service)
- [Sandbox](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [Sources](#sources)

## Catalog Service {#catalog-service}

Catalog Service est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, Catalog conserve les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

| Fonctionnalité | Description |
| --- | --- |
| Optimisation du stockage des données avec des règles de conservation au niveau des jeux de données | Gérez efficacement le stockage des données avec des politiques de conservation qui suppriment les données obsolètes selon le délai spécifié. <ul><li>**Conservation des jeux de données** : définissez des règles de jeu de données pour supprimer les données obsolètes du lac de données et du magasin de profils.</li><li>**Storage Insights** : surveillez l’utilisation et assurez-vous que les droits sous licence sont respectés au moyen de mesures intégrées.</li><li>**Visibilité améliorée** : suivez l’activité des jeux de données, de l’ingestion à la suppression, grâce à une surveillance améliorée.</li><li>**Gestion rationalisée** : accédez aux paramètres de conservation, à la surveillance, aux journaux d’audit et aux informations dans une vue unifiée unique.</li></ul> Lisez le guide sur les [règles de conservation des jeux de données](../../catalog/datasets/user-guide.md#data-retention-policy) pour plus d’informations. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation du service de catalogue](../../catalog/home.md).

## Préparation des données {#data-prep}

Utilisez la préparation des données pour mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge des mappages d’import et d’export pour Adobe Analytics | Vous pouvez désormais utiliser les fonctionnalités de mappage d’import et d’export pour les données de votre suite de rapports Adobe Analytics lors de l’utilisation du connecteur source Adobe Analytics. <br><br>Exportez vos mappages dans un fichier CSV et configurez-les localement sur une feuille de calcul. Vous pouvez ensuite importer vos mappages mis à jour dans Experience Platform à l’aide de l’interface de mappage de l’IU. Vous pouvez utiliser cette fonctionnalité pour configurer un grand nombre de mappages sans avoir à les créer manuellement dans l’IU. De plus, lors de la création d’un flux de données, vous pouvez charger une copie de vos mappages directement dans Experience Platform pour accélérer votre workflow. <br><br>Pour plus d’informations, consultez le guide sur [la connexion d’Adobe Analytics à Experience Platform](../../sources/tutorials/ui/create/adobe-applications/analytics.md).</br> |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble de la préparation de données](../../data-prep/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalité nouvelle ou mise à jour** {#destinations-new-updated-functionality}

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge d’identifiants supplémentaires pour le ciblage de [Google](../../destinations/catalog/advertising/google-customer-match.md) | La destination Correspondance client de Google prend désormais en charge le mappage des champs liés aux adresses pour des taux de correspondance améliorés dans la plateforme Google. <br><br>Pour que Google corresponde à l’adresse, vous devez mapper les quatre champs d’adresse (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` et `address_info_postal_code`) et vous assurer qu’aucun de ces champs ne manque de données dans les profils exportés. <br> Si un champ n’est pas mappé ou contient des données manquantes, Google ne correspond pas à l’adresse. |
| Colonne Expiration du compte pour les connexions [Facebook](../../destinations/catalog/social/facebook.md) | Les dates d’expiration des jetons de compte Facebook apparaissent désormais dans les onglets [Parcourir](../../destinations/ui/destinations-workspace.md#browse) et [Comptes](../../destinations/ui/destinations-workspace.md#accounts). |
| Exporter les jeux de données créés par l’API | Vous pouvez désormais exporter des jeux de données créés par API. La limitation précédente, en vertu de laquelle seuls les jeux de données créés dans l’interface utilisateur étaient disponibles pour l’exportation, a été levée. En savoir plus sur l’[exportation de jeux de données](../../destinations/ui/export-datasets.md). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des destinations](../../destinations/home.md).

## Service d’identités {#identity}

Utilisez le service d’identités d’Adobe Experience Platform pour créer une vue complète de votre clientèle et de ses comportements en reliant les identités entre les appareils et les systèmes, vous permettant ainsi de proposer des expériences numériques personnelles et percutantes en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!DNL Identity Graph Linking Rules] | [!DNL Identity Graph Linking Rules] est désormais disponible pour tous. [!DNL Identity Graph Linking Rules] éviter la « réduction du graphique », en garantissant des profils clients distincts et précis pour un marketing personnalisé dans Experience Platform et les applications. Les principales fonctionnalités sont les suivantes :<ul><li>[Outil de simulation graphique](../../identity-service/identity-graph-linking-rules/graph-simulation.md) : explorez l’algorithme et testez les configurations du paramètre d’identité.</li><li> [Paramètres d’identité](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md) : configurez des espaces de noms uniques et définissez des priorités.</li><li>[Tableau de bord des identités](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) : surveiller les graphiques et valider les paramètres d’identité.</li></ul> **Remarque** : vos données ne seront pas modifiées tant que vous n’aurez pas configuré manuellement vos paramètres d’identité. |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la présentation d’Identity Service [](../../identity-service/home.md).

## Service de requête {#query-service}

Interrogez des données dans le lac de données Adobe Experience Platform à l’aide de SQL standard avec le service de requête. Combinez en toute transparence des jeux de données et générez-en de nouveaux à partir des résultats de vos requêtes pour alimenter les rapports, activer les workflows de science des données ou faciliter l’ingestion dans le profil client en temps réel. Vous pouvez, par exemple, fusionner les données de transaction client avec les données comportementales afin d’identifier les audiences à forte valeur ajoutée pour les campagnes marketing ciblées.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
|--------|-------------|
| Migration des informations d’identification JWT vers OAuth | Les informations d’identification JWT non expirantes doivent être migrées vers OAuth de serveur à serveur d’ici le 30 juin 2025, afin d’éviter les interruptions de service. Cette modification améliore la sécurité et la cohérence de la plateforme. Pour plus d’informations, consultez le guide [Migration des informations d’identification de serveur à serveur de JWT vers OAuth](../../query-service/ui/migrate-jwt-to-oauth.md). |
| Ancien Tableau De Résultats (Disponibilité Limitée) | Les utilisateurs qui dépendent des workflows glisser-sélectionner peuvent demander l’accès à un tableau de résultats hérité qui prend en charge la sélection native du navigateur et le comportement de copie. La sortie collée est délimitée par des tabulations, de sorte que les colonnes restent alignées et lisibles dans Excel, ce qui facilite la révision des feuilles de calcul et les processus d’assurance qualité. Pour plus d’informations, consultez le [guide de l’interface utilisateur de Query Editor](../../query-service/ui/user-guide.md#legacy-results-table). |

Pour plus d’informations sur Query Service [!DNL Query Service], consultez la [[!DNL Query Service] présentation](../../query-service/home.md) de Query Service.

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des sandbox qui divisent une instance d’Experience Platform unique en plusieurs environnements virtuels pour favoriser le développement et l’évolution d’applications d’expérience digitale.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Extension de prise en charge du plug-in d’outils relatifs au sandbox | Les campagnes peuvent désormais être migrées avec d’autres objets dépendants par le biais des outils Sandbox, notamment la configuration des canaux, la décision unifiée, les paramètres/variantes d’expérience, etc. Pour obtenir la liste complète des objets Campaign pris en charge, ainsi que tous les objets Adobe Journey Optimizer pris en charge, consultez le guide [sandbox tooling](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects). |

{style="table-layout:auto"}

Pour plus d’informations sur les sandbox, consultez la [vue d’ensemble des sandbox](../../sandboxes/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de série temporelle représentant les interactions des clients avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mise à jour des critères de segmentation en streaming | À compter de la version de mai 2025, les critères d’éligibilité de vos audiences à la segmentation en flux continu ont été mis à jour. Vous trouverez plus d’informations sur ces modifications dans la [mise à jour des critères d’éligibilité à la segmentation en streaming](../../segmentation/eligibility-criteria-update.md). |

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de l’authentification de base pour [!DNL MySQL] | Vous pouvez désormais utiliser l’authentification de base pour connecter votre base de données [!DNL MySQL] à Experience Platform. Lisez la [[!DNL MySQL] présentation de la source](../../sources/connectors/databases/mysql.md) pour plus d’informations. |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../../sources/home.md).