---
keywords: activation des destinations de diffusion en continu de segments ; activation des destinations de diffusion en continu de segments ; activation des données
title: Activation des données d’audience vers des destinations d’exportation de segments de diffusion
type: Tutorial
seo-title: Activate audience data to streaming segment export destinations
description: Découvrez comment activer les données d’audience que vous avez dans Adobe Experience Platform en mappant les segments aux destinations de diffusion en continu de segments.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to segment streaming destinations.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 8%

---

# Activation des données d’audience vers des destinations d’exportation de segments de diffusion

## Présentation {#overview}

Cet article explique le workflow requis pour activer les données d’audience dans les destinations de diffusion en continu de segments Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Pour activer les données vers les destinations, vous devez être [connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue des destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

## Sélectionner votre destination {#select-destination}

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Onglet Catalogue de destinations](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Sélectionnez **[!UICONTROL Activer les segments]** sur la carte correspondant à la destination vers laquelle vous souhaitez activer vos segments, comme illustré dans l’image ci-dessous.

   ![Boutons Activer](../assets/ui/activate-segment-streaming-destinations/activate-segments-button.png)

1. Sélectionnez la connexion de destination à utiliser pour activer vos segments, puis cliquez sur **[!UICONTROL Suivant]**.

   ![Sélectionner la destination](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Passez à la section suivante pour [sélectionner vos segments](#select-segments).

## Sélection de vos segments {#select-segments}

Utilisez les cases à cocher situées à gauche des noms de segment pour sélectionner les segments que vous souhaitez activer vers la destination, puis sélectionnez **[!UICONTROL Suivant]**.

![Sélection de segments](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## Mise en correspondance des attributs et des identités {#mapping}

>[!IMPORTANT]
>
>Cette étape s’applique uniquement à certaines destinations de diffusion en continu de segments. Si votre destination ne comporte pas d’étape **[!UICONTROL Mapping]**, passez à [Planification de l’exportation de segments](#scheduling).

Certaines destinations de diffusion en continu de segments nécessitent que vous sélectionniez des attributs source ou des espaces de noms d’identité à mapper en tant qu’identités cibles dans la destination.

1. Dans la page **[!UICONTROL Mapping]** , sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**.

   ![Ajouter un nouveau mappage](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Sélectionnez la flèche située à droite de l&#39;entrée **[!UICONTROL Champ source]**.

   ![Sélectionner le champ source](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. Dans la page **[!UICONTROL Sélectionner le champ source]** , utilisez les options **[!UICONTROL Sélectionner les attributs]** ou **[!UICONTROL Sélectionner l’espace de noms de l’identité]** pour basculer entre les deux catégories de champs sources disponibles. Dans les [!DNL XDM] attributs de profil et espaces de noms d’identité disponibles, sélectionnez ceux que vous souhaitez mapper à la destination, puis choisissez **[!UICONTROL Sélectionner]**.

   ![Sélectionner la page du champ source](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Sélectionnez le bouton situé à droite de l’entrée **[!UICONTROL Champ cible]**.

   ![Sélectionner le champ cible](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. Dans la page **[!UICONTROL Sélectionner un champ cible]** , sélectionnez l’espace de noms d’identité cible auquel vous souhaitez mapper le champ source, puis sélectionnez **[!UICONTROL Sélectionner]**.

   ![Sélectionner la page de champ cible](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Pour ajouter d’autres mappages, répétez les étapes 1 à 5.

### Appliquer la transformation {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Appliquer la transformation"
>abstract="Cochez cette option lorsque vous utilisez des champs source non hachés afin que Adobe Experience Platform les hache automatiquement lors de l’activation."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#apply-transformation" text="En savoir plus dans la documentation"

Lorsque vous mappez des attributs source non hachés avec des attributs cibles que la destination s’attend à être hachée (par exemple : `email_lc_sha256` ou `phone_sha256`), cochez l’option **Appliquer la transformation** pour que Adobe Experience Platform hache automatiquement les attributs source lors de l’activation.

![Mappage des identités](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Planification de l’exportation de segments {#scheduling}

Par défaut, la page [!UICONTROL Planification du segment] affiche uniquement les segments que vous avez choisis dans le flux d’activation actuel.

![Nouveaux segments](../assets/ui/activate-segment-streaming-destinations/new-segments.png)

Pour voir tous les segments activés vers votre destination, utilisez l’option de filtrage et désactivez le filtre **[!UICONTROL Afficher les nouveaux segments uniquement]** .

![Tous les segments](../assets/ui/activate-segment-streaming-destinations/all-segments.png)

1. Sur la page **[!UICONTROL Planification du segment]** , sélectionnez chaque segment, puis utilisez les sélecteurs **[!UICONTROL Date de début]** et **[!UICONTROL Date de fin]** pour configurer l’intervalle d’envoi des données à votre destination.

   ![Planification du segment](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * Pour certaines destinations, vous devez sélectionner **[!UICONTROL Origine de l’audience]** pour chaque segment, à l’aide du menu déroulant situé sous les sélecteurs de calendrier. Si votre destination n’inclut pas ce sélecteur, ignorez cette étape.

      ![ID de mappage](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Certaines destinations nécessitent que vous mappiez manuellement des segments [!DNL Platform] à leur contrepartie dans la destination cible. Pour ce faire, sélectionnez chaque segment, puis saisissez l’identifiant de segment correspondant à partir de la plateforme de destination dans le champ **[!UICONTROL Identifiant du mappage]** . Si votre destination n’inclut pas ce champ, ignorez cette étape.

      ![ID de mappage](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Certaines destinations nécessitent que vous saisissiez un **[!UICONTROL ID d’application]** lors de l’activation de segments [!DNL IDFA] ou [!DNL GAID]. Si votre destination n’inclut pas ce champ, ignorez cette étape.

      ![ID d’application](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Sélectionnez **[!UICONTROL Suivant]** pour accéder à la page [!UICONTROL Révision].

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

>[!IMPORTANT]
>
>Au cours de cette étape, Adobe Experience Platform recherche les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation d’une stratégie. Vous ne pouvez pas terminer le workflow d’activation du segment tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la manière de résoudre les violations de stratégie, voir [Application de la stratégie](../../rtcdp/privacy/data-governance-overview.md#enforcement) dans la section de documentation sur la gouvernance des données.

![violation de la politique de données](../assets/common/data-policy-violation.png)

Si aucune violation de stratégie n’a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

![Révision](../assets/ui/activate-segment-streaming-destinations/review.png)

## Vérification de l’activation des segments {#verify}

Consultez la [documentation sur la surveillance des destinations](../../dataflows/ui/monitor-destinations.md) pour obtenir des informations détaillées sur la manière de surveiller le flux de données vers vos destinations.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
