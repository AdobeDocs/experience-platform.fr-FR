---
keywords: 'la publicité; bing; '
title: Connexion Microsoft Bing
description: Avec la destination de connexion Microsoft Bing, vous pouvez exécuter le reciblage et l’audience des campagnes numériques ciblées sur Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 1%

---

# [!DNL Microsoft Bing] connection {#bing-destination}

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

## Type d&#39;export {#export-type}

**[!DNL Segment Export]** : vous exportez tous les membres d’un segment (audience) vers la  [!DNL Microsoft Bing] destination.

## Conditions préalables {#prerequisites}

Si vous souhaitez créer votre première destination avec [!DNL Microsoft Bing] et que vous n’avez pas activé la [fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) dans le service d’ID Experience Cloud par le passé (avec Adobe Audience Manager ou d’autres applications), contactez Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez précédemment configuré des intégrations [!DNL Microsoft Bing] dans Audience Manager, les synchronisations des identifiants que vous avez configurées sont transférées vers Platform.

Lors de la configuration de la destination, vous devez fournir les informations suivantes :

* [!UICONTROL ID] du compte : il s’agit de votre  [!DNL Bing Ads CID], au format entier.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL ID]** du compte : Votre  [!DNL Bing Ads CID].

## Activation des segments vers cette destination {#activate}

Voir [Activation des profils et des segments vers une destination](../../ui/activate-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers des destinations.

À l’étape [Planification du segment](../../ui/activate-destinations.md#segment-schedule) , vous devez mapper manuellement vos segments à leur identifiant ou nom convivial correspondant dans la destination.

Lors du mappage des segments, nous vous recommandons d’utiliser le nom du segment [!DNL Platform] ou une forme plus courte, afin de faciliter son utilisation. Cependant, l’identifiant ou le nom du segment dans votre destination ne doit pas nécessairement correspondre à celui de votre compte [!DNL Platform]. Toute valeur que vous insérez dans le champ de mappage sera répercutée par la destination.

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Microsoft Bing], vérifiez votre compte [!DNL Microsoft Bing Ads]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.
