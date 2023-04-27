---
title: Notes de mise à jour d’Adobe Experience Platform
description: Les notes de mise à jour d’avril 2023 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 7c4bdee9f8599e27ffab776c4df5083d2e29e26c
workflow-type: tm+mt
source-wordcount: '1421'
ht-degree: 38%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 26 avril 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Tableaux de bord](#dashboards)
- [Préparation des données](#data-prep)
- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Modèle de données d’expérience](#xdm)
- [Profil client en temps réel](#profile)
- [Sources](#sources)

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit de nombreux tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre organisation, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour** {#dashboards-new-updated-features}

| Fonctionnalité | Description |
| --- | --- |
| Tableaux de bord définis par l’utilisateur ou l’utilisatrice | Vous pouvez désormais **filtrer les données historiques** à partir de vos informations sur les widgets et utilisez des données récentes ou une période d’analyse personnalisée. Voir [Guide des tableaux de bord définis par l’utilisateur](../../dashboards/user-defined-dashboards.md#filter-historical-data) pour plus d’informations.<br>Vous pouvez également **dupliquer vos widgets existants**. En personnalisant un doublon et en modifiant leurs attributs, vous pouvez éviter de redémarrer dès le début lors de la création d’un widget unique. Lisez le [guide de duplication de widgets](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) pour en savoir plus. |

{style="table-layout:auto"}

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [Présentation des tableaux de bord](../../dashboards/home.md).

## Préparation des données {#data-prep}

La préparation des données permet aux personnes travaillant dans l’ingénierie de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mises à jour de la période de renvoi d’Adobe Analytics dans les environnements de test hors production | La période de renvoi d’Adobe Analytics dans les environnements de test hors production a été réduite à trois mois. Le renvoi des environnements de test de production reste le même au bout de 13 mois. Cette modification s’applique uniquement aux nouveaux flux et n’affecte pas les flux existants. Pour plus d’informations, reportez-vous à la section [Présentation d’Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nouvelle fonction de mappeur pour convertir les chaînes FPID en ECID | Utilisez la variable `fpid_to_ecid` pour convertir des chaînes FPID en ECID en vue de les utiliser dans des applications Experience Platform et Experience Cloud. Pour plus d’informations, consultez le [guide des fonctions de préparation de données](../../data-prep/functions.md). |

{style="table-layout:auto"}

Pour plus d’informations sur la préparation des données, consultez la [présentation de la préparation des données](../../data-prep/home.md).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Obscurcissement des adresses IP pour les flux de données | Vous pouvez désormais définir des options d’obscurcissement d’IP au niveau d’un flux de données partiel ou complet dans la variable [interface utilisateur de configuration de datastream](../../edge/datastreams/configure.md). <br><br>Le paramètre d’obscurcissement de l’adresse IP au niveau du flux de données est prioritaire par rapport à toute obscurcissement d’adresse IP configuré dans Adobe Target et Audience Manager. <br><br>Les données envoyées à Adobe Analytics ne sont pas affectées par le niveau du flux de données. [!UICONTROL Obscurcissement d’IP] . Adobe Analytics reçoit actuellement des adresses IP non obscurcies. Pour qu’Analytics reçoive des adresses IP obscurcies, vous devez configurer l’obscurcissement des adresses IP séparément, dans Adobe Analytics. Ce comportement sera mis à jour dans les prochaines versions.<br><br> Pour plus d’informations sur l’obscurcissement des adresses IP et pour obtenir des instructions sur la façon de le configurer, voir [documentation sur la configuration de datastream](../../edge/datastreams/configure.md#advanced-options). |
| [Remplacements de la configuration des flux de données](../../edge/datastreams/overrides.md) | Vous pouvez désormais définir des options de configuration supplémentaires pour les flux de données, que vous utiliserez pour remplacer des paramètres spécifiques, tels que les jeux de données d’événement, les jetons de propriété Target, les conteneurs de synchronisation d’identifiants et les suites de rapports Analytics. <br><br>Le remplacement des configurations de flux de données est un processus en deux étapes : <ol><li>Tout d’abord, vous devez définir vos remplacements de configuration de flux de données dans la variable [page de configuration de datastream](../../edge/datastreams/configure.md).</li><li>Ensuite, vous devez envoyer les remplacements au réseau Edge par le biais d’une commande de SDK Web ou à l’aide du SDK Web. [extension de balise](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |

{style="table-layout:auto"}

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations** {#new-destinations}

| Destination | Description |
| ----------- | ----------- |
| Connexion [[!DNL Salesforce Marketing Cloud Account Engagement] ](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Utilisez la destination Engagement du compte de Marketing Cloud Salesforce (anciennement appelée Pardot) pour capturer, suivre, noter et évaluer des pistes. Utilisez cette destination pour les cas d’utilisation B2B impliquant plusieurs ministères et décideurs qui nécessitent des cycles de vente et de décision plus longs. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| Surveillance du flux de données pour [!DNL Custom Personalization] et [!DNL Adobe Commerce] destinations | <p> Vous pouvez désormais afficher les mesures d’activation pour la variable [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Personnalisation personnalisée](../../destinations/catalog/personalization/custom-personalization.md) et le [Personnalisation Personnalisée Avec Attributs](../../destinations/catalog/personalization/custom-personalization.md) connexions. </p> <p>![Image Adobe Commerce](/help/destinations/assets/common/adobe-commerce-metrics.png "Mesures Adobe Commerce"){width="100" zoomable="yes"}</p>  Voir [Surveillance des flux de données dans l’espace de travail des destinations](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) pour plus d’informations. |
| Nouveau **[!UICONTROL Ajout d’un identifiant de segment au nom du segment]** pour le champ [!DNL Google Ad Manager] et [!DNL Google Ad Manager 360] destinations | <p>Le nom du segment peut maintenant apparaître dans la variable [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) et [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) incluez l’identifiant de segment de l’Experience Platform, comme suit : `Segment Name (Segment ID)`.</p><p>![Ajout d’une image d’identifiant de segment](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Nouveau champ Ajouter un identifiant de segment au nom du segment "){width="100" zoomable="yes"}</p> |
| Renvois d’audience planifiés | <p>Pour le [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) destination, l’activation des renvoi d’audience vers la destination est planifiée 24 à 48 heures après le premier mappage d’un segment à une connexion de destination. Cette mise à jour répond à la stratégie de Google consistant à attendre 24 heures avant d’ingérer des données et améliorera les taux de correspondance entre la plateforme de données clients en temps réel et [!DNL Google Display & Video 360].</p> <p>Notez qu’il s’agit d’une configuration de serveur principal applicable uniquement à cette destination et qui n’est liée à aucune option de planification configurable par le client dans l’interface utilisateur.</p> |

{style="table-layout:auto"}

**Correctifs et améliorations** {#destinations-fixes-and-enhancements}

- Nous avons corrigé un problème dans la variable **Identités exclues** mesures de création de rapports pour les exportations de destination basées sur des fichiers. Les clients recevaient tous les identifiants exportés à partir de l’exportation activée comme prévu. Toutefois, la variable **Identités exclues** la mesure de création de rapports dans l’interface utilisateur affichait incorrectement un grand nombre d’identités exclues en raison d’un comptage incorrect des identités qui n’étaient jamais censées être exportées. (PLAT-149774)
- Nous avons corrigé un problème dans la variable **Planification** de l’étape du workflow d’activation. Pour les destinations qui nécessitent un ID de mappage, les clients n’ont pas pu ajouter d’ID de mappage pour les segments ajoutés aux connexions de destination existantes. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Bascule des noms d’affichage | L’éditeur de schémas propose désormais un bouton d’activation/désactivation pour modifier les noms de champ d’origine et les noms d’affichage plus lisibles.<br>![L’éditeur de schémas avec le bouton bascule du nom d’affichage mis en surbrillance.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Bascule du nom d’affichage de l’éditeur de schémas"){width="100" zoomable="yes"}<br>Cette flexibilité permet d’améliorer la visibilité des champs et l’édition de vos schémas. Les noms d’affichage des groupes de champs standard sont générés par le système, mais peuvent également être personnalisés via l’interface utilisateur si nécessaire. Veuillez lire la [documentation sur le basculement de nom d’affichage](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) pour en savoir plus. |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue holistique de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le Profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Expiration des données de profil pseudonyme | L’expiration des données de profil anonymes est désormais disponible en général. Cette version supprimera en permanence les profils pseudonymes obsolètes de votre instance d’Experience Platform une fois activée. Pour en savoir plus sur cette fonctionnalité et les profils pseudonymes, veuillez lire la section [Guide d’expiration des données de profil pseudonyme](../../profile/pseudonymous-profiles.md). |

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de l’API pour le filtrage des données au niveau des lignes pour Microsoft Dynamics, Salesforce CRM et le Marketing Cloud Salesforce | Utilisez des opérateurs logiques et de comparaison pour filtrer les données de niveau ligne pour les sources de Marketing Cloud Microsoft Dynamics, Salesforce CRM et Salesforce. Pour plus d’informations, lisez le guide sur le [filtrage des données d’une source à l’aide de l’API](../../sources/tutorials/api/filter.md). |
| Disponibilité bêta de Shopify Streaming | Le [Shopify Streaming source](../../sources/connectors/ecommerce/shopify-streaming.md) est désormais disponible en version bêta. Utilisez la source de diffusion en continu Shopify pour diffuser des données de votre compte de partenaires Shopify vers Experience Platform. |
| Disponibilité générale de l’intégration OneTrust | Le [Source d’intégration OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) est désormais GA. Utilisez la source d’intégration OneTrust pour importer les données de consentement et de préférences de votre compte d’intégration OneTrust vers Experience Platform. |
| Disponibilité générale d’Oracle Service Cloud | Le [Source Oracle Service Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md) est désormais GA. Utilisez la source Oracle Service Cloud pour importer vos données Oracle Service Cloud dans Experience Platform. |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).