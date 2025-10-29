---
title: Connexion Snap Inc
description: Découvrez comment vous connecter à la plateforme Snapchat Ads et exporter vos audiences à partir d’Experience Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 23%

---

# Connexion Snap Inc

## Vue d’ensemble {#overview}

[Les publicités Snapchat](https://forbusiness.snapchat.com/) sont conçues pour chaque entreprise, quelle que soit sa taille ou son secteur d&#39;activité. Prenez part aux conversations quotidiennes de Snapchatters avec des publicités numériques en plein écran qui inspirent l&#39;action des personnes qui comptent le plus pour votre entreprise.

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et conservés par l’équipe *Snap Inc*. Pour toute question ou demande de mise à jour, contactez-les directement à l’adresse *dev-support@snap.com*

## Cas d’utilisation {#use-cases}

Cette destination permet aux marketeurs d’importer dans Snapchat Ads les audiences d’utilisateurs créées dans Experience Platform et de les utiliser pour cibler leurs annonces.

## Conditions préalables {#prerequisites}

Pour utiliser cette destination, vous devez disposer d’un compte Snapchat Ads. Reportez-vous à cette documentation pour plus d’informations sur la création d’une interface :

[Prise en main de Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Limites {#limitations}

* Snap Inc ne prend pas en charge les identités multiples pour un segment d’audience donné. Mappez une seule identité lors de l’activation d’un segment.
* Snap Inc ne prend pas en charge le changement de nom des segments. Pour renommer un segment, vous devez le désactiver, le renommer, puis l’activer.
* Il n’est pas possible de définir une période de conservation pour les membres d’un segment ciblé. Tous les membres disposent d’une rétention à vie et resteront dans l’audience jusqu’à leur suppression.

## Identités prises en charge {#supported-identities}

La destination *Snap Inc* prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

Tous les identifiants envoyés à la destination *Snap Inc* doivent être hachés au format SHA-256. Pour hacher les identifiants en texte brut avant de les envoyer à la destination, cochez l’option **[!UICONTROL Apply transformation]** lors du mappage des identifiants de cible pour la destination.

>[!WARNING]
> 
> Les identifiants non hachés ne seront pas acceptés par la destination Snap Inc et leur envoi pourrait entraîner des erreurs.


>[!IMPORTANT]
> 
> La destination Snap Inc ne prend pas en charge les identités multiples. Sélectionnez une seule identité.

| Identité cible | Description | Considérations |
|---|---|---|
| Adresse e-mail | Adresse électronique hachée SHA-256 | Mappez les adresses électroniques dans le champ d’identité cible *emailAddress*. |
| Numéro de téléphone | Numéro de téléphone haché SHA-256 | Mappez les adresses e-mail dans le champ d’identité cible *phoneNumber*. |
| GAID | Identifiant Advertising Google haché SHA-256 | Mappez les identifiants Google Advertising dans le champ d’identité cible *gaid*. |
| IDFA | SHA-256 haché Apple Advertising ID | Mappez les identifiants Apple Advertising dans le champ d’identité cible *idfa*. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |
| [!DNL Federated Audience Composition] | ✓ | Audiences importées dans Experience Platform via [Federated Audience Composition](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination Snap Inc. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connexion à Snap Inc {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, procédez comme suit :

1. Recherchez la destination *Snap Inc* dans le Catalogue des destinations Adobe Experience Platform et sélectionnez **Configurer**.
2. Sélectionnez **[!UICONTROL Connect to destination]**. Vous serez redirigé vers l’écran suivant :
   ![Écran d’authentification 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Saisissez vos identifiants Snapchat et sélectionnez **Connexion**.
4. Les données Snapchat auxquelles Adobe Experience Platform aura accès vous seront présentées. Sélectionnez **Continuer** pour poursuivre le processus de connexion.

![Écran d’authentification 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Après avoir sélectionné Continuer, attendez d’être redirigé(e) vers Adobe Experience Platform.

### Renseigner les détails de la destination {#destination-details}

![Détails de la destination](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Pour configurer les détails de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Next]**.

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Account ID]** : ID du compte publicitaire associé au compte publicitaire vers lequel vous souhaitez importer vos audiences. Pour plus d’informations sur la façon de le trouver, reportez-vous à [cette documentation sur le Centre d’aide aux entreprises Snapchat](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>La saisie d’un identifiant de compte publicitaire Snapchat incorrect ou non valide entraîne l’échec de l’activation de l’audience. Vérifiez bien que vous avez saisi l’ID de compte publicitaire approprié.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**[](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Valider l’exportation des données {#exported-data}

Après avoir activé les audiences vers la destination *Snap Inc*, vous pourrez voir les audiences dans la section [**Audiences** de Snap Ads Manager](https://businesshelp.snapchat.com/s/article/audience-sharing). Pour accéder à cette section, procédez comme suit :

1. Connectez-vous à [Snap Ads Manager](https://ads.snapchat.com/)
2. Sélectionnez **Audiences** dans le menu déroulant situé dans le coin supérieur gauche de l’écran. Les audiences que vous avez activées dans Adobe Experience Platform s’affichent dans la bibliothèque d’audiences :

![Audiences](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Notez que lorsqu’une audience Adobe est activée pour la première fois sur Snap Inc, elle s’affiche initialement comme une audience vide. En effet, Adobe Experience Platform n’exporte pas les données des membres vers Snap Inc tant qu’il n’a pas évalué l’audience. Pour plus d’informations sur l’évaluation des audiences dans Experience Platform, reportez-vous à la [ présentation de Segmentation Service ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html#evaluate-segments).

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
