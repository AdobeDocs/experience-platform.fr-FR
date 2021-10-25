---
keywords: activer les destinations de profil ; activer les destinations ; activer les données ; activer les destinations de marketing par courrier électronique ; activation de destinations de stockage cloud
title: Activer les données d’audience vers les destinations d’exportation de profil de diffusion en continu
type: Tutorial
seo-title: Activate audience data to streaming profile export destinations
description: Découvrez comment activer les données d’audience que vous avez dans Adobe Experience Platform en envoyant des segments à des destinations basées sur des profils en flux continu.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by sending segments to streaming profile-based destinations.
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 7%

---

# Activer les données d’audience vers les destinations d’exportation de profil de diffusion en continu

## Présentation {#overview}

Cet article explique le flux de travaux requis pour activer les données d’audience dans les destinations basées sur le profil de diffusion en continu Adobe Experience Platform, telles que Kinesis.

## Conditions préalables {#prerequisites}

Pour activer des données vers des destinations, vous devez avoir réussi [connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez à la section [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

## Sélectionnez votre destination {#select-destination}

1. Aller à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez l’option **[!UICONTROL Catalogue]** .

   ![Onglet Catalogue de destination](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Sélectionner **[!UICONTROL Activation de segments]** sur la carte correspondant à la destination où vous souhaitez activer vos segments, comme illustré dans l’image ci-dessous.

   ![Bouton Activer les segments](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. Sélectionnez la connexion de destination que vous souhaitez utiliser pour activer vos segments, puis sélectionnez **[!UICONTROL Suivant]**.

   ![Sélectionner la destination](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Passer à la section suivante [sélection de vos segments](#select-segments).

## Sélection de vos segments {#select-segments}

Utilisez les cases à cocher à gauche des noms de segment pour sélectionner les segments que vous souhaitez activer vers la destination, puis sélectionnez **[!UICONTROL Suivant]**.

![Sélection de segments](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## Sélectionner des attributs de profil {#select-attributes}

Sélectionnez les attributs de profil que vous souhaitez envoyer à la destination cible.

>[!NOTE]
>
> Adobe Experience Platform préremplit votre sélection avec quatre attributs recommandés, couramment utilisés, de votre schéma : `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Les exportations de fichiers varient de la façon suivante, selon que `segmentMembership.status` est sélectionné :
* Si la `segmentMembership.status` est sélectionné, les fichiers exportés incluent **[!UICONTROL Actif]** membres dans l&#39;instantané complet initial et **[!UICONTROL Actif]** et **[!UICONTROL Expiré]** membres dans les exportations incrémentielles suivantes.
* Si la `segmentMembership.status` champ non sélectionné, les fichiers exportés incluent uniquement **[!UICONTROL Actif]** membres dans l&#39;instantané complet initial et dans les exportations incrémentielles ultérieures.

![attributs recommandés](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. Dans la boîte de dialogue **[!UICONTROL Sélection d’attributs]** , sélectionnez **[!UICONTROL Ajouter un nouveau champ]**.

   ![Ajouter un nouveau mappage](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Sélectionnez la flèche à droite du **[!UICONTROL Champ Schéma]** entrée.

   ![Sélectionner le champ source](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. Dans la boîte de dialogue **[!UICONTROL Sélectionner un champ]** , sélectionnez les attributs XDM que vous souhaitez envoyer à la destination, puis choisissez **[!UICONTROL Sélectionner]**.

   ![Page Sélectionner le champ source](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. Pour ajouter d’autres mappages, répétez les étapes 1 à 3, puis sélectionnez **[!UICONTROL Suivant]**.

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

>[!IMPORTANT]
>
>À cette étape, Adobe Experience Platform vérifie les violations de la stratégie d&#39;utilisation des données. Voici un exemple de violation d&#39;une stratégie. Vous ne pouvez pas terminer le processus d’activation du segment tant que vous n’avez pas résolu la violation. Pour plus d&#39;informations sur la résolution des violations de stratégie, consultez [Application des règles](../../rtcdp/privacy/data-governance-overview.md#enforcement) dans la section documentation sur la gouvernance des données.

![violation de la stratégie de données](../assets/common/data-policy-violation.png)

Si aucune violation de stratégie n&#39;a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer des données à la destination.

![Révision](../assets/ui/activate-streaming-profile-destinations/review.png)

## Vérification de l’activation des segments {#verify}

Votre exportation [!DNL Experience Platform] atterrit dans votre destination cible au format JSON. Par exemple, l’événement ci-dessous contient l’attribut de profil d’adresse électronique d’un public qui s’est qualifié pour un certain segment et a quitté un autre segment. Les identités de ce prospect sont ECID et e-mail.

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
