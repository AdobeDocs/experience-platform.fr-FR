---
keywords: la publicité; bing;
title: Connexion Microsoft Bing
description: Avec la destination de connexion Microsoft Bing, vous pouvez exécuter le reciblage et l’audience des campagnes numériques ciblées dans Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: aec9708680c2a4cb3c70af12f95c67ec37b2e129
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 13%

---

# Connexion [!DNL Microsoft Bing] {#bing-destination}

## Présentation {#overview}

Le [!DNL Microsoft Bing] la destination vous aide à envoyer des données de profil à [!DNL Microsoft Display Advertising].

Pour envoyer des données de profil à [!DNL Microsoft Bing], vous devez d’abord vous connecter à la destination.

## Cas d&#39;utilisation {#use-cases}

En tant que marketeur, je souhaite pouvoir utiliser des segments reposant sur [!DNL Microsoft Advertising IDs] pour cibler les utilisateurs via des publicités display à l’échelle de [!DNL Microsoft Advertising] canaux.

## Identités prises en charge {#supported-identities}

[!DNL Microsoft Bing] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Description |
|---|---|
| MAID | Microsoft Advertising ID |

{style=&quot;table-layout:auto&quot;}

## Type et fréquence d&#39;export {#export-type-frequency}

**[!DNL Segment Export]** : vous exportez tous les membres d’un segment (audience) vers le [!DNL Microsoft Bing] destination.

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) vers le [!DNL Microsoft Bing] destination. |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec [!DNL Microsoft Bing] et n’ont pas activé la variable [Fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) dans le service d’ID Experience Cloud par le passé (avec Adobe Audience Manager ou d’autres applications), veuillez contacter Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez déjà configuré [!DNL Microsoft Bing] intégrations dans Audience Manager, les synchronisations d’ID que vous avez configurées sont transférées à Platform.

Lors de la configuration de la destination, vous devez fournir les informations suivantes :

* [!UICONTROL Identifiant de compte]: ceci est votre [!DNL Bing Ads CID], au format entier.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Identifiant de compte]**: Votre [!DNL Bing Ads Customer ID] (CID). Votre ID de client est un entier, qui se trouve dans l’URL lorsque vous vous connectez. [!DNL Microsoft Advertising].

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur l’état du flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de fournir des détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Identifiant de mappage"
>abstract="Saisissez l’identifiant numérique du segment Bing auquel vous souhaitez mapper le segment sélectionné. Si la variable [!UICONTROL ID de mappage] ne correspond pas à un identifiant de segment dans la destination Bing. Vous ne verrez pas les données d’audience attendues dans votre compte Bing."

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de segments par flux](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

Dans le [Planification du segment](../../ui/activate-segment-streaming-destinations.md#scheduling) , vous devez mapper manuellement le nom du segment dans la variable [!UICONTROL ID de mappage] champ . Cela permet de s’assurer que les métadonnées de segment sont correctement transmises à [!DNL Bing].

![Image de l’interface utilisateur montrant l’écran de planification des segments avec un exemple de mappage du nom du segment à l’identifiant de mappage Bing.](../../assets/catalog/advertising/bing/mapping-id.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la variable [!DNL Microsoft Bing] destination, vérifiez votre [!DNL Microsoft Bing Ads] compte . Si l’activation a réussi, les audiences sont renseignées dans votre compte.
