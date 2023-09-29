---
title: Notes de mise à jour d’Adobe Experience Platform
description: Les notes de mise à jour de septembre 2023 pour Adobe Experience Platform.
source-git-commit: c2563d43b9ee8b3191954275bd0102507a981071
workflow-type: tm+mt
source-wordcount: '2149'
ht-degree: 31%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 28 septembre 2023**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Attributs calculés](#computed-attributes)

Mises à jour des fonctionnalités existantes dans  Experience Platform :

- [Alertes](#alerts)
- [Tableaux de bord](#dashboards)
- [Collecte de données](#data-collection)
- [Gouvernance des données](#data-governance)
- [Hygiène des données](#hygiene)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Service d’identités](#identity-service)
- [Query Service](#query-service)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Attributs calculés {#computed-attributes}

Les attributs calculés permettent de synthétiser facilement les données d’événement dans les attributs de profil via une interface utilisateur intuitive pour une segmentation, une personnalisation et une activation optimisées basées sur le comportement. Grâce à cette fonctionnalité, vous pouvez créer des attributs calculés en libre-service, les gérer et les utiliser dans la segmentation, les destinations Real-Time CDP ou Adobe Journey Optimizer. En outre, les attributs calculés simplifient la segmentation et les workflows de parcours pour vous aider à fournir facilement des expériences pertinentes. Pour en savoir plus sur les attributs calculés, veuillez lire le [présentation des attributs calculés](../../profile/computed-attributes/overview.md).

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités de Platform. Vous pouvez vous abonner à différentes règles d’alerte à l’aide de l’onglet [!UICONTROL Alertes] dans l’interface utilisateur de Platform. Vous pouvez aussi choisir de recevoir les messages d’alerte dans l’interface utilisateur elle-même ou par le biais de notifications par e-mail.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Onglet Historique des alertes | Alertes [!UICONTROL Histoire] comprend désormais tous les événements, notamment les retards, les démarrages, les succès et les échecs. Lisez la section [Documentation de l’interface utilisateur des alertes](../../observability/alerts/ui.md) pour plus d’informations sur l’onglet history . |

{style="table-layout:auto"}

Pour en savoir plus sur les alertes, veuillez lire le [[!DNL Observability Insights] aperçu](../../observability/home.md).

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit de nombreux [!DNL dashboards] grâce auxquels vous pouvez afficher des informations importantes sur les données de votre entreprise, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

| Fonctionnalité | Description |
| --- | --- |
| [Amélioration du tableau de bord d’utilisation des licences](../../dashboards/guides/license-usage.md) | Contrôlez vos contrats de licence grâce à de meilleurs rapports et à des visualisations des mesures clés concernant l’utilisation des licences de votre entreprise. Ces améliorations offrent un niveau élevé de granularité par rapport à vos mesures d’utilisation des licences pour tous les produits Experience Platform que vous avez achetés. |

{style="table-layout:auto"}

Pour en savoir plus sur le tableau de bord de l’utilisation des licences, voir [tableau de bord d’utilisation des licences - Aperçu](../../dashboards/guides/destinations.md).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Type | Fonctionnalité | Description |
| --- | --- | --- |
| Trains de données | Prise en charge de la recherche de périphérique | Lors de la configuration d’un flux de données, vous pouvez désormais sélectionner le niveau des informations de recherche d’appareil à collecter. Les informations de recherche de périphérique incluent des données sur le périphérique, le matériel, le système d’exploitation et le navigateur utilisés pour interagir avec votre page. <br>  Les informations de recherche de périphérique ne peuvent pas être collectées avec l’agent utilisateur et les conseils client. Si vous choisissez de collecter des informations sur l’appareil, la collecte de l’agent utilisateur et des conseils client sera désactivée, et vice versa. Toutes les informations de recherche de périphérique sont stockées dans la variable `xdm:device` groupe de champs. Pour en savoir plus, consultez la documentation sur [configuration des flux de données](../../datastreams/configure.md#geolocation-device-lookup). |
| Extensions | [!DNL TikTok] extension de l’API des événements web | La variable [[!DNL TikTok] API des événements web](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) l’extension vous permet d’exploiter les données capturées dans Adobe Experience Platform Edge Network et de les envoyer à [!DNL TikTok] sous la forme d’événements côté serveur à l’aide de la variable [!DNL TikTok] API des événements web. |

{style="table-layout:auto"}

Pour en savoir plus sur la collecte de données, veuillez lire la section [présentation de la collecte de données](../../tags/home.md).

## Gouvernance des données {#data-governance}

Dans Adobe Experience Platform, la gouvernance des données désigne un ensemble de politiques et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle clé dans Experience Platform à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’accès aux données et le contrôle de l’accès aux données pour les actions marketing.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles étiquettes écosystème de partenaire pour les données tierces | De nouveaux libellés d’utilisation des données pour l’enrichissement et la prospection tiers sont disponibles. Voir [documentation sur les étiquettes Ecosystem des partenaires](../../data-governance/labels/reference.md#partner) pour plus d’informations. |

{style="table-layout:auto"}

Pour en savoir plus sur la gouvernance des données, veuillez consulter la [vue d’ensemble de la gouvernance des données](../../data-governance/home.md).

## Hygiène des données {#hygiene}

Experience Platform offre toute une gamme de fonctionnalités d’hygiène des données. Celles-ci vous permettent de gérer vos données stockées par le biais de suppressions programmées d’enregistrements de consommateurs et de jeux de données. À l’aide de la fonction [!UICONTROL Cycle de vie des données] dans l’interface utilisateur ou par le biais d’appels à l’API Data Hygiene, vous pouvez gérer efficacement vos entrepôts de données. Utilisez ces fonctionnalités pour vous assurer que les informations sont utilisées comme prévu, qu’elles sont mises à jour lorsque des données incorrectes doivent être corrigées et qu’elles sont supprimées lorsque les stratégies organisationnelles le jugent nécessaire.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Version Beta]{type=Informative} | Gérez votre cycle de vie des données dans tous les entrepôts de données afin de respecter les engagements des clients et les contrats de licence avec les fonctionnalités avancées de gestion du cycle de vie des données de Adobe Experience Platform : expiration automatisée du jeu de données et suppression des enregistrements.<br>Avec l’expiration automatisée des jeux de données, vous pouvez supprimer des jeux de données entiers et définir une date et une heure pour le jeu de données à supprimer.<br>La suppression d’enregistrements vous permet de supprimer des profils clients individuels en ciblant leurs identités principales. Vous pouvez fournir les identités principales individuellement par le biais de l’interface utilisateur ou via le téléchargement de fichier CSV/JSON. Voir [Documentation sur la suppression des enregistrements](../../hygiene/ui/record-delete.md) pour plus d’informations |
| Expirations de jeux de données | Limitez vos données et gardez le contrôle de vos contrats de licence avec l’expiration automatisée du jeu de données. Réduire les volumes de données en supprimant des jeux de données entiers et en définissant une date et une heure pour le jeu de données à supprimer. Voir [documentation sur l’expiration des jeux de données](../../hygiene/ui/dataset-expiration.md) pour plus d’informations. |

{style="table-layout:auto"}

Pour plus d’informations sur les fonctionnalités d’hygiène des données de Platform, consultez la section [présentation de l’hygiène des données](../../hygiene/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#new-updated-destinations}

| Destination | Nouveau ou mis à jour | Description |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | Nouveau  | Activation des audiences précédemment intégrées à [!DNL LiveRamp] aux éditeurs Premium sur les médias mobiles, web, display et télévisés. <br> Après l’intégration d’audiences à vos [!DNL LiveRamp] compte par le biais de [LiveRamp - Intégration](../../destinations/catalog/advertising/liveramp-onboarding.md) connexion, utilisez la nouvelle [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) connexion pour activer les audiences vers les destinations en aval. |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | Nouveau | [[!DNL HubSpot]](https://www.hubspot.com) est une plateforme CRM avec tous les logiciels, intégrations et ressources dont vous avez besoin pour connecter le marketing, les ventes, la gestion de contenu et le service client. Il vous permet de connecter vos données, vos équipes et vos clients sur une seule plateforme CRM. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Mis à jour | Ajout de la prise en charge de [!DNL Dynamics 365] préfixes de champ personnalisés pour les champs personnalisés qui n’ont pas été créés dans la solution par défaut dans [!DNL Dynamics 365]. un nouveau champ de saisie, **[!UICONTROL Préfixe de personnalisation]**, a été ajouté dans la variable [Renseignement des détails de destination](#destination-details) étape . |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Mis à jour | La destination Audiences Experience Cloud est désormais disponible en général. Utilisez cette destination pour activer les audiences de Real-Time CDP vers Audience Manager et Adobe Analytics. Vous avez besoin d’une licence d’Audience Manager pour envoyer des audiences à Adobe Analytics. |

{style="table-layout:auto"}

<!-- 


Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 

-->

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| Exports de données dans Real-Time CDP | La variable [export du jeu de données](../../destinations/ui/export-datasets.md) La fonctionnalité est désormais disponible en général. Voir [les jeux de données que vous pouvez exporter en fonction de l’application Experience Platform ;](../../destinations/ui/export-datasets.md#datasets-to-export) que vous avez acheté, puis vérifiez la variable [barrières de sécurité pour l’exportation de jeux de données](/help/destinations/guardrails.md#dataset-exports). |
| (Version bêta) Prise en charge de l’exportation d’objets de type tableau | Exportez des tableaux de valeurs primitives (valeurs string, int ou boolean) en tant que fichiers de schéma plats vers des destinations de stockage dans le cloud. En savoir plus sur les fonctionnalités de la section [documentation](../../destinations/ui/export-arrays-calculated-fields.md). |
| Sélecteurs de liste déroulante dynamiques dans Destination SDK | Lors de la création d’une destination via Destination SDK, vous pouvez désormais utiliser [sélecteurs de liste déroulante dynamiques](../../destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) pour remplir les champs d’un sélecteur de liste déroulante avec des valeurs récupérées à partir d’une API. |

**Correctifs et améliorations** {#destinations-fixes-and-enhancements}

- Utilisez [surveillance de la transparence](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) désormais disponibles pour les destinations d’entreprise ([API HTTP](../../destinations/catalog/streaming/http-destination.md), [Amazon Kinesis](../../destinations/catalog/cloud-storage/amazon-kinesis.md) et [Centre d’événements Azure](../../destinations/catalog/cloud-storage/azure-event-hubs.md)) au niveau de l’exécution du flux de données pour surveiller les mesures d’activation et l’état dans la variable [vue détaillée du flux de données](../../dataflows/ui/monitor-destinations.md#dataflow-run-details-page), avec des informations supplémentaires via les codes d’erreur et les messages de dépannage.
- Lorsque vous mettez à jour le nom des audiences mappées à la variable [Google Ad Manager](../../destinations/catalog/advertising/google-ad-manager.md), [Google Display &amp; Video 360](../../destinations/catalog/advertising/google-dv360.md), ainsi que d’autres destinations qui utilisent [modèles de mise à jour d’audience](../../destinations/destination-sdk/metadata-api/update-audience-template.md), ces modifications de nom sont désormais répercutées en aval dans la destination.

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Actions rapides ajoutées à l’éditeur de schémas | De nouvelles actions rapides ont été ajoutées au canevas de l’éditeur de schémas. Vous pouvez désormais copier la structure JSON ou supprimer le schéma directement à partir de l’éditeur.<br>![Actions rapides dans l’éditeur de schémas.](../2023/assets/schema-editor-copy-json.png "L’éditeur de schémas avec plus et Copier dans JSON est mis en surbrillance."){width="100" zoomable="yes"} |
| Filtrage des ressources XDM par créateur personnalisé ou standard | Les listes des schémas, des groupes de champs, des types de données et des classes disponibles sont désormais préfiltrées en fonction de leur méthode de création. Vous pouvez ainsi filtrer les ressources selon qu’elles ont été créées ou créées par Adobe.<br>![Filtres standard et personnalisés dans l’espace de travail des schémas.](../2023/assets/standard-and-custom-classes.png "Espace de travail des schémas avec les filtres standard et personnalisés mis en surbrillance."){width="100" zoomable="yes"} <br> Voir [documentation sur la création et la modification de ressources](../../xdm/ui/resources/classes.md#filter.md) pour plus d’informations. |

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Workflow de création de schéma mis à jour | Un nouveau workflow de création de schéma a été mis en oeuvre pour rationaliser le processus. <br> ![Nouvelle interface utilisateur de création de schéma.](../2023/assets/schema-class-options.png "Nouveau sélecteur de détails de schéma mis en surbrillance."){width="100" zoomable="yes"} <br> Voir [documentation sur la création de schémas](../../xdm/ui/resources/schemas.md#create) pour plus d’informations. |

## Identity Service {#identity-service}

Adobe Experience Platform Identity Service vous offre la possibilité de mieux connaître vos clients et clientes ainsi que leur comportement en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Améliorations de l’interface utilisateur d’Identity Service | Utilisez l’outil amélioré de création d’espaces de noms personnalisés dans l’interface utilisateur de l’Experience Platform pour mieux gérer vos espaces de noms personnalisés et leurs types d’identité correspondants. L’interface utilisateur améliorée d’Identity Service vous permet d’effectuer les opérations suivantes : <ul><li>Expérience contextuelle : indices visuels, clarté et contexte relatifs à l’espace de noms d’identité et aux types d’identité.</li><li>Précision : meilleure gestion des erreurs, sans plus de noms d’identité en double.</li><li>Discover : accès à la documentation depuis une boîte de dialogue intégrée au produit.</li></ul> Pour plus d’informations, consultez le guide sur [création d’espaces de noms personnalisés](../../identity-service/namespaces.md#create-namespaces). |
| Modifications des limites des graphiques d’identités | La limite du graphique d’identités est passée de 150 identités à 50 identités. Lorsqu’une nouvelle identité est ingérée dans un graphique complet, l’identité la plus ancienne basée sur l’horodatage d’ingestion et le type d’identité est supprimée. Les types d’identité de cookie sont prioritaires pour la suppression. Contactez votre équipe de compte d’Adobe pour demander un changement de type d’identité si votre environnement de test de production contient : <ul><li>un espace de noms personnalisé dans lequel les identifiants de personne (tels que les identifiants CRM) sont configurés en tant que type d’identité de cookie/appareil.</li><li>espace de noms personnalisé dans lequel les identifiants de cookie/d’appareil sont configurés en tant que type d’identité multi-appareils.</li></ul> L’ingénierie d’Adobe traitera manuellement ces demandes. Pour plus d’informations, consultez la section [Barrières de sécurité pour les données Identity Service](../../identity-service/guardrails.md). |

{style="table-layout:auto"}

Pour en savoir plus sur Identity Service, veuillez lire le [Présentation d’Identity Service](../../identity-service/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou pour l’ingestion dans le profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mises à jour de l’interface utilisateur de filtrage de journal | Le filtrage amélioré du journal des requêtes améliore la visibilité des journaux générés par l’utilisateur pour la surveillance, l’administration et la résolution des problèmes. Vous pouvez filtrer la liste des logs de requête en fonction de différents paramètres. <br> ![Paramètres du filtre du journal des requêtes.](../2023/assets/log-filter-settings.png "Les nouveaux filtres de logs de requête sont mis en surbrillance."){width="100" zoomable="yes"}  <br> Voir [documentation sur les journaux de requête](../../query-service/ui/query-logs.md#filter-logs) pour plus d’informations. |
| Mises à jour de l’interface utilisateur de l’éditeur de requêtes multiples | Vous pouvez désormais exécuter plusieurs requêtes séquentielles dans l’éditeur de requêtes ou écrire plusieurs requêtes et exécuter toutes les requêtes de manière séquentielle. Pour plus de flexibilité dans l&#39;exécution de votre requête, vous pouvez mettre en surbrillance la requête de votre choix et sélectionner cette requête spécifique à exécuter indépendamment des autres. Voir [Guide de l’interface utilisateur de Query Editor](../../query-service/ui/user-guide.md#execute-multiple-sequential-queries) pour plus d’informations. |

{style="table-layout:auto"}

Pour plus d’informations sur Query Service, consultez la section [présentation de Query Service](../../query-service/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] permet de segmenter en audiences les données stockées dans [!DNL Experience Platform] qui se rapportent aux personnes (tels que les clientes et clients, les prospects, les utilisateurs et utilisatrices ou les organisations). Vous pouvez créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur [!DNL Platform] et sont facilement accessibles à partir de n’importe quelle solution Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Colonnes personnalisables | Vous pouvez désormais personnaliser la mise en page d’Audience Portal avec des colonnes redimensionnables. Pour plus d’informations sur cette fonctionnalité, veuillez lire la section [guide de l’interface utilisateur de segmentation](../../segmentation/ui/overview.md#customize). |
| Ventilation des fréquences de mise à jour | Vous pouvez désormais afficher la ventilation des fréquences de mise à jour des audiences de votre entreprise. Pour plus d’informations sur cette fonctionnalité, veuillez lire la section [guide de l’interface utilisateur de segmentation](../../segmentation/ui/overview.md#browse). |

Pour en savoir plus sur les sources, veuillez lire le [présentation des sources](../../sources/home.md).

Pour en savoir plus sur Segmentation Service, consultez la [présentation de Segmentation Service](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouveaux paramètres pour `offset` pagination dans les sources en libre-service (SDK par lots) | Vous pouvez désormais définir une `endConditionName` et `endConditionValue` pour votre source lors de l’utilisation `offset` pagination. Ces paramètres vous permettent d’indiquer la condition qui mettra fin à la boucle de pagination dans la requête HTTP suivante. Pour plus d’informations, consultez la section [Guide de pagination pour les sources en libre-service (SDK par lots)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, veuillez lire le [présentation des sources](../../sources/home.md).
