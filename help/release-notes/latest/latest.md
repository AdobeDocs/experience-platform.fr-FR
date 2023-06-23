---
title: Notes de mise à jour d’Adobe Experience Platform
description: Les notes de mise à jour de juin 2023 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e56a6c2bac46778afcc24db8d51e77ec3700dd96
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 35%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 21 juin 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Authentification aux API Experience Platform](#authentication-platform-apis)
- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
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

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| Prise en charge de Workspace pour [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) destinations. | Vous pouvez désormais sélectionner l’espace de travail Adobe Target vers lequel vous souhaitez partager des audiences lors de la configuration d’une nouvelle connexion à la destination Adobe Target. Voir [paramètres de connexion](../../destinations/catalog/personalization/adobe-target-connection.md#parameters) pour plus d’informations. En outre, consultez le tutoriel sur [configuration des espaces de travail](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en) dans Adobe Target pour plus d’informations sur les espaces de travail. |

{style="table-layout:auto"}

<!--

**Fixes and enhancements** {#destinations-fixes-and-enhancements}

- Placeholder for fixes and enhancements

-->

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Extension (Prospect-Profile) | [[!UICONTROL Extension Adobe Unified Profile Service Prospect-Profile Union]](https://github.com/adobe/xdm/pull/1735/files) | Ajout des champs requis pour le schéma d’union Prospect-Profile. |
| Extension | [[!UICONTROL Ressource de prise de décision]](https://github.com/adobe/xdm/pull/1732/files) | Ajoutez un type de données pour représenter les ressources utilisées dans la prise de décision. [!UICONTROL Ressource de prise de décision] fournit une référence aux ressources utilisées pour effectuer le rendu de la variable `decisionItems`. |
| Type de données | [[!UICONTROL Commerce]](https://github.com/adobe/xdm/pull/1747/files) | [!UICONTROL Commerce] stocke des enregistrements liés à l’activité d’achat et de vente. |
| Groupe de champs | [[!UICONTROL Enrichissement du partenaire de profil (exemple)]](https://github.com/adobe/xdm/pull/1747/files) | Un exemple de schéma a été ajouté pour l’enrichissement du partenaire de profil. |
| Groupe de champs | [[!UICONTROL Détails du projet partenaire (exemple)]](https://github.com/adobe/xdm/pull/1747/files) | Un exemple de schéma a été ajouté pour les extensions de profil de fournisseur de données prospect. |
| Type de données | [[!UICONTROL Portée du commerce]](https://github.com/adobe/xdm/pull/1747/files) | [!UICONTROL Portée du commerce] identifie l’endroit où un événement s’est produit. Par exemple, dans la vue de magasin, le magasin ou le site web, etc. |
| Type de données | [[!UICONTROL Facturation]](https://github.com/adobe/xdm/pull/1734/files) | Les informations de facturation, pour un ou plusieurs paiements, ont été ajoutées à la variable [!UICONTROL Commerce] schéma. |

{style="table-layout:auto"}

**Composants XDM mis à jour**

| Type de composant | Nom | Description de la mise à jour |
| --- | --- | --- |
| Groupe de champs | [[!UICONTROL Détails de l’interaction MediaAnalytics]](https://github.com/adobe/xdm/pull/1736/files) | Modifié `bitrateAverageBucket` de 100 à &quot;800-899&quot;. |
| Type de données | [[!UICONTROL Informations détaillées sur les données de la QoE]](https://github.com/adobe/xdm/pull/1736/files) | Modifié `bitrateAverageBucket` type de données en chaîne. |
| Groupe de champs | [[!UICONTROL Détails de l’appartenance à un segment]](https://github.com/adobe/xdm/pull/1735/files) | Ajout à la classe Prospect Profile. |
| Schéma | [[!UICONTROL Schéma du système des attributs calculés]](https://github.com/adobe/xdm/pull/1735/files) | Mappage d’identités ajouté à la variable [!UICONTROL Schéma système des attributs calculés]. |
| Type de données | [[!UICONTROL Réseau de diffusion de contenu]](https://github.com/adobe/xdm/pull/1733/files) | Champ ajouté à [!UICONTROL Informations détaillées sur la session] pour décrire le réseau de diffusion de contenu utilisé. |
| Extension | [[!UICONTROL Extension d’union de compte de service de profil unifié Adobe]](https://github.com/adobe/xdm/pull/1731/files) | Mappage d’identités ajouté à la variable [!UICONTROL Extension d’union de compte de service de profil unifié Adobe]. |
| Type de données | [[!UICONTROL Commande]](https://github.com/adobe/xdm/pull/1730/files) | `discountAmount` a été ajouté à [!UICONTROL Commande]. Ceci fait la différence entre le prix normal de la commande et le prix spécial. Elle s’applique à l’ensemble de la commande plutôt qu’à des produits individuels. |
| Schéma | [[!UICONTROL Demande d’opération d’hygiène AEP]](https://github.com/adobe/xdm/pull/1728/files) | Le `targetServices` a été ajouté pour fournir les noms des services qui traitent les opérations d’hygiène des données. |
| Type de données | [[!UICONTROL Expédition]](https://github.com/adobe/xdm/pull/1727/files) | `currencyCode` a été ajouté aux informations d’expédition pour un ou plusieurs produits. Il s’agit d’un code de devise alphabétique ISO 4217 utilisé pour évaluer le produit. |
| Type de données | [[!UICONTROL Application]](https://github.com/adobe/xdm/pull/1726/files) | Le `language` a été ajouté pour fournir les préférences linguistiques, géographiques ou culturelles de l’utilisateur à l’application. |
| Extension | [[!UICONTROL Champs d’entité AJO]](https://github.com/adobe/xdm/pull/1746/files) | [!UICONTROL Entité d’horodatage AJO] a été ajouté pour indiquer l’heure de la dernière modification du message. |
| Type de données | (Multiple) | [Suppression de plusieurs détails multimédia](https://github.com/adobe/xdm/pull/1739/files) sur plusieurs types de données pour assurer la cohérence. |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md)

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger des données dans le lac de données Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou à ingérer en tant que profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Modèles &#x200B; intégrés | Query Service prend désormais en charge l’utilisation de modèles qui référencent d’autres modèles dans votre SQL. Réduisez votre charge de travail et évitez les erreurs en utilisant des modèles intégrés dans vos requêtes. Vous pouvez réutiliser des instructions ou des conditions et référencer des modèles imbriqués pour une plus grande flexibilité dans votre SQL. La taille des requêtes pouvant être stockées en tant que modèles n’est pas limitée, ni le nombre de modèles pouvant être référencés à partir de votre requête d’origine. Pour plus d’informations, reportez-vous à la section [guide de modèle intégré](../../query-service/essential-concepts/inline-templates.md). | | Mises à jour de l’interface utilisateur des requêtes planifiées | Gérez toutes vos requêtes planifiées à partir d’un seul emplacement de l’interface utilisateur à l’aide de la fonction [[!UICONTROL Onglet Requêtes planifiées]](../../query-service/ui/monitor-queries.md#inline-actions). Le [!UICONTROL Requêtes planifiées] L’interface utilisateur a été améliorée avec l’ajout d’actions de requête intégrées et de la nouvelle colonne d’état de requête. Les ajouts récents incluent la possibilité d’activer, de désactiver et de supprimer un planning, ou de s’abonner à des alertes pour les exécutions de requête à venir directement depuis le [!UICONTROL Requêtes planifiées] vue. <p>![Actions intégrées mises en surbrillance dans la variable [!UICONTROL Requêtes planifiées] vue.](../../query-service/images/ui/monitor-queries/disable-inline.png "Actions intégrées mises en surbrillance dans la variable [!UICONTROL Requêtes planifiées] vue."){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}

Pour plus d’informations sur Query Service, reportez-vous à la section [Présentation de Query Service](../../query-service/home.md).

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
