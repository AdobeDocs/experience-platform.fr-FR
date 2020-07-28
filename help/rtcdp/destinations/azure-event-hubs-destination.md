---
title: (bêta) Destination des centres de Événement Azure
seo-title: (bêta) Destination des centres de Événement Azure
description: Créez une connexion sortante en temps réel à votre enregistrement Azure Événement Hubs pour diffuser les données de l'Experience Platform.
seo-description: Créez une connexion sortante en temps réel à votre enregistrement Azure Événement Hubs pour diffuser les données de l'Experience Platform.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 7%

---


# (bêta) [!DNL Azure Event Hubs] destination

>[!IMPORTANT]
>
>La [!DNL Azure Event Hubs] destination en temps réel Adobe du CDP est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

[!DNL Azure Event Hubs] est une plate-forme de diffusion de données massives et un service d’assimilation de événements. Il peut recevoir et traiter des millions de événements par seconde. Les données envoyées à un hub de événement peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou de cartes de traitement par lot/d’enregistrement.

Vous pouvez créer une connexion sortante en temps réel vers votre [!DNL Azure Event Hubs] enregistrement pour diffuser en continu des données à partir de l’Adobe Experience Platform.

* Pour plus d&#39;informations sur [!DNL Azure Event Hubs]Microsoft, consultez la documentation [](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)Microsoft.
* Pour vous connecter à [!DNL Azure Event Hubs] l’aide d’appels d’API, consultez le didacticiel [sur l’API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)de destinations de diffusion en continu.
* Pour vous connecter à [!DNL Azure Event Hubs] l&#39;aide de l&#39;interface utilisateur CDP en temps réel de l&#39;Adobe, consultez les sections ci-dessous.

![Kinesis AWS dans l’interface utilisateur](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## Cas d’utilisation {#use-cases}

En utilisant des destinations de diffusion en flux continu, telles que [!DNL Azure Event Hubs], vous pouvez facilement intégrer des événements de segmentation à forte valeur ajoutée et des attributs de profil associés dans vos systèmes de choix.

Par exemple, une prospect a téléchargé un livre blanc qui les classe dans un segment &quot;forte propension à la conversion&quot;. En mappant le segment dans lequel la prospect arrive à la [!DNL Azure Event Hubs] destination, vous recevrez ce événement dans [!DNL Azure Event Hubs]. Vous pouvez y appliquer une approche par soi-même et décrire la logique d&#39;entreprise en plus du événement, comme vous pensez qu&#39;elle fonctionne le mieux avec vos systèmes informatiques d&#39;entreprise.

## Connexion à la destination {#connect-destination}

See [Cloud storage destinations workflow ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)for instructions on how to connect to your cloud storage destinations, including [!DNL Azure Event Hubs].

For [!DNL Azure Event Hubs] destinations, enter the following information in the create destination workflow:

### Dans l’étape d’authentification {#authentication-step}

* **[!UICONTROL Nom]** de la clé SAS et clé **** SAS : Renseignez votre clé et votre nom de clé SAS. Découvrez comment vous authentifier à [!DNL Azure Event Hubs] l&#39;aide de clés SAS dans la documentation [](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* **[!UICONTROL Espace de nommage]**: Remplissez votre [!DNL Azure Event Hubs] espace de nommage. Découvrez les [!DNL Azure Event Hubs] espaces de nommage dans la documentation [](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)Microsoft.

![Entrée requise dans l’étape d’authentification](/help/rtcdp/destinations/assets/event-hubs-authentication.png)

### Dans l’étape de configuration {#setup-step}

* **[!UICONTROL Nom]**: Renseignez le nom de la connexion à [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Fournissez une description de la connexion.  Exemples : &quot;Clients Premium&quot;, &quot;Hommes intéressés par le kitesurf&quot;.
* **[!UICONTROL eventHubName]**: Attribuez un nom au flux jusqu’à votre [!DNL Azure Event Hubs] destination.

![Données requises à l’étape de configuration](/help/rtcdp/destinations/assets/event-hubs-setup-step.png)

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](/help/rtcdp/destinations/activate-destinations.md).


## Données exportées {#exported-data}

Vos données [!DNL Experience Platform] exportées s’affichent [!DNL Azure Event Hubs] au format JSON. Par exemple, le événement ci-dessous contient l’attribut profil d’adresse électronique d’une audience qui s’est qualifiée pour un certain segment et a quitté un autre segment. Les identités de cette prospect sont ECID et email.

```
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
>* [Se connecter à Azure Événement Hubs et activer des données à l&#39;aide d&#39;appels d&#39;API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Destination AWS Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [Types et catégories de destination](/help/rtcdp/destinations/destination-types.md)