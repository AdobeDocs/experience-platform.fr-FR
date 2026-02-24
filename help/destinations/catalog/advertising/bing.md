---
keywords: publicité ; bing ;
title: Connexion Microsoft Bing
description: Avec la destination de connexion Microsoft Bing, vous pouvez exécuter des campagnes numériques de reciblage et d’audience ciblées sur l’ensemble du réseau Microsoft Advertising, y compris l’affichage publicitaire, la recherche et le natif.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 26%

---

# Connexion [!DNL Microsoft Bing] {#bing-destination}

## Vue d’ensemble {#overview}

Utilisez la destination [!DNL Microsoft Bing] pour envoyer des données de profil à l’ensemble du [!DNL Microsoft Advertising Network], y compris [!DNL Display Advertising], [!DNL Search] et [!DNL Native].

La destination [!DNL Microsoft Bing] crée des *[!DNL Custom Audiences]* dans Microsoft. Ils sont disponibles dans les [!DNL Microsoft Search Network] et [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]), comme indiqué dans la documentation Microsoft Advertising [](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Pour envoyer des données de profil à [!DNL Microsoft Bing], vous devez d’abord vous connecter à la destination .

## Cas d’utilisation {#use-cases}

En tant que spécialiste marketing, je souhaite pouvoir utiliser des audiences créées à partir de [!DNL Microsoft Advertising IDs] pour cibler les utilisateurs et utilisatrices par le biais de publicités display ou search sur plusieurs canaux [!DNL Microsoft Advertising].

## Identités prises en charge {#supported-identities}

[!DNL Microsoft Bing] prend en charge l’activation des audiences en fonction des identités présentées dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

Toutes les identités du tableau ci-dessous sont préconfigurées et automatiquement mappées lors de l’activation. Vous n’avez pas besoin de configurer manuellement ces mappages.

| Identité | Description | Considérations |
|---|---|---|
| MAID | MICROSOFT ADVERTISING ID | Activé lorsqu’un Microsoft Advertising ID est présent sur le profil. |
| ECID | Experience Cloud ID | **Obligatoire.** Tous les profils doivent disposer d’un ECID avec un mappage d’Advertising ID Microsoft correspondant à exporter. |

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
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

**[!DNL Audience Export]** - vous exportez tous les membres d’une audience vers la destination [!DNL Microsoft Bing].

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience vers la destination [!DNL Microsoft Bing]. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

La destination [!DNL Microsoft Bing] nécessite la configuration suivante pour fonctionner correctement :

1. **Activer la fonctionnalité de synchronisation des identifiants** : si c’est la première fois que vous configurez [!DNL Microsoft Bing] activation et que vous n’avez pas activé la fonctionnalité de synchronisation des [identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=fr) dans le service Experience Cloud ID dans le passé (avec Adobe Audience Manager ou d’autres applications), contactez Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants.
   * Si vous avez configuré précédemment des intégrations [!DNL Microsoft Bing] dans Audience Manager, les synchronisations des identifiants existantes sont automatiquement transférées vers Experience Platform.

2. **Assurez-vous que l’ECID est présent sur les profils** : tous les profils doivent avoir un ECID présent pour pouvoir être exportés. L’ECID est **obligatoire** pour cette destination.

Lors de la configuration de la destination, vous devez fournir les informations suivantes :

* [!UICONTROL Account ID] : il s’agit de votre [!DNL Bing Ads CID], au format entier.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Renseigner les détails de la destination {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Account ID]** : votre [!DNL Bing Ads Customer ID] (CID). Votre CID est un entier qui se trouve dans l’URL lorsque vous vous connectez à [!DNL Microsoft Advertising].

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Identifiant de mappage"
>abstract="Saisissez l’identifiant numérique de l’audience Bing auquel vous souhaitez mapper le segment sélectionné. Si le [!UICONTROL Mapping ID] fourni ne correspond pas à un ID d&#39;audience dans la destination Bing, vous ne verrez pas les données d&#39;audience attendues dans votre compte Bing."

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_bing"
>title="Jeux de mappages préconfigurés"
>abstract="Nous avons préconfiguré ces deux jeux de mappages pour vous. Lorsque vous activez des données vers Microsoft Bing, les profils qualifiés pour les audiences activées doivent avoir au moins une identité ECID associée à leur profil, afin de pouvoir être exportés vers la destination."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/bing#preconfigured-mappings" text="En savoir plus sur les mappages préconfigurés"

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

Dans l’étape [Planning des audiences](../../ui/activate-segment-streaming-destinations.md#scheduling), vous devez mapper manuellement le nom de l’audience dans le champ [!UICONTROL Mapping ID]. Cela permet de s’assurer que les métadonnées d’audience sont correctement transmises à [!DNL Bing].

![Image de l’interface utilisateur affichant l’écran du planning d’audience avec un exemple de la manière de mapper le nom de l’audience à l’identifiant de mappage Bing.](../../assets/catalog/advertising/bing/mapping-id.png)

### Mappages préconfigurés {#preconfigured-mappings}

Les mappages d’identité suivants sont **préconfigurés et automatiquement renseignés** pendant le workflow d’activation de l’audience :

* **MAID** (Microsoft Advertising ID)
* **ECID** (Experience Cloud ID)

Ces mappages sont grisés et en lecture seule. Dans cette étape, vous n’avez rien à configurer. Sélectionnez **[!UICONTROL Next]** pour continuer.

>[!IMPORTANT]
>
>**ECID est requis pour que l’exportation réussisse.** Les profils sans ECID ou sans mappage de synchronisation des identifiants entre ECID et l’Advertising ID Microsoft ne seront pas exportés.

### Exemples d’activation

* **Profil avec mappage ECID et Microsoft Advertising ID :** le profil a bien été exporté et activé
* **Profil avec ECID uniquement (pas de mappage Microsoft Advertising ID) :** profil n’est **pas exporté**. Le mappage de synchronisation des identifiants entre ECID et MAID est obligatoire.
* **Profil sans ECID :** le profil n’est **pas exporté**. L’ECID est obligatoire pour cette destination.

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Microsoft Bing], vérifiez votre compte [!DNL Microsoft Bing Ads]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.
