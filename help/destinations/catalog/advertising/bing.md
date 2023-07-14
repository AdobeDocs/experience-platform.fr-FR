---
keywords: la publicité; bing;
title: Connexion Microsoft Bing
description: Avec la destination de connexion Microsoft Bing, vous pouvez exécuter le reciblage et l’audience des campagnes numériques ciblées dans Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 1c9725c108d55aea5d46b086fbe010ab4ba6cf45
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 45%

---

# Connexion [!DNL Microsoft Bing] {#bing-destination}

## Présentation {#overview}

Le [!DNL Microsoft Bing] la destination vous aide à envoyer des données de profil à [!DNL Microsoft Display Advertising].

Pour envoyer des données de profil à [!DNL Microsoft Bing], vous devez d’abord vous connecter à la destination.

## Cas d’utilisation {#use-cases}

En tant que marketeur, je souhaite pouvoir utiliser des audiences composées de [!DNL Microsoft Advertising IDs] pour cibler les utilisateurs via des publicités display à l’échelle de [!DNL Microsoft Advertising] canaux.

## Identités prises en charge {#supported-identities}

[!DNL Microsoft Bing] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description |
|---|---|
| MAID | Microsoft Advertising ID |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit toutes les audiences que vous pouvez exporter vers cette destination.

Toutes les destinations prennent en charge l’activation des audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md).

En outre, cette destination prend également en charge l’activation des audiences décrites dans le tableau ci-dessous.

| Type d’audience | Description |
---------|----------|
| Chargements personnalisés | Audiences ingérées dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

**[!DNL Audience Export]** : vous exportez tous les membres d’une audience vers le [!DNL Microsoft Bing] destination.

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation de l’audience]** | Vous exportez tous les membres d’une audience vers le [!DNL Microsoft Bing] destination. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu&#39;un profil est mis à jour en Experience Platform en fonction de l&#39;évaluation de l&#39;audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec [!DNL Microsoft Bing] et n’ont pas activé la variable [Fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=fr) dans le service d’ID Experience Cloud par le passé (avec Adobe Audience Manager ou d’autres applications), veuillez contacter Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez configuré précédemment des intégrations [!DNL Microsoft Bing] dans Audience Manager, les synchronisations d’identifiant que vous aviez configurées sont transférées vers Platform.

Lors de la configuration de la destination, vous devez fournir les informations suivantes :

* [!UICONTROL Identifiant de compte]: ceci est votre [!DNL Bing Ads CID], au format entier.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant de compte]**: Votre [!DNL Bing Ads Customer ID] (CID). Votre ID de client est un entier, qui se trouve dans l’URL lorsque vous vous connectez. [!DNL Microsoft Advertising].

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer les audiences vers cette destination {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Identifiant de mappage"
>abstract="Saisissez l’ID d’audience Bing numérique auquel vous souhaitez mapper le segment sélectionné. Si la variable [!UICONTROL ID de mappage] ne correspond pas à un ID d’audience dans la destination Bing. Vous ne verrez pas les données d’audience attendues dans votre compte Bing."

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation d’audience par flux](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

Dans le [Planification de l’audience](../../ui/activate-segment-streaming-destinations.md#scheduling) vous devez mapper manuellement le nom de l’audience dans la variable [!UICONTROL ID de mappage] champ . Ainsi, les métadonnées d’audience sont correctement transmises à [!DNL Bing].

![Image de l’interface utilisateur montrant l’écran de planification de l’audience avec un exemple de mappage du nom de l’audience à l’identifiant de mappage Bing.](../../assets/catalog/advertising/bing/mapping-id.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Microsoft Bing], vérifiez votre compte [!DNL Microsoft Bing Ads]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.
