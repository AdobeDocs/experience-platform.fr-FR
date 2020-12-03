---
keywords: Azure event hub destination;azure event hub;azure eventhub
title: (bêta) Destination des centres de Événement Azure
seo-title: (bêta) Destination des centres de Événement Azure
description: Créez une connexion sortante en temps réel à votre enregistrement Azure Événement Hubs pour diffuser les données de l'Experience Platform.
seo-description: Créez une connexion sortante en temps réel à votre enregistrement Azure Événement Hubs pour diffuser les données de l'Experience Platform.
translation-type: tm+mt
source-git-commit: 7484e64d0d359f40ef242dfc9d2d1704018a8ed6
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 6%

---


# (bêta) [!DNL Azure Event Hubs] destination

>[!IMPORTANT]
>
>La [!DNL Azure Event Hubs] destination en temps réel du CDP est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

[!DNL Azure Event Hubs] est une plate-forme de diffusion de données massives et un service d’assimilation de événements. Il peut recevoir et traiter des millions de événements par seconde. Les données envoyées à un hub de événement peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou de cartes de traitement par lot/d’enregistrement.

Vous pouvez créer une connexion sortante en temps réel vers votre [!DNL Azure Event Hubs] enregistrement pour diffuser des données à partir de Adobe Experience Platform.

* Pour plus d&#39;informations sur [!DNL Azure Event Hubs]Microsoft, consultez la documentation [](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)Microsoft.
* Pour vous connecter à [!DNL Azure Event Hubs] l’aide d’appels d’API, consultez le didacticiel [sur l’API](../../api/streaming-destinations.md)de destinations de diffusion en continu.
* Pour vous connecter à [!DNL Azure Event Hubs] l’aide de l’interface utilisateur CDP en temps réel, consultez les sections ci-dessous.

![Kinesis AWS dans l’interface utilisateur](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Cas d’utilisation {#use-cases}

En utilisant des destinations de diffusion en flux continu, telles que [!DNL Azure Event Hubs], vous pouvez facilement intégrer des événements de segmentation à forte valeur ajoutée et des attributs de profil associés dans vos systèmes de choix.

Par exemple, une prospect a téléchargé un livre blanc qui les classe dans un segment &quot;forte propension à la conversion&quot;. En mappant le segment dans lequel la prospect arrive à la [!DNL Azure Event Hubs] destination, vous recevrez ce événement dans [!DNL Azure Event Hubs]. Vous pouvez y appliquer une approche par soi-même et décrire la logique d&#39;entreprise en plus du événement, comme vous pensez qu&#39;elle fonctionne le mieux avec vos systèmes informatiques d&#39;entreprise.

## Type d’exportation {#export-type}

**Basé sur** le profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [d’activation de](../../ui/activate-destinations.md#select-attributes)destination.

## Connexion à la destination {#connect-destination}

See [Cloud storage destinations workflow ](./workflow.md)for instructions on how to connect to your cloud storage destinations, including [!DNL Azure Event Hubs].

For [!DNL Azure Event Hubs] destinations, enter the following information in the create destination workflow:

### Dans l’étape d’authentification {#authentication-step}

* **[!UICONTROL Nom]** de la clé SAS et clé **** SAS : Renseignez votre clé et votre nom de clé SAS. Découvrez comment vous authentifier à [!DNL Azure Event Hubs] l&#39;aide de clés SAS dans la documentation [](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* **[!UICONTROL Espace de nommage]**: Remplissez votre [!DNL Azure Event Hubs] espace de nommage. Découvrez les [!DNL Azure Event Hubs] espaces de nommage dans la documentation [](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)Microsoft.

![Entrée requise dans l’étape d’authentification](../../assets/catalog/cloud-storage/event-hubs/authentication.png)

### Dans l’étape de configuration {#setup-step}

* **[!UICONTROL Nom]**: Renseignez le nom de la connexion à [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Fournissez une description de la connexion.  Exemples : &quot;Clients Premium&quot;, &quot;Hommes intéressés par le kitesurf&quot;.
* **[!UICONTROL eventHubName]**: Attribuez un nom au flux jusqu’à votre [!DNL Azure Event Hubs] destination.

![Données requises à l’étape de configuration](../../assets/catalog/cloud-storage/event-hubs/setup.png)

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](../../ui/activate-destinations.md).


## Données exportées {#exported-data}

Vos données [!DNL Experience Platform] exportées s’affichent [!DNL Azure Event Hubs] au format JSON. Par exemple, le événement ci-dessous contient l’attribut profil d’adresse électronique d’une audience qui s’est qualifiée pour un certain segment et a quitté un autre segment. Les identités de cette prospect sont ECID et email.

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
>* [Se connecter à Azure Événement Hubs et activer des données à l&#39;aide d&#39;appels d&#39;API](../../api/streaming-destinations.md)
>* [Destination AWS Kinesis](./amazon-kinesis.md)
>* [Types et catégories de destination](../../destination-types.md)