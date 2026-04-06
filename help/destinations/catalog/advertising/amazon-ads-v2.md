---
title: Amazon Ads v2
description: Amazon Ads v2 offre toute une gamme d’options pour vous aider à atteindre vos objectifs publicitaires. Les partenaires de vente enregistrés, les vendeurs, les marchands de livres, les auteurs Kindle Direct Publishing (KDP), les développeurs d’applications ou les agences peuvent tirer parti de ces options. L’intégration d’Amazon Ads v2 à Adobe Experience Platform offre une intégration clé en main aux produits Amazon Ads.
last-substantial-update: 2026-03-31T00:00:00Z
source-git-commit: 1e93c78b13159a2aed24d283e3768c670ad14097
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 16%

---

# Connexion Amazon Ads v2 {#amazon-ads-v2}

## Vue d’ensemble {#overview}

[!DNL Amazon Ads v2] permet aux annonceurs d’ingérer, de gérer, d’activer et de réutiliser efficacement les données d’audience dans les produits [!DNL Amazon Ads].

>[!IMPORTANT]
>
>[!DNL Amazon Ads v2] est la destination actuelle de toutes les nouvelles connexions [!DNL Amazon Ads]. Si vous disposez d’une connexion [ (héritée) [!DNL Amazon Ads]](./amazon-ads.md) existante, elle continue à fonctionner sans aucune modification requise. [!DNL Amazon Ads v2] se connecte à [!DNL Ads Data Manager], qui prend en charge les types d’identité étendus, les champs liés aux adresses et le partage de données entre les produits [!DNL Amazon Ads], ce qui améliore le ciblage et les taux de correspondance d’audience par rapport à [ (hérité) [!DNL Amazon Ads]](./amazon-ads.md).
>
>Après la fin avril 2026, [!DNL Amazon Ads v2] sera renommé [!DNL Amazon Ads] et la carte héritée sera masquée, laissant une seule carte de destination dans le catalogue. Les flux de données hérités existants continueront à fonctionner et vous pouvez les gérer dans l’onglet **[!UICONTROL Browse]** au-delà de cette date.

L’intégration de [!DNL Amazon Ads v2] à [!DNL Adobe Experience Platform] fournit une connexion directe pour ingérer des membres d’audience dans [!DNL Amazon Ads]. Les audiences chargées sont disponibles dans la console [!DNL Ads Data Manager (ADM)] dans [!DNL Amazon Ads]. Vous pouvez utiliser la console [!DNL Ads Data Manager] pour partager des données entre différents produits [!DNL Amazon Ads].

Pour en savoir plus sur [!DNL Ads Data Manager], voir :

