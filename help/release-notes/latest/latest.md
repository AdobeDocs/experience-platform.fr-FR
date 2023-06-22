---
title: Notes de mise à jour d’Adobe Experience Platform
description: Les notes de mise à jour de juin 2023 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 77c7fbfba2a1ccc6df31abc2f6b926ed90942c4c
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 29%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 21 juin 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Authentification aux API Experience Platform](#authentication-platform-apis)
- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Query Service](#query-service)
- [Sources](#sources)

## Authentification aux API Experience Platform {#authentication-platform-apis}

Pour les utilisateurs d’API Experience Platform, la méthode d’obtention des jetons d’accès requis pour s’authentifier et effectuer des appels vers des points de terminaison d’API est désormais simplifiée. La méthode JWT pour obtenir des jetons d’accès est obsolète et remplacée par une méthode d’authentification OAuth serveur à serveur plus simple.<p>![Nouvelle méthode d’authentification OAuth pour mettre les jetons d’accès en surbrillance.](/help/landing/images/api-authentication/oauth-authentication-method.png "Nouvelle méthode d’authentification OAuth pour mettre les jetons d’accès en surbrillance."){width="100" zoomable="yes"}</p>

Bien que les intégrations d’API existantes utilisant la méthode d’authentification JWT continueront à fonctionner jusqu’au 1er janvier 2025, Adobe recommande vivement de migrer les intégrations existantes vers la nouvelle méthode OAuth Server-to-Server avant cette date. Lisez le guide sur [migration des informations d’identification du compte de service (JWT) vers les informations d’identification OAuth serveur à serveur](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Lire la mise à jour [Tutoriel sur l’authentification des Experience Platform](/help/landing/api-authentication.md) pour plus d’informations.

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Type | Fonctionnalité | Description |
| --- | --- | --- |
| Extension | Extension de transfert d’événement [!DNL Google Cloud Platform] | Le [[!DNL Google Cloud Platform]](../../tags/extensions/server/google-cloud-platform/overview.md) l’extension de transfert d’événement vous permet de transférer des données d’événement vers Google pour activation via [!DNL Google Pub/Sub]. |
| Extension | Extension [!DNL Cloud connector for Google Analytics 4 (ga4)] | Le [[!DNL Cloud connector for Google Analytics 4 (ga4)]](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.109820.html) l’extension de transfert d’événement vous permet d’effectuer le suivi des analyses via la nouvelle [!DNL Google Analytics 4 (ga4)] standard. |
| Secret | Secret JWT OAuth 2 | Le [Secret JWT OAuth 2](../../tags/ui/event-forwarding/secrets.md) vous permet d’utiliser l’Adobe et [!DNL Google] Jetons de service pour prendre en charge les interactions serveur-serveur dans le transfert d’événement. |
| Balises et transfert d’événements | Attribution des utilisateurs | L’attribution de l’utilisateur fournit les données d’activité clés dans l’ensemble de [Balises](../../tags/home.md) et [Transfert d’événement](../../tags/ui/event-forwarding/overview.md) Interface utilisateur.<br><br>Les données incluent qui a apporté les modifications et à quelle heure. Ces données sont visibles dans l’interface utilisateur Balises et Transfert d’événement dans les écrans suivants :<br><ul><li> Présentation des propriétés</li><li> Extensions installées</li><li>Comparaison et révision des règles</li><li>Comparaison des éléments de données</li><li>Comparaison des extensions - Révision</li><li>Modifications des ressources de bibliothèque</li><li>Dernier build de bibliothèque et publication</li></ul> |

{style="table-layout:auto"}

Pour en savoir plus sur la collecte de données, lisez le [présentation de la collecte de données](../../tags/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#new-updated-destinations}

| Destination | Description |
| ----------- | ----------- |
| [[!BADGE Beta]{type=Informative} [!DNL Amazon Ads] connection](../../destinations/catalog/advertising/amazon-ads.md) | Le [!DNL Amazon Ads] L’intégration à Adobe Experience Platform prend désormais en charge le routage régional vers les différentes [!DNL Amazon Ads] les marchés. En savoir plus dans la section [changement de destination](../../destinations/catalog/advertising/amazon-ads.md#changelog). |

{style="table-layout:auto"}

<!-- 

**New or updated functionality** {#destinations-new-updated-functionality}

| Functionality | Description |
| ----------- | ----------- |
| Workspace support for [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) destinations. | You can now select the Adobe Target workspace that you want to share audiences to, when configuring a new Adobe Target destination connection. See the [connection parameters](../../destinations/catalog/personalization/adobe-target-connection.md#parameters) section for more information. Additionally, see the tutorial on [configuring workspaces](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en) in Adobe Target for more information about workspaces. |

{style="table-layout:auto"}

-->

<!--

**Fixes and enhancements** {#destinations-fixes-and-enhancements}

- Placeholder for fixes and enhancements

-->

Pour des informations plus générales sur les destinations, reportez-vous à la [présentation des destinations](../../destinations/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger des données dans le lac de données Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou à ingérer en tant que profil client en temps réel.
&#x200B;
**Fonctionnalités mises à jour**
&#x200B; | Fonctionnalité | Description | | — | — | | Modèles &#x200B; intégrés | Query Service prend désormais en charge l’utilisation de modèles qui référencent d’autres modèles dans votre SQL. Réduisez votre charge de travail et évitez les erreurs en utilisant des modèles intégrés dans vos requêtes. Vous pouvez réutiliser des instructions ou des conditions et référencer des modèles imbriqués pour une plus grande flexibilité dans votre SQL. La taille des requêtes pouvant être stockées en tant que modèles n’est pas limitée, ni le nombre de modèles pouvant être référencés à partir de votre requête d’origine. Pour plus d’informations, reportez-vous à la section [guide de modèle intégré](../../query-service/essential-concepts/inline-templates.md). | | Mises à jour de l’interface utilisateur des requêtes planifiées | Gérez toutes vos requêtes planifiées à partir d’un seul emplacement de l’interface utilisateur à l’aide de la fonction [[!UICONTROL Onglet Requêtes planifiées]](../../query-service/ui/monitor-queries.md#inline-actions). Le [!UICONTROL Requêtes planifiées] L’interface utilisateur a été améliorée avec l’ajout d’actions de requête intégrées et de la nouvelle colonne d’état de requête. Les ajouts récents incluent la possibilité d’activer, de désactiver et de supprimer un planning, ou de s’abonner à des alertes pour les exécutions de requête à venir directement depuis le [!UICONTROL Requêtes planifiées] vue. <p>![Actions intégrées mises en surbrillance dans la variable [!UICONTROL Requêtes planifiées] vue.](../../query-service/images/ui/monitor-queries/disable-inline.png "Actions intégrées mises en surbrillance dans la variable [!UICONTROL Requêtes planifiées] vue."){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}
&#x200B; Pour plus d’informations sur Query Service, reportez-vous à la section [Présentation de Query Service](../../query-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources, telles que les applications d’Adobe, le stockage dans le cloud, les logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de la suppression des flux de données source de classification Adobe Analytics | Vous pouvez désormais supprimer les flux de données source qui utilisent les classifications Adobe Analytics comme source. Sous **[!UICONTROL Sources]** > **[!UICONTROL Flux de données]**, sélectionnez le flux de données de votre choix, puis cliquez sur supprimer. Pour plus d’informations, consultez le guide sur [création d’une connexion source pour les données de classification Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/classifications.md). |
| Prise en charge du filtrage pour [!DNL Microsoft Dynamics] utilisation de l’API | Utilisez des opérateurs logiques et de comparaison pour filtrer les données au niveau de la ligne pour le [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) source. Pour plus d’informations, consultez le guide sur [filtrage des données pour une source à l’aide de l’API](../../sources/tutorials/api/filter.md). |
| [!BADGE Version bêta]{type=Informative}[!DNL RainFocus] | Vous pouvez désormais utiliser la variable [!DNL RainFocus] intégration de sources pour obtenir des données d’analyse et de gestion des événements de votre [!DNL RainFocus] compte à Experience Platform. Pour plus d’informations, reportez-vous à la section [[!DNL RainFocus] présentation de la source](../../sources/connectors/analytics/rainfocus.md). |
| Prise en charge d’Adobe Commerce  | Vous pouvez désormais utiliser l’intégration de sources Adobe Commerce pour importer les données de votre compte Adobe Commerce vers Experience Platform. Pour plus d’informations, reportez-vous à la section [Présentation de la source Adobe Commerce](../../sources/connectors/adobe-applications/commerce.md). |
| Prise en charge de [!DNL Mixpanel] | Vous pouvez désormais utiliser la variable [!DNL Mixpanel] intégration de sources pour importer les données d’analyse de votre [!DNL Mixpanel] à Experience Platform à l’aide des API ou de l’interface utilisateur. Pour plus d’informations, reportez-vous à la section [[!DNL Mixpanel] présentation de la source](../../sources/connectors/analytics/mixpanel.md). |
| Prise en charge de [!DNL Zendesk] | Vous pouvez désormais utiliser la variable [!DNL Zendesk] intégration de sources pour obtenir des données de succès client de votre [!DNL Zendesk] à Experience Platform à l’aide des API ou de l’interface utilisateur. Pour plus d’informations, reportez-vous à la section [[!DNL Zendesk] présentation de la source](../../sources/connectors/customer-success/zendesk.md). |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).
