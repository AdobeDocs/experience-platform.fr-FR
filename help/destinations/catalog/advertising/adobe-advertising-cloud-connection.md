---
title: Connexion à Adobe Advertising Cloud DSP
description: Adobe Advertising Cloud DSP est une destination intégrée pour Adobe Real-Time Customer Data Platform, ce qui vous permet de partager des audiences propriétaires authentifiées avec des annonceurs et des utilisateurs approuvés pour l’activation de la campagne.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 22%

---

# Connexion à Adobe Advertising Cloud DSP

## Vue d’ensemble {#overview}

La destination Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) vous permet de partager des audiences propriétaires authentifiées avec des annonceurs et des utilisateurs approuvés pour l’activation de la campagne avec DSP. Pour en savoir plus sur l’intégration de Real-Time CDP à DSP, voir [À propos de l’activation d’audiences authentifiées à partir de sources d’audience](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html?lang=fr).

>[!IMPORTANT]
>
>Cette page a été créée par l’équipe de DSP. Pour toute demande ou information, contactez directement l’assistance Advertising Cloud à l’adresse `adcloud_support@adobe.com`.

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination Advertising Cloud DSP, consultez les exemples de cas d’utilisation ci-dessous que la clientèle Adobe Experience Platform peut résoudre.

### Cas d’utilisation de Brand Advertising

Un retailer en ligne souhaite recibler ses clients à forte valeur ajoutée par le biais d’une campagne d’affichage sans utiliser de cookies de ciblage. Le retailer partage une audience composée des ID d’e-mail hachés de ses clients à forte valeur ajoutée depuis son compte Adobe Real-Time Customer Data Platform (Real-Time CDP) vers son compte DSP. DSP convertit ensuite les identifiants d’e-mail hachés en [!DNL RampIDs] authentifiés grâce à un partenariat entre DSP et LiveRamp. Le [!DNL RampIDs] obtenu peut être utilisé dans une campagne d’affichage pour cibler l’audience.

### Cas d’utilisation de l’agence

Une agence de médias disposant d’un compte DSP mène une campagne de reciblage pour le compte de son client, une marque de premier plan dans le secteur de l’hôtellerie. La marque souhaite recibler tous ses invités de l&#39;année passée avec une nouvelle offre promotionnelle. La marque héberge toutes les informations des clients en [!DNL Real-Time CDP]. La marque peut partager une audience qui consiste en les identifiants d’e-mail hachés de ses invités de son compte [!DNL Real-Time CDP] vers le compte DSP de l’agence de presse afin de recibler les invités par le biais d’une campagne multimédia.

## Conditions préalables {#prerequisites}

* Paramètres au niveau du compte DSP et au niveau de la campagne pour activer le partage d’audience avec [!DNL LiveRamp RampID], qui traduira les données client en [!DNL RampIDs] afin de créer des segments cibles. Votre équipe de compte DSP effectuera cette configuration. [!DNL RampID] est disponible via un partenariat entre DSP et [!DNL LiveRamp], et vous n’avez pas besoin de votre propre adhésion [!DNL LiveRamp] pour l’utiliser.
* Identifiant d’organisation Experience Cloud du compte Experience Platform. Votre identifiant figure sur la page de votre profil utilisateur [!DNL Real-Time CDP].
* Une [[!DNL Real-Time CDP] source dans DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=fr) pour recevoir les audiences pour l’activation de la campagne. Votre équipe de compte DSP créera la source à l’aide de votre ID d’organisation Experience Cloud.
* La clé source du compte ou de l’annonceur DSP, qui est générée lorsqu’une [[!DNL Real-Time CDP] source est créée dans DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=fr). L’équipe de votre compte DSP partagera cette clé avec vous. Vous l’utiliserez dans Experience Platform pour créer une connexion de destination à la destination Advertising Cloud DSP, comme [expliqué ci-dessous](#authenticate).
* Données client composées d’e-mails ou d’e-mails hachés.

## Identités prises en charge {#supported-identities}

La destination Adobe Advertising Cloud DSP prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Experience Platform prend en charge le texte brut et les adresses e-mail hachées SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour qu’Experience Platform hache automatiquement les données lors de l’activation. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau suivant pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience avec les identifiants (e-mail ou e-mail haché) utilisés dans la destination Advertising Cloud DSP. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Lorsqu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation de l’audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [contrôle d’accès](/help/access-control/home.md#permissions) d’Experience Platform. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à la destination, suivez les instructions [création d’une connexion de destination](/help/destinations/ui/connect-destination.md) à l’aide de l’interface utilisateur d’Experience Platform. Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous connecter à la destination, indiquez le paramètre suivant dans la section [!UICONTROL Connection type], puis sélectionnez **[!UICONTROL Connect to destination]**. :

* **[!UICONTROL Account or Advertiser Key]** : ce [!UICONTROL Source Key] est généré lorsqu’une [[!DNL Real-Time CDP]  source est créée dans l’interface utilisateur de DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=fr). L’équipe de votre compte DSP partagera cette clé avec vous après la création de la source.

![&#x200B; Champ de type de connexion &#x200B;](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

![Champs de détails de destination](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Valider l’exportation des données {#exported-data}

Pour vérifier que l’audience de données a été partagée avec Advertising Cloud, vérifiez les points suivants :

* Le flux de données dans la destination [!DNL Real-Time CDP] a réussi.

* Dans DSP, l’audience est disponible lorsque vous créez ou modifiez une audience à partir de [!UICONTROL Audiences] > [!UICONTROL All Audiences] ou dans la section [!UICONTROL Audience Targeting] des paramètres d’emplacement. L’audience doit être visible dans l’onglet [!UICONTROL Adobe Segments] sous le dossier [!UICONTROL Real-Time CDP] .

![audiences Real-Time CDP dans les paramètres d’audience DSP](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [présentation de la gouvernance des données](/help/data-governance/home.md).
