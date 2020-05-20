---
title: Destination Google Display & Video 360
seo-title: Destination Google Display & Video 360
description: Display & Video 360, anciennement appelé DoubleClick Bid Manager, est un outil utilisé pour exécuter le reciblage et des campagnes digitales ciblées dans des sources d’inventaire Display, Video et Mobile.
seo-description: 'Display & Video 360, anciennement appelé DoubleClick Bid Manager, est un outil utilisé pour exécuter le reciblage et des campagnes digitales ciblées dans des sources d’inventaire Display, Video et Mobile. '
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 27%

---


# Destination Google Display &amp; Video 360

## Présentation

Display &amp; Video 360, anciennement connu sous le nom de DoubleClick Bid Manager, est un outil utilisé pour exécuter des campagnes numériques ciblées de reciblage et d’audience sur plusieurs sources d’inventaire Display, Video et Mobile.

## Spécifications de la destination

Notez les détails suivants spécifiques aux destinations Google Display &amp; Video 360 :

* Vous pouvez envoyer les [identités](../../identity-service/namespaces.md) suivantes aux destinations Google Display &amp; Video 360 : **ID de cookie Google, IDFA, GAID, ID de Roku, ID Microsoft, ID** Amazon Fire TV.
* Les audiences activées sont créées par programmation dans la plateforme Google.
* La plateforme CDP en temps réel Adobe n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Reportez-vous au décompte des audiences dans Google pour valider l’intégration et comprendre la taille du ciblage des audiences.

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec Google Display &amp; Video 360 et que vous n’avez pas activé la fonctionnalité [de synchronisation des](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) identifiants dans le service d’ID d’Experience Cloud dans le passé (avec Adobe Audience Manager ou d’autres applications), contactez le service à la clientèle ou le service de conseil d’Adobe pour activer la synchronisation des identifiants. Si vous aviez précédemment configuré des intégrations Google dans Audience Manager, les synchronisations d’identifiants que vous avez configurées sont transférées au CDP en temps réel d’Adobe.

## Conditions préalables

### Liste blanche

>[!NOTE]
>
>La liste blanche est obligatoire avant de configurer votre première destination Google Display &amp; Video 360 dans Adobe Real-time CDP. Assurez-vous que la procédure de liste blanche décrite ci-dessous a été effectuée par Google avant de créer une destination.

Avant de créer la destination Google Display &amp; Video 360 dans Adobe Real-time CDP, vous devez contacter Google pour demander qu’Adobe soit autorisé en tant que fournisseur de données et que votre compte soit autorisé. Contactez Google et fournissez les informations suivantes :

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec Google. Contactez le service à la clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec Google. Contactez le service à la clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Type** de compte : permet **[!DNL Invite advertiser]** aux audiences d’être partagées uniquement avec une marque spécifique de votre compte Display &amp; Video 360 ou **[!DNL Invite partner]** d’être partagées avec toutes les marques de votre compte Display &amp; Video 360.

## Créer une destination

1. In **[!UICONTROL Connections > Destinations]**, select Google Display &amp; Video 360, and select **[!UICONTROL Create destination]**.
   ![Connecter la destination Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. In the Create destination workflow, fill in the [!UICONTROL Basic Information] for the destination.
   ![Informations de base Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-basic-information.png)
* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte avec Google :
   * Permet `Invite Advertiser` d’autoriser le partage d’audiences uniquement à une marque spécifique dans votre compte Display &amp; Video 360.
   * Permet `Invite Partner` de partager des audiences avec toutes les marques de votre compte Display &amp; Video 360.
* **[!UICONTROL ID]** du compte : Renseignez votre **[!DNL Invite partner]** ID de **[!DNL Invite advertiser]** compte ou votre identifiant de compte auprès de Google. En règle générale, il s’agit d’un identifiant à six ou sept chiffres.

>[!NOTE]
>
>Lors de la configuration d’une destination Google Display &amp; Video 360, contactez votre gestionnaire de compte Google ou votre représentant Adobe pour savoir quel type de compte vous possédez.

## Activer les segments dans Google Display &amp; Video 360

For instructions on how to activate segments to Google Display &amp; Video 360, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).