---
keywords: diffusion en continu;
title: Connexion HTTP
description: La destination d’API HTTP dans Adobe Experience Platform vous permet d’envoyer des données de profil à des points de terminaison HTTP tiers.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 3bec18f1b7209b1f329dc90aadb597edb6143291
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 9%

---

# (Version bêta) [!DNL HTTP] Connexion API

>[!IMPORTANT]
>
>Le [!DNL HTTP] destination dans Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

Le [!DNL HTTP] La destination de l’API est une [!DNL Adobe Experience Platform] destination de diffusion en continu qui vous aide à envoyer des données de profil à des tiers [!DNL HTTP] points de fin.

Pour envoyer des données de profil à [!DNL HTTP] points de fin, vous devez d’abord vous connecter à la destination dans [[!DNL Adobe Experience Platform]](#connect-destination).

## Cas d’utilisation {#use-cases}

Le [!DNL HTTP] destination est ciblée sur les clients qui doivent exporter les données de profil XDM et les segments d’audience vers des segments génériques [!DNL HTTP] points de fin.

[!DNL HTTP] Les points de terminaison peuvent être les systèmes des clients ou des solutions tierces.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL httpEndpoint]**: la valeur [!DNL URL] du point de terminaison HTTP auquel vous souhaitez envoyer les données de profil.
   * Vous pouvez éventuellement ajouter des paramètres de requête au [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: la valeur [!DNL URL] du point de terminaison HTTP utilisé pour [!DNL OAuth2] authentification.
* **[!UICONTROL ID client]**: la valeur [!DNL clientID] du paramètre utilisé dans la variable [!DNL OAuth2] informations d’identification du client.
* **[!UICONTROL Secret du client]**: la valeur [!DNL clientSecret] du paramètre utilisé dans la variable [!DNL OAuth2] informations d’identification du client.

   >[!NOTE]
   >
   >Uniquement [!DNL OAuth2] les informations d’identification du client sont actuellement prises en charge.

* **[!UICONTROL Nom]**: saisissez un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: saisissez une description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL En-têtes personnalisés]**: saisissez les en-têtes personnalisés que vous souhaitez inclure dans les appels de destination, selon le format suivant : `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >L’implémentation actuelle nécessite au moins un en-tête personnalisé. Cette limitation sera résolue dans une prochaine mise à jour.

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers des destinations d’exportation de profils en continu](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Attributs de destination {#attributes}

Dans le [[!UICONTROL Sélectionner des attributs]](../../ui/activate-streaming-profile-destinations.md#select-attributes) , Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination.

## Données exportées {#exported-data}

Votre exportation [!DNL Experience Platform] Les données arrivent dans votre [!DNL HTTP] destination au format JSON. Par exemple, l’événement ci-dessous contient l’attribut de profil d’adresse électronique d’une audience qui s’est qualifiée pour un certain segment et qui a quitté un autre segment. Les identités de ce prospect sont [!DNL ECID] et par e-mail.

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
