---
title: Google AdsDestination
seo-title: Destination des publicités Google
description: Google Ads, anciennement appelé Google AdWords, est un service de publicité en ligne qui permet aux entreprises de payer la publicité par clic sur les recherches textuelles, les affichages graphiques, les vidéos YouTube et les affichages mobiles in-app.
seo-description: Google Ads, anciennement appelé Google AdWords, est un service de publicité en ligne qui permet aux entreprises de payer la publicité par clic sur les recherches textuelles, les affichages graphiques, les vidéos YouTube et les affichages mobiles in-app.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Destination des publicités Google

## Présentation

Google Ads, anciennement appelé Google AdWords, est un service de publicité en ligne qui permet aux entreprises de payer la publicité par clic sur les recherches textuelles, les affichages graphiques, les vidéos YouTube et les affichages mobiles in-app.

## Spécifications de la destination

Notez les détails suivants qui sont spécifiques aux destinations de publicités Google :

* Vous pouvez envoyer les [identités](../../identity-service/namespaces.md) suivantes vers les destinations de publicités Google : Identifiant de cookie **Google, IDFA, GAID, ID Roku, ID Microsoft, ID Amazon Fire TV**.
* Les audiences activées sont créées par programmation dans la plateforme Google.
* La plateforme CDP en temps réel Adobe n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Reportez-vous au nombre de  de  dans Google pour valider l’intégration et comprendre la taille de ciblage des  de  de de Google.

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec des publicités Google et que vous n’avez pas activé la fonctionnalité [de synchronisation des](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) identifiants dans le service d’ID Experience Cloud par le passé (avec  Gestionnaire de  de ou d’autres applications), contactez le service de conseil ou le service à la clientèle d’Adobe pour activer la synchronisation des identifiants. Si vous aviez précédemment configuré des intégrations Google dans  Gestionnaire de  de, les synchronisations d’ID que vous avez configurées sont transférées au CDP en temps réel d’Adobe.

## Conditions préalables

### Compte de publicités Google existant

Google a suspendu toute nouvelle intégration Google Ads avec des fournisseurs tiers. Vous devez disposer d’une intégration existante avec les publicités Google afin de pouvoir exécuter les étapes de liste blanche dans la section suivante et de créer une destination des publicités Google dans le CDP en temps réel d’Adobe.

### Liste blanche

>[!NOTE]
>
>La liste blanche est obligatoire avant de configurer votre première destination de publicités Google dans Adobe CDP en temps réel. Veuillez vous assurer que le processus de liste blanche décrit ci-dessous a été terminé par Google avant de créer une destination.

Avant de créer la destination des publicités Google dans Adobe CDP en temps réel, vous devez contacter Google pour demander à Adobe d’être autorisé en tant que fournisseur de données et à ce que votre compte soit autorisé. Contactez Google et fournissez les informations suivantes :

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec Google. Contactez le service à la clientèle Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec Google. Contactez le service à la clientèle Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* Votre type de compte : **AdWords**
* **Identifiant** Google AdWords : C&#39;est votre identifiant avec Google. Le format d’ID est généralement 123-456-7890.

## Créer une destination

1. Dans **[!UICONTROL Connections > Destinations]**, sélectionnez Publicités Google, puis sélectionnez **[!UICONTROL Create destination]**.
   ![Connecter la destination des publicités Google](/help/rtcdp/destinations/assets/google-2-destination.png)

2. Dans le flux de travail Créer une destination, renseignez le champ [!UICONTROL Basic Information] pour la destination.
   ![Informations de base Publicités Google](/help/rtcdp/destinations/assets/google-2-basic-information.png)
* **[!UICONTROL Name]**: Renseignez le nom préféré pour cette destination.
* **[!UICONTROL Description]**: Facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Account Type]**: AdWords est la seule option disponible.
* **[!UICONTROL Account ID]**: Renseignez votre ID de compte avec les publicités Google. Le format d’ID est généralement 123-456-7890.

## Activer les segments dans les publicités Google

For instructions on how to activate segments to Google Ads, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).

