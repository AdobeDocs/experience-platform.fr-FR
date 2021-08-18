---
keywords: activer les destinations de profil ; activer les destinations ; activer les données ; activer les destinations de marketing par e-mail ; Activation des destinations de stockage dans le cloud
title: Activation des données d’audience vers des destinations d’exportation de profils en continu
type: Tutorial
seo-title: Activation des données d’audience vers des destinations d’exportation de profils en continu
description: Découvrez comment activer les données d’audience que vous avez dans Adobe Experience Platform en envoyant des segments vers des destinations basées sur un profil en continu.
seo-description: Découvrez comment activer les données d’audience que vous avez dans Adobe Experience Platform en envoyant des segments vers des destinations basées sur un profil en continu.
source-git-commit: f0c854e1b6b89d499c720328fa5054611147772f
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 7%

---


# Activation des données d’audience vers des destinations d’exportation de profils en continu

## Présentation {#overview}

Cet article explique le processus requis pour activer les données d’audience dans des destinations basées sur des profils de diffusion en continu Adobe Experience Platform, telles qu’Amazon Kinesis.

## Conditions préalables {#prerequisites}

Pour activer les données vers les destinations, vous devez être [connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue des destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

## Sélectionner votre destination {#select-destination}

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Parcourir]**.

   ![Onglet Parcourir la destination](../assets/ui/activate-streaming-profile-destinations/browse-tab.png)

1. Sélectionnez le bouton **[!UICONTROL Ajouter des segments]** correspondant à la destination vers laquelle vous souhaitez activer vos segments, comme illustré dans l’image ci-dessous.

   ![Boutons Activer](../assets/ui/activate-streaming-profile-destinations/activate-buttons-browse.png)

1. Passez à la section suivante pour [sélectionner vos segments](#select-segments).

## Sélection de vos segments {#select-segments}

Utilisez les cases à cocher situées à gauche des noms de segment pour sélectionner les segments que vous souhaitez activer vers la destination, puis sélectionnez **[!UICONTROL Suivant]**.

![Sélection de segments](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## Sélection des attributs de profil {#select-attributes}

Sélectionnez les attributs de profil à envoyer à la destination cible.

>[!NOTE]
>
> Adobe Experience Platform préremplit votre sélection avec quatre attributs recommandés couramment utilisés de votre schéma : `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Les exportations de fichiers varient comme suit, selon que `segmentMembership.status` est sélectionné ou non :
* Si le champ `segmentMembership.status` est sélectionné, les fichiers exportés incluent des membres **[!UICONTROL Principal]** dans l’instantané complet initial et **[!UICONTROL Principal]** et des membres **[!UICONTROL expirés]** dans les exportations incrémentielles suivantes.
* Si le champ `segmentMembership.status` n’est pas sélectionné, les fichiers exportés incluent uniquement les membres **[!UICONTROL Principal]** dans l’instantané complet initial et dans les exportations incrémentielles suivantes.

![attributs recommandés](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. Dans la page **[!UICONTROL Sélectionner les attributs]**, sélectionnez **[!UICONTROL Ajouter un nouveau champ]**.

   ![Ajouter un nouveau mappage](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Sélectionnez la flèche située à droite de l&#39;entrée **[!UICONTROL Champ de schéma]** .

   ![Sélectionner le champ source](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. Dans la page **[!UICONTROL Sélectionner un champ]** , sélectionnez les attributs XDM à envoyer à la destination, puis choisissez **[!UICONTROL Sélectionner]**.

   ![Sélectionner la page du champ source](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. Pour ajouter d’autres mappages, répétez les étapes 1 à 3, puis sélectionnez **[!UICONTROL Suivant]**.

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

>[!IMPORTANT]
>
>Au cours de cette étape, Adobe Experience Platform recherche les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation d’une stratégie. Vous ne pouvez pas terminer le workflow d’activation du segment tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la manière de résoudre les violations de stratégie, voir [Application de la stratégie](../../rtcdp/privacy/data-governance-overview.md#enforcement) dans la section de documentation sur la gouvernance des données.

![violation de la politique de données](../assets/common/data-policy-violation.png)

Si aucune violation de stratégie n’a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

![Révision](../assets/ui/activate-streaming-profile-destinations/review.png)

## Vérification de l’activation des segments {#verify}

Vos données [!DNL Experience Platform] exportées arrivent dans votre destination cible au format JSON. Par exemple, l’événement ci-dessous contient l’attribut de profil d’adresse électronique d’une audience qui s’est qualifiée pour un certain segment et qui a quitté un autre segment. Les identités de ce prospect sont ECID et email.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
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
