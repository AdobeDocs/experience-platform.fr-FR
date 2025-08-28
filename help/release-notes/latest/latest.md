---
title: Notes de mise à jour d’Adobe Experience Platform - Août 2025
description: Les notes de mise à jour d’août 2025 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: bbeab81e64a86a59a1f85ca139935abf220ef361
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 78%

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

**Date de publication : 19 août 2025**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [Catalog Service](#catalog-service)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Sandbox](#sandboxes)
- [Service de segmentation](#segmentation-service)
- [Sources](#sources)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités Experience Platform. Vous pouvez vous abonner à différentes règles d’alerte à l’aide de l’onglet [!UICONTROL Alertes] dans l’interface d’utilisation d’Experience Platform. Vous pouvez aussi choisir de recevoir les messages d’alerte dans l’UI elle-même ou par le biais de notifications par e-mail.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Alertes de capacité de débit de streaming | Trois nouvelles alertes permettent de s’abonner aux alertes et de les configurer pour gérer et surveiller de manière proactive les performances de la capacité de débit du streaming. Les nouvelles alertes s’affichent lorsque le débit de streaming atteint 80 % ou 90 % ou dépasse les limites de capacité. Pour plus d’informations, consultez le guide des [règles d’alerte de capacité](../../observability/alerts/rules.md#capacity). |

Pour plus d’informations sur les alertes, consultez la [[!DNL Observability Insights] vue d’ensemble](../../observability/home.md).

## Catalog Service {#catalog-service}

Catalog Service est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, Catalog conserve les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Conservation des données pour le profil client en temps réel | Vous ne pouvez mettre à jour la période de conservation des données pour le profil client en temps réel **qu’une fois** tous les 30 jours. |

Pour plus d’informations sur Catalog Service, consultez la [vue d’ensemble de Catalog Service](../../catalog/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

>[!IMPORTANT]
>
>**Prolongation du planning d’export du jeu de données**
>
>Si votre organisation a créé des flux de données d’export de jeux de données avant novembre 2024, ces flux cesseront de fonctionner le **1er septembre 2025**. Si vous avez besoin que les flux de données continuent d’exporter des données après le 1er septembre 2025, vous devez prolonger leur planning pour chaque destination vers laquelle vous exportez des jeux de données, en suivant les étapes de [ce guide](../../destinations/ui/dataset-expiration-update.md).

>[!IMPORTANT]
>
>**Mise à jour de la liste des adresses IP autorisées requise pour les destinations basées sur les API**
>
>En raison des mises à niveau du moteur d’export des destinations de streaming, les organisations qui utilisent des [listes d’adresses IP autorisées](../../destinations/catalog/streaming/ip-address-allow-list.md) pour les destinations basées sur les API doivent ajouter les adresses IP suivantes à leurs listes autorisées **avant le 15 septembre 2025** :
>
>**Adresses IP requises :**
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
>**Cette modification s’applique aux types de destinations suivants :**
>
>- [Destinations d’export d’audiences de streaming](../../destinations/destination-types.md#streaming-destinations) ([Audience en temps réel Pega CDH](/help/destinations/catalog/personalization/pega-v2.md), intégrations basées sur les API avec [Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) et [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md))
>- Destinations publiques ou privées créées via [Destination SDK](../../destinations/destination-sdk/getting-started.md)
>
>**Action requise :** si vous avez collaboré avec Adobe pour placer des adresses IP sur la liste autorisée des destinations de streaming basées sur les API, vous devez ajouter les adresses IP ci-dessus à votre liste autorisée pour assurer des flux de données ininterrompus vers vos destinations basées sur les API.

**Nouvelles destinations**

| Destination | Description |
| --- | --- |
| Destination [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | Utilisez la destination [!DNL Acxiom Real ID Audience Connection] pour améliorer les audiences avec la technologie [Real ID](https://www.acxiom.com/real-id/real-id/) [!DNL Acxiom's] et activer les audiences vers plusieurs plateformes, telles que [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], etc. |
| Destination [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) améliorée | La destination [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) améliorée est une version mise à niveau du connecteur [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) existant. Ce nouveau connecteur apporte des fonctionnalités de synchronisation de profil en plus des fonctionnalités de synchronisation d’audience existantes du connecteur hérité, offrant une intégration plus étroite à [!DNL Marketo Engage]. <br> Le connecteur [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) sera abandonné en **mars 2026**. Pour garantir une transition en douceur vers la nouvelle destination **[[!UICONTROL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)**, passez en revue les points clés suivants et les actions requises : <ul><li>Tous les utilisateurs du Marketo Engage **[!UICONTROL (hérité) (V2)]** existant doivent migrer vers la nouvelle destination **[!UICONTROL Marketo Engage]** d’ici mars 2026.</li><li> **Les flux de données existants ne seront pas migrés automatiquement.** Vous devez [configurer une nouvelle connexion](../../destinations/ui/connect-destination.md) à la nouvelle destination **[!UICONTROL Marketo Engage]** et y activer vos audiences.</li></ul> |

**Destinations mises à jour**

| Destination | Description |
| --- | --- |
| Mise à niveau interne de [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) | À compter du 11 août 2025, pendant une courte période, vous avez peut-être vu deux cartes **[!DNL Microsoft Bing]** côte à côte dans le catalogue des destinations. Cela est dû à une mise à niveau interne du service de destinations. Le connecteur de destination **[!DNL Microsoft Bing]** existant a été renommé **[!UICONTROL (obsolète) Microsoft Bing]** et une nouvelle carte portant le nom **[!UICONTROL Microsoft Bing]** est désormais disponible. <br> La mise à niveau est terminée et la carte obsolète a été supprimée du catalogue de destination. Utilisez la connexion **[!UICONTROL Microsoft Bing]** dans le catalogue pour les nouveaux flux de données d’activation. Si vous aviez des flux de données actifs vers la destination **[!UICONTROL (obsolète) Microsoft Bing]** , ils seront mis à jour automatiquement. Aucune action n’est donc requise de votre part. <br><br>Si vous créez des flux de données par le biais de l’[API Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/), vous devez mettre à jour vos [!DNL flow spec ID] et [!DNL connection spec ID] avec les valeurs suivantes :<ul><li>ID de spécification de flux : `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>ID de spécification de connexion : `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Suite à cette mise à niveau, il se peut que **le nombre de profils activés baisse** dans vos flux de données vers [!DNL Microsoft Bing]. Cette baisse est due à l’introduction de l’**exigence de mappage ECID** pour toutes les activations vers cette plateforme de destination. |
| Détails d’expiration de l’authentification pour les destinations [[!DNL LinkedIn]](../../destinations/catalog/social/linkedin.md) et [Audiences correspondantes LinkedIn](../../destinations/catalog/social/linkedin-b2b.md) | Les informations d’expiration de l’authentification pour les destinations [!DNL LinkedIn] sont désormais visibles directement dans l’interface d’Experience Platform. Vous pouvez ainsi voir quand votre authentification arrivera à expiration et la renouveler avant qu’elle ne cause des interruptions de vos flux de données. Vous pouvez surveiller les dates d’expiration de votre jeton à partir de la colonne **[!UICONTROL Date d’expiration du compte]** dans les onglets **[[!UICONTROL Comptes]](../../destinations/ui/destinations-workspace.md#accounts)** ou **[[!UICONTROL Parcourir]](../../destinations/ui/destinations-workspace.md#browse)**. |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Amélioration des fonctionnalités de recherche, de filtrage et de balisage pour les destinations | Améliorez votre workflow de gestion des destinations avec des fonctionnalités améliorées de recherche, de filtrage et de balisage dans les onglets [Parcourir](../../destinations/ui/destinations-workspace.md#browse) et [Comptes](../../destinations/ui/destinations-workspace.md#accounts). <br> Vous pouvez désormais rechercher des flux de données et des comptes spécifiques par nom, filtrer selon divers critères, notamment la plateforme de destination, le statut et les dates, et créer des balises personnalisées pour organiser vos destinations. Le tri des colonnes est également disponible pour les champs clés tels que l’heure d’exécution du dernier flux de données, ce qui facilite l’identification et la gestion de vos connexions de destination. <br> ![ Démonstration animée de la recherche d’un flux de données de destination dans l’onglet Parcourir ](../../destinations/assets/ui/workspace/search.gif) |


## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Schémas basés sur des modèles | Simplifiez la modélisation des données à l’aide de schémas basés sur des modèles. Vous pouvez désormais créer plus facilement des schémas à l’aide d’exemples et de conseils pratiques complets. Cette fonctionnalité est actuellement disponible pour les personnes titulaires de licences Campaign Orchestration. Elle sera étendue aux clientes et clients de Data Distiller lors de la phase de disponibilité générale, ce qui rendra la modélisation des données plus accessible et plus efficace. |

Pour plus d’informations, consultez la [vue d’ensemble XDM](../../xdm/home.md).

<!--

## Real-Time Customer Profile {#profile}

Real-Time Customer Profile provides a unified, actionable view of each customer by consolidating data from all channels into a single profile.

**New or updated features**

| Feature | Description |
| --- | --- |
| Enhanced lookup functionality in the Entities API | The Entities API now supports the following: <ul><li>Person (Profile)</li><li>Experience Events</li><li>Account</li><li>Opportunity</li></ul> This update simplifies API usage and helps ensure optimal performance and reliability. If you previously used lookups for other entity types—including join tables and custom Multi-Entity types—now is a great opportunity to review your API usage and take advantage of the improved experience. For more information, read the [Real-Time CDB B2B Edition architecture upgrade guide](../../rtcdp/b2b-architecture-upgrade.md). |

For more information on Real-Time Customer Profile, read the [Profile overview](../../profile/home.md).

-->

## Sandbox {#sandboxes}

Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Déduplication des objets de dépendance dans le workflow d’import | Les outils de sandbox réutiliseront désormais toujours les objets existants si des objets portant le même nom sont détectés, et ce afin d’éviter la prolifération d’objets. Cette modification s’applique aux objets suivants : <ul><li>Schéma</li><li>Groupe de champs</li><li>Audience</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> Pour plus d’informations, consultez le [guide sur les objets pris en charge pour les outils sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Prise en charge de l’ensemble du sandbox pour le partage de packages entre organisations | Les outils de sandbox prennent désormais en charge le type **Sandbox entier** dans le partage de packages entre organisations. Vous pouvez désormais partager des packages de sandbox entiers et multi-objets entre les organisations. Pour plus d’informations, consultez le [guide sur les objets pris en charge pour les outils sandbox](../../sandboxes/ui/sharing-packages-across-orgs.md). |

Pour plus d’informations sur les sandbox, consultez la [vue d’ensemble des sandbox](../../sandboxes/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Estimations d’audience | Les estimations d’audience sont désormais générées automatiquement dans le créateur de segments. Cette valeur sera mise à jour chaque fois que vous modifiez l’audience et reflète toujours les dernières règles d’audience. En outre, l’estimation s’affiche désormais sous la forme d’une **plage**, qui est basée sur l’intervalle de confiance des données d’échantillonnage. |

Pour plus d’informations, consultez la [[!DNL Segmentation Service] vue d’ensemble](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Authentification améliorée pour [!DNL Azure Blob Storage] | Vous pouvez désormais utiliser l’authentification basée un principal pour connecter votre source [!DNL Azure Blob Storage] à Experience Platform. Utilisez l’authentification basée un principal de service pour une sécurité renforcée, une rotation plus facile des informations d’identification et un contrôle d’accès plus granulaire pour votre compte. Pour plus d’informations, consultez la [[!DNL Azure Blob Storage] vue d’ensemble](../../sources/connectors/cloud-storage/blob.md). |

Pour plus d’informations, consultez la [vue d’ensemble des sources](../../sources/home.md).

<!---

| [!BADGE Beta]{type=Informative} Support for [!DNL Azure Private Links] in the UI | You can now use [!DNL Azure Private Links] for a select group of sources in the UI. Use this feature to create a private endpoint that which your source can connect to. With private endpoints, you can set up connections and dataflows that bypass the public internet, giving you enhanced security and network isolation for your sensitive data. Support for [!DNL Azure Private Links] is available to the following following sources: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> For more information, read the guide on [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |

-->

