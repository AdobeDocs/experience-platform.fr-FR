---
keywords: activation des destinations de requête de profil;activation des données;destinations de requête de profil
title: Activation des données d’audience vers les destinations de requête de profil
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: Découvrez comment activer les données d’audience que vous avez dans Adobe Experience Platform en mappant les segments aux destinations de requête de profil.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
source-git-commit: caccd096c9165139d9b966bbfcb311456276192a
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 10%

---

# Activation des données d’audience vers les destinations de requête de profil (version bêta)

## Présentation {#overview}

>[!IMPORTANT]
>
>Les destinations de demande de profil dans Adobe Experience Platform sont actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Cet article explique le workflow requis pour activer les données d’audience dans les destinations de demande de profil Adobe Experience Platform. Les [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) et les [connexions personnalisées](../../destinations/catalog/personalization/custom-personalization.md) sont des exemples de destinations de demande de profil.

## Conditions préalables {#prerequisites}

Pour activer les données vers les destinations, vous devez être [connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue des destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

### Stratégie de fusion de segments {#merge-policy}

Actuellement, les destinations de requête de profil ne prennent en charge que l’activation des segments qui utilisent la stratégie de fusion par défaut. Toute tentative d’activation de segments avec une stratégie de fusion différente entraîne une erreur dans la page [[!UICONTROL Réviser]](#review).

## Sélectionner votre destination {#select-destination}

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Onglet Catalogue de destinations](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Sélectionnez **[!UICONTROL Activer les segments]** sur la carte correspondant à la destination vers laquelle vous souhaitez activer vos segments, comme illustré dans l’image ci-dessous.

   ![Boutons Activer](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Sélectionnez la connexion de destination à utiliser pour activer vos segments, puis cliquez sur **[!UICONTROL Suivant]**.

   ![Sélectionner la destination](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Passez à la section suivante pour [sélectionner vos segments](#select-segments).

## Sélection de vos segments {#select-segments}

Utilisez les cases à cocher situées à gauche des noms de segment pour sélectionner les segments que vous souhaitez activer vers la destination, puis sélectionnez **[!UICONTROL Suivant]**.

![Sélection de segments](../assets/ui/activate-profile-request-destinations/select-segments.png)

## Planification de l’exportation de segments {#scheduling}

Par défaut, la page [!UICONTROL Planification du segment] affiche uniquement les segments que vous avez choisis dans le flux d’activation actuel.

![Nouveaux segments](../assets/ui/activate-profile-request-destinations/new-segments.png)

Pour voir tous les segments activés vers votre destination, utilisez l’option de filtrage et désactivez le filtre **[!UICONTROL Afficher les nouveaux segments uniquement]** .

![Tous les segments](../assets/ui/activate-profile-request-destinations/all-segments.png)

Sur la page **[!UICONTROL Planification du segment]** , sélectionnez chaque segment, puis utilisez les sélecteurs **[!UICONTROL Date de début]** et **[!UICONTROL Date de fin]** pour configurer l’intervalle d’envoi des données à votre destination.

![Planification du segment](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Sélectionnez **[!UICONTROL Suivant]** pour accéder à la page [!UICONTROL Révision].

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

>[!IMPORTANT]
>
>Au cours de cette étape, Adobe Experience Platform recherche les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation d’une stratégie. Vous ne pouvez pas terminer le workflow d’activation du segment tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la manière de résoudre les violations de stratégie, voir [Application de la stratégie](../../rtcdp/privacy/data-governance-overview.md#enforcement) dans la section de documentation sur la gouvernance des données.

![violation de la politique de données](../assets/common/data-policy-violation.png)

Si aucune violation de stratégie n’a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

![Révision](../assets/ui/activate-profile-request-destinations/review.png)

## Vérification de l’activation des segments {#verify}

Consultez la [documentation sur la surveillance des destinations](../../dataflows/ui/monitor-destinations.md) pour obtenir des informations détaillées sur la manière de surveiller le flux de données vers vos destinations.