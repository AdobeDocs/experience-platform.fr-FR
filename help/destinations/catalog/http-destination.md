---
keywords: diffusion ;
title: Connexion HTTP
description: La destination HTTP dans Adobe Experience Platform vous permet d’envoyer des données de profil à des points de terminaison HTTP tiers.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 9%

---

# (Alpha) [!DNL HTTP] connexion

>[!IMPORTANT]
>
>Le [!DNL HTTP] dans la plate-forme est actuellement en alpha. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

Le [!DNL HTTP] destination est [!DNL Adobe Experience Platform] destination de diffusion qui vous aide à envoyer des données de profil à des tiers [!DNL HTTP] points de terminaison.

Pour envoyer des données de profil à [!DNL HTTP] points de terminaison, vous devez d’abord vous connecter à la destination dans [[!DNL Adobe Experience Platform]](#connect-destination).

## Cas d’utilisation {#use-cases}

Le [!DNL HTTP] destination est destinée aux clients qui doivent exporter des données de profil XDM et des segments d’audience vers des [!DNL HTTP] points de terminaison.

[!DNL HTTP] les points de terminaison peuvent être soit les propres systèmes des clients, soit des solutions tierces.

## Se connecter à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans la section [didacticiel sur la configuration de destination](../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

En [configuration](../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL httpEndpoint]**: le [!DNL URL] du point de terminaison HTTP auquel vous souhaitez envoyer les données de profil.
   * Si vous le souhaitez, vous pouvez ajouter des paramètres de requête au fichier [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: le [!DNL URL] du point de terminaison HTTP utilisé pour [!DNL OAuth2] authentification.
* **[!UICONTROL ID client]**: le [!DNL clientID] utilisé dans le paramètre [!DNL OAuth2] informations d&#39;identification du client.
* **[!UICONTROL Secret client]**: le [!DNL clientSecret] utilisé dans le paramètre [!DNL OAuth2] informations d&#39;identification du client.

   >[!NOTE]
   >
   >Seulement [!DNL OAuth2] les informations d&#39;identification des clients sont actuellement prises en charge.

* **[!UICONTROL Nom]**: entrez un nom par lequel vous reconnaîtrez cette destination dans le futur.
* **[!UICONTROL Description]**: entrez une description qui vous aidera à identifier cette destination à l&#39;avenir.
* **[!UICONTROL En-têtes personnalisés]**: entrez les en-têtes personnalisés que vous souhaitez inclure dans les appels de destination, selon le format suivant : `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >La mise en oeuvre actuelle nécessite au moins un en-tête personnalisé. Cette limitation sera résolue dans une prochaine mise à jour.

## Activer les segments vers cette destination {#activate}

Voir [Activer les données d’audience vers les destinations d’exportation de profil de diffusion en continu](../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Attributs de destination {#attributes}

Dans la boîte de dialogue [[!UICONTROL Sélection d’attributs]](../ui/activate-streaming-profile-destinations.md#select-attributes) , l’Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d&#39;union](../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination.

## Données exportées {#exported-data}

Votre exportation [!DNL Experience Platform] les données atterrissent dans votre [!DNL HTTP] au format JSON. Par exemple, l’événement ci-dessous contient l’attribut de profil d’adresse électronique d’un public qui s’est qualifié pour un certain segment et a quitté un autre segment. Les identités de cette perspective sont : [!DNL ECID] et par e-mail.

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
