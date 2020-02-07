---
title: Destination Google
seo-title: Destination Google
description: Adobe Real-time CDP s’intègre à Google pour vous permettre d’exécuter et d’activer vos données sur DV360, Google Ad Manager, Google AdWords et Google AdX.
seo-description: Adobe Real-time CDP s’intègre à Google pour vous permettre d’exécuter et d’activer vos données sur DV360, Google Ad Manager, Google AdWords et Google AdX.
translation-type: tm+mt
source-git-commit: 5396bee00044e5046bd768a863fceca0aec1d24e

---


# Destination Google

## Aperçu

Adobe Real-time CDP s’intègre à Google pour vous permettre d’exécuter et d’activer vos données sur DV360, Google Ad Manager, Google AdWords Display et Google AdX.

## Caractéristiques de destination

Notez les informations suivantes spécifiques aux destinations Google :

* Vous pouvez envoyer les [identités](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) suivantes vers les destinations Google : ID de cookie **Google, IDFA, GAID**.
* Les audiences activées sont créées par programmation dans la plateforme Google.
* Le CDP Adobe en temps réel n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Reportez-vous au nombre d’audiences dans Google pour valider l’intégration et comprendre les abandons de données.

## Conditions préalables

### Liste blanche

Avant de connecter la destination Google dans le CDP en temps réel d’Adobe, vous devez contacter Google pour demander que votre compte soit autorisé. Contactez Google et fournissez les informations suivantes :

* **ID** de compte : il s’agit de l’ID de compte Adobe avec Google. Contactez le support technique d’Adobe pour obtenir cet ID.
* **ID** client : il s’agit de l’ID de compte client d’Adobe avec Google. Contactez le support technique d’Adobe pour obtenir cet ID.
* **ID** de partenaire : Il s’agit de votre identifiant de partenaire à trois chiffres avec Google ;
* **ID** réseau : il s’agit de votre compte auprès de Google ;
* **ID** du lien d’audience : il s’agit de votre compte auprès de Google ;
* Type de compte. Il peut s’agir d’ **inviter un annonceur**, un partenaire **** d’invitation, **DFP**, **AdWords, AdX.******


## Connecter la destination

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez Google, puis **[!UICONTROL Créer une destination]**.
   ![Connecter une destination Google](/help/rtcdp/destinations/assets/google-destination.png)

2. Dans l’assistant de connexion à la destination, renseignez les informations de base de la destination.
   ![Informations de base Google](/help/rtcdp/destinations/assets/google-basic-information.png)
* **Nom**: Renseignez le nom préféré pour cette destination.
* **Description**: Facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **Type** de compte : Sélectionnez une option, selon votre compte auprès de Google :
   * Utilisation `Invite advertiser` pour Google DV360
   * Utilisation `Invite partner` pour Google DV360
   * Utiliser `DFP by Google` pour Google Ad Manager
   * Utiliser `AdWords` pour l’affichage Google AdWords
   * Utilisation `AdX buyer` pour Google AdX
* **ID** de compte : Renseignez votre ID de compte avec Google.

>[!NOTE]
>
>Lors de la configuration d’une destination Google, demandez à votre gestionnaire de compte Google ou à votre représentant Adobe de déterminer le type de produit sous lequel votre compte se trouve. Pour Google DV360, demandez à votre gestionnaire de compte Google le type de produit sous lequel votre compte se trouve. 

## Activer les segments dans Google

Pour savoir comment activer des segments dans Google, voir [Activation des données vers des destinations](/help/rtcdp/destinations/activate-destinations.md).