---
title: Destination Google Ads
seo-title: Destination Google Ads
description: Google Ads, appelé auparavant Google AdWords, est un service de publicité en ligne qui permet aux entreprises faire de la publicité avec paiement par clic sur des recherches textuelles, des affichages graphiques, des vidéos YouTube et des affichages mobiles in-app.
seo-description: Google Ads, appelé auparavant Google AdWords, est un service de publicité en ligne qui permet aux entreprises faire de la publicité avec paiement par clic sur des recherches textuelles, des affichages graphiques, des vidéos YouTube et des affichages mobiles in-app.
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 28%

---


# Destination Google Ads

## Présentation

Google Ads, appelé auparavant Google AdWords, est un service de publicité en ligne qui permet aux entreprises faire de la publicité avec paiement par clic sur des recherches textuelles, des affichages graphiques, des vidéos YouTube et des affichages mobiles in-app.

## Spécifications de la destination

Notez les détails suivants spécifiques aux destinations de publicités Google :

* Vous pouvez envoyer les [identités](../../identity-service/namespaces.md) suivantes vers les destinations de publicités Google : **ID de cookie Google, IDFA, GAID, ID de Roku, ID Microsoft, ID** Amazon Fire TV.
* Les audiences activées sont créées par programmation dans la plateforme Google.
* La plateforme CDP en temps réel Adobe n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Reportez-vous au décompte des audiences dans Google pour valider l’intégration et comprendre la taille du ciblage des audiences.

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec des publicités Google et que vous n’avez pas activé la fonctionnalité [de synchronisation des](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) identifiants dans le service d’identification des Experience Cloud dans le passé (avec Audience Manager ou d’autres applications), contactez le service de conseil ou d’assistance clientèle Adobe pour activer la synchronisation des identifiants. Si vous aviez précédemment configuré des intégrations Google dans l’Audience Manager, les synchronisations d’identifiants que vous avez configurées sont transférées au CDP Adobe Real-time.

## Conditions préalables

### Compte Publicités Google existant

Google a suspendu toute nouvelle intégration de publicités Google avec des fournisseurs tiers. Vous devez disposer d’une intégration existante avec les publicités Google afin de pouvoir exécuter les étapes de liste autorisée de la section suivante et de créer une destination des publicités Google dans le fichier CDP en temps réel Adobe.

### Liste autorisée

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première destination de publicités Google dans Adobe Real-time CDP. Assurez-vous que le processus de liste autorisée décrit ci-dessous a été effectué par Google avant de créer une destination.

Avant de créer la destination des publicités Google dans le CDP en temps réel d’Adobe, vous devez contacter Google pour que Adobe soit mis sur la liste des fournisseurs de données autorisés et que votre compte soit ajouté à la liste autorisée. Contactez Google et fournissez les informations suivantes :

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec Google. Contactez le service à la clientèle Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec Google. Contactez le service à la clientèle Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* Votre type de compte : **AdWords**
* **Identifiant** Google AdWords : C&#39;est votre identifiant avec Google. Le format d’ID est généralement 123-456-7890.

## Créer une destination

1. In **[!UICONTROL Connections > Destinations]**, select Google Ads, and select **[!UICONTROL Create destination]**.
   ![Connecter la destination des publicités Google](/help/rtcdp/destinations/assets/google-2-destination.png)

2. À l’étape **Configuration** du processus de création de destination, renseignez les informations [!UICONTROL de] base de la destination. <br>

   ![Informations de base Publicités Google](/help/rtcdp/destinations/assets/google-ads-setup-step.png)
* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type]** de compte : AdWords est la seule option disponible.
* **[!UICONTROL ID]** du compte : Renseignez votre ID de compte avec des publicités Google. Le format d’ID est généralement 123-456-7890.
* **[!UICONTROL Cas]** d’utilisation marketing : Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi les cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis individuellement par Adobe, voir l’aperçu [des stratégies d’utilisation des](/help/data-governance/policies/overview.md#core-actions)données.

## Activer des segments dans des publicités Google

For instructions on how to activate segments to Google Ads, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).

