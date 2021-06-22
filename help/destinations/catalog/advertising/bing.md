---
keywords: 'la publicité; bing; '
title: Connexion Microsoft Bing
description: Avec la destination de connexion Microsoft Bing, vous pouvez exécuter le reciblage et l’audience des campagnes numériques ciblées sur Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 2931efa6f67a042255fb1d31c0683f73d817b55b
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 5%

---

# [!DNL Microsoft Bing] connection  {#bing-destination}

## Présentation {#overview}

La destination [!DNL Microsoft Bing] vous aide à envoyer des données de profil à [!DNL Microsoft Display Advertising].

Pour envoyer des données de profil à [!DNL Microsoft Bing], vous devez d’abord vous connecter à la destination.

## Cas d&#39;utilisation {#use-cases}

En tant que marketeur, je souhaite pouvoir utiliser des segments créés à partir de [!DNL Microsoft Advertising IDs] pour cibler les utilisateurs par le biais de publicités display sur les canaux [!DNL Microsoft Advertising].

## Identités prises en charge {#supported-identities}

[!DNL Microsoft Bing] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description |
|---|---|
| MAID | Microsoft Advertising ID |

## Type d’exportation {#export-type}

**[!DNL Segment Export]** : vous exportez tous les membres d’un segment (audience) vers la  [!DNL Microsoft Bing] destination.

## Conditions préalables {#prerequisites}

Si vous souhaitez créer votre première destination avec [!DNL Microsoft Bing] et que vous n’avez pas activé la [fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) dans le service d’ID Experience Cloud par le passé (avec Adobe Audience Manager ou d’autres applications), contactez Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez précédemment configuré des intégrations [!DNL Microsoft Bing] dans Audience Manager, les synchronisations des identifiants que vous avez configurées sont transférées vers Platform.

Lors de la configuration de la destination, vous devez fournir les informations suivantes :

* [!UICONTROL ID] du compte : il s’agit de votre  [!DNL Bing Ads CID], au format entier.

## Se connecter à la destination {#connect-destination}

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL Microsoft Bing], puis **[!UICONTROL Configurer]**.

![Configuration de la destination Microsoft Bing](../../assets/catalog/advertising/bing/configure.png)

Si une connexion avec cette destination existe déjà, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d’informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l’espace de travail de destination.

![Activation de la destination Microsoft Bing](../../assets/catalog/advertising/bing/activate.png)

## Étape d’authentification {#authentication}

À l’étape **[!UICONTROL Authentification]**, vous devez saisir les détails de la connexion de destination :

* **[!UICONTROL Nom]** : Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL ID]** du compte : Votre  [!DNL Bing Ads CID].
* **[!UICONTROL Action]** marketing : Les actions marketing indiquent l’intention pour laquelle les données seront exportées vers la destination. Vous pouvez effectuer un choix parmi des actions marketing définies par l’Adobe ou créer votre propre action marketing. Pour plus d’informations sur les actions marketing, consultez la page [Gouvernance des données dans Adobe Experience Platform](../../../data-governance/policies/overview.md) . Pour plus d’informations sur les actions marketing définies par l’Adobe, consultez la [Présentation des stratégies d’utilisation des données](../../../data-governance/policies/overview.md).

![Authentification de destination Microsoft Bing](../../assets/catalog/advertising/bing/authentication.png)

Cliquez sur **[!UICONTROL Créer une destination]**. Votre destination est maintenant créée. Vous pouvez cliquer sur [!UICONTROL Enregistrer et quitter] si vous souhaitez activer les segments ultérieurement. Vous pouvez également cliquer sur [!UICONTROL Suivant] pour poursuivre le workflow et sélectionner les segments à activer. Dans les deux cas, reportez-vous à la section suivante, [Activate Segments](#activate-segments), pour le reste du workflow.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](../../ui/activate-destinations.md#select-attributes).

À l’étape [Planification du segment](../../ui/activate-destinations.md#segment-schedule) , vous devez mapper manuellement vos segments à leur identifiant ou nom convivial correspondant dans la destination.

Lors du mappage des segments, nous vous recommandons d’utiliser le nom du segment [!DNL Platform] ou une forme plus courte, afin de faciliter son utilisation. Cependant, l’identifiant ou le nom du segment dans votre destination ne doit pas nécessairement correspondre à celui de votre compte [!DNL Platform]. Toute valeur que vous insérez dans le champ de mappage sera répercutée par la destination.

![Identifiant de mappage de segment](../../assets/common/segment-mapping-id.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Microsoft Bing], vérifiez votre compte [!DNL Microsoft Bing Ads]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.
