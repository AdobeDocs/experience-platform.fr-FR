---
title: Notes de mise à jour d’Adobe Experience Platform - Août 2025
description: Les notes de mise à jour d’août 2025 pour Adobe Experience Platform.
exl-id: d93e98f3-d165-4710-ad1d-2ad3857cd0f8
source-git-commit: 6672ed3fd4ee4f48952dcf5ffb6561de026fe55b
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 35%

---

# Notes de mise à jour d’Adobe Experience Platform

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/e-release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : mercredi 19 août 2025**


Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [Catalog Service](#catalog-service)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Profil client en temps réel](#profile)
- [Sandbox](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [Sources](#sources)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités Experience Platform. Vous pouvez vous abonner à différentes règles d’alerte par le biais de l’onglet [!UICONTROL Alertes] de l’interface utilisateur d’Experience Platform et choisir de recevoir des messages d’alerte dans l’interface utilisateur elle-même ou par le biais de notifications par e-mail.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Alertes de capacité de débit en flux continu | Trois nouvelles alertes permettent aux utilisateurs de s’abonner et de configurer des alertes pour gérer et surveiller de manière proactive les performances de la capacité de débit de diffusion en continu. Les nouvelles alertes s’affichent lorsque le débit de diffusion en continu a atteint 80 % ou 90 % ou dépasse les limites de capacité. Pour plus d’informations, consultez le guide [règles d’alerte de capacité](../../observability/alerts/rules.md#capacity). |

Pour plus d’informations sur les alertes, consultez la [[!DNL Observability Insights] vue d’ensemble](../../observability/home.md).

## Catalog Service {#catalog-service}

Catalog Service est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, Catalog conserve les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Conservation des données pour le profil client en temps réel | Vous pouvez **uniquement** mettre à jour la période de conservation des données pour le profil client en temps réel une fois tous les 30 jours. |

Pour plus d’informations sur le service de catalogue, consultez la [présentation du service de catalogue](../../catalog/home.md).

## Destinations {#destinations}

[!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

>[!IMPORTANT]
>
>**Extension du planning d’exportation du jeu de données**
>
>Si votre organisation a créé des flux de données d’exportation de jeux de données avant novembre 2024, ces flux de données cesseront de fonctionner le **1er septembre 2025**. Si vous avez besoin des flux de données pour continuer à exporter des données après le 1er septembre 2025, vous devez étendre leurs plannings pour chaque destination vers laquelle vous exportez des jeux de données, en suivant les étapes de [ce guide](../../destinations/ui/dataset-expiration-update.md).

>[!IMPORTANT]
>
>**Mise à jour de la liste autorisée IP requise pour les destinations basées sur l’API**
>
>En raison des mises à niveau du moteur d’exportation des destinations de diffusion en continu, les organisations qui utilisent des [places sur la liste autorisée IP](../../destinations/catalog/streaming/ip-address-allow-list.md) pour les destinations basées sur les API doivent ajouter les adresses IP suivantes à leurs places sur la liste autorisée **avant le 15 septembre 2025** :
>
>**Adresses IP requises :**
>
>```
>3.209.222.108
>3.211.230.204
>35.169.227.49
>66.117.18.133
>66.117.18.134
>66.117.18.135
>```
>
>**Cette modification s’applique aux types de destinations suivants :**
>
>- [Destinations d’exportation d’audiences de streaming](../../destinations/destination-types.md#streaming-destinations) ([Audience en temps réel Pega CDH](/help/destinations/catalog/personalization/pega-v2.md), intégrations basées sur les API avec [Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) et [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md))
>- Destinations publiques ou privées créées via [Destination SDK](../../destinations/destination-sdk/getting-started.md)
>
>**Action requise :** si vous avez travaillé avec Adobe pour des adresses IP aux destinations de streaming basées sur les API, vous devez ajouter les adresses IP ci-dessus à votre placer sur la liste autorisée place sur la liste autorisée pour assurer des flux de données ininterrompus vers vos destinations basées sur les API.

**Nouvelles destinations**

| Destination | Description |
| --- | --- |
| [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) destination | Utilisez la destination [!DNL Acxiom Real ID Audience Connection] pour améliorer les audiences avec [!DNL Acxiom's] technologie [Real ID](https://www.acxiom.com/real-id/real-id/) et activer les audiences vers plusieurs plateformes, telles que [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], etc. |

**Destinations mises à jour**

| Destination | Description |
| --- | --- |
| Mise à niveau interne de [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) | À compter du mardi 11 août 2025, vous pourrez voir deux cartes **[!DNL Microsoft Bing]** côte à côte dans le catalogue des destinations. Cela est dû à une mise à niveau interne du service de destinations. Le connecteur de destination **[!DNL Microsoft Bing]** existant a été renommé **[!UICONTROL (obsolète) Microsoft Bing]** et une nouvelle carte portant le nom **[!UICONTROL Microsoft Bing]** est désormais disponible. Utilisez la nouvelle connexion **[!UICONTROL Microsoft Bing]** dans le catalogue pour les nouveaux flux de données d’activation. Si vous avez des flux de données actifs vers la destination **[!UICONTROL (obsolète) Microsoft Bing]**, ils seront mis à jour automatiquement. Aucune action n’est donc requise de votre part. <br><br>Si vous créez des flux de données par le biais de l’[API Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/), vous devez mettre à jour vos [!DNL flow spec ID] et [!DNL connection spec ID] avec les valeurs suivantes :<ul><li>ID de spécification de flux : `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>ID de spécification de connexion : `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Suite à cette mise à niveau, il se peut que le nombre de profils activés **baisse** soit réduit dans vos flux de données à [!DNL Microsoft Bing]. Cette baisse est due à l’introduction de l’exigence de mappage **ECID** pour toutes les activations sur cette plateforme de destination. |


**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Amélioration des fonctionnalités de recherche, de filtrage et de balisage pour les destinations | Améliorez votre workflow de gestion des destinations avec des fonctionnalités améliorées de recherche, de filtrage et de balisage dans les onglets [Parcourir](../../destinations/ui/destinations-workspace.md#browse) et [Comptes](../../destinations/ui/destinations-workspace.md#accounts). <br> Vous pouvez désormais rechercher des flux de données et des comptes spécifiques par nom, filtrer selon divers critères, notamment la plateforme de destination, le statut et les dates, et créer des balises personnalisées pour organiser vos destinations. Le tri des colonnes est également disponible pour les champs clés tels que l’heure d’exécution du dernier flux de données, ce qui facilite l’identification et la gestion de vos connexions de destination. <br> ![ Démonstration animée de la recherche d’un flux de données de destination dans l’onglet Parcourir ](../../destinations/assets/ui/workspace/search.gif) |

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification open source qui fournit des structures et des définitions communes (schémas) pour les données importées dans Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Schémas basés sur des modèles | Simplifiez la modélisation de vos données à l’aide de schémas basés sur des modèles. Vous pouvez désormais créer plus facilement des schémas à l’aide d’exemples et de conseils pratiques complets. Cette fonctionnalité est actuellement disponible pour les titulaires de licence Campaign Orchestration. Elle sera étendue aux clients de Data Distiller lors de la phase de disponibilité générale, ce qui rendra la modélisation des données plus accessible et plus efficace. |

Pour plus d’informations, consultez la [présentation de XDM](../../xdm/home.md).

## Profil client en temps réel {#profile}

Le profil client en temps réel offre une vue unifiée et exploitable de chaque client en consolidant les données de tous les canaux en un seul profil.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Amélioration de la fonctionnalité de recherche dans l’API Entities | L’API Entities prend désormais en charge les éléments suivants : <ul><li>Personne (Profil)</li><li>Événements d’expérience</li><li>Compte</li><li>Opportunité</li></ul> Cette mise à jour simplifie l’utilisation des API et permet d’assurer des performances et une fiabilité optimales. Si vous utilisiez auparavant des recherches pour d’autres types d’entités (y compris les tables de jointure et les types d’entités multiples personnalisés), c’est maintenant l’occasion de passer en revue votre utilisation de l’API et de tirer parti de l’expérience améliorée. Pour plus d’informations, consultez le [guide de mise à niveau de l’architecture de B2B edition Real-Time CDB](../../rtcdp/b2b-architecture-upgrade.md). |

Pour plus d’informations sur le profil client en temps réel, consultez la [présentation du profil](../../profile/home.md).

## Sandbox {#sandboxes}

Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Déduplication des objets de dépendance dans le workflow d’import | L’outil Sandbox réutilisera désormais toujours les objets existants si des objets portant le même nom sont détectés, afin d’éviter la prolifération d’objets. Cette modification s’applique aux objets suivants : <ul><li>Schéma</li><li>Groupe de champs</li><li>Audience</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> Pour plus d’informations, consultez le [guide sur les objets pris en charge pour les outils sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Prise en charge complète du sandbox pour le partage de packages entre organisations | L’outil Sandbox prend désormais en charge le type **Sandbox entier** dans le partage de packages d’organisation. Vous pouvez désormais partager des packages sandbox entiers et multi-objets entre les organisations. Pour plus d’informations, consultez le [guide sur les objets pris en charge pour les outils sandbox](../../sandboxes/ui/sharing-packages-across-orgs.md). |

Pour plus d’informations sur les sandbox, consultez la [vue d’ensemble des sandbox](../../sandboxes/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Estimations d’audience | Les estimations d’audience sont désormais générées automatiquement dans le créateur de segments. Cette valeur sera mise à jour chaque fois que vous modifiez l’audience et reflète toujours les dernières règles d’audience. En outre, l’estimation s’affiche désormais sous la forme d’une **plage**, qui est basée sur l’intervalle de confiance des données d’échantillonnage. |

Pour plus d’informations, consultez la [[!DNL Segmentation Service] présentation](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Beta &#x200B;]{type=Informative} Prise en charge des [!DNL Azure Private Links] dans l’interface utilisateur | Vous pouvez désormais utiliser [!DNL Azure Private Links] pour un groupe sélectionné de sources dans l’interface utilisateur. Utilisez cette fonctionnalité pour créer un point d’entrée privé auquel votre source peut se connecter. Grâce aux points d’entrée privés, vous pouvez configurer des connexions et des flux de données qui contournent l’Internet public, ce qui vous offre une sécurité et une isolation réseau accrues pour vos données sensibles. La prise en charge de [!DNL Azure Private Links] est disponible pour les sources suivantes : <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> Pour plus d’informations, consultez le guide sur les [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |
| Authentification améliorée pour [!DNL Azure Blob Storage] | Vous pouvez désormais utiliser l’authentification basée sur le principal de service pour connecter votre source [!DNL Azure Blob Storage] à Experience Platform. Utilisez l’authentification basée sur le principal de service pour une sécurité renforcée, une rotation plus facile des informations d’identification et un contrôle d’accès plus granulaire pour votre compte. Pour plus d’informations, consultez la [[!DNL Azure Blob Storage] présentation](../../sources/connectors/cloud-storage/blob.md). |

Pour plus d’informations, consultez la [vue d’ensemble des sources](../../sources/home.md).

<!--
| [!DNL Marketo] source documentation updates | Get complete visibility into how your [!DNL Marketo] data is transformed when it enters Experience Platform. All field mappings now include detailed explanations of data transformations, so you can understand exactly how your `PersonID` becomes `leadID` and `eventType` becomes `activityType`. |
-->
