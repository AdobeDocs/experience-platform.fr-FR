---
keywords: la publicité; le bureau de commerce; pupitre publicitaire
title: La connexion au bureau de commerce
description: Le bureau commercial est une plateforme en libre-service permettant aux acheteurs de publicités d’exécuter le reciblage et d’exécuter des campagnes numériques ciblées sur l’affichage, la vidéo et les sources d’inventaire mobiles.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 169a7ad1adfa3282bd0503ce277373b654ec57cd
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 2%

---

# [!DNL The Trade Desk] connection

## Présentation {#overview}

[!DNL The Trade Desk] la destination vous aide à envoyer des données de profil à [!DNL The Trade Desk].

[!DNL The Trade Desk] est une plateforme en libre-service permettant aux acheteurs d’annonces publicitaires d’exécuter un reciblage et d’exécuter des campagnes numériques ciblées sur l’ensemble des sources d’inventaire Display, Video et Mobile.

Pour envoyer des données de profil à [!DNL Trade Desk], vous devez d’abord vous connecter à la destination.

## Cas d’utilisation {#use-cases}

En tant que marketeur, je souhaite pouvoir utiliser des segments reposant sur [!DNL Trade Desk IDs] ou des identifiants d’appareil pour créer un reciblage ou des campagnes numériques ciblées.

## Identités prises en charge {#supported-identities}

[!DNL The Trade Desk] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Description |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| ID de bureau commercial | Identifiant publicitaire sur la plateforme Trade Desk |

## Type d&#39;export {#export-type}

**[!DNL Segment export]** : vous exportez tous les membres d’un segment (audience) vers la destination.

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec [!DNL The Trade Desk] et n’ont pas activé la variable [Fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) dans le service d’ID Experience Cloud par le passé (avec Adobe Audience Manager ou d’autres applications), veuillez contacter Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez déjà configuré [!DNL The Trade Desk] intégrations dans Audience Manager, les synchronisations d’ID que vous avez configurées sont transférées à Platform.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Identifiant de compte]**: Votre [!DNL Trade Desk] [!UICONTROL Identifiant de compte].
* **[!UICONTROL Emplacement du serveur]**: Demandez à votre [!DNL Trade Desk] représente le serveur régional que vous devez utiliser. Il s’agit des serveurs régionaux disponibles :
   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapour]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL Amérique du Nord Est]**
   * **[!UICONTROL Amérique du Nord Ouest]**
   * **[!UICONTROL Amérique latine]**

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers des destinations d’exportation de segments par flux](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

Dans le [Planification du segment](../../ui/activate-segment-streaming-destinations.md#scheduling) , vous devez mapper manuellement vos segments à leur identifiant ou nom convivial correspondant dans la plateforme de destination.

Lors du mappage des segments, nous vous recommandons d’utiliser le nom du segment Platform ou une forme plus courte de celui-ci, afin de faciliter son utilisation. Cependant, l’identifiant ou le nom du segment dans votre destination ne doit pas nécessairement correspondre à celui de votre compte Platform. Toute valeur que vous insérez dans le champ de mappage sera répercutée par la destination.

Si vous utilisez plusieurs mappages d’appareils (identifiants de cookie), [!DNL IDFA], [!DNL GAID]), veillez à utiliser la même valeur de mappage pour les trois mappages. [!DNL The Trade Desk] les combinent toutes dans un seul segment, avec une ventilation au niveau de l’appareil.

![Identifiant de mappage de segment](../../assets/common/segment-mapping-id.png)

## Données exportées {#exported-data}

Vérification de la réussite de l’exportation des données vers [!DNL The Trade Desk] destination, vérifiez votre [!DNL Trade Desk] compte . Si l’activation a réussi, les audiences sont renseignées dans votre compte.
