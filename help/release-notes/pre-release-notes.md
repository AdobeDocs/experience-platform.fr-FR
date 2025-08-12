---
title: Notes de mise à jour préliminaires d’Experience Platform
description: Aperçu des dernières notes de mise à jour de Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: a26ad18b1e44b3198db9e8a36ad3749ed8a0afa2
workflow-type: tm+mt
source-wordcount: '1116'
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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/e-release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : août 2025**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Segmentation Service](#segmentation-service)
- [Sources](#sources)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités Experience Platform. Vous pouvez vous abonner à différentes règles d’alerte par le biais de l’onglet [!UICONTROL Alertes] de l’interface utilisateur d’Experience Platform et choisir de recevoir des messages d’alerte dans l’interface utilisateur elle-même ou par le biais de notifications par e-mail.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Alertes de capacité de débit en flux continu | Trois nouvelles alertes permettent aux utilisateurs de s’abonner et de configurer des alertes pour gérer et surveiller de manière proactive les performances de la capacité de débit de diffusion en continu. Les nouvelles alertes s’affichent lorsque le débit de diffusion en continu a atteint 80 % ou 90 % ou dépasse les limites de capacité. Pour plus d’informations, consultez le guide [règles d’alerte de capacité](../observability/alerts/rules.md#capacity). |

Pour plus d’informations sur les alertes, consultez la [[!DNL Observability Insights] vue d’ensemble](../observability/home.md).

## Destinations {#destinations}

[!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations**

| Destination | Description |
| --- | --- |
| [!DNL Acxiom Real ID Audience] destination | Utilisez la destination [!DNL Acxiom Real ID Audience Connection] pour améliorer les audiences avec [!DNL Acxiom's] technologie [Real ID™](https://www.acxiom.com/real-id/real-id/) et activer les audiences vers plusieurs plateformes, telles que [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], etc. |


**Destinations mises à jour**

| Destination | Description |
| --- | --- |
| Détails d’expiration de l’authentification pour les destinations [!DNL LinkedIn] | Ne vous inquiétez plus des informations d’identification expirées. Les informations sur l’expiration du compte sont désormais visibles directement dans l’interface d’Experience Platform. Vous pouvez ainsi savoir quand votre authentification [!DNL LinkedIn] expirera et la renouveler avant qu’elle ne cause des perturbations dans vos flux de données. |
| Prise en charge du chiffrement pour les destinations [!DNL Data Landing Zone] | Protégez les données exportées avec le chiffrement. Vous pouvez désormais joindre des clés publiques au format RSA pour chiffrer vos fichiers exportés, ce qui vous offre le même niveau de sécurité que les autres destinations de stockage dans le cloud pour vos informations sensibles. |
| Mise à niveau interne de [[!DNL Microsoft Bing]](../destinations/catalog/advertising/bing.md) | À compter du mardi 11 août 2025, vous pourrez voir deux cartes **[!DNL Microsoft Bing]** côte à côte dans le catalogue des destinations. Cela est dû à une mise à niveau interne du service de destinations. Le connecteur de destination **[!DNL Microsoft Bing]** existant a été renommé **[!UICONTROL (obsolète) Microsoft Bing]** et une nouvelle carte portant le nom **[!UICONTROL Microsoft Bing]** est désormais disponible. Utilisez la nouvelle connexion **[!UICONTROL Microsoft Bing]** dans le catalogue pour les nouveaux flux de données d’activation. Si vous avez des flux de données actifs vers la destination **[!UICONTROL (obsolète) Microsoft Bing]**, ils seront mis à jour automatiquement. Aucune action n’est donc requise de votre part. <br><br>Si vous créez des flux de données par le biais de l’[API Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/), vous devez mettre à jour vos [!DNL flow spec ID] et [!DNL connection spec ID] avec les valeurs suivantes :<ul><li>ID de spécification de flux : `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>ID de spécification de connexion : `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Suite à cette mise à niveau, il se peut que le nombre de profils activés **baisse** soit réduit dans vos flux de données à [!DNL Microsoft Bing]. Cette baisse est due à l’introduction de l’exigence de mappage **ECID** pour toutes les activations sur cette plateforme de destination. |
| Identifiants supplémentaires pour les destinations [!DNL Amazon Ads] | La destination Amazon Ads prend désormais en charge les nouvelles identités (`firstName`, `lastName`, `street`, `city`, `state`, `zip`, `country`). Ces champs sont destinés à améliorer les taux de correspondance d’audience. Ils sont transmis en texte brut, avec un hachage de SHA256 facultatif. |
| Consolidation des cartes de destination [!DNL Marketo] | Simplifiez votre configuration de destination [!DNL Marketo] avec notre carte de destination unifiée. Nous avons regroupé [!DNL Marketo] cartes V2 et V3 en une seule option simplifiée, ce qui facilite le choix de la bonne destination et la prise en main rapide. |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Étendre les plannings d’exportation de jeux de données pour les flux de données créés avant novembre 2024 | Si votre organisation a créé des flux de données d’exportation de jeux de données avant novembre 2024, ces flux de données cesseront de fonctionner le 1er septembre 2025. Si vous avez besoin des flux de données pour continuer à exporter des données après le 1er septembre 2025, vous devez étendre leurs plannings pour chaque destination vers laquelle vous exportez des jeux de données, en suivant les étapes de [ce guide](../destinations/ui/dataset-expiration-update.md). |
| Amélioration des fonctionnalités de recherche, de filtrage et de balisage pour les destinations | Améliorez votre workflow de gestion des destinations avec des fonctionnalités améliorées de recherche, de filtrage et de balisage dans les onglets Parcourir et Comptes . Vous pouvez désormais rechercher des flux de données et des comptes spécifiques par nom, filtrer selon divers critères, notamment la plateforme de destination, le statut et les dates, et créer des balises personnalisées pour organiser vos destinations. Le tri des colonnes est également disponible pour les champs clés tels que l’heure d’exécution du dernier flux de données, ce qui facilite l’identification et la gestion de vos connexions de destination. |

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification open source qui fournit des structures et des définitions communes (schémas) pour les données importées dans Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Schémas basés sur des modèles | Simplifiez la modélisation de vos données à l’aide de schémas basés sur des modèles. Vous pouvez désormais créer plus facilement des schémas à l’aide d’exemples et de conseils pratiques complets. Cette fonctionnalité est actuellement disponible pour les titulaires de licence Campaign Orchestration. Elle sera étendue aux clients de Data Distiller lors de la phase de disponibilité générale, ce qui rendra la modélisation des données plus accessible et plus efficace. |

Pour plus d’informations, consultez la [présentation de XDM](../xdm/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Estimations d’audience | Les estimations d’audience sont désormais générées automatiquement dans le créateur de segments. Cette valeur sera mise à jour chaque fois que vous modifiez l’audience et reflète toujours les dernières règles d’audience. |

Pour plus d’informations, consultez la [[!DNL Segmentation Service] présentation](../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} Prise en charge d’Azure Private Link dans l’interface utilisateur | Gardez vos données en sécurité grâce aux connexions réseau privées. Vous pouvez désormais créer des points d’entrée privés et configurer des flux de données qui contournent l’Internet public, ce qui vous offre une sécurité renforcée et une isolation réseau pour vos données sensibles. |
| Mises à jour de la documentation d’[!DNL Marketo] source | Obtenez une visibilité complète sur la manière dont vos données [!DNL Marketo] sont transformées lorsqu’elles entrent dans Experience Platform. Tous les mappages de champs incluent désormais des explications détaillées sur les transformations de données, afin que vous puissiez comprendre exactement comment votre `PersonID` devient `leadID` et `eventType` devient `activityType`. |
| Prise en charge de l’authentification principale du service pour [!DNL Azure Blob Storage] | Vous pouvez désormais connecter votre compte [!DNL Azure Blob Storage] à Experience Platform à l’aide de l’authentification principale du service. |

Pour plus d’informations, consultez la [vue d’ensemble des sources](../sources/home.md).

<!--

## Query Service {#query-service}

Adobe Experience Platform Query Service provides a robust SQL interface for data analysis and exploration across the platform.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Data Distiller Session Management | Take control of your data analysis sessions with enhanced session management. You can now monitor and manage your sessions more effectively across development and production environments, giving you better visibility into your query performance and resource usage. |

For more information, read the [Query Service overview](../query-service/home.md).

## B2B CDP {#b2b-cdp}

Real-Time CDP B2B Edition provides comprehensive B2B customer data management capabilities, enabling organizations to build unified customer profiles, create sophisticated B2B audiences, and activate data across various marketing channels.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Lookup Support for B2B Classes Only | Streamline your B2B data access with focused lookup support. You can now look up Person (Profile), Experience Events, Account, and Opportunity entities directly through the Entities API. This simplified approach helps you access the most important B2B data more efficiently while reducing complexity. |
| B2B Namespace and Schema Updates | Experience a cleaner, more streamlined B2B data model. We've simplified the B2B namespace and schema structure by removing complex relationship mappings and non-primary identity support for certain B2B classes. This makes your B2B data easier to work with and understand. |

For more information, read the [Real-Time CDP B2B Edition overview](../rtcdp/b2b-overview.md).

-->
