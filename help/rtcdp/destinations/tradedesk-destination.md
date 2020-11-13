---
keywords: advertising; the trade desk;
title: Destination du bureau de commerce
seo-title: Destination du bureau de commerce
description: 'Le Trade Desk est une plate-forme en libre-service permettant aux acheteurs d''annonces publicitaires d''exécuter des reciblages et d''audience de campagnes numériques ciblées à l''échelle de l''affichage, de la vidéo et des sources d''inventaire mobiles. '
seo-description: Le Trade Desk est une plate-forme en libre-service permettant aux acheteurs d'annonces publicitaires d'exécuter des reciblages et d'audience de campagnes numériques ciblées à l'échelle de l'affichage, de la vidéo et des sources d'inventaire mobiles.
translation-type: tm+mt
source-git-commit: c9fb63b390d4c7dddcdb35a85710ff664614ad63
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 5%

---


# [!DNL The Trade Desk] destination

## Présentation {#overview}

[!DNL The Trade Desk] destination vous aide à envoyer des données de profil à [!DNL The Trade Desk].

[!DNL The Trade Desk] est une plateforme en libre-service permettant aux acheteurs d’annonces publicitaires d’exécuter des reciblages et d’audience de campagnes numériques ciblées sur l’affichage, la vidéo et les sources d’inventaire mobiles.

Pour envoyer des données de profil à [!DNL The Trade Desk], vous devez d&#39;abord vous connecter à la destination.

## Spécifications de la destination {#destination-specs}

Note the following details that are specific to the [!DNL The Trade Desk] destination:

* Vous pouvez envoyer les [identités](../../identity-service/namespaces.md) suivantes vers [!DNL The Trade Desk] les destinations : [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

## Cas d’utilisation {#use-cases}

En tant que spécialiste du marketing, je souhaite pouvoir utiliser des segments créés à partir d’identifiants [!DNL Trade Desk IDs] ou d’appareils pour créer des campagnes numériques ciblées de reciblage ou d’audience.

## Type d’exportation {#export-type}

**[!DNL Segment export]** - vous exportez tous les membres d&#39;un segment (audience) vers la destination.

## Se connecter à la destination {#connect-destination}

1. Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL The Trade Desk], puis **[!UICONTROL Configurer]**.

   ![Configuration de la destination du bureau de commerce](assets/tradedesk-destination-configure.png)

   >[!NOTE]
   >
   >Si une connexion à cette destination existe déjà, un bouton **[!UICONTROL Activer]** s’affiche sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../destinations/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.
   >
   >![Activer la destination du bureau de commerce](assets/tradedesk-destination-activate.png)

1. A l’étape [!UICONTROL Authentification] , vous devez entrer les détails de [!DNL The Trade Desk] connexion :

   * **[!UICONTROL Nom]**: Nom par lequel vous reconnaîtrez cette destination dans le futur.
   * **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination dans le futur.
   * **[!UICONTROL ID]** du compte : ID [!DNL Trade Desk] de votre compte.
   * **[!UICONTROL Secret]** client : Paramètre `clientSecret` utilisé dans les informations d’identification du [!DNL OAuth2] client.
   * **[!UICONTROL Emplacement]** du serveur : Demandez à votre [!DNL The Trade Desk] représentant quel serveur régional vous devez utiliser. Voici les serveurs régionaux disponibles :

      * **[!UICONTROL Europe]**
      * **[!UICONTROL Singapour]**
      * **[!UICONTROL Tokyo]**
      * **[!UICONTROL Amérique du Nord Est]**
      * **[!UICONTROL Amérique du Nord Ouest]**
      * **[!UICONTROL Amérique latine]**
   * **[!UICONTROL Cas]** d’utilisation marketing : Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation du marketing, voir la page Gouvernance des [données dans Adobe Experience Platform](../privacy/data-governance-overview.md#destinations) . Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](../../data-governance/policies/overview.md#core-actions)données.

   ![Étape d&#39;authentification du bureau de commerce](assets/tradedesk-destination-authentication.png)

1. Cliquez sur **[!UICONTROL Créer une destination]**. Votre destination est maintenant créée. You can click [!UICONTROL Save &amp; Exit] if you want to activate segments later, or you can select [!UICONTROL Next] to continue the workflow and select segments to activate. In either case, see the next section, [Activate Segments](#activate-segments), for the rest of the workflow.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](activate-destinations.md#select-attributes).

Au cours de l’étape de planification [du](activate-destinations.md#segment-schedule) segment, vous devez mapper manuellement vos segments à leur identifiant ou nom convivial correspondant dans la destination.

Lors du mappage de segments, nous vous recommandons d’utiliser le nom du [!DNL Platform] segment ou une forme plus courte de celui-ci, afin de faciliter son utilisation. Cependant, l’ID ou le nom du segment dans votre destination ne doit pas nécessairement correspondre à celui de votre [!DNL Platform] compte. Toute valeur que vous insérez dans le champ de mappage est répercutée par la destination.

Si vous utilisez plusieurs mappages de périphériques (identifiants de cookie, [!DNL IDFA], [!DNL GAID]), veillez à utiliser la même valeur de mappage pour les trois mappages. [!DNL The Trade Desk] les agrégat tous dans un seul segment, avec une ventilation au niveau du périphérique.

![ID de mappage de segments](assets/segment-mapping-id.png)


## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers [!DNL The Trade Desk] la destination, vérifiez votre [!DNL The Trade Desk] compte. Si l’activation a réussi, les audiences sont renseignées dans votre compte.
