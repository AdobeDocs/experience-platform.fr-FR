---
title: Notes de mise à jour d’Adobe Experience Platform - Mai 2025
description: Notes de mise à jour de mai 2025 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 3f143c34d31483e91e176b1c69d82db38a8bc6b5
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 83%

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

**Date de mise à jour : 20 mai 2025**

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
| Optimiser le stockage de données avec des règles de conservation au niveau du jeu de données | Gérez efficacement le stockage des données avec des politiques de conservation qui suppriment les données obsolètes selon le délai spécifié. <ul><li>**Conservation des jeux de données** : définissez des règles de jeu de données pour supprimer les données obsolètes du lac de données et du magasin de profils.</li><li>**Informations de stockage** : surveillez l’utilisation et assurez-vous que les droits sous licence sont respectés au moyen de mesures intégrées.</li><li>**Visibilité améliorée** : suivez l’activité des jeux de données, de l’ingestion à la suppression, grâce à une surveillance améliorée.</li><li>**Gestion rationalisée** : accédez aux paramètres de conservation, à la surveillance, aux journaux d’audit et aux informations dans une vue unifiée unique.</li></ul> Pour plus d’informations, lisez le guide sur les [règles de conservation des jeux de données](../../catalog/datasets/user-guide.md#data-retention-policy). |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des services de catalogue](../../catalog/home.md).

## Préparation des données {#data-prep}

Utilisez la préparation des données pour mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prendre en charge des mappages d’import et d’export pour Adobe Analytics | Vous pouvez désormais utiliser les fonctionnalités de mappage d’import et d’export pour les données de votre suite de rapports Adobe Analytics lors de l’utilisation du connecteur source Adobe Analytics. <br><br>Exportez des mappages vers un fichier CSV et configurez-les localement sur une feuille de calcul. Vous pouvez ensuite importer vos mappages mis à jour dans Experience Platform à l’aide de l’interface de mappage de l’IU. Vous pouvez utiliser cette fonctionnalité pour configurer un grand nombre de mappages sans avoir à les créer manuellement dans l’IU. De plus, lors de la création d’un flux de données, vous pouvez charger une copie de vos mappages directement dans Experience Platform pour accélérer votre workflow. <br><br>Pour plus d’informations, consultez le guide sur la [connexion d’Adobe Analytics à Experience Platform](../../sources/tutorials/ui/create/adobe-applications/analytics.md).</br> |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble de la préparation de données](../../data-prep/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalité nouvelle ou mise à jour** {#destinations-new-updated-functionality}

| Fonctionnalité | Description |
| --- | --- |
| [Audience personnalisée Facebook](../../destinations/catalog/social/facebook.md) mise à niveau et prise en charge des identifiants liés aux adresses | À compter du 23 mai 2025 et tout au long du mois de juin 2025, il se peut que vous voyiez temporairement deux cartes de destination **[!DNL Facebook Custom Audience]** dans le catalogue des destinations, pour une durée maximale de quelques heures. Cela est dû à une mise à niveau interne du service de destinations et à la prise en charge de nouveaux champs pour un ciblage amélioré et une correspondance avec les profils sur les propriétés Facebook. Pour plus d’informations sur les nouveaux champs liés à l’adresse, consultez la section [identités prises en charge](#supported-identities). <br><br>Si vous voyez une carte intitulée **[!UICONTROL (Nouvelle) Audience personnalisée Facebook]**, utilisez-la pour les nouveaux flux de données d’activation. Vos flux de données existants seront mis à jour automatiquement. Aucune action n’est donc requise de votre part. Toute modification apportée aux flux de données existants au cours de cette période sera conservée après la mise à niveau. Une fois la mise à niveau terminée, la carte de destination **[!UICONTROL (Nouvelle) Audience personnalisée Facebook]** sera renommée **[!DNL Facebook Custom Audience]**. <br><br>Si vous créez des flux de données à l’aide de l’API [Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/), vous devez mettre à jour vos [!DNL flow spec ID] et [!DNL connection spec ID] avec les valeurs suivantes : <ul><li>ID de spécification de flux : `bb181d00-58d7-41ba-9c15-9689fdc831d3`</li><li>ID de spécification de connexion : `c8b97383-2d65-4b7a-9913-db0fbfc71727`</li></ul> |
| Prise en charge d’identifiants supplémentaires pour le [ciblage par liste de clients de Google](../../destinations/catalog/advertising/google-customer-match.md) | La destination Ciblage par liste de clients de Google prend désormais en charge le mappage des champs liés aux adresses pour des taux de correspondance améliorés dans la plateforme Google. <br><br>Pour que Google assure la correspondance de l’adresse, vous devez mapper les quatre champs d’adresse (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` et `address_info_postal_code`) et vous assurer qu’il n’existe pas de données de champs manquantes dans les profils exportés. <br> Si un champ n’est pas mappé ou contient des données manquantes, Google n’assure pas la correspondance de l’adresse. |
| Colonne Expiration du compte pour les connexions [Facebook](../../destinations/catalog/social/facebook.md) | Les dates d’expiration des jetons de compte Facebook apparaissent désormais dans les onglets [Parcourir](../../destinations/ui/destinations-workspace.md#browse) et [Comptes](../../destinations/ui/destinations-workspace.md#accounts). |
| Exporter les jeux de données créés par l’API | Vous pouvez désormais exporter des jeux de données créés par API. La limitation précédente, en vertu de laquelle seuls les jeux de données créés dans l’UI étaient disponibles pour l’export, a été levée. En savoir plus sur l’[export de jeux de données](../../destinations/ui/export-datasets.md). |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../../destinations/home.md).

## Service d’identités {#identity}

Utilisez le service d’identités d’Adobe Experience Platform pour créer une vue complète de votre clientèle et de ses comportements en reliant les identités entre les appareils et les systèmes, vous permettant ainsi de proposer des expériences numériques personnelles et percutantes en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!DNL Identity Graph Linking Rules] | [!DNL Identity Graph Linking Rules] est désormais disponible pour tous. [!DNL Identity Graph Linking Rules] éviter la « réduction du graphique », en garantissant des profils clients distincts et précis pour un marketing personnalisé dans Experience Platform et les applications. Les principales fonctionnalités sont les suivantes :<ul><li>[Outil de simulation graphique](../../identity-service/identity-graph-linking-rules/graph-simulation.md) : explorez l’algorithme et testez les configurations du paramètre d’identité.</li><li> [Paramètres d’identité](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md) : configurez des espaces de noms uniques et définissez des priorités.</li><li>[Tableau de bord des identités](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) : surveiller les graphiques et valider les paramètres d’identité.</li></ul> **Remarque** : vos données ne seront pas modifiées tant que vous n’aurez pas configuré manuellement vos paramètres d’identité. |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble du Service d’identités](../../identity-service/home.md).

## Service de requête {#query-service}

Interrogez des données dans le lac de données Adobe Experience Platform à l’aide de SQL standard avec le service de requête. Combinez en toute transparence des jeux de données et générez-en de nouveaux à partir des résultats de vos requêtes pour alimenter les rapports, activer les workflows de science des données ou faciliter l’ingestion dans le profil client en temps réel. Vous pouvez, par exemple, fusionner les données de transaction client avec les données comportementales afin d’identifier les audiences à forte valeur ajoutée pour les campagnes marketing ciblées.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
|--------|-------------|
| Migration des informations d’identification JWT vers OAuth | Afin d’éviter les interruptions de service, les informations d’identification JWT sans date d’expiration doivent être migrées vers OAuth de serveur à serveur d’ici le 30 juin 2025. Cette modification améliore la sécurité et la cohérence de la plateforme. Pour plus d’informations, consultez le [guide Migrer des informations d’identification de JWT vers OAuth de serveur à serveur](../../query-service/ui/migrate-jwt-to-oauth.md). |
| Tableau de résultats hérité (disponibilité limitée) | Les utilisateurs et utilisatrices qui dépendent des workflows glisser-sélectionner peuvent demander l’accès à un tableau de résultats hérité qui prend en charge le comportement natif du navigateur pour la sélection et la copie. La sortie collée est délimitée par des tabulations, de sorte que les colonnes restent alignées et lisibles dans Excel, ce qui facilite la révision des feuilles de calcul et les processus d’assurance qualité. Voir le [guide de l’UI du requêteur](../../query-service/ui/user-guide.md#legacy-results-table) pour plus d’informations. |

Pour plus d’informations sur Query Service [!DNL Query Service], consultez la [[!DNL Query Service] présentation](../../query-service/home.md) de Query Service.

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des sandbox qui divisent une instance d’Experience Platform unique en plusieurs environnements virtuels pour favoriser le développement et l’évolution d’applications d’expérience digitale.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Extension de prise en charge du plug-in d’outils relatifs au sandbox | Les campagnes peuvent désormais être migrées avec d’autres objets dépendants par le biais des outils de sandbox, notamment la configuration des canaux, la décision unifiée, les paramètres/variantes d’expérience, etc. Pour obtenir la liste complète des objets de campagne pris en charge, ainsi que tous les objets Adobe Journey Optimizer pris en charge, voir le guide [des outils de sandbox](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects). |

{style="table-layout:auto"}

Pour plus d’informations sur les sandbox, consultez la [vue d’ensemble des sandbox](../../sandboxes/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clientes et clients avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mise à jour des critères de segmentation en streaming | À compter de la version de mai 2025, les critères permettant aux audiences d’être éligibles pour la segmentation en streaming ont été mis à jour. Vous trouverez plus d’informations sur ces modifications dans la [mise à jour des critères d’éligibilité à la segmentation en streaming](../../segmentation/eligibility-criteria-update.md). |

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prendre en charge l’authentification de base pour [!DNL MySQL] | Vous pouvez désormais utiliser l’authentification de base pour connecter votre base de données [!DNL MySQL] à Experience Platform. Pour plus d’informations, consultez la [[!DNL MySQL] vue d’ensemble des sources](../../sources/connectors/databases/mysql.md). |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../../sources/home.md).