* [Ads Data Manager - Aperçu De La Console](https://advertising.amazon.com/API/docs/en-us/adm/1_ads-data-manager-console-overview)
* [Utilisation de la console Ads Data Manager](https://advertising.amazon.com/API/docs/en-us/adm/2_ads-data-manager-console)
* [Configuration du compte dans Ads Data Manager](https://advertising.amazon.com/API/docs/en-us/adm/2a_ads-data-manager_account_setup)

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe *[!DNL Amazon Ads]*. Pour toute demande ou information, contactez directement l’équipe d’Amazon Ads à l’adresse *`amc-support@amazon.com`.*

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Amazon Ads v2], consultez les exemples de cas d’utilisation ci-dessous que [!DNL Adobe Experience Platform] clients peuvent résoudre à l’aide de cette destination.

### Ingestion et activation des audiences {#activation-and-targeting}

Une marque de vêtements de sport souhaite atteindre ses clients existants avec des publicités pertinentes dans tout le [!DNL Amazon Ads]. La marque peut ingérer les adresses e-mail des clients de son CRM dans [!DNL Adobe Experience Platform], créer des audiences à l’aide de ses données hors ligne propriétaires et activer ces audiences pour les [!DNL Amazon Ads] via la destination [!DNL Amazon Ads v2]. Après l’activation, vous pouvez utiliser ces audiences pour cibler les annonces publicitaires vers ces clients dans [!DNL Amazon Ads] inventaire, ce qui permet à la marque de réengager des clients connus et de générer des achats répétés. Pour en savoir plus, voir [Gérer les données](https://advertising.amazon.com/API/docs/en-us/adm/6_adm-manage-data).

## Conditions préalables {#prerequisites}

Pour utiliser la connexion [!DNL Amazon Ads v2] avec [!DNL Adobe Experience Platform], vous devez avoir accès à **[!DNL Amazon Ads Data Manager]** à l’aide d’un compte [Manager](https://advertising.amazon.com/help/G69CDSR9MNSWJH95). Pour plus d’informations, consultez [Prise en main d’Amazon Ads Data Manager](https://advertising.amazon.com/API/docs/en-us/adm/1_ads-data-manager-console-overview).

### Accepter les conditions générales du gestionnaire de données Amazon Ads {#accept-terms}

Avant de configurer la destination [!DNL Amazon Ads v2], connectez-vous à votre compte [!DNL Amazon Ads] et acceptez les conditions générales de [!DNL Ads Data Manager]. Accédez à la console [!DNL Ads Data Manager] dans [!DNL Amazon Ads] et acceptez les conditions lorsque vous y êtes invité. Si vous n’acceptez pas les conditions générales, les audiences ne sont pas créées dans [!DNL Amazon Ads].

## Identités prises en charge {#supported-identities}

La destination [!DNL Amazon Ads v2] prend en charge l’activation des identités suivantes. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| `phone` | Numéros de téléphone hachés avec l’algorithme SHA256 | Le texte brut et les numéros de téléphone hachés SHA256 sont pris en charge par [!DNL Adobe Experience Platform]. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `email` | Adresses e-mail (en minuscules) hachées avec l’algorithme SHA256 | Le texte brut et les adresses e-mail hachées SHA256 sont pris en charge par [!DNL Adobe Experience Platform]. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `firstname` | Prénom de l’utilisateur | Le texte brut et les prénoms hachés SHA256 sont pris en charge par [!DNL Adobe Experience Platform]. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `lastname` | Nom de famille de l&#39;utilisateur | Le texte brut et les noms hachés SHA256 sont pris en charge par [!DNL Adobe Experience Platform]. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `address` | Adresse postale de l&#39;utilisateur | Le texte brut et SHA256 rues hachées sont pris en charge par [!DNL Adobe Experience Platform]. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `city` | Ville de l’utilisateur | Le texte brut et les villes hachées SHA256 sont pris en charge par [!DNL Adobe Experience Platform]. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `state` | Département ou province de l&#39;utilisateur | Les états de texte brut et haché SHA256 sont pris en charge par [!DNL Adobe Experience Platform]. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `zip` | Code postal de l’utilisateur | Le texte brut et les fichiers ZIP hachés SHA256 sont pris en charge par [!DNL Adobe Experience Platform]. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `countryCode` | Pays de l&#39;utilisateur (code ISO à 2 caractères) | Prend en charge la saisie de texte brut. |
| `experianId` | Identifiant attribué par [!DNL Experian] | Prend en charge la saisie de texte brut. |
| `kantarId` | Identifiant attribué par [!DNL Kantar] | Prend en charge la saisie de texte brut. |
| `liveRampId` | Identifiant attribué par [!DNL LiveRamp] | Prend en charge la saisie de texte brut. |
| `maId` | Identifiant attribué par une application mobile | Prend en charge la saisie de texte brut. |
| `merkleId` | Identifiant attribué par [!DNL Merkle] | Prend en charge la saisie de texte brut. |
| `neustarId` | Identifiant attribué par [!DNL Neustar] | Prend en charge la saisie de texte brut. |
| `realId` | Identifiant attribué par le graphique d’identités Real ID | Prend en charge la saisie de texte brut. |
| `sambaTvId` | Identifiant attribué par [!DNL Samba TV] | Prend en charge la saisie de texte brut. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via le [!DNL Experience Platform] [Segmentation Service](/help/segmentation/home.md). |
| Toutes les autres origines d’audience | Oui | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](/help/segmentation/ui/audience-portal.md#import-audience) dans [!DNL Experience Platform] à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications [!DNL Experience Platform] telles que [!DNL Adobe Journey Optimizer], </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}

Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données [!DNL Adobe Experience Platform]. | Rapports, workflows de science des données |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Le tableau ci-dessous décrit le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
| ---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience dont les identifiants sont pris en charge par [!DNL Amazon Ads]. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Les mises à jour des audiences dans [!DNL Experience Platform] sont immédiatement envoyées à [!DNL Ads Data Manager]. |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](/help/destinations/ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Account name]** : saisissez un nom qui vous aide à identifier ce compte de destination. Cela s’avère particulièrement utile si vous disposez de plusieurs connexions à la même destination.
* **[!UICONTROL Description]** (facultatif) : ajoutez des détails qui vous aident, vous ou votre équipe, à faire la distinction entre les comptes, tels que l’objectif de la connexion ou le contexte commercial approprié.

![Boîte de dialogue Se connecter à la destination dans Experience Platform pour Amazon Ads](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-connect-to-destination.png)

Vous êtes redirigé vers l’interface [!DNL Amazon Ads v2]. Sélectionnez **[!UICONTROL Allow]** pour vous connecter à votre compte Amazon.

![Invite d’autorisation OAuth Amazon Ads demandant à l’utilisateur d’autoriser](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-allow.png)

Après l’authentification, vous êtes redirigé vers [!DNL Adobe Experience Platform] avec votre nouvelle connexion.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Champs de configuration de destination Amazon Ads v2 dans Experience Platform](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-configure-destination.png)

* **[!UICONTROL Name]** : nom par lequel vous reconnaissez cette destination.
* **[!UICONTROL Description]** : description qui vous aide à identifier cette destination.
* **[!UICONTROL Manager Account]** : identifiant du compte du gestionnaire de Target dans la liste déroulante.
* **[!UICONTROL All audience members sent to Amazon are consented for use for Advertising]** : spécifiez le consentement pour l’utilisation des données (`GRANTED` ou `DENIED`).
* **[!UICONTROL Ads data manager Terms & Conditions]** : acceptez les conditions générales du [!DNL Amazon Ads] Data Manager. Lisez la section [accepter les conditions](#accept-terms) pour plus de détails.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](/help/destinations/ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des identités, vous avez besoin de l’autorisation **[!UICONTROL View Identity Graph]** [contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mappages obligatoires {#map}

La destination [!DNL Amazon Ads v2] nécessite que vous configuriez les mappages suivants pour une activation réussie des données.

| Champ source | Champ cible | Description |
|---------|----------|---------|
| `IdentityMap: Email_LC_SHA256` ou `IdentityMap: Email`. | `Identity: email` | Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `xdm: homeAddress.countryCode` | `Identity: countryCode` | Pays de l&#39;utilisateur (code ISO à 2 caractères) |

![Configuration du mappage des champs d’identité pour la destination Amazon Ads v2](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-mapping.png)

### Bonnes pratiques de mappage {#mapping-best-practices}

Combinez des identifiants internes (tels que le numéro de téléphone et l’adresse) avec des identifiants fournis par les partenaires. Cela [!DNL Amazon Ads] permet d’utiliser plusieurs signaux d’identité lors de la correspondance d’audience, ce qui entraîne de meilleurs taux de correspondance.

Utilisez les identifiants fournis par les partenaires uniquement lorsqu’ils sont renseignés dans vos données source. Si un champ d’identifiant de partenaire mappé est vide ou absent pour un profil donné, il est ignoré lors de la correspondance d’audience et ne contribue pas aux taux de correspondance.

### Exemples {#examples}

* Utilisez des `kantarId` lors de l’activation d’audiences créées ou enrichies à l’aide de données d’identité [!DNL Kantar].
* Utilisez des `merkleId` lorsque les données d’audience proviennent de solutions d’identité gérées par [!DNL Merkle].
* Utilisez des `neustarId` lorsque vos données sont liées par le biais d’[!DNL Neustar] résolution d’identité.
* Utilisez des `experianId` pour les audiences enrichies à l’aide de données d’identité [!DNL Experian].
* Utilisez des `liveRampId` lors de l’activation des audiences qui reposent sur une résolution d’identité [!DNL LiveRamp].
* Utilisez des `sambaTvId` lorsque vous utilisez des données d’audience fournies par [!DNL Samba TV].

Ces identifiants sont généralement fournis par les partenaires respectifs en tant qu’identifiants de texte brut et ne nécessitent pas de hachage.

## Valider l’exportation des données {#exported-data}

Après l’activation, validez l’ingestion de votre audience dans la console **[!DNL Ads Data Manager].**

Accédez à **[!UICONTROL Audiences]** → **[!UICONTROL Uploaded Sources]**. Vérifiez le statut d’ingestion de votre audience, sa taille et les journaux d’erreurs. Les pages [Gérer les données](https://advertising.amazon.com/API/docs/en-us/adm/6_adm-manage-data) et [Destinations](https://advertising.amazon.com/API/docs/en-us/adm/7_adm-destinations) de la documentation [!DNL Amazon Ads] fournissent d’autres conseils de validation.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations sur [!DNL Amazon Ads Data Manager], consultez la ressource suivante :

* [Présentation Du Gestionnaire De Données Amazon Ads](https://advertising.amazon.com/API/docs/en-us/adm/1_ads-data-manager-console-overview)
