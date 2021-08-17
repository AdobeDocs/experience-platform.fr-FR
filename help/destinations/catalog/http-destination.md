---
keywords: diffusion en continu;
title: Connexion HTTP
description: La destination HTTP dans Adobe Experience Platform vous permet d’envoyer des données de profil à des points de terminaison HTTP tiers.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 9%

---

# (Alpha) [!DNL HTTP] connexion

>[!IMPORTANT]
>
>La destination [!DNL HTTP] de Platform est actuellement en alpha. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

La destination [!DNL HTTP] est une destination de diffusion en continu [!DNL Adobe Experience Platform] qui vous permet d’envoyer des données de profil à des points de terminaison [!DNL HTTP] tiers.

Pour envoyer des données de profil aux points de terminaison [!DNL HTTP], vous devez d’abord vous connecter à la destination dans [[!DNL Adobe Experience Platform]](#connect-destination).

## Cas d&#39;utilisation {#use-cases}

La destination [!DNL HTTP] est destinée aux clients qui doivent exporter les données de profil XDM et les segments d’audience vers des points de terminaison [!DNL HTTP] génériques.

[!DNL HTTP] Les points de terminaison peuvent être les systèmes des clients ou des solutions tierces.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL httpEndpoint]**: l’identifiant  [!DNL URL] du point de terminaison HTTP auquel vous souhaitez envoyer les données de profil.
   * Vous pouvez éventuellement ajouter des paramètres de requête à [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]** : l’identifiant  [!DNL URL] du point de terminaison HTTP utilisé pour l’ [!DNL OAuth2] authentification.
* **[!UICONTROL ID]** client : le  [!DNL clientID] paramètre utilisé dans les informations d’identification du  [!DNL OAuth2] client.
* **[!UICONTROL Client Secret]** : le  [!DNL clientSecret] paramètre utilisé dans les informations d’identification du  [!DNL OAuth2] client.

   >[!NOTE]
   >
   >Seules les informations d’identification du client [!DNL OAuth2] sont actuellement prises en charge.

* **[!UICONTROL Nom]** : saisissez un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : saisissez une description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL En-têtes personnalisés]** : saisissez les en-têtes personnalisés que vous souhaitez inclure dans les appels de destination, selon le format suivant :  `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >L’implémentation actuelle nécessite au moins un en-tête personnalisé. Cette limitation sera résolue dans une prochaine mise à jour.

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers les destinations d’exportation de profils en continu](../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Attributs de destination {#attributes}

À l’étape [[!UICONTROL Sélectionner les attributs]](../ui/activate-streaming-profile-destinations.md#select-attributes) , Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination.

## Données exportées {#exported-data}

Vos données [!DNL Experience Platform] exportées se trouvent dans votre destination [!DNL HTTP] au format JSON. Par exemple, l’événement ci-dessous contient l’attribut de profil d’adresse électronique d’une audience qui s’est qualifiée pour un certain segment et qui a quitté un autre segment. Les identités de ce prospect sont [!DNL ECID] et e-mail.

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
