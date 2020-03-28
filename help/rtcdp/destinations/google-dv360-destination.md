---
title: Destination Google Display & Video 360
seo-title: Destination Google Display & Video 360
description: Display & Video 360, anciennement connu sous le nom de DoubleClick Bid Manager, est un outil utilisé pour exécuter le reciblage et  des campagnes numériques ciblées  des sources d’inventaire Display, Video et Mobile.
seo-description: 'Display & Video 360, anciennement connu sous le nom de DoubleClick Bid Manager, est un outil utilisé pour exécuter le reciblage et  des campagnes numériques ciblées  des sources d’inventaire Display, Video et Mobile. '
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Destination Google Display &amp; Video 360

## Présentation

Display &amp; Video 360, anciennement connu sous le nom de DoubleClick Bid Manager, est un outil utilisé pour exécuter le reciblage et  des campagnes numériques ciblées  des sources d’inventaire Display, Video et Mobile.

## Spécifications de la destination

Notez les détails suivants qui sont spécifiques aux destinations Google Display &amp; Video 360 :

* Vous pouvez envoyer les [identités](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) suivantes aux destinations Google Display &amp; Video 360 : Identifiant de cookie **Google, IDFA, GAID, ID Roku, ID Microsoft, ID Amazon Fire TV**.
* Les audiences activées sont créées par programmation dans la plateforme Google.
* La plateforme CDP en temps réel Adobe n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Reportez-vous au nombre de  de  dans Google pour valider l’intégration et comprendre la taille de ciblage des  de  de de Google.

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec Google Display &amp; Video 360 et que vous n’avez pas activé la fonctionnalité [de synchronisation des](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) identifiants dans le service d’ID d’Experience Cloud par le passé (avec Adobe   Manager ou d’autres applications), contactez le service à la clientèle ou le service de conseil d’Adobe pour activer la synchronisation des identifiants. Si vous aviez précédemment configuré des intégrations Google dans  Gestionnaire de  de, les synchronisations d’ID que vous avez configurées sont transférées au CDP en temps réel d’Adobe.

## Conditions préalables

### Liste blanche

>[!NOTE]
>
>La liste blanche est obligatoire avant de configurer votre première destination Google Display &amp; Video 360 dans Adobe Real-time CDP. Veuillez vous assurer que le processus de liste blanche décrit ci-dessous a été terminé par Google avant de créer une destination.

Avant de créer la destination Google Display &amp; Video 360 dans le CDP en temps réel d’Adobe, vous devez contacter Google pour demander qu’Adobe soit autorisé en tant que fournisseur de données et que votre compte soit autorisé. Contactez Google et fournissez les informations suivantes :

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec Google. Contactez le service à la clientèle Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec Google. Contactez le service à la clientèle Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Type** de compte : permet **[!DNL Invite advertiser]** à   d’être partagé uniquement avec une marque spécifique de votre compte Display &amp; Video 360 ou **[!DNL Invite partner]** de permettre à  d’être partagé avec toutes les marques de votre compte Display &amp; Video 360.

## Créer une destination

1. Dans **[!UICONTROL Connections > Destinations]** Google Display &amp; Video 360, sélectionnez **[!UICONTROL Create destination]**.
   ![Connectez la destination Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. Dans le flux de travail Créer une destination, renseignez le champ [!UICONTROL Basic Information] pour la destination.
   ![Informations de base Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-basic-information.png)
* **[!UICONTROL Name]**: Renseignez le nom préféré pour cette destination.
* **[!UICONTROL Description]**: Facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Account Type]**: Sélectionnez une option, selon votre compte auprès de Google :
   * Utilisez `Invite Advertiser` cette option pour autoriser   à être partagés uniquement avec une marque spécifique dans votre compte Display &amp; Video 360.
   * Utilisez `Invite Partner` cette option pour permettre   d’être partagés avec toutes les marques de votre compte Display &amp; Video 360.
* **[!UICONTROL Account ID]**: Renseignez votre **[!DNL Invite partner]** ID de compte ou votre **[!DNL Invite advertiser]** ID de compte auprès de Google. En règle générale, il s’agit d’un identifiant à six ou sept chiffres.

>[!NOTE]
>
>Lors de la configuration d’une destination Google Display &amp; Video 360, contactez votre gestionnaire de compte Google ou votre représentant Adobe pour savoir quel type de compte vous avez.

## Activer les segments dans Google Display &amp; Video 360

For instructions on how to activate segments to Google Display &amp; Video 360, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).