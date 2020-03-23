---
title: Destination Google Ad Manager
seo-title: Destination Google Ad Manager
description: 'Google Ad Manager, anciennement connu sous le nom de DoubleClick for Publishers ou DoubleClick AdX, est une plateforme de service publicitaire de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites Web, par le biais de vidéos et dans des applications mobiles. '
seo-description: 'Google Ad Manager, anciennement connu sous le nom de DoubleClick for Publishers ou DoubleClick AdX, est une plateforme de service publicitaire de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites Web, par le biais de vidéos et dans des applications mobiles. '
translation-type: tm+mt
source-git-commit: 3e510c891c84fb3dc1632bd1182ef1e010ea898f

---


# Destination Google Ad Manager

## Présentation

Google Ad Manager, anciennement connu sous le nom de DoubleClick for Publishers ou DoubleClick AdX, est une plateforme de service publicitaire de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites Web, par le biais de vidéos et dans des applications mobiles.

## Spécifications de la destination

Notez les détails suivants qui sont spécifiques aux destinations Google Ad Manager :

* Vous pouvez envoyer les [identités](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) suivantes aux destinations Google Ad Manager : Identifiant de cookie **Google, IDFA, GAID, ID Roku, ID Microsoft, ID Amazon Fire TV**.
* Les audiences activées sont créées par programmation dans la plateforme Google.
* La plateforme CDP en temps réel Adobe n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Reportez-vous au nombre de  de  dans Google pour valider l’intégration et comprendre la taille de ciblage des  de  de de Google.

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec Google Ad Manager et que vous n’avez pas activé la fonctionnalité [de synchronisation des](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) identifiants dans le service d’ID d’Experience Cloud dans le passé (avec  Gestionnaire de  de ou d’autres applications), contactez le service de conseil ou le service à la clientèle d’Adobe pour activer la synchronisation des identifiants. Si vous aviez précédemment configuré des intégrations Google dans  Gestionnaire de  de, les synchronisations d’ID que vous avez configurées sont transférées au CDP en temps réel d’Adobe.

## Conditions préalables

### Liste blanche

>[!NOTE]
>
>La liste blanche est obligatoire avant de configurer votre première destination Google Ad Manager dans Adobe CDP en temps réel. Veuillez vous assurer que le processus de liste blanche décrit ci-dessous a été terminé par Google avant de créer une destination.

Avant de créer la destination Google Ad Manager dans le CDP en temps réel d’Adobe, vous devez contacter Google pour demander à Adobe d’être autorisé en tant que fournisseur de données et à ce que votre compte soit autorisé. Contactez Google et fournissez les informations suivantes :

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec Google. Contactez le service à la clientèle Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec Google. Contactez le service à la clientèle Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **ID** réseau : ceci est votre compte avec Google Ad Manager
* **ID** de lien  de : ceci est votre compte avec Google Ad Manager
* Votre type de compte. **DFP par acheteur** Google **ou** AdX.

## Créer une destination

1. In **[!UICONTROL Connections > Destinations]**, select Google Ad Manager, and select **[!UICONTROL Create destination]**.
   ![Connecter la destination Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination.png)

2. Dans l’assistant de création de destination, renseignez les informations de base de la destination.
   ![Informations de base Google Ad Manager](/help/rtcdp/destinations/assets/google-1-basic-information.png)
* **Nom** : renseignez le nom de votre choix pour cette destination.
* **Description** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **Type de compte** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utilisation `DFP by Google` de DoubleClick pour les éditeurs
   * Utilisez `AdX buyer` pour Google AdX.
* **Identifiant de compte** : renseignez votre identifiant de compte avec Google. Il peut s’agir de votre ID de réseau ou de votre ID de lien  . En règle générale, il s’agit d’un identifiant à huit chiffres.

>[!NOTE]
>
>Lors de la configuration d’une destination Google Ad Manager, contactez votre gestionnaire de compte Google ou votre représentant Adobe pour savoir quel type de compte vous avez.

## Activer les segments dans Google Ad Manager

For instructions on how to activate segments to Google Ad Manager, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).