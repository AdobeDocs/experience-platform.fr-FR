---
title: Notes de mise à jour d’Adobe Experience Platform - Février 2024
description: Notes de mise à jour de février 2024 pour Adobe Experience Platform.
exl-id: 7e4b76b7-4027-4890-b869-1dbb79670c3e
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 33%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de mise à jour : jeudi 21 février 2024**

Mises à jour des fonctionnalités existantes dans Experience Platform :

- [Alertes](#alerts)
- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Sandbox](#sandboxes)
- [Service de segmentation](#segmentation)
- [Sources](#sources)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités Experience Platform. Vous pouvez vous abonner à différentes règles d’alerte via l’onglet [!UICONTROL Alerts] de l’interface utilisateur d’Experience Platform et choisir de recevoir des messages d’alerte dans l’interface utilisateur elle-même ou par e-mail de notification.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Onglet Historique des alertes | En tant qu’administrateur Experience Platform, vous pouvez utiliser la fonctionnalité de gestion des abonnés aux alertes pour affecter une alerte à un identifiant utilisateur Adobe, une adresse e-mail externe ou une liste de groupes d’adresses e-mail. Pour plus d’informations, voir la [documentation de l’interface utilisateur des alertes](/help/observability/alerts/ui.md) pour plus d’informations sur l’onglet Historique. |

{style="table-layout:auto"}

Pour en savoir plus sur les alertes, consultez la [[!DNL Observability Insights] présentation](/help/observability/home.md).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de la messagerie Web In-App dans Web SDK | Adobe Experience Platform Web SDK prend désormais en charge la configuration de la messagerie Web In-App pour les campagnes Adobe Journey Optimizer. |

{style="table-layout:auto"}

Pour en savoir plus sur les collections de données, veuillez consulter la [vue d’ensemble des collections de données](/help/tags/home.md).

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](/help/data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](/help/data-prep/home.md). -->

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations** {#new-destinations}

| Destination | Description |
| ----------- | ----------- |
| [Connexion Gainsight PX](/help/destinations/catalog/analytics/gainsight-px.md) | Gainsight PX est une plateforme d’expérience de produit qui permet aux équipes produit de comprendre comment les utilisateurs utilisent leurs produits, de collecter des commentaires et de créer des engagements in-app tels que des présentations de produits pour stimuler l’intégration des utilisateurs et l’adoption de produits. |
| [Connexion Balises Mailchimp](/help/destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp est une plateforme d’automatisation du marketing et un service de marketing par e-mail populaire. Vous pouvez utiliser le connecteur Balises Mailchimp pour structurer, étiqueter ou catégoriser vos contacts. |
| [Connexion SAP Commerce](/help/destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce est une solution de plateforme d’e-commerce cloud destinée aux entreprises B2B et B2C et disponible dans le cadre du portefeuille d’expériences client SAP. Vous pouvez utiliser cette destination pour mettre à jour les détails de votre client dans SAP Commerce à partir d’une audience Experience Platform existante. |

{style="table-layout:auto"}

**Fonctionnalité nouvelle ou mise à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| Activer les audiences de compte généralement disponibles | La fonctionnalité d’activation des audiences de compte vers certaines destinations est désormais généralement disponible pour les sociétés qui achètent les éditions [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) et [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) de Real-Time Customer Data Platform. Lisez le tutoriel sur l’[activation des audiences de compte](/help/destinations/ui/activate-account-audiences.md) pour obtenir des informations complètes, y compris les destinations prises en charge. |
| Outils d’application du consentement de la Loi sur les marchés numériques pour les destinations Google | Google publie des modifications de l’API [Google Ads](https://developers.google.com/google-ads/api/docs/start), de l’API [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) et de l’API [Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) afin de prendre en charge les exigences de conformité et de consentement définies dans le [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) de l’Union européenne ([EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/)). L&#39;application de ces modifications aux exigences en matière de consentement devrait entrer en vigueur à compter du 6 mars 2024. <br/><br/> Pour se conformer à la politique de consentement des utilisateurs de l’UE et continuer à créer des listes d’audience pour les utilisateurs dans l’Espace économique européen (EEE), les annonceurs et les partenaires doivent s’assurer de transmettre le consentement de l’utilisateur final lors du téléchargement des données d’audience. En tant que partenaire Google, Adobe vous fournit les outils nécessaires pour vous conformer à ces exigences de consentement en vertu de la DMA dans l’Union européenne.<br/><br/>Les clients qui ont acheté Adobe Privacy &amp; Security Shield et configuré une [politique de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) pour filtrer les profils non consentis n’ont aucune action à effectuer.<br/><br/>Les clients qui n’ont pas acheté Adobe Privacy &amp; Security Shield doivent utiliser les fonctionnalités [définition de segment](/help/segmentation/home.md#segment-definitions) du [créateur de segments](/help/segmentation/ui/segment-builder.md) pour filtrer les profils non consentis, afin de continuer à utiliser les destinations Real-Time CDP Google existantes sans interruption. |
| [!BADGE Beta &#x200B;]{type=Informative} réorganiser les champs de mappage pour les destinations par lots | Vous pouvez désormais modifier l’ordre des colonnes dans vos exportations de fichiers CSV en faisant glisser les champs de mappage dans l’étape [mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping). L’ordre des champs mappés dans l’interface utilisateur se reflète dans l’ordre des colonnes dans le fichier CSV exporté, du haut vers le bas, la ligne supérieure étant la colonne la plus à gauche du fichier CSV. <br/><br/> Cette fonctionnalité est en version bêta et disponible uniquement pour certains clients. Pour demander l’accès à cette fonctionnalité, contactez votre représentant Adobe. |
| [!BADGE Beta &#x200B;]{type=Informative} plannings d’exportation par défaut présélectionnés pour les destinations par lots | Experience Platform définit désormais automatiquement un planning par défaut pour chaque export de fichier. Consultez la documentation sur la [planification des exportations d’audience](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) pour savoir comment modifier la planification par défaut. <br/><br/> Cette fonctionnalité est en version bêta et disponible uniquement pour certains clients. Pour demander l’accès à cette fonctionnalité, contactez votre représentant Adobe. |
| [!BADGE Beta &#x200B;]{type=Informative} Modification en masse des plannings d’activation des audiences pour les destinations par lots | Vous pouvez désormais modifier le planning d’activation de plusieurs audiences en bloc, à partir de la page [Données d’activation](/help/destinations/ui/destination-details-page.md#bulk-edit-schedule). <br/><br/> Cette fonctionnalité est en version bêta et disponible uniquement pour certains clients. Pour demander l’accès à cette fonctionnalité, contactez votre représentant Adobe. |
| [!BADGE Beta &#x200B;]{type=Informative} Exporter des fichiers en bloc à la demande vers des destinations par lots | Vous pouvez désormais exporter des audiences en bloc vers des destinations par lots, grâce à la fonctionnalité [exporter des fichiers à la demande](/help/destinations/ui/export-file-now.md). <br/><br/> Cette fonctionnalité est en version bêta et disponible uniquement pour certains clients. Pour demander l’accès à cette fonctionnalité, contactez votre représentant Adobe. |

{style="table-layout:auto"}

Pour obtenir des informations plus générales sur les destinations, consultez la [présentation des destinations](/help/destinations/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des sandbox qui divisent une instance d’Experience Platform unique en plusieurs environnements virtuels pour favoriser le développement et l’évolution d’applications d’expérience digitale.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Outils sandbox | En plus de prendre désormais en charge les types d’objets pour les règles de consentement et de gouvernance, utilisez l’outil sandbox pour importer des schémas sans activer de profils unifiés, vérifiez les attributs manquants dans le sandbox cible lors de l’importation d’un segment et utilisez par défaut la politique de fusion existante. Pour plus d’informations sur ces fonctionnalités, consultez le [guide de l’interface utilisateur des outils Sandbox](/help/sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

Pour plus d’informations sur les sandbox, consultez la [vue d’ensemble des sandbox](/help/sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] permet de segmenter en audiences les données stockées dans [!DNL Experience Platform] qui se rapportent aux personnes (tels que les clientes et clients, les prospects, les utilisateurs et utilisatrices ou les organisations). Vous pouvez créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur [!DNL Experience Platform] et sont facilement accessibles à partir de n’importe quelle solution Adobe.

**Nouvelle fonctionnalité**

| Fonctionnalité | Description |
| ------- | ----------- |
| Audiences de compte | Les audiences de compte sont désormais disponibles pour tous. Vous pouvez désormais utiliser la segmentation de compte pour apporter la facilité et la sophistication complètes de l’expérience de segmentation marketing, des audiences basées sur les personnes aux audiences basées sur les comptes dans les éditions B2B et B2P de Real-time Customer Experience Platform. Cette version vous permet d’utiliser les audiences basées sur les personnes comme prédicat pour les audiences basées sur les comptes, ajoute des fonctionnalités de recherche, prend en charge l’utilisation d’entités personnalisées et est conforme à la gouvernance des données. Pour plus d’informations sur cette fonctionnalité, consultez la [vue d’ensemble des audiences de compte](/help/segmentation/types/account-audiences.md). |

{style="table-layout:auto"}

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Beta &#x200B;]{type=Informative} source [!DNL Acxiom] | Utilisez la [[!DNL Acxiom Prospecting Data Import] source](/help/sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) pour récupérer et mapper des données [!DNL Acxiom] service de prospect à Experience Platform. |

{style="table-layout:auto"}

Pour plus d’informations sur les sources, consultez la [vue d’ensemble des sources](/help/sources/home.md).
