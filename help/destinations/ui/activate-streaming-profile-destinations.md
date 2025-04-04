---
title: Activer les audiences vers des destinations d’export de profils en flux continu
type: Tutorial
description: Découvrez comment activer les données d’audience disponibles dans Adobe Experience Platform en envoyant des audiences vers des destinations basées sur des profils de diffusion en continu.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 23%

---


# Activer les audiences vers des destinations d’export de profils en flux continu

>[!IMPORTANT]
> 
> * Pour activer les données et activer l’[étape de mappage](#mapping) du workflow, vous devez disposer des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [](/help/access-control/home.md#permissions).
> * Pour activer les données sans passer par l’étape [mappage](#mapping) du workflow, vous devez disposer des **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation du segment sans mappage]**, **[!UICONTROL Affichage des profils]** et **[!UICONTROL Affichage des segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions).
> 
> Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

## Présentation {#overview}

Cet article explique le processus requis pour activer des données d’audience dans Adobe Experience Platform vers des destinations basées sur des profils de diffusion en continu (également appelées [destinations d’entreprise](/help/destinations/destination-types.md#advanced-enterprise-destinations)).

Cet article s’applique aux trois destinations suivantes :

* [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)
* [Destination de l’API HTTP](/help/destinations/catalog/streaming/http-destination.md).

## Conditions préalables {#prerequisites}

Pour activer des données vers des destinations, vous devez avoir réussi à vous [connecter à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

## Sélectionner votre destination {#select-destination}

1. Accédez à **[!UICONTROL Connexions et destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Image illustrant l’onglet Catalogue de destinations.](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Sélectionnez **[!UICONTROL Activer les audiences]** sur la vignette correspondant à la destination vers laquelle vous souhaitez activer vos audiences, comme illustré dans l’image ci-dessous.

   ![Image mettant en surbrillance la commande Activer les audiences dans l’onglet Catalogue de destinations.](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. Sélectionnez la connexion de destination à utiliser pour activer les audiences, puis sélectionnez **[!UICONTROL Suivant]**.

   ![Image montrant une sélection de deux destinations auxquelles vous pouvez vous connecter.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Accédez à la section suivante pour [sélectionner vos audiences](#select-audiences).

## Sélectionner vos audiences {#select-audiences}

Pour sélectionner les audiences à activer vers la destination, utilisez les cases à cocher situées à gauche des noms d’audience, puis sélectionnez **[!UICONTROL Suivant]**.

Vous pouvez effectuer un choix parmi plusieurs types d’audiences, selon leur origine :

* **[!UICONTROL Segmentation Service]** : audiences générées dans Experience Platform par le service de segmentation. Pour plus d’informations, consultez la [documentation d’Audience Portal](../../segmentation/ui/audience-portal.md).
* **[!UICONTROL Chargement personnalisé]** : audiences générées en dehors d’Experience Platform et chargées dans Experience Platform au format CSV. Pour en savoir plus sur les audiences externes, consultez la documentation sur [importation d’une audience](../../segmentation/ui/audience-portal.md#import-audience).
* Autres types d’audiences, provenant d’autres solutions Adobe, telles que [!DNL Audience Manager].

![Image mettant en surbrillance la sélection des cases à cocher à l’étape Sélectionner des audiences du workflow d’activation.](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## Sélectionner des attributs de profil {#select-attributes}

À l’étape **[!UICONTROL Mappage]**, sélectionnez les attributs de profil à envoyer à la destination cible.

1. Sur la page **[!UICONTROL Sélectionner des attributs]**, sélectionnez **[!UICONTROL Ajouter un nouveau champ]**.

   ![Image mettant en surbrillance le contrôle Ajouter un nouveau champ à l’étape de mappage.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Sélectionnez la flèche située à droite de l’entrée **[!UICONTROL Champ de schéma]**.

   ![Image mettant en surbrillance le processus de sélection d’un champ source dans l’étape de mappage.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. Sur la page **[!UICONTROL Sélectionner un champ]**, sélectionnez les attributs XDM à envoyer à la destination puis choisissez **[!UICONTROL Sélectionner]**.

   ![Image montrant une sélection de champs XDM que vous pouvez sélectionner comme champs source.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. Pour ajouter d’autres champs, répétez les étapes 1 à 3, puis sélectionnez **[!UICONTROL Suivant]**.

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

![Résumé de la sélection à l’étape de révision.](../assets/ui/activate-streaming-profile-destinations/review.png)

### Évaluation des politiques de consentement {#consent-policy-evaluation}

L’[évaluation de la politique de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) n’est actuellement pas prise en charge dans les exportations vers les trois destinations d’entreprise : Amazon Kinesis, Azure Event Hubs et l’API HTTP.

Cela signifie que les profils qui n’ont pas consenti à être ciblés *sont inclus* dans les exportations vers ces trois destinations.

<!--

If your organization purchased **Adobe Healthcare Shield** or **Adobe Privacy & Security Shield**, select **[!UICONTROL View applicable consent policies]** to see which consent policies are applied and how many profiles are included in the activation as a result of them. Read about [consent policy evaluation](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) for more information.

-->

### Vérifications des politiques d’utilisation des données {#data-usage-policy-checks}

À l’étape **[!UICONTROL Révision]**, Experience Platform vérifie également les violations de la politique d’utilisation des données. Vous trouverez ci-dessous un exemple de violation de la politique. Vous ne pouvez pas terminer le workflow d’activation de l’audience tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la résolution des violations de politique, consultez la section sur les violations de politique d’utilisation des données [data usage policy violations](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) dans la documentation sur la gouvernance des données .

![violation de la politique de données](../assets/common/data-policy-violation.png)

### Filtrer les audiences {#filter-audiences}

Au cours de cette étape également, vous pouvez utiliser les filtres disponibles sur la page pour afficher uniquement les audiences dont le planning ou le mappage a été mis à jour dans le cadre de ce workflow.

![Enregistrement d’écran affichant les filtres d’audience disponibles à l’étape de révision.](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

Si vous êtes satisfait(e) de votre sélection et qu’aucune violation de politique n’a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer des données à la destination.

## Vérifier l’activation de l’audience {#verify}

Les données [!DNL Experience Platform] exportées arrivent dans votre destination cible au format JSON. Par exemple, l’événement ci-dessous contient l’attribut d’adresse e-mail d’un profil qui s’est qualifié pour une certaine audience et qui a quitté une autre audience. Les identités de ce prospect sont `ECID` et `email_lc_sha256`.

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
