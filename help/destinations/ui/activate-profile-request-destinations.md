---
keywords: activation des destinations de requête de profil;activation des données;destinations de requête de profil
title: Activer les données d’audience vers les destinations de requête de profil
type: Tutorial
description: Découvrez comment activer les données d’audience que vous avez dans Adobe Experience Platform en mappant les segments aux destinations de requête de profil.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 26e7a3e78a4513aa69cdfbed7902509609e114cc
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 32%

---

# Activer les données d’audience vers les destinations de requête de profil

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

## Présentation {#overview}

Cet article explique le workflow requis pour activer les données d’audience dans les destinations de demande de profil Adobe Experience Platform. Utilisé conjointement avec [segmentation de périphérie](../../segmentation/ui/edge-segmentation.md), ces destinations activent des cas d’utilisation de la personnalisation de la même page et de la page suivante sur vos propriétés web. En savoir plus sur [activation des cas d’utilisation de la personnalisation de la même page et de la page suivante](/help/destinations/ui/configure-personalization-destinations.md).

Voici des exemples de destinations de requête de profil : [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) et le [Personnalisation personnalisée](../../destinations/catalog/personalization/custom-personalization.md) connexions.

## Conditions préalables {#prerequisites}

Pour activer des données vers des destinations, vous devez avoir réussi à vous [connecter à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [destinations](../catalog/overview.md), parcourez les destinations de personnalisation prises en charge et configurez la destination que vous souhaitez utiliser.

### Stratégie de fusion de segments {#merge-policy}

Actuellement, les destinations de requête de profil ne prennent en charge que l’activation des segments qui utilisent la variable [Stratégie de fusion principale sur périphérie](../../segmentation/ui/segment-builder.md#merge-policies) défini comme valeur par défaut.

## Sélectionnez votre destination {#select-destination}

1. Accédez à **[!UICONTROL Connexions et destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Onglet Catalogue de destinations](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Sélectionner **[!UICONTROL Activation des segments]** sur la carte correspondant à la destination de personnalisation à laquelle vous souhaitez activer vos segments, comme illustré dans l’image ci-dessous.

   ![Boutons Activer](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Sélectionnez la connexion de destination à utiliser pour activer des segments, puis sélectionner **[!UICONTROL Suivant]**.

   ![Sélectionnez des destinations](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Accédez à la section suivante pour [sélectionner des segments](#select-segments).

## Sélectionnez vos segments {#select-segments}

Utilisez les cases à cocher situées à gauche des noms de segment pour sélectionner les segments que vous souhaitez activer vers la destination, puis sélectionnez **[!UICONTROL Suivant]**.

![Sélectionnez des segments](../assets/ui/activate-profile-request-destinations/select-segments.png)

## (Version bêta) Mise en correspondance des attributs {#map-attributes}

>[!IMPORTANT]
>
>L’étape de mappage qui active la personnalisation basée sur les attributs pour [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) et [destinations de personnalisation générique](/help/destinations/catalog/personalization/custom-personalization.md), est actuellement en version bêta et votre entreprise n’y a peut-être pas encore accès. Cette documentation peut être modifiée.

Sélectionnez les attributs sur lesquels vous souhaitez activer des cas d’utilisation de personnalisation pour vos utilisateurs. Cela signifie que si la valeur d’un attribut change ou qu’un attribut est ajouté à un profil, ce profil devient membre du segment et est activé sur la destination de personnalisation.

L’ajout d’attributs est facultatif. Vous pouvez toujours passer à l’étape suivante et activer la personnalisation de la même page et de la page suivante sans sélectionner d’attributs. Si vous n’ajoutez pas d’attributs à cette étape, la personnalisation continuera à se produire en fonction des qualifications d’appartenance aux segments et de mappage d’identité pour les profils.

![Image montrant l’étape de mappage avec un attribut sélectionné](../assets/ui/activate-profile-request-destinations/mapping-step.png)

Pour ajouter des attributs, sélectionnez la variable **[!UICONTROL Ajouter un nouveau champ]** contrôlez et recherchez ou accédez au champ d’attribut XDM souhaité, comme illustré ci-dessous.

![Enregistrement d’écran montrant comment sélectionner un attribut XDM à l’étape de mappage](../assets/ui/activate-profile-request-destinations/mapping-step-select-attribute.gif)

## Planifier l’exportation de segments {#scheduling}

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
>Au cours de cette étape, Adobe Experience Platform recherche les violations de la stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation de la stratégie. Vous ne pouvez pas terminer le processus d’activation des segments tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la résolution des violations de stratégie, voir [Application des stratégies](../../rtcdp/privacy/data-governance-overview.md#enforcement) dans la section documentation sur la gouvernance des données.

![violation de la stratégie de données](../assets/common/data-policy-violation.png)

Si aucune violation de stratégie n’a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer la sélection et commencer à envoyer des données à la destination.

![Révision](../assets/ui/activate-profile-request-destinations/review.png)

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->