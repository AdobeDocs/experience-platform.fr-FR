---
keywords: activation des destinations de requête de profil;activation des données;destinations de requête de profil
title: Activation des données d’audience vers les destinations de requête de profil (version bêta)
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: Découvrez comment activer les données d’audience que vous avez dans Adobe Experience Platform en mappant les segments aux destinations de requête de profil.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: d0660f29df93659990d80353f86dcbf856afb733
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 8%

---

# Activation des données d’audience vers les destinations de requête de profil

## Présentation {#overview}

Cet article explique le workflow requis pour activer les données d’audience dans les destinations de demande de profil Adobe Experience Platform. Voici des exemples de destinations de requête de profil : [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) et le [Personnalisation personnalisée](../../destinations/catalog/personalization/custom-personalization.md) connexions.

## Conditions préalables {#prerequisites}

Pour activer les données vers les destinations, vous devez avoir réussi [connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

### Stratégie de fusion de segments {#merge-policy}

Actuellement, les destinations de requête de profil ne prennent en charge que l’activation des segments qui utilisent la variable [Stratégie de fusion principale sur périphérie](../../segmentation/ui/segment-builder.md#merge-policies) défini comme valeur par défaut.

## Sélectionner votre destination {#select-destination}

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez la variable **[!UICONTROL Catalogue]** .

   ![Onglet Catalogue de destinations](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Sélectionner **[!UICONTROL Activation des segments]** sur la carte correspondant à la destination vers laquelle vous souhaitez activer vos segments, comme illustré dans l’image ci-dessous.

   ![Boutons Activer](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Sélectionnez la connexion de destination à utiliser pour activer vos segments, puis sélectionnez **[!UICONTROL Suivant]**.

   ![Sélectionner la destination](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Accédez à la section suivante pour [sélectionner vos segments ;](#select-segments).

## Sélection de vos segments {#select-segments}

Utilisez les cases à cocher situées à gauche des noms de segment pour sélectionner les segments que vous souhaitez activer vers la destination, puis sélectionnez **[!UICONTROL Suivant]**.

![Sélection de segments](../assets/ui/activate-profile-request-destinations/select-segments.png)

## Planification de l’exportation de segments {#scheduling}

Par défaut, la variable [!UICONTROL Planification du segment] affiche uniquement les segments que vous avez sélectionnés dans le flux d’activation actuel.

![Nouveaux segments](../assets/ui/activate-profile-request-destinations/new-segments.png)

Pour afficher tous les segments activés vers votre destination, utilisez l’option de filtrage et désactivez la variable **[!UICONTROL Afficher les nouveaux segments uniquement]** filtre.

![Tous les segments](../assets/ui/activate-profile-request-destinations/all-segments.png)

Sur le **[!UICONTROL Planification du segment]** , sélectionnez chaque segment, puis utilisez la méthode **[!UICONTROL Date de début]** et **[!UICONTROL Date de fin]** sélecteurs pour configurer l’intervalle d’envoi des données à votre destination.

![Planification du segment](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Sélectionner **[!UICONTROL Suivant]** pour accéder au [!UICONTROL Réviser] page.

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

>[!IMPORTANT]
>
>Au cours de cette étape, Adobe Experience Platform recherche les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation d’une stratégie. Vous ne pouvez pas terminer le workflow d’activation du segment tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la résolution des violations de stratégie, voir [Application des stratégies](../../rtcdp/privacy/data-governance-overview.md#enforcement) dans la section documentation sur la gouvernance des données .

![violation de la politique de données](../assets/common/data-policy-violation.png)

Si aucune violation de stratégie n’a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer des données à la destination.

![Révision](../assets/ui/activate-profile-request-destinations/review.png)

## Vérification de l’activation des segments {#verify}

Vérifiez les [documentation sur la surveillance des destinations](../../dataflows/ui/monitor-destinations.md) pour obtenir des informations détaillées sur la manière de surveiller le flux de données vers vos destinations.
