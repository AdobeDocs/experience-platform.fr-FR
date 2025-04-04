---
title: Notes de mise à jour d’Adobe Experience Platform - Mars 2023
description: Les notes de mise à jour de mars 2023 pour Adobe Experience Platform.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2081'
ht-degree: 81%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 29 mars 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Tableaux de bord](#dashboards)
- [Collecte de données](#data-collection)
- [Préparation des données](#data-prep)
- [Destinations](#destinations)
- [Modèle de données d’expérience](#xdm)
- [Query Service](#query-service)
- [Édition B2B de Real-Time Customer Data Platform](#b2b)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit de nombreux tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre organisation, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour** {#dashboards-new-updated-features}

| Fonctionnalité | Description |
| --- | --- |
| Tableaux de bord définis par l’utilisateur ou l’utilisatrice | Vous pouvez désormais **échantillonner les valeurs d’attribut** avant d’ajouter un attribut à un widget dans le compositeur de widget de tableaux de bord définis par l’utilisateur ou l’utilisatrice. Quelques exemples de valeurs de cette colonne d’attributs sont disponibles pour les attributs individuels lors de la création d’un widget.<br>Vous pouvez désormais **intervertir les axes X et Y** sur votre widget à l’aide du bouton d’interversion des axes. Vous gagnez ainsi du temps et bénéficiez d’une expérience plus ergonomique lors de l’ajout d’attributs à vos widgets. Vous pouvez également réenregistrer les deux attributs à partir du panneau Attributs.<br>Vous pouvez désormais **modifier l’emplacement et le titre de la légende** dans vos widgets. Une fois qu’une légende est présente sur un widget, vous pouvez en redéfinir l’emplacement n’importe où autour du graphique et renommer son titre, comme vous le pouvez le faire avec les libellés d’axe et le titre du widget. |

{style="table-layout:auto"}

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [Présentation des tableaux de bord](../../dashboards/home.md).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouveau workflow de démarrage rapide pour l’API Meta Conversions (Beta) | Accédez aux nouveaux workflows de démarrage rapide sous « Prise en main » à partir de l’écran d’accueil Collecte de données. Le [workflow de démarrage rapide pour l’API Meta Conversions](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=fr#quick-start) permet aux clientes et clients de collecter et de transférer rapidement des données d’événement côté serveur vers les métadonnées pour les conversions publicitaires en quelques étapes simples. |
| Nouveau workflow de démarrage rapide pour le SDK mobile (Beta) | Accédez aux nouveaux workflows de démarrage rapide sous « Prise en main » à partir de l’écran d’accueil Collecte de données. Le [workflow de démarrage rapide pour le SDK mobile](https://developer.adobe.com/client-sdks/documentation/) vous permet d’implémenter rapidement le SDK mobile et de valider les événements mobiles de base en quelques étapes simples. |
| Extension de transfert d’événement [!DNL Braze] | L’extension de transfert d’événement [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=fr) vous permet de tirer parti des données capturées dans le réseau Edge d’Adobe Experience Platform et de les envoyer à [!DNL Braze] sous la forme d’événements côté serveur à l’aide des API de suivi des utilisateurs et utilisatrices [!DNL Braze]. |
| Extension de transfert d’événement [!DNL Epsilon] | L’extension [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) vous permet d’exploiter le transfert d’événement pour capturer des informations d’événement dans l’Edge Network Adobe Experience Platform et les envoyer à [!DNL Epsilon] à l’aide de l’API d’événement [!DNL Epsilon]. |
| Extension de transfert d’événement [!DNL Mixpanel] | L’extension [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=fr) permet aux clientes et clients d’exploiter le transfert d’événement pour capturer des informations d’événement dans le réseau Edge d’Adobe Experience Platform et les envoyer à Mixpanel à l’aide de l’API de suivi des événements. |

{style="table-layout:auto"}

## Préparation des données {#data-prep}

La préparation des données permet aux personnes travaillant dans l’ingénierie de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité générale du filtrage des données d’Adobe Analytics | Vous pouvez désormais utiliser les fonctionnalités de préparation de données pour appliquer des règles et des conditions afin de filtrer vos données Analytics avant de les ingérer dans le profil client en temps réel. Pour plus d’informations, consultez le guide sur le [filtrage des données Analytics pour l’ingestion de profils](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nouvelles fonctions de codage et de décodage des chaînes URL | <ul><li>La fonction `get_url_encoded` prend une URL comme entrée et remplace ou encode les caractères spéciaux par des caractères ASCII.</li><li>La fonction `get_url_decoded` prend une URL comme entrée et décode les caractères ASCII en caractères spéciaux.</li></ul> Pour plus d’informations, consultez le [guide des fonctions de préparation de données](../../data-prep/functions.md). Pour obtenir la liste complète des caractères réservés et les caractères codés correspondants, consultez le guide sur les [caractères spéciaux](../../data-prep/functions.md#special-characters). |

Pour plus d’informations sur la préparation des données, consultez la [présentation de la préparation des données](../../data-prep/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations** {#new-destinations}

| Destination | Description |
| ----------- | ----------- |
| Connexion GA [[!DNL Adobe Commerce] ](../../destinations/catalog/personalization/adobe-commerce.md) | Le connecteur de destination [!DNL Adobe Commerce] (désormais généralement disponible) vous permet de sélectionner une ou plusieurs audiences Real-Time CDP à activer dans votre compte [!DNL Adobe Commerce], pour offrir une expérience personnalisée dynamique à vos clientes et clients. |
| Connexion GA [[!DNL Snap Inc] ](../../destinations/catalog/advertising/snap-inc.md) | Le connecteur de destination [!DNL Snap Inc] (à présent généralement disponible) permet aux personnes spécialisées dans le marketing d’importer des segments d’utilisateurs et d’utilisatrices créés dans Experience Platform vers [!DNL Snapchat Ads] et de les utiliser pour cibler leurs annonces. |
| [Connexion Oracle Eloqua (API)](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Utilisez la connexion basée sur l’API vers [!DNL Oracle Eloqua] pour planifier et exécuter des campagnes tout en offrant une expérience personnalisée à vos clientes et clients pour leurs prospects dans [!DNL Oracle Eloqua]. |
| [Connexion à  [!DNL Amazon Ads]  (Beta)](../../destinations/catalog/advertising/amazon-ads.md) | L’intégration d’[!DNL Amazon Ads] à Adobe Experience Platform permet une intégration clé en main aux produits d’[!DNL Amazon Ads], y compris à [!DNL Amazon DSP (ADSP)]. En utilisant la destination [!DNL Amazon Ads] dans Adobe Experience Platform, les utilisateurs et utilisatrices peuvent définir les audiences de l’annonceur pour le ciblage et l’activation sur l’[!DNL Amazon DSP]. |
| Connexion [[!DNL Marketo Measure Ultimate] ](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (anciennement Bizible) donne aux personnes spécialisées dans le marketing un aperçu des actions marketing les plus efficaces pour générer du chiffre d’affaires et optimiser le retour sur investissement de leur entreprise. La destination active les flux de données B2B (business-to-business) d’Adobe Experience Platform vers [!DNL Marketo Measure]. La carte n’est disponible que pour les clientes et clients de [!DNL Marketo Measure Ultimate]. |
| [Connexion à TikTok](../../destinations/catalog/social/tiktok.md) | Créez des audiences personnalisées sur TikTok avec vos données pour le ciblage de vos campagnes publicitaires. |
| [Connexion à Zendesk](../../destinations/catalog/crm/zendesk.md) | Utilisez cette destination pour créer et mettre à jour des identités dans un segment en tant que contacts dans [!DNL Zendesk]. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| Nouvelle autorisation de contrôle d’accès pour les destinations : [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | La nouvelle autorisation permet aux utilisateurs et utilisatrices d’activer des segments vers des destinations existantes, sans afficher l’[étape de mappage](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Les utilisateurs et utilisatrices peuvent ajouter et supprimer des segments dans les workflows d’activation, mais ne peuvent pas ajouter ni supprimer des attributs ou des identités mappés. |

{style="table-layout:auto"}

**Correctifs et améliorations** {#destinations-fixes-and-enhancements}

Nous publions un correctif pour le chiffrement PGP/GPG dans les destinations basées sur des fichiers pour Real-Time CDP. Avec cette modification, les destinations basées sur des fichiers qui utilisent actuellement le chiffrement généreront un nom de fichier avec une extension différente de la précédente.

- Extension actuelle lors de l’utilisation du chiffrement : `filename.csv`
- Extension future lors de l’utilisation du chiffrement : `filename.csv.gpg`

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Recommandation CSV en schéma | Vous pouvez désormais charger vos fichiers locaux pour créer des schémas générés par le machine learning qui éliminent la nécessité de créer manuellement un schéma. Dans l’espace de travail [!UICONTROL Sources], téléchargez un exemple de fichier CSV pour que les algorithmes de machine learning d’Adobe vous suggèrent un schéma en fonction des champs cibles. Pour plus d’informations, consultez la [documentation](../../ingestion/tutorials/map-csv/recommendations.md). |

{style="table-layout:auto"}

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Classe | [[!UICONTROL Article de l’offre]](https://github.com/adobe/xdm/pull/1678/files) | Classe qui représente une offre. |
| Classe | [[!UICONTROL Élément de décision]](https://github.com/adobe/xdm/pull/1678/files) | Élément pouvant faire l’objet d’une prise de décision. La sortie d’un processus de prise de décision est composée d’un ou de plusieurs éléments de décision. |
| Classe | [[!UICONTROL Délai d’expiration du serveur de session multimédia]](https://github.com/adobe/xdm/pull/1676/files) | Cette valeur indique le temps écoulé, en secondes, entre la dernière interaction connue de l’utilisateur et le moment où la session a été fermée. |
| Groupe de champs | [[!UICONTROL Attributs calculés du profil XDM]](https://github.com/adobe/xdm/pull/1686/files) | Cela permet d’ajouter des attributs calculés des services Adobe internes aux données client entrantes. Elle ne doit pas être utilisée par les clients pour ingérer des données. |
| Type de données | [[!UICONTROL Objet remboursé]](https://github.com/adobe/xdm/pull/1685/files) | Indique si un remboursement est associé à une commande et définit le type de remboursement, le montant et la devise associée. |
| Type de données | [[!UICONTROL Données de catégorie]](https://github.com/adobe/xdm/pull/1677/files) | Ce nouveau type de données représente la catégorie d’un produit. |
| Schéma | [[!UICONTROL Champs de classification Adobe Target]](https://github.com/adobe/xdm/pull/1682/files) | Un nouveau schéma XDM a été créé pour les jeux de données de classification Target. Il contient un ensemble de champs de métadonnées qui classent les activités et expériences Target. |

{style="table-layout:auto"}

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Groupe de champs | [[!UICONTROL  Détails du composant de contenu ]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` a été supprimé de [!UICONTROL  Détails du composant de contenu ] |
| Groupe de champs | [[!UICONTROL Balises d’entité AJO]](https://github.com/adobe/xdm/pull/1672/files) | Ajout de balises d’entité AJO aux [!UICONTROL champs d’entité AJO], qui correspondent à un Parcours ou à une campagne |
| Groupe de champs | (Multiple) | Ajout de plusieurs champs pour les [[!UICONTROL champs communs des événements d’étape Journey Orchestration]](https://github.com/adobe/xdm/pull/1671/files) |
| Groupe de champs | (Multiple) | [Ajout de plusieurs types d’événements XDM pour [!UICONTROL Rapports multimédia]](https://github.com/adobe/xdm/pull/1670/files). |
| Groupe de champs | [!UICONTROL Événement de modification Workfront] | Les groupes de champs `Full Record` et `Accessor Employee Ids` ont été ajoutés. |
| Type de données | [[!UICONTROL Élément de liste de produits]](https://github.com/adobe/xdm/pull/1685/files) | Le [!UICONTROL  Montant du remboursement ] a été ajouté pour indiquer le montant remboursé pour l’article, le cas échéant. |
| Type de données | [[!UICONTROL Order ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Liste des remboursements] a été ajouté à la liste des remboursements pour cette commande. |
| Type de données | [](https://github.com/adobe/xdm/pull/1677/files) d’élément de liste de produits | Les catégories de produits ont été ajoutées à la liste des données de catégorie de ce produit. |
| Type de données | [!UICONTROL Informations détaillées sur la session] | Ajout du champ de chaîne `pev3` qui [indique le type de flux de médias utilisé pour la création de rapports](https://github.com/adobe/xdm/pull/1676/files). Ajout également de la propriété `pccr` qui indique si une redirection s’est produite. |
| Type de données | [!UICONTROL Liste des demandes internes] | Fournit les [propriétés de la liste de demandes](https://github.com/adobe/xdm/pull/1675/files). Ils comprennent le nom, l’ID et la description. |
| Type de données | [!UICONTROL Commerce] | Le type de données [Commerce a été mis à jour](https://github.com/adobe/xdm/pull/1675/files) afin d&#39;inclure `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals` et `requisitionList`. |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Experience Platform, consultez la [ Présentation du système XDM ](../../xdm/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou à ingérer en tant que profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Contrôle d’accès basé sur les attributs sur la boutique accélérée | Utilisez le contrôle d’accès basé sur les attributs avec Data Distiller pour définir le contrôle d’accès sur tous les jeux de données de la boutique accélérée. Cela contrôle l’accès aux modèles de données personnalisés créés par les utilisateurs et utilisatrices et stockés dans une boutique accélérée pour alimenter les tableaux de bord personnalisés. |

{style="table-layout:auto"}

Pour plus d’informations sur Query Service, consultez la section [présentation de Query Service](../../query-service/home.md).

## Édition B2B de Real-Time Customer Data Platform {#b2b}

Basée sur Real-time Customer Data Platform (Real-time CDP), l’édition B2B de Real-time CDP a été conçue pour les professionnels du marketing travaillant dans un modèle de service business-to-business. Elle rassemble des données provenant de sources multiples et les combine en une vue unique des profils de comptes et d’utilisateurs. Ces données unifiées permettent aux spécialistes marketing de cibler précisément des audiences spécifiques afin de stimuler leur engagement sur tous les canaux disponibles.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Correction de bug | Pour mieux refléter les profils au sein de votre système, le système n’inclut plus les profils internes dans le nombre total de profils ou la mesure d’audience adressable pour l’édition B2B de Real-time Customer Data Platform. À compter d’aujourd’hui, le nombre total de profils et la mesure d’audience adressable peuvent afficher des chiffres inférieurs. Cette baisse reflète la nouvelle méthode de calcul et ne se produira qu’une seule fois. Aucune donnée n’a été effacée, seule la méthode de calcul est différente. Si vous avez des questions, contactez votre représentant Adobe. |

{style="table-layout:auto"}

Pour en savoir plus sur l’édition B2B de Real-time CDP, consultez la [présentation de l’édition B2B de Real-time CDP](../../rtcdp/overview.md).

## Service de segmentation {#segmentation}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mesures de profil | Pour mieux refléter les mesures de profil, la répartition des abonnements et les mesures d’attrition sont désormais combinées et calculées sur une période de 24 heures. Pour plus d’informations, consultez le [Guide de l’interface utilisateur de segmentation](../../segmentation/ui/overview.md#browse). |

{style="table-layout:auto"}

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes et vous permet de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité Beta de [!DNL Chatlio] | La source [!DNL Chatlio] est maintenant disponible en version Beta. Utilisez la source [!DNL Chatlio] pour diffuser vos données d’événements de [!DNL Chatlio] à Experience Platform. Pour plus d’informations, consultez la [[!DNL Chatlio] présentation](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilité Beta de [!DNL Customer.io] | La source [!DNL Customer.io] est maintenant disponible en version Beta. Utilisez la source [!DNL Customer.io] pour diffuser les données d’événements client vers Experience Platform. Pour plus d’informations, consultez la [[!DNL Customer.io] présentation](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilité Beta de [!DNL Pendo] | La source [!DNL Pendo] est maintenant disponible en version Beta. Utilisez la source [!DNL Pendo] pour diffuser les données d’événements client vers Experience Platform. Pour plus d’informations, consultez la [[!DNL Pendo] présentation](../../sources/connectors/analytics/pendo-webhook.md). |
| Prise en charge des brouillons de flux de données | Vous pouvez désormais utiliser l’API Flow Service pour définir vos flux de données sur l’état de brouillon. Vous pouvez ensuite modifier les informations du brouillon de flux de données et le publier. Pour plus d’informations, consultez le guide sur la [définition des flux de données sources en tant que brouillons](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).
