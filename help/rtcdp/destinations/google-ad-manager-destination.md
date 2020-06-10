---
title: Destination Google Ad Manager
seo-title: Destination Google Ad Manager
description: 'Google Ad Manager, anciennement appelé DoubleClick for Publishers ou DoubleClick AdX, est une plateforme de service publicitaire de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles. '
seo-description: 'Google Ad Manager, anciennement appelé DoubleClick for Publishers ou DoubleClick AdX, est une plateforme de service publicitaire de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles. '
translation-type: tm+mt
source-git-commit: dc5ee796ca390d06fc8e08bd6c30e88a0d96dd53
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 38%

---


# Destination Google Ad Manager

## Présentation

Google Ad Manager, anciennement appelé DoubleClick for Publishers ou DoubleClick AdX, est une plateforme de service publicitaire de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles.

## Spécifications de la destination

Notez les détails suivants spécifiques aux destinations Google Ad Manager :

* Vous pouvez envoyer les [identités](../../identity-service/namespaces.md) suivantes aux destinations Google Ad Manager : **ID de cookie Google, IDFA, GAID, ID de Roku, ID Microsoft, ID** Amazon Fire TV.
* Les audiences activées sont créées par programmation dans la plateforme Google.
* La plateforme CDP en temps réel Adobe n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Reportez-vous au décompte des audiences dans Google pour valider l’intégration et comprendre la taille du ciblage des audiences.

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec Google Ad Manager et que vous n’avez pas activé la fonctionnalité [de synchronisation des](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) identifiants dans le service d’identification d’Experience Cloud (avec Audience Manager ou d’autres applications) par le passé, contactez le service de conseil ou d’assistance clientèle de Adobe pour activer la synchronisation des identifiants. Si vous aviez précédemment configuré des intégrations Google dans Audience Manager, les synchronisations d’identifiants que vous avez configurées sont transférées au fichier CDP Adobe Real-time.

## Conditions préalables

### Autoriser la liste

>[!NOTE]
>
>La liste d’autorisation est obligatoire avant de configurer votre première destination Google Ad Manager dans Adobe Real-time CDP. Assurez-vous que le processus d&#39;autorisation de liste décrit ci-dessous a été effectué par Google avant de créer une destination.

Avant de créer la destination Google Ad Manager dans Adobe Real-time CDP, vous devez contacter Google pour que Adobe soit mis sur la liste des fournisseurs de données autorisés et que votre compte soit ajouté à la liste autorisée. Contactez Google et fournissez les informations suivantes :

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec Google. Contactez le service à la clientèle Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec Google. Contactez le service à la clientèle Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **ID** réseau : Il s’agit de votre compte auprès de Google Ad Manager
* **ID** de lien d&#39;Audience : Il s’agit de votre compte auprès de Google Ad Manager
* Votre type de compte. **DFP par un acheteur** Google **ou** AdX.

## Créer une destination

1. In **[!UICONTROL Connections > Destinations]**, select Google Ad Manager, and select **[!UICONTROL Create destination]**.
   ![Connexion à la destination de Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination.png)

2. In the Create destination workflow, fill in the [!UICONTROL Basic Information] for the destination. <br>

   ![Informations de base Google Ad Manager](/help/rtcdp/destinations/assets/google-1-basic-information.png)
* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utilisation `DFP by Google` pour DoubleClick pour les éditeurs
   * Utilisez `AdX buyer` pour Google AdX.
* **[!UICONTROL Identifiant de compte]** : renseignez votre identifiant de compte avec Google. Il peut s’agir de votre ID réseau ou de votre ID de lien d’Audience. En règle générale, il s’agit d’un identifiant à huit chiffres.

>[!NOTE]
>
>Lors de la configuration d’une destination Google Ad Manager, demandez à votre gestionnaire de compte Google ou à votre représentant Adobe de déterminer le type de compte qui vous appartient.

## Activer les segments dans Google Ad Manager

For instructions on how to activate segments to Google Ad Manager, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).