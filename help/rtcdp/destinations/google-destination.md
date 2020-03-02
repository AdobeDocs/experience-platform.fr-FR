---
title: Destination Google
seo-title: Destination Google
description: La plateforme CDP en temps réel Adobe s’intègre à Google pour vous permettre d’exécuter et d’activer vos données sur DV360, Google Ad Manager, Google AdWords et Google AdX.
seo-description: La plateforme CDP en temps réel Adobe s’intègre à Google pour vous permettre d’exécuter et d’activer vos données sur DV360, Google Ad Manager, Google AdWords et Google AdX.
translation-type: ht
source-git-commit: 5396bee00044e5046bd768a863fceca0aec1d24e

---


# Destination Google

## Présentation

La plateforme CDP en temps réel Adobe s’intègre à Google pour vous permettre d’exécuter et d’activer vos données sur DV360, Google Ad Manager, Google AdWords Display et Google AdX.

## Spécifications de la destination

Notez les détails suivants qui sont spécifiques aux destinations Google :

* Vous pouvez envoyer les [identités](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) suivantes vers les destinations Google : **ID de cookie Google, IDFA, GAID**.
* Les audiences activées sont créées par programmation dans la plateforme Google.
* La plateforme CDP en temps réel Adobe n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Consultez le nombre d’audiences dans Google pour valider l’intégration et comprendre les abandons de données.

## Conditions préalables

### Liste blanche

Avant de connecter la destination Google dans la plateforme CDP en temps réel Adobe, vous devez contacter Google pour demander que votre compte soit placé sur liste blanche. Contactez Google et fournissez les informations suivantes :

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec Google. Contactez l’Assistance Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec Google. Contactez l’Assistance Adobe pour obtenir cet identifiant.
* **Identifiant de partenaire** : il s’agit de l’identifiant de partenaire à trois chiffres avec Google.
* **Identifiant réseau** : il s’agit de votre compte avec Google.
* **Identifiant du lien d’audience** : il s’agit de votre compte avec Google.
* Votre type de compte. Il peut s’agir d’**Invite advertiser**, d’**Invite partner**, de **DFP**, d’**AdWords** ou d’**AdX**.


## Se connecter à la destination

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez Google, puis **[!UICONTROL Créer une destination]**.
   ![Se connecter à la destination Google](/help/rtcdp/destinations/assets/google-destination.png)

2. Dans l’assistant de connexion à la destination, renseignez les informations de base de la destination.
   ![Informations de base de Google](/help/rtcdp/destinations/assets/google-basic-information.png)
* **Nom** : renseignez le nom de votre choix pour cette destination.
* **Description** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **Type de compte** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utilisez `Invite advertiser` pour Google DV360.
   * Utilisez `Invite partner` pour Google DV360.
   * Utilisez `DFP by Google` pour Google Ad Manager.
   * Utilisez `AdWords` pour Google AdWords Display.
   * Utilisez `AdX buyer` pour Google AdX.
* **Identifiant de compte** : renseignez votre identifiant de compte avec Google.

>[!NOTE]
>
>Lors de la configuration d’une destination Google, demandez à votre gestionnaire de compte Google ou à votre représentant Adobe de vous indiquer à quel type de produit votre compte appartient. Pour Google DV360, demandez à votre gestionnaire de compte Google de vous indiquer à quel type de produit votre compte appartient. 

## Activer les segments vers Google

Pour plus d’informations sur l’activation des segments vers Google, consultez [Activation des données vers des destinations](/help/rtcdp/destinations/activate-destinations.md).