---
title: Connexion Adobe Advertising Cloud DSP
description: Adobe Advertising Cloud DSP est une destination intégrée d’Adobe Real-Time Customer Data Platform, qui vous permet de partager des audiences propriétaires authentifiées avec des annonceurs et des utilisateurs approuvés pour l’activation de la campagne.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 25%

---

# Connexion Adobe Advertising Cloud DSP

## Vue d’ensemble {#overview}

La destination Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) vous permet de partager des audiences propriétaires authentifiées avec des annonceurs et des utilisateurs approuvés pour l’activation de la campagne avec DSP. Pour en savoir plus sur l’intégration de Real-Time CDP avec DSP, voir [À propos de l’activation des audiences authentifiées à partir des sources d’audience](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Cette page a été créée par l’équipe DSP. Pour toute question ou demande de mise à jour, contactez le support Advertising Cloud directement à l’adresse `adcloud_support@adobe.com`.

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination Advertising Cloud DSP, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation de la publicité de marque

Un détaillant en ligne souhaite recibler ses clients à forte valeur ajoutée par le biais d’une campagne d’affichage sans utiliser de cookies pour le ciblage. Le détaillant partage une audience composée des e-mails hachés de ses clients à forte valeur ajoutée depuis son compte Adobe Real-Time Customer Data Platform (Real-Time CDP) jusqu’à son compte DSP. DSP convertit ensuite les ID de courrier électronique haché en [!DNL RampIDs] authentifiés par le biais d’un partenariat entre DSP et LiveRamp. Le [!DNL RampIDs] obtenu peut être utilisé dans une campagne d’affichage pour cibler l’audience.

### Cas d’utilisation de l’agence

Une agence de médias disposant d’un compte DSP gère une campagne de reciblage pour le compte de son client, une marque de pointe dans l’industrie hôtelière. La marque souhaite recibler tous ses invités l&#39;année dernière avec une nouvelle offre promotionnelle. La marque héberge toutes les informations sur les invités dans [!DNL Real-Time CDP]. La marque peut partager une audience qui se compose des e-mails hachés de ses invités de son compte [!DNL Real-Time CDP] au compte DSP de l’agence de médias pour recibler les invités par le biais d’une campagne de médias.

## Conditions préalables {#prerequisites}

* DSP des paramètres au niveau du compte et de la campagne pour activer le partage d’audience avec [!DNL LiveRamp RampID], ce qui convertira les données client en [!DNL RampIDs] pour créer des segments pouvant être ciblés. Votre équipe DSP compte effectuera cette configuration. [!DNL RampID] est disponible via un partenariat entre DSP et [!DNL LiveRamp], et vous n&#39;avez pas besoin de votre propre abonnement [!DNL LiveRamp] pour l&#39;utiliser.
* Identifiant de l’organisation Experience Cloud pour le compte Experience Platform. Vous pouvez trouver votre ID sur votre page de profil utilisateur [!DNL Real-Time CDP].
* Une [[!DNL Real-Time CDP] source dans DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) pour recevoir des audiences pour l’activation de la campagne. Votre équipe de compte DSP va créer la source à l’aide de votre ID d’organisation Experience Cloud.
* La clé source du compte DSP ou de l’annonceur, qui est générée lorsqu’une source [[!DNL Real-Time CDP] est créée dans DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Votre équipe de compte DSP partagera cette clé avec vous. Vous l’utiliserez dans Experience Platform pour créer une connexion de destination à la destination Advertising Cloud DSP, comme [expliqué ci-dessous](#authenticate).
* Données client composées d’emails ou de courriers électroniques hachés.

## Identités prises en charge {#supported-identities}

La destination Adobe Advertising Cloud DSP prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que l’Experience Platform hache automatiquement les données lors de l’activation. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau suivant pour plus d’informations sur le type et la fréquence d’exportation de destination.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (email ou email haché) utilisés dans la destination Advertising Cloud DSP. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Lorsqu’un profil est mis à jour en Experience Platform en fonction de l’évaluation de l’audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’autorisation de **[!UICONTROL Affichage des destinations]** et de **[!UICONTROL Gestion des destinations]** [&#128279;](/help/access-control/home.md#permissions) pour l’Experience Platform. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à la destination, suivez les instructions pour [créer une connexion de destination](/help/destinations/ui/connect-destination.md) à l’aide de l’interface utilisateur de l’Experience Platform. Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous connecter à la destination, indiquez le paramètre suivant dans la section [!UICONTROL Type de connexion], puis sélectionnez **[!UICONTROL Se connecter à la destination]** :

* **[!UICONTROL Clé de compte ou de publicitaire]** : cette [!UICONTROL clé Source] est générée lorsqu’une [[!DNL Real-Time CDP] source est créée dans l’interface utilisateur DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Votre équipe DSP compte partagera cette clé avec vous une fois qu’elle aura créé la source.

![Champ de type de connexion](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

![Champs de détail de destination](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des **&#x200B;**, **[!UICONTROL Activer les destinations]**, **&#x200B;**&#x200B;et **&#x200B;**&#x200B;[  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Valider l’exportation des données {#exported-data}

Pour vérifier que l’audience de données a été partagée avec Advertising Cloud, vérifiez les points suivants :

* Le flux de données de votre destination [!DNL Real-Time CDP] a réussi.

* Dans DSP, l’audience est disponible lorsque vous créez ou modifiez une audience à partir de [!UICONTROL Audiences] > [!UICONTROL Toutes les audiences] ou dans la section [!UICONTROL Ciblage d’audience] des paramètres de placement. L’audience doit être visible dans l’onglet [!UICONTROL Segments d’Adobe] sous le dossier [!UICONTROL Real-Time CDP] .

![Audiences Real-Time CDP dans DSP paramètres d’audience](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour plus d’informations sur la façon dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [présentation de la gouvernance des données](/help/data-governance/home.md).
