---
title: Connexion Adobe Advertising Cloud DSP
description: 'Adobe Advertising Cloud DSP est une destination intégrée pour la variable [!DNL Adobe Real-time Customer Data Profile], ce qui vous permet de partager des segments propriétaires authentifiés avec des annonceurs et des utilisateurs approuvés pour l’activation de la campagne.  '
source-git-commit: 2b1e74a704003bbbf1d72e4a01b2fb9f9c8d22ca
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 4%

---


# Connexion Adobe Advertising Cloud DSP

## Présentation {#overview}

La destination Advertising Cloud DSP vous permet de partager des segments propriétaires authentifiés avec des annonceurs et des utilisateurs approuvés pour l’activation de la campagne avec DSP.<!-- To learn more about the Real-Time CDP integration with DSP, see [About Activating Authenticated Segments from Audience Sources](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html). -->

>[!IMPORTANT]
>
>Cette page a été créée par l’équipe DSP. Pour toute question ou demande de mise à jour, contactez le support Advertising Cloud directement à l’adresse `adcloud_support@adobe.com`.

## Cas dʼutilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination Advertising Cloud DSP, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation de la publicité de marque

Un détaillant en ligne souhaite recibler ses clients à forte valeur ajoutée par le biais d’une campagne d’affichage sans utiliser de cookies pour le ciblage. Le détaillant partage un segment constitué des ID d’e-mail hachés de ses clients à forte valeur ajoutée provenant de ses [!DNL Real-Time CDP] à son compte DSP. DSP convertit ensuite les ID de courrier électronique haché en ID authentifiés. [!DNL RampIDs] grâce à un partenariat entre DSP et LiveRamp. Le résultat [!DNL RampIDs] peut être utilisé dans une campagne d’affichage pour cibler l’audience.

### Cas d’utilisation de l’agence

Une agence de médias disposant d’un compte DSP gère une campagne de reciblage pour le compte de son client, une marque de pointe dans l’industrie hôtelière. La marque souhaite recibler tous ses invités l&#39;année dernière avec une nouvelle offre promotionnelle. La marque héberge toutes les informations sur les invités dans [!DNL Real-Time CDP]. La marque peut partager un segment constitué des ID d’email haché de ses invités à partir de ses [!DNL Real-Time CDP] compte sur le compte DSP de l&#39;agence de presse pour recibler les invités à travers une campagne médiatique.

## Conditions préalables {#prerequisites}

* Paramètres au niveau du compte et au niveau de la campagne DSP pour activer le partage de segments avec [!DNL LiveRamp RampID], qui convertit les données client en [!DNL RampIDs] pour créer des segments pouvant être ciblés. Votre équipe DSP compte effectuera cette configuration.
* Identifiant de l’organisation Experience Cloud pour le compte Experience Platform. Vous pouvez trouver votre ID sur votre [!DNL Real-Time CDP] page du profil utilisateur.
* A [!DNL Real-Time CDP] source dans DSP<!-- [[!DNL Real-Time CDP] source in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) --> pour recevoir des segments pour l’activation de la campagne. Votre équipe de compte DSP va créer la source à l’aide de votre ID d’organisation Experience Cloud.
* Clé source du compte DSP ou de l’annonceur, générée lors de la génération d’un événement [!DNL Real-Time CDP] source est créé dans DSP<!-- [[!DNL Real-Time CDP] source is created in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) -->. Votre équipe de compte DSP partagera cette clé avec vous. Vous l’utiliserez dans Experience Platform pour créer une connexion de destination à la destination Advertising Cloud DSP, en tant que [expliqué ci-dessous](#authenticate).
* Données client composées d’emails ou de courriers électroniques hachés.

## Identités prises en charge {#supported-identities}

La destination Adobe Advertising Cloud DSP prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** pour que l’Experience Platform hache automatiquement les données lors de l’activation. |

{style=&quot;table-layout:auto&quot;}

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau suivant pour plus d’informations sur le type et la fréquence d’exportation de destination.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) avec les identifiants (email ou email haché) utilisés dans la destination Advertising Cloud DSP. |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Lorsqu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions) pour Experience Platform. Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à la destination, suivez les instructions de la section [création d’une connexion de destination](/help/destinations/ui/connect-destination.md) à l’aide de l’interface utilisateur de l’Experience Platform. Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### Authentification à la destination {#authenticate}

Pour vous connecter à la destination, indiquez le paramètre suivant dans la variable [!UICONTROL Type de connexion] , puis sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL Clé de compte ou de publicitaire]**: Ceci [!UICONTROL Clé source] est généré lorsqu’une [!DNL Real-Time CDP] La source est créée dans l’interface utilisateur DSP<!-- [[!DNL Real-Time CDP] source is created in the DSP user interface](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) -->. Votre équipe DSP compte partagera cette clé avec vous une fois qu’elle aura créé la source.

![Champ de type de connexion](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Renseignement des détails de destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs requis du [!UICONTROL Détails de la destination] , puis sélectionnez **[!UICONTROL Suivant]**.

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.

![Champs des détails de la destination](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation des profils et des segments vers des destinations d’exportation de segments en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Validation de l’exportation des données {#exported-data}

Pour vérifier que le segment de données a été partagé avec Advertising Cloud, vérifiez les points suivants :

* Le flux de données dans votre [!DNL Real-Time CDP] destination réussie.

* Dans DSP, le segment est disponible lorsque vous créez ou modifiez une audience à partir de [!UICONTROL Audiences] > [!UICONTROL Toutes les audiences] ou depuis l’ [!UICONTROL Ciblage d’audience] des paramètres de placement. Le segment doit être visible dans la variable [!UICONTROL Adobe de segments] sous l’onglet [!UICONTROL Real-Time CDP] dossier.

![Segments Real-Time CDP dans les paramètres DSP audience](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](/help/data-governance/home.md).
