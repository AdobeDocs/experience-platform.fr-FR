---
keywords: publicité, bureau de commerce, bureau de publicité
title: Connexion à The Trade Desk
description: Le bureau commercial est une plateforme en libre-service permettant aux acheteurs de publicités d’exécuter le reciblage et d’exécuter des campagnes numériques ciblées sur l’affichage, la vidéo et les sources d’inventaire mobiles.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 41%

---

# Connexion [!DNL The Trade Desk]

## Présentation {#overview}

La destination [!DNL The Trade Desk] vous aide à envoyer des données de profil à [!DNL The Trade Desk].

[!DNL The Trade Desk] est une plateforme en libre-service permettant aux acheteurs de publicités d’exécuter le reciblage et d’exécuter des campagnes numériques ciblées sur l’affichage, la vidéo et les sources d’inventaire mobiles.

Pour envoyer des données de profil à [!DNL Trade Desk], vous devez d’abord vous connecter à la destination.

## Cas d’utilisation {#use-cases}

En tant que marketeur, je souhaite pouvoir utiliser des audiences créées à partir de [!DNL Trade Desk IDs] ou des identifiants d’appareil pour créer un reciblage ou des campagnes numériques ciblées d’audience.

## Identités prises en charge {#supported-identities}

[!DNL The Trade Desk] prend en charge l’activation des audiences en fonction des identités affichées dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité | Description |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| ID de bureau commercial | Identifiant publicitaire sur la plateforme Trade Desk |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience vers la destination. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec [!DNL The Trade Desk] et que vous n’avez pas activé par le passé la [fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=fr) dans le service d’ID Experience Cloud (avec Adobe Audience Manager ou d’autres applications), contactez Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez configuré précédemment des intégrations [!DNL The Trade Desk] dans Audience Manager, les synchronisations d’identifiant que vous aviez configurées sont transférées vers Platform.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL ID de compte]** : votre [!DNL Trade Desk] [!UICONTROL ID de compte].
* **[!UICONTROL Emplacement du serveur]** : demandez à votre représentant [!DNL Trade Desk] quel serveur régional vous devriez utiliser. Il s’agit des serveurs régionaux disponibles :
   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapour]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL Amérique du Nord-Est]**
   * **[!UICONTROL Amérique du Nord Ouest]**
   * **[!UICONTROL Amérique latine]**

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

À l’étape [Planification de l’audience](../../ui/activate-segment-streaming-destinations.md#scheduling), vous devez mapper manuellement vos audiences à leur identifiant ou nom convivial correspondant dans la plateforme de destination.

Lors du mappage des segments, nous vous recommandons d’utiliser le nom de l’audience Platform ou une forme plus courte de celui-ci, afin de faciliter son utilisation. Toutefois, l’ID ou le nom de l’audience dans votre destination ne doit pas nécessairement correspondre à celui de votre compte Platform. Toute valeur que vous insérez dans le champ de mappage sera répercutée par la destination.

Si vous utilisez plusieurs mappages d’appareils (identifiants de cookie, [!DNL IDFA], [!DNL GAID]), veillez à utiliser la même valeur de mappage pour les trois mappages. [!DNL The Trade Desk] les agrégera tous en un seul segment, avec une ventilation au niveau de l’appareil.

![Identifiant de mappage de segment](../../assets/common/segment-mapping-id.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL The Trade Desk], vérifiez votre compte [!DNL Trade Desk]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.
