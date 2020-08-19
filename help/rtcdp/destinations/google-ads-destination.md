---
keywords: Google ads;google ads;google adwords;Google AdWords;Google Adwords
title: Destination Google Ads
seo-title: Destination Google Ads
description: Google Ads, appelé auparavant Google AdWords, est un service de publicité en ligne qui permet aux entreprises faire de la publicité avec paiement par clic sur des recherches textuelles, des affichages graphiques, des vidéos YouTube et des affichages mobiles in-app.
seo-description: Google Ads, appelé auparavant Google AdWords, est un service de publicité en ligne qui permet aux entreprises faire de la publicité avec paiement par clic sur des recherches textuelles, des affichages graphiques, des vidéos YouTube et des affichages mobiles in-app.
translation-type: tm+mt
source-git-commit: 2dfa46906374151628d46c309df724a59f8dc50e
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 44%

---


# [!DNL Google Ads] Destination

## Présentation

[!DNL Google Ads], appelé auparavant , est un service de publicité en ligne qui permet aux entreprises faire de la publicité avec paiement par clic sur des recherches textuelles, des affichages graphiques, des vidéos et des affichages mobiles in-app.[!DNL Google AdWords][!DNL YouTube]

## Spécifications de la destination

Note the following details that are specific to [!DNL Google Ads] destinations:

* Vous pouvez envoyer les [identités](../../identity-service/namespaces.md)[!DNL Google Ads] suivantes vers les destinations  : **identifiant de cookie Google, IDFA, GAID, identifiants Roku, identifiants Microsoft, identifiants Amazon Fire TV**.
* Activated audiences are created programmatically in the [!DNL Google] platform.
* La plateforme CDP en temps réel Adobe n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Consultez le nombre d’audiences dans Google pour valider l’intégration et comprendre la taille de ciblage des audiences.

>[!IMPORTANT]
>
>If you are looking to create your first destination with [!DNL Google Ads] and have not enabled the [ID sync functionality](https://docs.adobe.com/content/help/fr-FR/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in the past (with Audience Manager or other applications), please reach out to Adobe Consulting or Customer Care to enable ID syncs. Si vous avez configuré précédemment les intégrations Google dans Audience Manager, les synchronisations d’identifiant que vous aviez configurées sont transférées vers la plateforme de données clients en temps réel d’Adobe.

## Conditions préalables

### Compte [!DNL Google Ads] existant

[!DNL Google] a suspendu toute nouvelle [!DNL Google Ads] intégration avec des fournisseurs tiers. You must have an existing integration with [!DNL Google Ads] in order to be able to perform the allow list steps in the next section and to create a [!DNL Google Ads] destination in Adobe Real-time CDP.

### Liste autorisée

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première [!DNL Google Ads] destination dans le CDP en temps réel Adobe. Please ensure the allow list process described below has been completed by [!DNL Google] before creating a destination.

Avant de créer la destination dans le CDP en temps réel Adobe, vous devez contacter [!DNL Google Ads] [!DNL Google] pour que l’Adobe soit mis sur la liste des fournisseurs de données autorisés et que votre compte soit ajouté à la liste autorisée. Contact [!DNL Google] and provide the following information:

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec [!DNL Google]. Contactez l’assistance clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec [!DNL Google]. Contactez l’assistance clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* Votre type de compte : **AdWords**
* **Identifiant** Google AdWords : C&#39;est votre carte d&#39;identité avec [!DNL Google]. Le format d’identifiant est généralement 123-456-7890.

## Configurer la destination

1. Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL Google Ads], puis **[!UICONTROL Configurer]**.
   ![Connexion à la destination Google Ads](/help/rtcdp/destinations/assets/google-2-destination.png)

   >[!NOTE]
   >
   >Si une connexion à cette destination existe déjà, un bouton **[!UICONTROL Activer]** s’affiche sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](/help/rtcdp/destinations/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

2. In the **Setup** step of the create destination workflow, fill in the [!UICONTROL Basic Information] for the destination. <br>

   ![Informations de base de Google Ads](/help/rtcdp/destinations/assets/google-2-destination-setup-step.png)
* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type de compte]** : AdWords est la seule option disponible.
* **[!UICONTROL Identifiant de compte]** : renseignez votre identifiant de compte avec [!DNL Google Ads]. Le format d’identifiant est généralement 123-456-7890.
* **[!UICONTROL Cas]** d’utilisation marketing : Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](/help/data-governance/policies/overview.md#core-actions)données.

## Activate segments to [!DNL Google Ads]

For instructions on how to activate segments to [!DNL Google Ads], see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).

## Données exportées

Pour vérifier si les données ont bien été exportées vers la [!DNL Google Ads] destination, vérifiez votre [!DNL Google Ads] compte. Si l’activation a réussi, les audiences sont renseignées dans votre compte.