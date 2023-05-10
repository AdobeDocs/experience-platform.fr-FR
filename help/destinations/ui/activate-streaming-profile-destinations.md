---
keywords: Activer des destinations de profils;activer des destinations;activer des données;activer des destinations de marketing par e-mail;activer des destinations d’espace de stockage dans le cloud
title: Activer les données d’audience vers des destinations d’exportation de profils de diffusion en continu
type: Tutorial
description: Découvrez comment activer les données d’audience que vous avez dans Adobe Experience Platform en envoyant des segments vers des destinations basées sur un profil en continu.
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 5bb2981b8187fcd3de46f80ca6c892421b3590f6
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 51%

---

# Activer les données d’audience vers des destinations d’exportation de profils de diffusion en continu

>[!IMPORTANT]
> 
> * Pour activer les données et activer la variable [étape de mappage](#mapping) du workflow, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions).
> * Pour activer les données sans passer par la fonction [étape de mappage](#mapping) du workflow, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation du segment sans mappage]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions).
> 
> Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

## Présentation {#overview}

Cet article explique le processus requis pour activer les données d’audience dans des destinations basées sur des profils de diffusion en continu Adobe Experience Platform, telles qu’Amazon Kinesis.

## Conditions préalables {#prerequisites}

Pour activer des données vers des destinations, vous devez avoir réussi à vous [connecter à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

## Sélectionner votre destination {#select-destination}

1. Accédez à **[!UICONTROL Connexions et destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Image montrant l’onglet Catalogue de destinations.](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Sélectionnez **[!UICONTROL Activer des segments]** sur la vignette correspondant à la destination vers laquelle vous souhaitez activer des segments, tel qu’indiqué sur l’image ci-dessous.

   ![Image mettant en surbrillance le contrôle Activer les segments dans l’onglet Catalogue de destinations .](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. Sélectionnez la connexion de destination à utiliser pour activer des segments, puis sélectionnez **[!UICONTROL Suivant]**.

   ![Image montrant une sélection de deux destinations auxquelles vous pouvez vous connecter.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Accédez à la section suivante pour [sélectionner des segments](#select-segments).

## Sélectionnez vos segments {#select-segments}

Utilisez les cases à cocher situées à gauche des noms de segment pour sélectionner les segments que vous souhaitez activer vers la destination, puis sélectionnez **[!UICONTROL Suivant]**.

![Image mettant en surbrillance la sélection des cases à cocher à l’étape Sélection de segments du workflow d’activation.](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## Sélectionner des attributs de profil {#select-attributes}

Dans le **[!UICONTROL Mappage]** sélectionnez les attributs de profil à envoyer à la destination cible.

>[!NOTE]
>
> Adobe Experience Platform préremplit votre sélection avec quatre attributs recommandés couramment utilisés de votre schéma : `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Les exportations de fichiers varient comme suit, selon que `segmentMembership.status` est sélectionné :
* Si le champ `segmentMembership.status` est sélectionné, les fichiers exportés incluent les membres **[!UICONTROL actifs]** dans l’instantané complet initial ainsi que les membres **[!UICONTROL actifs]** et **[!UICONTROL expirés]** dans les exportations incrémentielles suivantes.
* Si le champ `segmentMembership.status` n’est pas sélectionné, les fichiers exportés incluent uniquement les membres **[!UICONTROL actifs]** dans l’instantané complet initial et dans les exportations incrémentielles suivantes.

![Image montrant les attributs préremplis et recommandés dans l’étape de mappage.](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. Sur la page **[!UICONTROL Sélectionner des attributs]**, sélectionnez **[!UICONTROL Ajouter un nouveau champ]**.

   ![Image mettant en surbrillance le contrôle Ajouter un nouveau champ dans l’étape de mappage.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Sélectionnez la flèche située à droite de l’entrée **[!UICONTROL Champ de schéma]**.

   ![Image mettant en surbrillance la manière de sélectionner un champ source dans l’étape de mappage.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. Sur la page **[!UICONTROL Sélectionner un champ]**, sélectionnez les attributs XDM à envoyer à la destination puis choisissez **[!UICONTROL Sélectionner]**.

   ![Image montrant une sélection de champs XDM que vous pouvez sélectionner comme champs source.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. Pour ajouter d’autres mappages, répétez les étapes 1 à 3, puis sélectionnez **[!UICONTROL Suivant]**.

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

![Résumé de la sélection dans l’étape de révision.](/help/destinations/assets/ui/activate-streaming-profile-destinations/review.png)

### Évaluation des politiques de consentement {#consent-policy-evaluation}

Si votre organisation a acheté **Adobe HealthCare Shield** ou **Adobe Privacy &amp; Security Shield**, sélectionnez **[!UICONTROL Afficher les politiques de consentement applicables]** pour identifier les politiques de consentement appliquées et le nombre de profils inclus dans l&#39;activation qui en résulte. En savoir plus [évaluation des stratégies de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) pour plus d’informations.

### Vérifications des stratégies d’utilisation des données {#data-usage-policy-checks}

Dans le **[!UICONTROL Réviser]** , Experience Platform recherche également les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation de la politique. Vous ne pouvez pas terminer le processus d’activation des segments tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la résolution des violations de stratégie, reportez-vous à la section [violations de la stratégie d’utilisation des données](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) dans la section documentation sur la gouvernance des données .

![violation de la politique de données](../assets/common/data-policy-violation.png)

### Filtrer des segments {#filter-segments}

En outre, au cours de cette étape, vous pouvez utiliser les filtres disponibles sur la page pour afficher uniquement les segments dont la planification ou le mappage a été mis à jour dans le cadre de ce workflow.

![Enregistrement de l’écran montrant les filtres de segments disponibles dans l’étape de révision.](/help/destinations/assets/ui/activate-streaming-profile-destinations/filter-segments-review-step.gif)

Si vous êtes satisfait de votre sélection et qu’aucune violation de stratégie n’a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer des données à la destination.

## Vérifier l’activation des segments {#verify}

Votre exportation [!DNL Experience Platform] Les données arrivent dans votre destination cible au format JSON. Par exemple, l’événement ci-dessous contient l’attribut de profil d’adresse électronique d’une audience qui s’est qualifiée pour un certain segment et qui a quitté un autre segment. Les identités de ce prospect sont ECID et email.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
