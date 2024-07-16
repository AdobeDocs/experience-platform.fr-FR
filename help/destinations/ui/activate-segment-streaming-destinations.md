---
title: Activation des données d’audience vers des destinations de diffusion en continu
type: Tutorial
description: Découvrez comment activer les audiences que vous avez dans Adobe Experience Platform en les mappant aux destinations de diffusion en continu.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 19%

---


# Activation des audiences vers des destinations de diffusion en continu

>[!IMPORTANT]
> 
> * Pour activer les audiences et activer l’ [ étape de mappage](#mapping) du workflow, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès.
> * Pour activer les audiences sans passer par l’[ étape de mappage](#mapping) du workflow, vous avez besoin des autorisations **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer le segment sans mappage]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions).
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}
> 
> Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

## Présentation {#overview}

Cet article explique le processus requis pour activer les audiences dans les destinations de diffusion en continu Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Pour activer les audiences vers les destinations, [ doit être connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

## Sélectionner votre destination {#select-destination}

1. Accédez à **[!UICONTROL Connexions et destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Onglet Catalogue de destinations présentant diverses destinations de diffusion en continu.](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Sélectionnez **[!UICONTROL Activer les audiences]** sur la carte correspondant à la destination vers laquelle vous souhaitez activer vos audiences, comme illustré dans l’image ci-dessous.

   ![Activez le contrôle mis en surbrillance dans le catalogue des destinations.](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. Sélectionnez la connexion de destination que vous souhaitez utiliser pour activer vos audiences, puis sélectionnez **[!UICONTROL Suivant]**.

   ![Une connexion de destination mise en surbrillance à l’étape Sélectionner la destination.](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Passez à la section suivante pour [sélectionner vos audiences](#select-audiences).

## Sélectionner vos audiences {#select-audiences}

Pour sélectionner les audiences que vous souhaitez activer vers la destination, utilisez les cases à cocher à gauche des noms d’audience, puis sélectionnez **[!UICONTROL Suivant]**.

Vous pouvez sélectionner plusieurs types d’audiences, selon leur origine :

* **[!UICONTROL Service de segmentation]** : audiences générées dans Experience Platform par le service de segmentation. Pour plus d’informations, consultez la [documentation sur la segmentation](../../segmentation/ui/overview.md) .
* **[!UICONTROL Téléchargement personnalisé]** : audiences générées en dehors de l’Experience Platform et téléchargées dans Platform sous la forme de fichiers CSV. Pour en savoir plus sur les audiences externes, consultez la documentation sur l&#39; [import d&#39;une audience](../../segmentation/ui/audience-portal.md#import-audience).
* Autres types d’audiences, provenant d’autres solutions d’Adobe, telles que [!DNL Audience Manager].

![Plusieurs audiences mises en surbrillance à l’étape Sélectionner les audiences.](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## Mapper les attributs et les identités {#mapping}

>[!IMPORTANT]
>
>Cette étape s’applique uniquement à certaines destinations de diffusion en continu d’audience. Si votre destination ne comporte pas d’étape **[!UICONTROL Mapping]**, passez à la [planification de l’audience](#scheduling).
>
>Lors de l’activation d’audiences vers des destinations de diffusion en continu, vous devez également mapper *au moins un espace de noms d’identité cible*, en plus des attributs de profil cible. Sinon, les audiences ne seront pas activées sur la plateforme de destination.
> ![Image de l’étape de mappage montrant un mappage d’espace de noms d’identité obligatoire.](../assets/ui/activate-segment-streaming-destinations/identity-mapping-mandatory.png) {zoomable="yes"}


Certaines destinations de diffusion en continu d’audience nécessitent que vous sélectionniez des attributs source ou des espaces de noms d’identité à mapper en tant qu’identités cibles dans la destination.

1. Sur la page **[!UICONTROL Mapping]**, sélectionnez **[!UICONTROL Ajouter un nouveau mapping]**.

   ![Ajouter un nouveau contrôle de mappage en surbrillance.](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Sélectionnez la flèche située à droite de l’entrée **[!UICONTROL Champ source]**.

   ![Sélectionnez le contrôle de champ source en surbrillance.](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. Sur la page **[!UICONTROL Sélectionner le champ source]** , utilisez les options **[!UICONTROL Sélectionner les attributs]** ou **[!UICONTROL Sélectionner l’espace de noms d’identité]** pour basculer entre les deux catégories de champs sources disponibles. À partir des attributs de profil [!DNL XDM] disponibles et des espaces de noms d’identité, sélectionnez ceux que vous souhaitez mapper à la destination, puis choisissez **[!UICONTROL Sélectionner]**.

   Utilisez le bouton d’activation/désactivation **[!UICONTROL Afficher uniquement les champs avec données]** pour n’afficher que les champs de schéma renseignés avec des valeurs. Par défaut, seuls les champs de schéma renseignés sont affichés.

   ![Sélectionnez la page du champ source qui affiche plusieurs champs sources disponibles.](../assets/ui/activate-segment-streaming-destinations/select-source-field-modal.png)

1. Sélectionnez le bouton situé à droite de l’entrée **[!UICONTROL Champ cible]**.

   ![Sélectionnez le champ cible en surbrillance.](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. Sur la page **[!UICONTROL Sélectionner le champ cible]** , sélectionnez l’espace de noms de l’identité cible vers lequel vous souhaitez mapper le champ source, puis choisissez **[!UICONTROL Sélectionner]**.

   ![Sélectionnez la page de champ cible affichant les options disponibles pour les mappages de champ cible.](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Pour ajouter d’autres mappages, répétez les étapes 1 à 5.

### Appliquer la transformation {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Appliquer la transformation"
>abstract="Cochez cette option lorsque vous utilisez des champs sources non hachés afin qu’Adobe Experience Platform les hache automatiquement au moment de l’activation."

Quand vous mappez des attributs source non hachés avec des attributs cibles qui sont censés être hachés (par exemple, `email_lc_sha256` ou `phone_sha256`), cochez l’option **Apply transformation** (Appliquer la transformation) pour qu’Adobe Experience Platform hache automatiquement les attributs source au moment de l’activation.

![Appliquez le contrôle de transformation mis en surbrillance dans l’étape de mappage des identités.](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Planifier l’export d’audience {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Date de fin"
>abstract="L’ajout d’une date de fin pour le planning des audiences n’est pas disponible."

Par défaut, la page **[!UICONTROL Planification de l’audience]** n’affiche que les audiences nouvellement sélectionnées dans le flux d’activation actuel.

Pour afficher toutes les audiences activées vers votre destination, utilisez l’option de filtrage et désactivez le filtre **[!UICONTROL Afficher les nouvelles audiences uniquement]** .

![Toutes les audiences](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. Sur la page **[!UICONTROL Planification de l’audience]**, sélectionnez chaque audience, puis utilisez les sélecteurs **[!UICONTROL Date de début]** et **[!UICONTROL Date de fin]** pour configurer l’intervalle d’heure d’envoi des données à votre destination.

   ![Filtre de planification d’audience en surbrillance.](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * Pour certaines destinations, vous devez sélectionner l’ **[!UICONTROL origine de l’audience]** pour chaque audience à l’aide du menu déroulant sous les sélecteurs de calendrier. Si votre destination n’inclut pas ce sélecteur, ignorez cette étape.

     ![Liste déroulante ID de mappage mise en surbrillance.](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Certaines destinations nécessitent que vous mappiez manuellement [!DNL Platform] audiences à leur contrepartie dans la destination cible. Pour ce faire, sélectionnez chaque audience, puis saisissez l’ID d’audience correspondant à partir de la plateforme de destination dans le champ **[!UICONTROL ID de mappage]** . Si votre destination n’inclut pas ce champ, ignorez cette étape.

     ![Liste déroulante Origine de l’audience mise en surbrillance.](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Certaines destinations nécessitent que vous saisissiez un **[!UICONTROL ID d’application]** lors de l’activation d’audiences [!DNL IDFA] ou [!DNL GAID]. Si votre destination n’inclut pas ce champ, ignorez cette étape.

     ![Liste déroulante ID d’application mise en surbrillance.](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Sélectionnez **[!UICONTROL Suivant]** pour accéder à la page [!UICONTROL Réviser].

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

![Résumé de la sélection dans l’étape de révision.](../assets/ui/activate-segment-streaming-destinations/review.png)

### Évaluation des politiques de consentement {#consent-policy-evaluation}

Si votre organisation a acheté **Adobe HealthCare Shield** ou **Adobe Privacy &amp; Security Shield**, sélectionnez **[!UICONTROL Afficher les politiques de consentement applicables]** pour identifier les politiques de consentement appliquées et le nombre de profils inclus dans l&#39;activation qui en résulte. Pour plus d’informations, consultez la section [Évaluation de la stratégie de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) .

### Vérifications des stratégies d’utilisation des données {#data-usage-policy-checks}

À l’étape **[!UICONTROL Réviser]**, Experience Platform recherche également toutes les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation de la politique. Vous ne pouvez pas terminer le workflow d’activation de l’audience tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la façon de résoudre les violations de stratégie, reportez-vous à la section [Violations de stratégie d’utilisation des données](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) de la documentation sur la gouvernance des données.

![Exemple de violation de politique de données affichée dans le workflow d’activation.](../assets/common/data-policy-violation.png)

### Filtrage des audiences {#filter-audiences}

En outre, au cours de cette étape, vous pouvez utiliser les filtres disponibles sur la page pour afficher uniquement les audiences dont le planning ou le mapping a été mis à jour dans le cadre de ce workflow. Vous pouvez également basculer entre les colonnes du tableau que vous souhaitez afficher.

![Enregistrement de l’écran montrant les filtres d’audience disponibles dans l’étape de révision.](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

Si votre sélection vous satisfait et qu’aucune violation de stratégie n’a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

## Vérification de l’activation de l’audience {#verify}

Consultez la [documentation de surveillance des destinations](../../dataflows/ui/monitor-destinations.md) pour obtenir des informations détaillées sur la manière de surveiller le flux de données vers vos destinations.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
