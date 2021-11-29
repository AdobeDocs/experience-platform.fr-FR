---
keywords: 'la publicité; bing; '
title: Connexion à Microsoft Bing
description: Avec la destination de connexion Microsoft Bing, vous pouvez exécuter le reciblage et l’audience des campagnes numériques ciblées dans Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 169a7ad1adfa3282bd0503ce277373b654ec57cd
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 1%

---

# [!DNL Microsoft Bing] connection {#bing-destination}

## Présentation {#overview}

Le [!DNL Microsoft Bing] la destination vous aide à envoyer des données de profil à [!DNL Microsoft Display Advertising].

Pour envoyer des données de profil à [!DNL Microsoft Bing], vous devez d’abord vous connecter à la destination.

## Cas d’utilisation {#use-cases}

En tant que marketeur, je souhaite pouvoir utiliser des segments reposant sur [!DNL Microsoft Advertising IDs] pour cibler les utilisateurs via des publicités display à l’échelle de [!DNL Microsoft Advertising] canaux.

## Identités prises en charge {#supported-identities}

[!DNL Microsoft Bing] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Description |
|---|---|
| MAID | Microsoft Advertising ID |

## Type d&#39;export {#export-type}

**[!DNL Segment Export]** : vous exportez tous les membres d’un segment (audience) vers le [!DNL Microsoft Bing] destination.

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec [!DNL Microsoft Bing] et n’ont pas activé la variable [Fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) dans le service d’ID Experience Cloud par le passé (avec Adobe Audience Manager ou d’autres applications), veuillez contacter Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez déjà configuré [!DNL Microsoft Bing] intégrations dans Audience Manager, les synchronisations d’ID que vous avez configurées sont transférées à Platform.

Lors de la configuration de la destination, vous devez fournir les informations suivantes :

* [!UICONTROL Identifiant de compte]: ceci est votre [!DNL Bing Ads CID], au format entier.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Identifiant de compte]**: Votre [!DNL Bing Ads CID].

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers des destinations d’exportation de segments par flux](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

Dans le [Planification du segment](../../ui/activate-segment-streaming-destinations.md#scheduling) , vous devez mapper manuellement vos segments à leur identifiant ou nom convivial correspondant dans la destination.

Lors du mappage des segments, nous vous recommandons d’utiliser la variable [!DNL Platform] nom du segment ou une forme plus courte de celui-ci, pour en faciliter l’utilisation. Cependant, l’identifiant ou le nom du segment dans votre destination ne doit pas nécessairement correspondre à celui de votre [!DNL Platform] compte . Toute valeur que vous insérez dans le champ de mappage sera répercutée par la destination.

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la variable [!DNL Microsoft Bing] destination, vérifiez votre [!DNL Microsoft Bing Ads] compte . Si l’activation a réussi, les audiences sont renseignées dans votre compte.
