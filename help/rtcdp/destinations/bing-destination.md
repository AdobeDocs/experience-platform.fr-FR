---
keywords: advertising; bing;
title: Destination Microsoft Bing
seo-title: La destination Microsoft Bing vous aide à envoyer des données de profil à Microsoft Display Advertising.
description: Avec la destination Microsoft Bing, vous pouvez exécuter des campagnes numériques ciblées de reciblage et d'audience sur l'ensemble des campagnes Microsoft Display Advertising.
seo-description: Avec la destination Microsoft Bing, vous pouvez exécuter des campagnes numériques ciblées de reciblage et d'audience sur l'ensemble des campagnes Microsoft Display Advertising.
translation-type: tm+mt
source-git-commit: a64f9f1f078d8380cc25c9760eac1699512a5870
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 6%

---


# [!DNL Microsoft Bing] destination

## Présentation {#overview}

La [!DNL Microsoft Bing] destination vous aide à envoyer des données de profil à [!DNL Microsoft Display Advertising].

Pour envoyer des données de profil à [!DNL Microsoft Bing], vous devez d&#39;abord vous connecter à la destination.

## Spécifications de la destination {#destination-specs}

Note the following details that are specific to the [!DNL Microsoft Bing] destination:

* Vous pouvez envoyer les [identités](../../identity-service/namespaces.md) suivantes vers [!DNL Microsoft Bing] les destinations : [!DNL Microsoft ID].

## Cas d’utilisation {#use-cases}

En tant que spécialiste du marketing, je souhaite pouvoir utiliser des segments conçus pour les utilisateurs de [!DNL Microsoft Advertising IDs] cible au moyen de publicités affichées sur [!DNL Microsoft Advertising] des canaux.

## Type d’exportation {#export-type}

**[!DNL Segment Export]** - vous exportez tous les membres d&#39;un segment (audience) vers la [!DNL Microsoft Bing] destination.

## Conditions préalables  {#prerequisites}

Lors de la configuration de la destination, vous devez fournir les informations suivantes :

* [!UICONTROL ID]du compte : il s&#39;agit de votre [!DNL Bing Ads CID]format entier.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL Microsoft Bing], puis **[!UICONTROL Configurer]**.

   ![Configuration de la destination Microsoft Bing](assets/bing-destination-configure.png)

   >[!NOTE]
   >
   >Si une connexion à cette destination existe déjà, un bouton **[!UICONTROL Activer]** s’affiche sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../destinations/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.
   >
   >![Activer la destination Microsoft Bing](assets/bing-destination-activate.png)

1. A l’étape [!UICONTROL Authentification] , vous devez saisir les détails de la connexion de destination :

   * **[!UICONTROL Nom]**: Nom par lequel vous reconnaîtrez cette destination dans le futur.
   * **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination dans le futur.
   * **[!UICONTROL ID]** du compte : Votre [!DNL Bing Ads CID].
   * **[!UICONTROL Cas]** d’utilisation marketing : Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation du marketing, voir la page Gouvernance des [données dans Adobe Experience Platform](../privacy/data-governance-overview.md#destinations) . Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](../../data-governance/policies/overview.md#core-actions)données.

   ![Authentification de destination Microsoft Bing](assets/bing-destination-authentication.png)

1. Cliquez sur **[!UICONTROL Créer une destination]**. Votre destination est maintenant créée. You can click [!UICONTROL Save &amp; Exit] if you want to activate segments later on, or you can click [!UICONTROL Next] to continue the workflow and select segments to activate. In either case, see the next section, [Activate Segments](#activate-segments), for the rest of the workflow.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](activate-destinations.md#select-attributes).

À l’étape de planification [](activate-destinations.md#segment-schedule) des segments, vous devez mapper manuellement vos segments à leur identifiant ou nom convivial correspondant dans la destination.

Lors du mappage de segments, nous vous recommandons d’utiliser le nom du [!DNL Platform] segment ou une forme plus courte de celui-ci, afin de faciliter son utilisation. Cependant, l’ID ou le nom du segment dans votre destination ne doit pas nécessairement correspondre à celui de votre [!DNL Platform] compte. Toute valeur que vous insérez dans le champ de mappage est répercutée par la destination.

![ID de mappage de segments](assets/segment-mapping-id.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la [!DNL Microsoft Bing] destination, vérifiez votre [!DNL Microsoft Bing Ads] compte. Si l’activation a réussi, les audiences sont renseignées dans votre compte.