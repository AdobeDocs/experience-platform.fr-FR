---
keywords: la publicité;
title: Connexion Microsoft Bing
description: Avec la destination de connexion Microsoft Bing, vous pouvez exécuter le reciblage et l’audience de campagnes numériques ciblées sur l’ensemble du réseau Microsoft Advertising, y compris la publicité display, la recherche et les campagnes natives.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 52%

---

# Connexion [!DNL Microsoft Bing] {#bing-destination}

## Présentation {#overview}

Utilisez la variable [!DNL Microsoft Bing] destination pour envoyer les données de profil à l’ensemble de [!DNL Microsoft Advertising Network], y compris [!DNL Display Advertising], [!DNL Search], et [!DNL Native].

La variable [!DNL Microsoft Bing] création de destination *[!DNL Custom Audiences]* dans Microsoft. Elles sont disponibles dans les deux [!DNL Microsoft Search Network] et [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]) comme indiqué dans la variable [Documentation Microsoft Advertising](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Pour envoyer des données de profil à [!DNL Microsoft Bing], vous devez d’abord vous connecter à la destination.

## Cas d’utilisation {#use-cases}

En tant que marketeur, je souhaite pouvoir utiliser des audiences composées de [!DNL Microsoft Advertising IDs] pour cibler les utilisateurs par le biais de publicités display ou de recherche sur plusieurs [!DNL Microsoft Advertising] canaux.

## Identités prises en charge {#supported-identities}

[!DNL Microsoft Bing] prend en charge l’activation des audiences en fonction des identités affichées dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité | Description |
|---|---|
| MAID | MICROSOFT ADVERTISING ID |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

**[!DNL Audience Export]** : vous exportez tous les membres d’une audience vers le [!DNL Microsoft Bing] destination.

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience vers le [!DNL Microsoft Bing] destination. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec [!DNL Microsoft Bing] et n’ont pas activé la variable [fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=fr) dans le service d’ID Experience Cloud (avec Adobe Audience Manager ou d’autres applications), contactez Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez configuré précédemment des intégrations [!DNL Microsoft Bing] dans Audience Manager, les synchronisations d’identifiant que vous aviez configurées sont transférées vers Platform.

Lors de la configuration de la destination, vous devez fournir les informations suivantes :

* [!UICONTROL Identifiant de compte]: ceci est votre [!DNL Bing Ads CID], au format entier.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]** et **[!UICONTROL Gestion des destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Renseigner les détails de la destination {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant de compte]**: votre [!DNL Bing Ads Customer ID] (CID). Votre ID de client est un entier, qui se trouve dans l’URL lorsque vous vous connectez. [!DNL Microsoft Advertising].

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Identifiant de mappage"
>abstract="Saisissez l’identifiant numérique de l’audience Bing auquel vous souhaitez mapper le segment sélectionné. Si l’[!UICONTROL ID de mappage] ne correspond pas à un identifiant d’audience dans la destination Bing, vous ne verrez pas les données d’audience attendues dans votre compte Bing."

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

Dans le [Planification de l’audience](../../ui/activate-segment-streaming-destinations.md#scheduling) vous devez mapper manuellement le nom de l’audience dans la variable [!UICONTROL ID de mappage] champ . Ainsi, les métadonnées d’audience sont correctement transmises à [!DNL Bing].

![Image de l’interface utilisateur montrant l’écran de planification de l’audience avec un exemple de mappage du nom de l’audience à l’identifiant de mappage Bing.](../../assets/catalog/advertising/bing/mapping-id.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Microsoft Bing], vérifiez votre compte [!DNL Microsoft Bing Ads]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.
