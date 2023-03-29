---
title: Notes de mise à jour d’Adobe Experience Platform
description: Les notes de mise à jour de mars 2023 pour Adobe Experience Platform.
source-git-commit: 38c3461f1d84fca83fd04eef57aae28de4744e17
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 37%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 29 mars 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Collecte de données](#data-collection)
- [Préparation des données](#data-prep)
- [Destinations](#destinations)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouveau workflow de démarrage rapide pour l’API de métadonnées de conversion (version bêta) | Accédez aux nouveaux workflows de démarrage rapide sous &quot;Prise en main&quot; à partir de l’écran d’accueil de la collecte de données ! Le [workflow de démarrage rapide pour l’API des conversions de métadonnées](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) permet aux clients de collecter et de transférer rapidement des données d’événement côté serveur vers les métadonnées pour les conversions publicitaires en quelques étapes simples. |
| [!DNL Braze] extension de transfert d’événement | Le [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) l’extension de transfert d’événement vous permet d’exploiter les données capturées dans Adobe Experience Platform Edge Network et de les envoyer à [!DNL Braze] sous la forme d’événements côté serveur à l’aide de la variable [!DNL Braze] API de suivi des utilisateurs. |
| [!DNL Mixpanel] extension de transfert d’événement | Le [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) L’extension permet aux clients d’exploiter le transfert d’événement pour capturer des informations d’événement dans Adobe Experience Platform Edge Network et les envoyer à Mixpanel à l’aide de l’API Track Events. |

{style="table-layout:auto"}

## Préparation des données {#data-prep}

La préparation des données permet aux ingénieur(e)s de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles fonctions de codage et de décodage des chaînes URL | <ul><li>Le `get_url_encoded` prend une URL comme entrée et remplace ou code des caractères spéciaux avec des caractères ASCII.</li><li>Le `get_url_decoded` prend une URL comme entrée et décode les caractères ASCII en caractères spéciaux.</li></ul> Pour plus d’informations, reportez-vous à la section [Guide des fonctions de préparation de données](../../data-prep/functions.md). Pour une liste complète des caractères réservés et des caractères codés correspondants, lisez le guide sur [caractères spéciaux](../../data-prep/functions.md#special-characters). |

Pour plus d’informations sur la préparation des données, veuillez lire le [Aperçu de la préparation des données](../../data-prep/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations** {#new-destinations}

| Destination | Description |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] GA de connexion](../../destinations/catalog/personalization/adobe-commerce.md) | Le [!DNL Adobe Commerce] Le connecteur de destination (désormais disponible de manière générale) vous permet de sélectionner une ou plusieurs audiences Real-Time CDP à activer dans votre [!DNL Adobe Commerce] pour offrir une expérience personnalisée dynamique à vos clients. |
| [[!DNL Snap Inc] GA de connexion](../../destinations/catalog/advertising/snap-inc.md) | Le [!DNL Snap Inc] Le connecteur de destination (désormais disponible de manière générale) permet aux marketeurs d’importer les segments d’utilisateurs créés dans Experience Platform dans [!DNL Snapchat Ads] et les utiliser pour cibler leurs publicités. |
| [Connexion Oracle Eloqua (API)](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Utilisez la connexion basée sur l’API pour [!DNL Oracle Eloqua] planifier et exécuter des campagnes tout en offrant une expérience client personnalisée pour leurs prospects dans [!DNL Oracle Eloqua]. |
| [Connexion à  [!DNL Amazon Ads]  (Version bêta)](../../destinations/catalog/advertising/amazon-ads.md) | Le [!DNL Amazon Ads] l’intégration à Adobe Experience Platform permet une intégration clé en main à [!DNL Amazon Ads] les produits, y compris la variable [!DNL Amazon DSP (ADSP)]. En utilisant la variable [!DNL Amazon Ads] destination dans Adobe Experience Platform, les utilisateurs peuvent définir les audiences de l’annonceur pour le ciblage et l’activation sur la variable [!DNL Amazon DSP]. |
| Connexion [[!DNL Marketo Measure Ultimate] ](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (anciennement Bizible) donne aux marketeurs un aperçu des actions marketing les plus efficaces pour générer des recettes et optimiser le retour sur investissement pour leur entreprise. La destination active les flux de données B2B (business-to-business) de Adobe Experience Platform vers [!DNL Marketo Measure]. La carte n’est disponible que pour [!DNL Marketo Measure Ultimate] clients. |
| [Connexion TikTok](../../destinations/catalog/social/tiktok.md) | Créez des audiences personnalisées sur TikTok avec vos données pour le ciblage de vos campagnes publicitaires. |
| [Connexion Zendesk](../../destinations/catalog/crm/zendesk.md) | Utilisez cette destination pour créer et mettre à jour des identités dans un segment en tant que contacts dans [!DNL Zendesk]. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| Nouvelle autorisation de contrôle d’accès pour les destinations : [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | La nouvelle autorisation permet aux utilisateurs d’activer des segments vers des destinations existantes, sans afficher la variable [étape de mappage](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Les utilisateurs peuvent ajouter et supprimer des segments dans les workflows d’activation, mais ils ne peuvent pas ajouter ni supprimer des attributs ou des identités mappés. |

{style="table-layout:auto"}

**Correctifs et améliorations** {#destinations-fixes-and-enhancements}

Nous publions un correctif pour le chiffrement PGP/GPG dans les destinations basées sur des fichiers pour la plateforme de données clients en temps réel. Avec cette modification, les destinations basées sur des fichiers existantes qui utilisent actuellement le chiffrement généreront un nom de fichier avec une extension différente de celle précédemment.

- Extension actuelle lors de l’utilisation du chiffrement : `filename.csv`
- Extension future lors de l’utilisation du chiffrement : `filename.csv.gpg`

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mesures de profil | Pour vous donner une représentation plus précise des mesures de profil, la ventilation des adhésions et les mesures d’attrition sont combinées et sont désormais calculées sur une période de 24 heures. Pour plus d’informations, reportez-vous à la section [Guide de l’interface utilisateur de segmentation](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité bêta de [!DNL Chatlio] | Le [!DNL Chatlio] source est désormais disponible en version bêta. Utilisez la variable [!DNL Chatlio] source pour diffuser votre [!DNL Chatlio] données d’événements à Experience Platform. Pour plus d’informations, consultez la [[!DNL Chatlio] vue d’ensemble](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilité bêta de [!DNL Customer.io] | Le [!DNL Customer.io] source est désormais disponible en version bêta. Utilisez la variable [!DNL Customer.io] source pour diffuser les données d’événements client vers Experience Platform. Pour plus d’informations, consultez la [[!DNL Customer.io] vue d’ensemble](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilité bêta de [!DNL Pendo] | Le [!DNL Pendo] source est désormais disponible en version bêta. Utilisez la variable [!DNL Pendo] source pour diffuser en continu vos données d’analyse de produit vers Experience Platform. Pour plus d’informations, consultez la [[!DNL Pendo] vue d’ensemble](../../sources/connectors/analytics/pendo-webhook.md). |
| Prise en charge des flux de données de brouillon | Vous pouvez désormais utiliser l’API Flow Service pour définir vos flux de données sur un état de brouillon. Les flux de données préliminaires peuvent ensuite être mis à jour et publiés avec de nouvelles informations. Pour plus d’informations, consultez le guide sur [définition des flux de données sources en tant que brouillons](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).
