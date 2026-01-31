---
keywords: publicité ; trade desk ; advertising trade desk
title: Connexion à The Trade Desk
description: Trade Desk est une plateforme en libre-service permettant aux acheteurs de publicités d’exécuter des campagnes numériques de reciblage et de ciblage d’audience sur des sources d’affichage, de vidéo et d’inventaire mobile.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 138bfe721bb20fe3ba614a73ffffca3e00979acb
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 22%

---

# Connexion [!DNL The Trade Desk]

## Vue d’ensemble {#overview}

Utilisez ce connecteur de destination pour envoyer des données de profil à [!DNL The Trade Desk]. Ce connecteur envoie des données au point d’entrée propriétaire [!DNL The Trade Desk]. L’intégration entre Adobe Experience Platform et [!DNL The Trade Desk] ne prend pas en charge l’exportation de données vers le point d’entrée tiers [!DNL The Trade Desk].

[!DNL The Trade Desk] est une plateforme en libre-service permettant aux acheteurs d’annonces publicitaires d’exécuter des campagnes numériques de reciblage et de ciblage d’audience sur des sources d’affichage, de vidéo et d’inventaire mobile.

Pour envoyer des données de profil à [!DNL The Trade Desk], vous devez d’abord vous connecter à la destination, comme décrit dans les sections suivantes de cette page.

## Cas d’utilisation {#use-cases}

En tant que spécialiste marketing, je souhaite pouvoir utiliser des audiences créées à partir d’[!DNL Trade Desk IDs] ou d’identifiants d’appareil pour créer des campagnes numériques de reciblage ou de ciblage d’audience.

## Identités prises en charge {#supported-identities}

[!DNL The Trade Desk] prend en charge l’activation des audiences en fonction des identités présentées dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

Vous trouverez ci-dessous les identités prises en charge par [!DNL The Trade Desk] destination. Ces identités peuvent être utilisées pour activer des audiences à [!DNL The Trade Desk].

Toutes les identités du tableau ci-dessous sont préconfigurées et automatiquement mappées lors de l’activation. Vous n’avez pas besoin de configurer manuellement ces mappages dans le workflow d’activation.

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Activé lorsqu’un GAID est présent sur le profil. |
| IDFA | Identifiant Apple pour les annonceurs | Activé lorsqu’un IDFA est présent sur le profil. |
| ECID | Experience Cloud ID | Un espace de noms représentant l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Lisez le document suivant sur [ECID](/help/identity-service/features/ecid.md) pour plus d’informations. |
| [!DNL Tradedesk] | [!DNL TDID] dans la plateforme [!DNL The Trade Desk] | Activé lorsqu’un profil possède un ECID et qu’il existe un mappage ECID vers ID de bureau d’échanges dans Experience Platform. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience vers la destination . |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

Les conditions préalables dépendent des types d’identité que vous prévoyez d’utiliser pour l’activation de l’audience :

**Pour l’activation des ID mobiles uniquement** il n’y a pas de conditions préalables. Tant que vous collectez et gérez des identifiants (GAID et/ou IDFA) pour vos clients, vous pouvez commencer à activer les audiences sur [!DNL The Trade Desk].

**Pour le ciblage basé sur les cookies sur[!DNL The Trade Desk]**, assurez-vous qu’un mappage entre ECID et [!DNL Trade Desk ID] est établi. Procédez comme suit :

1. **Activer la fonctionnalité de synchronisation des identifiants** : si c’est la première fois que vous configurez [!DNL The Trade Desk ID] activation et que vous n’avez pas activé la fonctionnalité de synchronisation des [identifiants](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/idsync) dans le service Experience Cloud ID dans le passé (avec Adobe Audience Manager ou d’autres applications), contactez Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants.
   * Si vous avez précédemment configuré des intégrations [!DNL The Trade Desk] dans Audience Manager, les synchronisations d’identifiant existantes sont automatiquement transférées vers Experience Platform.

