---
title: Notes de mise à jour d’Adobe Experience Platform
description: Les notes de mise à jour de septembre 2023 pour Adobe Experience Platform.
source-git-commit: 05136ca1a44fa0ecbf2fd9941d047c3a0899f2d1
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 31%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 28 septembre 2023**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Attributs calculés](#computed-attributes)

Mises à jour des fonctionnalités existantes dans  Experience Platform :

- [Alertes](#alerts)
- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Identity Service](#identity-service)
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

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Type | Fonctionnalité | Description |
| --- | --- | --- |
| Trains de données | Prise en charge de la recherche de périphérique | Lors de la configuration d’un flux de données, vous pouvez désormais sélectionner le niveau des informations de recherche d’appareil à collecter. Les informations de recherche de périphérique incluent des données sur le périphérique, le matériel, le système d’exploitation et le navigateur utilisés pour interagir avec votre page. <br>  Les informations de recherche de périphérique ne peuvent pas être collectées avec l’agent utilisateur et les conseils client. Si vous choisissez de collecter des informations sur l’appareil, la collecte de l’agent utilisateur et des conseils client sera désactivée, et vice versa. Toutes les informations de recherche de périphérique sont stockées dans la variable `xdm:device` groupe de champs. Pour en savoir plus, consultez la documentation sur [configuration des flux de données](../../datastreams/configure.md#geolocation-device-lookup). |
| Extensions | [!DNL TikTok] extension de l’API des événements web | La variable [[!DNL TikTok] API des événements web](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) l’extension vous permet d’exploiter les données capturées dans Adobe Experience Platform Edge Network et de les envoyer à [!DNL TikTok] sous la forme d’événements côté serveur à l’aide de la variable [!DNL TikTok] API des événements web. |

{style="table-layout:auto"}

Pour en savoir plus sur la collecte de données, veuillez lire la section [présentation de la collecte de données](../../tags/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#new-updated-destinations}

| Destination | Nouveau ou mis à jour | Description |
| ----------- |----------------|----------- |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | Nouveau  | [[!DNL HubSpot]](https://www.hubspot.com) est une plateforme CRM avec tous les logiciels, intégrations et ressources dont vous avez besoin pour connecter le marketing, les ventes, la gestion de contenu et le service client. Il vous permet de connecter vos données, vos équipes et vos clients sur une seule plateforme CRM. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Mis à jour | Ajout de la prise en charge de [!DNL Dynamics 365] préfixes de champ personnalisés pour les champs personnalisés qui n’ont pas été créés dans la solution par défaut dans [!DNL Dynamics 365]. un nouveau champ de saisie, **[!UICONTROL Préfixe de personnalisation]**, a été ajouté dans la variable [Renseignement des détails de destination](#destination-details) étape . |

{style="table-layout:auto"}

<!-- 


Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | New | Activate audiences previously onboarded to [!DNL LiveRamp] to premium publishers across mobile, web, display, and connected TV mediums. <br> After onboarding audiences to your [!DNL LiveRamp] account through the [LiveRamp - Onboarding](liveramp-onboarding.md) connection, use the new [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) connection to activate the audiences to downstream destinations.  |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Updated | The Experience Cloud Audiences destination is now generally available. Use this destination to activate audiences from Real-Time CDP to Audience Manager and Adobe Analytics. You need an Audience Manager license to send audiences to Adobe Analytics. |

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

## Identity Service {#identity-service}

Adobe Experience Platform Identity Service vous offre la possibilité de mieux connaître vos clients et clientes ainsi que leur comportement en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Améliorations de l’interface utilisateur d’Identity Service | Utilisez l’outil amélioré de création d’espaces de noms personnalisés dans l’interface utilisateur de l’Experience Platform pour mieux gérer vos espaces de noms personnalisés et leurs types d’identité correspondants. L’interface utilisateur améliorée d’Identity Service vous permet d’effectuer les opérations suivantes : <ul><li>Expérience contextuelle : indices visuels, clarté et contexte relatifs à l’espace de noms d’identité et aux types d’identité.</li><li>Précision : meilleure gestion des erreurs, sans plus de noms d’identité en double.</li><li>Discover : accès à la documentation depuis une boîte de dialogue intégrée au produit.</li></ul> Pour plus d’informations, consultez le guide sur [création d’espaces de noms personnalisés](../../identity-service/namespaces.md#create-namespaces). |
| Modifications des limites des graphiques d’identités | La limite du graphique d’identités est passée de 150 identités à 50 identités. Lorsqu’une nouvelle identité est ingérée dans un graphique complet, l’identité la plus ancienne basée sur l’horodatage d’ingestion et le type d’identité est supprimée. Les types d’identité de cookie sont prioritaires pour la suppression. Contactez votre équipe de compte d’Adobe pour demander un changement de type d’identité si votre environnement de test de production contient : <ul><li>un espace de noms personnalisé dans lequel les identifiants de personne (tels que les identifiants CRM) sont configurés en tant que type d’identité de cookie/appareil.</li><li>espace de noms personnalisé dans lequel les identifiants de cookie/d’appareil sont configurés en tant que type d’identité multi-appareils.</li></ul> L’ingénierie d’Adobe traitera manuellement ces demandes. Pour plus d’informations, consultez la section [Barrières de sécurité pour les données Identity Service](../../identity-service/guardrails.md). |

{style="table-layout:auto"}

Pour en savoir plus sur Identity Service, veuillez lire le [Présentation d’Identity Service](../../identity-service/home.md).

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