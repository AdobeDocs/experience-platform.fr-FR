---
title: Destination Google Ad Manager
seo-title: Destination Google Ad Manager
description: 'Google Ad Manager, anciennement appelé DoubleClick for Publishers ou DoubleClick AdX, est une plateforme de service publicitaire de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles. '
seo-description: 'Google Ad Manager, anciennement appelé DoubleClick for Publishers ou DoubleClick AdX, est une plateforme de service publicitaire de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles. '
translation-type: tm+mt
source-git-commit: a251d843401d2f092e368a4cdac217171fa4687f
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 47%

---


# [!DNL Google Ad Manager Destination]

## Présentation

[!DNL Google Ad Manager], anciennement appelé for Publishers ou , est une plateforme de service publicitaire de qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles.[!DNL DoubleClick][!DNL DoubleClick AdX][!DNL Google]

## Spécifications de la destination

Note the following details that are specific to [!DNL Google Ad Manager] destinations:

* Vous pouvez envoyer les [identités](../../identity-service/namespaces.md)[!DNL Google Ad Manager] suivantes vers les destinations  : **identifiant de cookie Google, IDFA, GAID, identifiants Roku, identifiants Microsoft, identifiants Amazon Fire TV**.
* Activated audiences are created programmatically in the [!DNL Google] platform.
* La plateforme CDP en temps réel Adobe n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Consultez le nombre d’audiences dans Google pour valider l’intégration et comprendre la taille de ciblage des audiences.

>[!IMPORTANT]
>
>If you are looking to create your first destination with [!DNL Google Ad Manager] and have not enabled the [ID sync functionality](https://docs.adobe.com/content/help/fr-FR/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in the past (with Audience Manager or other applications), please reach out to Adobe Consulting or Customer Care to enable ID syncs. If you had previously set up [!DNL Google] integrations in Audience Manager, the ID syncs you had set up carry over to Adobe Real-time CDP.

## Conditions préalables 

### Liste autorisée

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première [!DNL Google Ad Manager] destination dans le CDP en temps réel Adobe. Please ensure the allow list process described below has been completed by [!DNL Google] before creating a destination.

Avant de créer la destination dans le CDP en temps réel Adobe, vous devez contacter [!DNL Google Ad Manager] [!DNL Google] pour que l’Adobe soit mis sur la liste des fournisseurs de données autorisés et que votre compte soit ajouté à la liste autorisée. Contact [!DNL Google] and provide the following information:

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec [!DNL Google]. Contactez l’assistance clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec [!DNL Google]. Contactez l’assistance clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant réseau** : il s’agit de votre compte avec [!DNL Google Ad Manager]
* **Identifiant du lien d’audience** : il s’agit de votre compte avec [!DNL Google Ad Manager]
* Votre type de compte. **DFP de Google** ou **AdX buyer**.

## Configurer la destination

1. Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL Google Ad Manager], puis **[!UICONTROL Configurer]**.
   ![Connexion à la destination Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination.png)

   >[!NOTE]
   >
   >Si une connexion à cette destination existe déjà, un bouton **[!UICONTROL Activer]** s’affiche sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](/help/rtcdp/destinations/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

2. In the **Setup** step of the create destination workflow, fill in the [!UICONTROL Basic Information] for the destination. <br>

   ![Informations de base de Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination-setup-step.png)
* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utilisez `DFP by Google` pour for Publishers[!DNL DoubleClick]
   * Use `AdX buyer` for [!DNL Google AdX]
* **[!UICONTROL Identifiant de compte]** : renseignez votre identifiant de compte avec [!DNL Google]. Il peut s’agir de votre identifiant réseau ou de votre identifiant du lien d’audience. En règle générale, il s’agit d’un identifiant à huit chiffres.
* **[!UICONTROL Cas]** d’utilisation marketing : Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](/help/data-governance/policies/overview.md#core-actions)données.

>[!NOTE]
>
> When setting up a [!DNL Google Ad Manager] destination please work with your [!DNL Google Account Manager] or Adobe representative to understand which account type you have.

## Activate segments to [!DNL Google Ad Manager]

For instructions on how to activate segments to [!DNL Google Ad Manager], see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).

## Données exportées

Pour vérifier si les données ont bien été exportées vers la [!DNL Google Ad Manager] destination, vérifiez votre [!DNL Google Ad Manager] compte. Si l’activation a réussi, les audiences sont renseignées dans votre compte.