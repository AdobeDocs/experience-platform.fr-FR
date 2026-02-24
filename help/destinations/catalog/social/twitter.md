---
title: Connexion des audiences personnalisées Twitter
description: Ciblez vos abonnés et clients existants sur Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 35%

---

# Connexion [!DNL Twitter Custom Audiences]

## Vue d’ensemble {#overview}

Ciblez vos abonnés et clients existants sur Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Avant de configurer votre destination [!DNL Twitter Custom Audiences], vérifiez les conditions préalables suivantes relatives à Twitter, qui doivent être remplies.

1. Votre compte [!DNL Twitter Ads] doit être éligible à la publicité. Les nouveaux comptes [!DNL Twitter Ads] ne sont pas éligibles à la publicité au cours des 2 premières semaines suivant leur création.
2. L’autorisation [!DNL Twitter Audience Manager] doit être activée pour votre compte utilisateur Twitter auquel vous avez autorisé l’accès dans *[!DNL Partner Audience Manager]*.

## Identités prises en charge {#supported-identities}

[!DNL Twitter Custom Audiences] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#getting-started).

| Identité cible | Description | Considérations |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Les Google Advertising ID (GAID) et Apple ID for Advertisers (IDFA) sont pris en charge dans Adobe Experience Platform. Mappez ces espaces de noms et/ou attributs de votre schéma source en conséquence dans l’[étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) du workflow d’activation de destination. |
| E-mail | Adresse(s) e-mail de l’utilisateur | Associez vos adresses e-mail en texte brut et vos adresses e-mail hachées au format SHA256 à ce champ. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. Si vous hachez les adresses e-mail de vos clients avant de les charger vers Adobe Experience Platform, notez que ces identités doivent être hachées à l’aide de SHA256, sans sel. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Oui | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}



Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects &#x200B;](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience avec les identifiants utilisés dans la destination Audiences personnalisées de Twitter. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Twitter Custom Audiences], consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Cas d’utilisation 1

Ciblez vos abonnés et clients existants sur Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform, comme [!DNL List Custom Audiences] sur Twitter.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

1. Recherchez la destination [!DNL Twitter Custom Audiences] dans le catalogue de destinations et sélectionnez **[!UICONTROL Set Up]**.
2. Sélectionnez **[!UICONTROL Connect to destination]**.
   ![S’authentifier sur LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Saisissez vos identifiants Twitter et sélectionnez **Connexion**.

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="Identifiant de compte"
>abstract="Identifiant de votre compte Twitter Ads. Vous pouvez le trouver dans vos paramètres Twitter Ads."

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Account ID]** : identifiant de votre compte [!DNL Twitter Ads]. Vous pouvez le trouver dans vos paramètres [!DNL Twitter Ads].

>[!IMPORTANT]
>
>N’utilisez pas de caractères spéciaux (+ &amp; , % : ; @ / = ? $ \n) dans les noms de mappage d’audience, de description et d’audience. Si le nom de votre audience Experience Platform contient ces caractères, supprimez-les avant de mapper l’audience à une destination Twitter.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Considérations relatives au mappage {#mapping-considerations}

Lors du mappage d’audiences à Twitter, fournissez des noms de mappage d’audiences lisibles. Nous vous recommandons d’utiliser le même nom que celui des segments Experience Platform.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).

## Ressources supplémentaires {#additional-resources}

Vous trouverez plus d’informations sur les [!DNL List Custom Audiences] dans Twitter dans la [documentation Twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
