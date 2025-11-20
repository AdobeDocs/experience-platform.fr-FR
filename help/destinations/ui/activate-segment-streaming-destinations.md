---
title: Activer les données d’audience vers des destinations de diffusion en continu
type: Tutorial
description: Découvrez comment activer les audiences que vous avez dans Adobe Experience Platform en les mappant aux destinations de diffusion en streaming.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 595856842a3890426bb196218bd8be4e321ff8aa
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 12%

---


# Activer les audiences vers des destinations de diffusion en continu

>[!IMPORTANT]
> 
> * Pour activer les audiences et activer l’[étape de mappage](#mapping) du workflow, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [&#128279;](/help/access-control/home.md#permissions).
> * Pour activer les audiences sans passer par l’étape [mappage](#mapping) du workflow, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [&#128279;](/help/access-control/home.md#permissions).
> * Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}
> 
> Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

## Présentation {#overview}

Cet article explique le processus requis pour activer des audiences dans les destinations de diffusion en streaming Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Pour activer des audiences vers des destinations, vous devez avoir réussi à vous [connecter à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

## Sélectionner votre destination {#select-destination}

1. Accédez à **[!UICONTROL Connections > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalog]** .

   ![Onglet Catalogue de destinations présentant diverses destinations de diffusion en streaming.](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Sélectionnez **[!UICONTROL Activate audiences]** sur la vignette correspondant à la destination vers laquelle vous souhaitez activer vos audiences, comme illustré dans l’image ci-dessous.

   ![Activer le contrôle en surbrillance dans le catalogue des destinations.](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. Sélectionnez la connexion de destination à utiliser pour activer des audiences, puis sélectionnez **[!UICONTROL Next]**.

   ![Une connexion de destination mise en surbrillance lors de l’étape Sélectionner la destination.](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Accédez à la section suivante pour [sélectionner vos audiences](#select-audiences).

## Sélectionner vos audiences {#select-audiences}

Pour sélectionner les audiences à activer vers la destination, utilisez les cases à cocher situées à gauche des noms d’audience, puis sélectionnez **[!UICONTROL Next]**.

Vous pouvez effectuer un choix parmi plusieurs types d’audiences, selon leur origine :

* **[!UICONTROL Segmentation Service]** : audiences générées dans Experience Platform par Segmentation Service. Voir la [documentation sur la segmentation](../../segmentation/ui/overview.md) pour plus d’informations.
* **[!UICONTROL Custom upload]** : audiences générées en dehors d’Experience Platform et chargées dans Experience Platform au format CSV. Pour en savoir plus sur les audiences externes, consultez la documentation sur [importation d’une audience](../../segmentation/ui/audience-portal.md#import-audience).
* Autres types d’audiences, provenant d’autres solutions Adobe, telles que [!DNL Audience Manager].

![Plusieurs audiences mises en surbrillance lors de l’étape Sélectionner des audiences.](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## Mapper les attributs et les identités {#mapping}

>[!IMPORTANT]
>
>Cette étape s’applique uniquement à certaines destinations de diffusion en continu d’audience. Si votre destination ne comporte pas d’étape **[!UICONTROL Mapping]**, passez à la [planification des audiences](#scheduling).
>
>Lors de l’activation des audiences vers des destinations de diffusion en continu, vous devez également mapper *au moins un espace de noms d’identité cible*, en plus des attributs de profil cible. Sinon, les audiences ne seront pas activées vers la plateforme de destination.
> ![Image de l’étape de mappage montrant un mappage obligatoire des espaces de noms d’identité.](../assets/ui/activate-segment-streaming-destinations/identity-mapping-mandatory.png) {zoomable="yes"}


Certaines destinations de diffusion en continu d’audience nécessitent que vous sélectionniez des attributs sources ou des espaces de noms d’identité à mapper en tant qu’identités cibles dans la destination.

1. Dans la page **[!UICONTROL Mapping]**, sélectionnez **[!UICONTROL Add new mapping]**.

   ![Ajouter un nouveau contrôle de mappage mis en surbrillance.](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Sélectionnez la flèche située à droite de l’entrée **[!UICONTROL Source field]**.

   ![Sélectionner le contrôle du champ source en surbrillance.](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. Dans la page **[!UICONTROL Select source field]**, utilisez les options **[!UICONTROL Select attributes]** ou **[!UICONTROL Select identity namespace]** pour basculer entre les deux catégories de champs sources disponibles. Dans les attributs de profil [!DNL XDM] et les espaces de noms d’identité disponibles, sélectionnez ceux que vous souhaitez mapper à la destination, puis choisissez **[!UICONTROL Select]**.

   Utilisez le bouton **[!UICONTROL Show only fields with data]** pour afficher uniquement les champs de schéma remplis de valeurs. Par défaut, seuls les champs de schéma renseignés s’affichent.

   ![Page Sélectionner le champ source présentant plusieurs champs source disponibles.](../assets/ui/activate-segment-streaming-destinations/select-source-field-modal.png)

1. Sélectionnez le bouton situé à droite de l’entrée **[!UICONTROL Target field]** .

   ![Sélectionner le champ cible en surbrillance.](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. Dans la page **[!UICONTROL Select target field]** , sélectionnez l’espace de noms d’identité cible vers lequel vous souhaitez mapper le champ source, puis choisissez **[!UICONTROL Select]**.

   ![Page Sélectionner un champ cible présentant les options disponibles pour les mappages de champs cibles.](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Pour ajouter d’autres mappages, répétez les étapes 1 à 5.

### Appliquer la transformation {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Appliquer la transformation"
>abstract="Cochez cette option lorsque vous utilisez des champs sources non hachés afin qu’Adobe Experience Platform les hache automatiquement au moment de l’activation."

Quand vous mappez des attributs source non hachés avec des attributs cibles qui sont censés être hachés (par exemple, `email_lc_sha256` ou `phone_sha256`), cochez l’option **Apply transformation** (Appliquer la transformation) pour qu’Adobe Experience Platform hache automatiquement les attributs source au moment de l’activation.

![Appliquez le contrôle de transformation mis en surbrillance à l’étape Mappage d’identité.](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Planifier l’export d’audience {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Date de fin"
>abstract="L’ajout d’une date de fin pour le planning des audiences n’est pas disponible."

Par défaut, la page **[!UICONTROL Audience schedule]** n’affiche que les audiences nouvellement sélectionnées que vous avez choisies dans le flux d’activation actuel.

Pour afficher toutes les audiences activées vers la destination, utilisez l’option de filtrage et désactivez le filtre **[!UICONTROL Show new audiences only]**.

![Toutes les audiences &#x200B;](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. Sur la page **[!UICONTROL Audience schedule]**, sélectionnez chaque audience, puis utilisez les sélecteurs **[!UICONTROL Start date]** et **[!UICONTROL End date]** pour configurer l’intervalle de temps pour envoyer les données vers la destination.

   ![Filtre du planning d’audience mis en surbrillance.](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * Certaines destinations nécessitent de sélectionner la **[!UICONTROL Origin of audience]** pour chaque audience à l’aide du menu déroulant situé sous les sélecteurs de calendrier. Si la destination n’inclut pas ce sélecteur, ignorez cette étape.

     ![Liste déroulante d’identifiant de mappage mise en surbrillance.](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Certaines destinations nécessitent que vous mappiez manuellement des audiences [!DNL Experience Platform] à leur homologue dans la destination cible. Pour cela, sélectionnez chaque audience, puis saisissez l’identifiant d’audience correspondant à partir de la plateforme de destination dans le champ **[!UICONTROL Mapping ID]** . Si la destination n’inclut pas ce champ, ignorez cette étape.

     ![Liste déroulante Origine de l’audience mise en surbrillance.](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Certaines destinations nécessitent de saisir un **[!UICONTROL App ID]** lors de l’activation d’audiences [!DNL IDFA] ou [!DNL GAID]. Si la destination n’inclut pas ce champ, ignorez cette étape.

     ![Liste déroulante d’ID d’application mise en surbrillance.](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Sélectionnez **[!UICONTROL Next]** pour accéder à la page [!UICONTROL Review].

## Réviser {#review}

Sur la page **[!UICONTROL Review]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Cancel]** pour interrompre le flux, **[!UICONTROL Back]** pour modifier vos paramètres ou **[!UICONTROL Finish]** pour confirmer votre sélection et commencer à envoyer des données à la destination.

![Résumé de la sélection à l’étape de révision.](../assets/ui/activate-segment-streaming-destinations/review.png)

### Évaluation des politiques de consentement {#consent-policy-evaluation}

Si votre organisation a acheté **Adobe Healthcare Shield** ou **Adobe Privacy &amp; Security Shield**, sélectionnez **[!UICONTROL View applicable consent policies]** pour identifier les politiques de consentement appliquées et le nombre de profils inclus dans l’activation qui en résulte. Pour plus d’informations, consultez [&#x200B; Évaluation des politiques de consentement &#x200B;](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) .

### Vérifications des politiques d’utilisation des données {#data-usage-policy-checks}

À l’étape **[!UICONTROL Review]**, Experience Platform vérifie également les violations de la politique d’utilisation des données. Vous trouverez ci-dessous un exemple de violation de la politique. Vous ne pouvez pas terminer le workflow d’activation de l’audience tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la résolution des violations de politique, consultez la section sur les violations de politique d’utilisation des données [data usage policy violations](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) dans la documentation sur la gouvernance des données .

![Exemple de violation de la politique de données affiché dans le workflow d’activation.](../assets/common/data-policy-violation.png)

### Filtrer les audiences {#filter-audiences}

Au cours de cette étape également, vous pouvez utiliser les filtres disponibles sur la page pour afficher uniquement les audiences dont le planning ou le mappage a été mis à jour dans le cadre de ce workflow. Vous pouvez également activer/désactiver les colonnes du tableau à afficher.

![Enregistrement d’écran affichant les filtres d’audience disponibles à l’étape de révision.](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

Si vous êtes satisfait(e) de votre sélection et qu’aucune violation de politique n’a été détectée, sélectionnez **[!UICONTROL Finish]** pour confirmer votre sélection et commencer à envoyer des données à la destination.

## Vérifier l’activation de l’audience {#verify}

Consultez la [documentation sur la surveillance des destinations](../../dataflows/ui/monitor-destinations.md) pour obtenir des informations détaillées sur la surveillance du flux de données vers les destinations.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
