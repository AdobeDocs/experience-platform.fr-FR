---
title: Connexion d’accrochage Inc
description: Découvrez comment vous connecter à la plateforme Snapchat Ads et exporter vos audiences depuis Experience Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 26%

---

# Connexion d’accrochage Inc

## Vue d’ensemble {#overview}

[Des Snapchat Ads](https://forbusiness.snapchat.com/) sont créés pour chaque entreprise, quelle que soit sa taille ou son industrie. Faites partie des conversations quotidiennes des Snapchatters avec des publicités numériques en plein écran qui inspirent l&#39;action des personnes qui comptent le plus pour votre entreprise.

>[!IMPORTANT]
>
>Cette page de documentation et de connecteur de destination est créée et conservée par l’équipe *Snapper Inc*. Pour toute question ou demande de mise à jour, contactez-les directement à l’adresse *dev-support@snap.com*

## Cas d’utilisation {#use-cases}

Cette destination permet aux marketeurs d’importer dans Snapchat Ads les audiences d’utilisateurs créées dans Experience Platform et de les utiliser pour cibler leurs publicités.

## Conditions préalables {#prerequisites}

Pour utiliser cette destination, vous devez disposer d’un compte Snapchat Ads. Reportez-vous à cette documentation pour plus d’informations sur la façon d’en créer une :

[Prise en main de Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Limites {#limitations}

* La fonction d’accrochage publicitaire ne prend pas en charge plusieurs identités pour un segment d’audience donné. Veuillez n’associer qu’une seule identité lors de l’activation d’un segment.
* La fonction d’accrochage Inc ne prend pas en charge le changement de nom des segments. Pour renommer un segment, vous devez le désactiver, le renommer, puis l’activer.
* Il n’est pas possible de définir une période de rétention pour les membres d’un segment d’audience. Tous les membres conservent leur durée de vie et resteront dans l’audience jusqu’à ce qu’ils soient supprimés.

## Identités prises en charge {#supported-identities}

La destination *Accrocher Inc* prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

Tous les identifiants envoyés à la destination *Accrocher Inc* doivent être hachés au format SHA-256. Pour hacher les identifiants en texte brut avant de les envoyer à la destination, cochez l’option **[!UICONTROL Appliquer la transformation]** lors du mappage des identifiants de cible pour la destination.

>[!WARNING]
> 
> Les identifiants non hachés ne seront pas acceptés par la destination de la fonction d’accrochage publicitaire et leur envoi pourrait entraîner des erreurs.


>[!IMPORTANT]
> 
> La destination de la fonction d’accrochage Inc ne prend pas en charge plusieurs identités. Veuillez sélectionner une seule identité.

| Identité cible | Description | Considérations |
|---|---|---|
| Adresse e-mail | Adresse électronique hachée SHA-256 | Mappez les adresses électroniques dans le champ d’identité cible *emailAddress*. |
| Numéro de téléphone | Numéro de téléphone haché SHA-256 | Mappez les adresses électroniques dans le champ d’identité cible *phoneNumber*. |
| GAID | GOOGLE Advertising ID haché SHA-256 | Mappez les Google Advertising ID dans le champ d&#39;identité cible *gaid*. |
| IDFA | APPLE Advertising ID haché SHA-256 | Mappez les Apple Advertising ID dans le champ d’identité cible *idfa*. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination *YOURDESTINATION*. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connexion à la fonction d’accrochage {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, procédez comme suit :

1. Recherchez la destination *Accrocher Inc* du catalogue de destinations Adobe Experience Platform et sélectionnez **Configurer**.
2. Sélectionnez **[!UICONTROL Se connecter à la destination]**. Vous serez redirigé vers l’écran suivant :
   ![Écran d’authentification 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Saisissez vos informations d’identification Snapchat et sélectionnez **Log In**.
4. Vous verrez apparaître les données Snapchat auxquelles Adobe Experience Platform aura accès. Sélectionnez **Continuer** pour poursuivre le processus de connexion.

![Auth Screen 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Après avoir sélectionné Continuer, attendez que vous soyez redirigé vers Adobe Experience Platform.

### Renseigner les détails de la destination {#destination-details}

![Détails de la destination](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Pour configurer les détails de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Suivant]**.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL ID de compte]** : ID de compte publicitaire associé au compte publicitaire dans lequel vous souhaitez importer vos audiences. Pour plus d&#39;informations sur la façon de trouver ceci, consultez [cette documentation sur le Centre d&#39;aide aux entreprises Snapchat](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>La saisie d’un identifiant de compte de publicité Snapchat incorrect ou non valide entraîne l’échec de l’activation de l’audience. Vérifiez deux fois que vous avez saisi l’identifiant de compte publicitaire approprié.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Valider l’exportation des données {#exported-data}

Après avoir activé les audiences sur la destination *Accrocher Inc*, vous pourrez voir les audiences dans la section [**Audiences** du Gestionnaire d’accrochage publicitaire ](https://businesshelp.snapchat.com/s/article/audience-sharing). Pour accéder à cette section, procédez comme suit :

1. Connectez-vous au [Gestionnaire d’accrochage d’annonces](https://ads.snapchat.com/)
2. Sélectionnez **Audiences** dans le menu déroulant dans le coin supérieur gauche de l’écran. Les audiences que vous avez activées dans Adobe Experience Platform s’affichent dans la bibliothèque d’audiences :

![Audiences](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Veuillez noter que lorsqu’une audience par Adobe est activée pour la première fois à la fonction de gestion dynamique des balises, elle s’affiche initialement comme une audience vide. Cela est dû au fait que Adobe Experience Platform n’exporte pas les données de membre vers la fonction de veille à ce qu’elle évalue l’audience. Pour plus d’informations sur la manière dont les audiences sont évaluées en Experience Platform, reportez-vous à la [présentation de Segmentation Service](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html#evaluate-segments).

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
