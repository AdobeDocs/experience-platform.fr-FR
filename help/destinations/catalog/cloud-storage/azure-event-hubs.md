---
keywords: Destination du concentrateur d'événements Azure ; concentrateur d'événements azure ; thub d'événements azure
title: (Bêta) [concentrateurs d’événements Azure DNL]
description: Créez une connexion sortante en temps réel à votre stockage !DNL Azure Event Hubs] pour diffuser des données à partir de l’Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 3%

---

# (Bêta) [!DNL Azure Event Hubs] connexion

## Présentation {#overview}

>[!IMPORTANT]
>
>Le [!DNL Azure Event Hubs] dans Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

[!DNL Azure Event Hubs] est une plate-forme de diffusion de données massives et un service d&#39;assimilation d&#39;événements. Il peut recevoir et traiter des millions d&#39;événements par seconde. Les données envoyées à un centre d&#39;événements peuvent être transformées et stockées à l&#39;aide de n&#39;importe quel fournisseur d&#39;analyse en temps réel ou de cartes de traitement/stockage.

Vous pouvez créer une connexion sortante en temps réel vers votre [!DNL Azure Event Hubs] pour diffuser des données à partir de Adobe Experience Platform.

* Pour plus d’informations sur [!DNL Azure Event Hubs], consultez la section [Documentation de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Pour vous connecter à [!DNL Azure Event Hubs] par programme, consultez la section [Didacticiel sur l’API des destinations en flux continu](../../api/streaming-destinations.md).
* Pour vous connecter à [!DNL Azure Event Hubs] à l’aide de l’interface utilisateur de la plate-forme, consultez les sections ci-dessous.

![AWS Kinesis dans l&#39;interface utilisateur](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Cas d’utilisation {#use-cases}

En utilisant des destinations de diffusion telles que [!DNL Azure Event Hubs], vous pouvez facilement insérer des événements de segmentation de grande valeur et des attributs de profil associés dans vos systèmes de votre choix.

Par exemple, un prospect a téléchargé un livre blanc qui les qualifie en un segment de &quot;forte propension à convertir&quot;. En mappant le segment dans lequel le prospect tombe sur le [!DNL Azure Event Hubs] destination, vous recevriez cet événement dans [!DNL Azure Event Hubs]. Vous pouvez alors utiliser une approche &quot;bricolage&quot; et décrire la logique métier en plus de l&#39;événement, comme vous pensez qu&#39;elle fonctionnerait mieux avec vos systèmes informatiques d&#39;entreprise.

## Type d’exportation {#export-type}

**Basé sur le profil** - vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités (par exemple : adresse e-mail, numéro de téléphone, nom de famille), comme choisi dans l’écran des attributs sélectionnés de la [workflow d’activation du public](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Se connecter à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans la section [didacticiel sur la configuration de destination](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

En [configuration](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom de clé SAS]** et **[!UICONTROL Clé SAS]**: Remplissez votre clé et votre nom de clé SAS. En savoir plus sur l’authentification auprès de [!DNL Azure Event Hubs] avec les clés SAS dans le dossier [Documentation de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Espace de noms]**: Remplissez votre [!DNL Azure Event Hubs] espace de noms. En savoir plus [!DNL Azure Event Hubs] espaces de noms dans [Documentation de Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nom]**: Renseignez un nom pour la connexion à [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Fournissez une description de la connexion.  Exemples : &quot;Clients de catégorie Premium&quot;, &quot;Hommes intéressés par le kitesurf&quot;.
* **[!UICONTROL eventHubName]**: Attribuez un nom au flux [!DNL Azure Event Hubs] destination.

## Activer les segments vers cette destination {#activate}

Voir [Activer les données d’audience vers les destinations d’exportation de profil de diffusion en continu](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Votre exportation [!DNL Experience Platform] les données atterrissent dans [!DNL Azure Event Hubs] au format JSON. Par exemple, l’événement ci-dessous contient l’attribut de profil d’adresse électronique d’un public qui s’est qualifié pour un certain segment et a quitté un autre segment. Les identités de ce prospect sont ECID et e-mail.

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


>[!MORELIKETHIS]
>
>* [Connexion à Azure Event Hubs et activation de données à l’aide de l’API Flow Service](../../api/streaming-destinations.md)
>* [Destination AWS Kinesis](./amazon-kinesis.md)
>* [Types et catégories de destination](../../destination-types.md)

