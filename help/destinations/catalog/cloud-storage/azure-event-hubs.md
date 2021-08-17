---
keywords: Destination du hub d’événements Azure ; hub d’événements Azure ; thub d’événements azure
title: (Version bêta) Connexion à !DNL Azure Event Hubs
description: Créez une connexion sortante en temps réel à votre stockage !DNL Azure Event Hubs] pour diffuser des données depuis l’Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 3%

---

# (Version bêta) [!DNL Azure Event Hubs] connexion

## Présentation {#overview}

>[!IMPORTANT]
>
>La destination [!DNL Azure Event Hubs] de Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

[!DNL Azure Event Hubs] est une plateforme de diffusion en continu de données volumineuses et un service d’ingestion d’événements. Il peut recevoir et traiter des millions d’événements par seconde. Les données envoyées à un hub d’événements peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’adaptateurs de traitement par lot/stockage.

Vous pouvez créer une connexion sortante en temps réel à votre stockage [!DNL Azure Event Hubs] pour diffuser des données depuis Adobe Experience Platform.

* Pour plus d’informations sur [!DNL Azure Event Hubs], consultez la [documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Pour vous connecter à [!DNL Azure Event Hubs] par programmation, consultez le [tutoriel sur l’API des destinations de diffusion en continu](../../api/streaming-destinations.md).
* Pour vous connecter à [!DNL Azure Event Hubs] à l’aide de l’interface utilisateur de Platform, reportez-vous aux sections ci-dessous.

![AWS Kinesis dans l’interface utilisateur](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Cas d’utilisation {#use-cases}

En utilisant des destinations de diffusion en continu telles que [!DNL Azure Event Hubs], vous pouvez facilement alimenter les événements de segmentation à valeur élevée et les attributs de profil associés dans vos systèmes de votre choix.

Par exemple, un prospect a téléchargé un livre blanc qui les qualifie en segment &quot;forte propension à convertir&quot;. En mappant le segment dans lequel le prospect est ajouté à la destination [!DNL Azure Event Hubs], vous recevrez cet événement dans [!DNL Azure Event Hubs]. Vous pouvez y utiliser une approche par vous-même et décrire la logique commerciale en plus de l’événement, comme vous le pensez, qui fonctionne le mieux avec vos systèmes informatiques d’entreprise.

## Type d&#39;export {#export-type}

**Basé sur un profil**  : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse email, numéro de téléphone, nom), tel que sélectionné dans l&#39;écran de sélection des attributs du workflow d&#39;activation de l&#39; [audience](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL SAS Key]** Name et  **[!UICONTROL SAS Key]** : Renseignez le nom et la clé de votre clé SAS. Découvrez comment vous authentifier sur [!DNL Azure Event Hubs] à l’aide de clés SAS dans la [documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Espace de noms]** : Renseignez votre  [!DNL Azure Event Hubs] espace de noms. Découvrez les [!DNL Azure Event Hubs] espaces de noms dans la [documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nom]** : Renseignez un nom pour la connexion à  [!DNL Azure Event Hubs].
* **[!UICONTROL Description]** : Fournissez une description de la connexion.  Exemples : &quot;Clients Premium&quot;, &quot;Hommes intéressés par le kitesurfing&quot;.
* **[!UICONTROL eventHubName]** : Attribuez un nom au flux vers votre  [!DNL Azure Event Hubs] destination.

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers les destinations d’exportation de profils en continu](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Vos données [!DNL Experience Platform] exportées se trouvent dans [!DNL Azure Event Hubs] au format JSON. Par exemple, l’événement ci-dessous contient l’attribut de profil d’adresse électronique d’une audience qui s’est qualifiée pour un certain segment et qui a quitté un autre segment. Les identités de ce prospect sont ECID et email.

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


>[!MORELIKETHIS]
>
>* [Connectez-vous à Azure Event Hubs et activez les données à l’aide de l’API Flow Service](../../api/streaming-destinations.md)
* [Destination AWS Kinesis](./amazon-kinesis.md)
* [Types et catégories de destination](../../destination-types.md)