2. **Instrumenter vos pages web** : implémentez du code sur vos pages web pour créer des mappages entre [!DNL The Trade Desk ID] et l’ECID Adobe. Experience Platform peut ainsi associer des identifiants Trade Desk à vos profils client.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Account ID]** : votre [!DNL The Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]** : demandez à votre représentant [!DNL The Trade Desk] quel serveur régional vous devez utiliser. Vous trouverez ci-dessous les serveurs régionaux disponibles que vous pouvez choisir :

   * **[!UICONTROL APAC]**
   * **[!UICONTROL China]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL UK/EU]**
   * **[!UICONTROL US East Coast]**
   * **[!UICONTROL US West Coast]**

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

Dans l’étape [Planning des audiences](../../ui/activate-segment-streaming-destinations.md#scheduling), vous devez mapper manuellement vos audiences à l’identifiant ou au nom convivial correspondant dans la plateforme de destination.

Lors du mappage des audiences, Adobe vous recommande d’utiliser le nom de l’audience Experience Platform ou une forme plus courte de celui-ci, pour plus de facilité d’utilisation. Cependant, l’identifiant ou le nom de l’audience dans la destination n’a pas besoin de correspondre à celui de votre compte Experience Platform. Toute valeur que vous insérez dans le champ de mappage est reflétée par la destination.

### Mappages préconfigurés {#preconfigured-mappings}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_ttd"
>title="Jeux de mappages préconfigurés"
>abstract="Nous avons préconfiguré ces quatre jeux de mappages pour vous. Lorsque vous activez des données vers The Trade Desk, les profils qualifiés pour les audiences activées n’ont pas nécessairement besoin que les quatre identités soient présentes sur les profils, car cette destination fonctionnera avec l’une des identités cibles affichées ici. <br> Pour le ciblage par cookies basé sur l’identifiant Trade Desk, vous devez disposer d’un ECID présent sur le profil et d’un mappage de synchronisation des identifiants entre l’identifiant Trade Desk et l’ECID."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/tradedesk#preconfigured-mappings" text="En savoir plus sur les mappages préconfigurés"

Les mappages d’identité suivants sont **préconfigurés et automatiquement renseignés** pour vous dans le workflow d’activation des audiences :

* GAID (Google Advertising ID)
* IDFA (Apple ID pour les annonceurs)
* ECID (Experience Cloud ID)
* [!DNL The Trade Desk ID]

![Capture d’écran affichant les mappages obligatoires](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

Ces mappages sont grisés et en lecture seule. Dans cette étape, vous n’avez rien à configurer. Sélectionnez **[!UICONTROL Next]** pour continuer.

Experience Platform vérifie automatiquement tous les types d’identité pris en charge pour chaque profil appartenant aux audiences mappées dans le workflow d’activation, puis active le profil à l’aide des identités présentes.

### Exigences d’identité par type d’activation

**Activation des ID mobiles (GAID/IDFA) :** profils utilisant uniquement GAID ou IDFA sont suffisants pour l’activation. Aucune identité ou condition préalable supplémentaire n’est requise.

**Ciblage basé sur les cookies ([!DNL Trade Desk ID]) :** requiert les deux éléments suivants :

* ECID présent sur le profil
* Mappage de synchronisation des identifiants entre le [!DNL Trade Desk ID] et l’ECID (configuré comme décrit dans la section [conditions préalables](#prerequisites))

**Comportement avec plusieurs identifiants :** si un profil contient plusieurs identités prises en charge, chaque identité sera activée séparément pour [!DNL The Trade Desk]. Cela garantit une portée et une flexibilité maximales dans l’activation de votre audience.

### Exemples d’activation

* **Profils d’ID mobiles :** les profils avec GAID et/ou IDFA sont activés à l’aide de leurs ID publicitaires respectifs. Si un profil contient à la fois GAID et IDFA, chaque identifiant est activé séparément.
* **Profil basé sur les cookies :** un profil doté d’un ECID et d’un mappage [!DNL Trade Desk ID] correspondant sera activé à l’aide de l’ID Trade Desk pour le ciblage basé sur les cookies.
* **Profil ECID uniquement :** un profil avec ECID uniquement et sans mappage [!DNL Trade Desk ID] ne sera **pas exporté**. L’ECID seul est insuffisant pour l’activation.

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL The Trade Desk], vérifiez votre compte [!DNL The Trade Desk]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.
