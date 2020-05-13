---
title: (bêta) Destination des centres de Événement Azure
seo-title: (bêta) Destination des centres de Événement Azure
description: Créez une connexion sortante en temps réel à votre enregistrement Azure Événement Hubs pour diffuser des données à partir de la plateforme d'expérience.
seo-description: Créez une connexion sortante en temps réel à votre enregistrement Azure Événement Hubs pour diffuser des données à partir de la plateforme d'expérience.
translation-type: tm+mt
source-git-commit: 47e03d3f58bd31b1aec45cbf268e3285dd5921ea
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 6%

---


# (bêta) Destination des centres de Événement Azure

>[!IMPORTANT]
>
>La [!DNL Azure Event Hubs] destination dans le CDP en temps réel d’Adobe est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Aperçu {#overview}

[!DNL Azure Event Hubs] est une plate-forme de diffusion de données massives et un service d’assimilation de événements. Il peut recevoir et traiter des millions de événements par seconde. Les données envoyées à un hub de événement peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou de cartes de traitement par lot/d’enregistrement.

Vous pouvez créer une connexion sortante en temps réel vers votre [!DNL Azure Event Hubs] enregistrement pour diffuser des données à partir d’Adobe Experience Platform.

* Pour plus d&#39;informations sur [!DNL Azure Event Hubs]Microsoft, consultez la documentation [](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)Microsoft.
* Pour vous connecter à [!DNL Azure Event Hubs] l’aide d’appels d’API, consultez le didacticiel [sur l’API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)de destinations de diffusion en continu.
* Pour vous connecter à [!DNL Azure Event Hubs] l’aide de l’interface utilisateur CDP en temps réel d’Adobe, reportez-vous aux sections ci-dessous.

![AWS Kinesis dans l’interface utilisateur](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## Cas d’utilisation {#use-cases}

En utilisant des destinations de diffusion en continu telles que les centres de Événement Azure, vous pouvez facilement alimenter des événements de segmentation à forte valeur ajoutée et des attributs de profil associés dans vos systèmes de choix.

Par exemple, une prospect a téléchargé un livre blanc qui les classe dans un segment &quot;forte propension à la conversion&quot;. En mappant le segment dans lequel la prospect arrive à la destination des centres de Événement Azure, vous recevriez ce événement dans les centres de Événement Azure. Vous pouvez y appliquer une approche par soi-même et décrire la logique d&#39;entreprise en plus du événement, comme vous pensez qu&#39;elle fonctionne le mieux avec vos systèmes informatiques d&#39;entreprise.

## Connexion à la destination {#connect-destination}

See [Cloud storage destinations workflow ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)for instructions on how to connect to your cloud storage destinations, including [!DNL Azure Event Hubs].

For [!DNL Azure Event Hubs] destinations, enter the following information in the create destination workflow:

### Dans l’étape Compte {#account-step}

* **[!UICONTROL Nom]** de la clé SAS et clé **** SAS : Renseignez votre clé et votre nom de clé SAS. Découvrez comment vous authentifier à [!DNL Azure Event Hubs] l&#39;aide de clés SAS dans la documentation [](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* **[!UICONTROL Espace de nommage]**: Remplissez votre [!DNL Azure Event Hubs] espace de nommage. Découvrez les [!DNL Azure Event Hubs] espaces de nommage dans la documentation [](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)Microsoft.

![Entrée requise dans l’étape d’authentification](/help/rtcdp/destinations/assets/event-hubs-account-step.png)

### Dans l’étape d’authentification {#authentication-step}

* **[!UICONTROL Nom]**: Renseignez le nom de la connexion à [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Fournissez une description de la connexion.  Exemples : &quot;Clients Premium&quot;, &quot;Hommes intéressés par le kitesurf&quot;.
* **[!UICONTROL eventHubName]**: Attribuez un nom au flux jusqu’à votre [!DNL Azure Event Hubs] destination.

![Données requises à l’étape de configuration](/help/rtcdp/destinations/assets/event-hubs-authentication-step.png)

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](/help/rtcdp/destinations/activate-destinations.md).


## Données exportées {#exported-data}

Vos données de plateforme d’expérience exportées s’affichent [!DNL Azure Event Hubs] au format JSON. Par exemple, un flux de événement contenant l’identité de courriel haché d’une audience qui a quitté un certain segment peut ressembler à ceci :

```
{
   "segmentMembership":{
      "ups":{
         "7841ba61-23c1-4bb3-a495-00d695fe1e93":{
            "lastQualificationTime":"2020-03-03T21:24:39Z",
            "status":"exited"
         }
      }
   }
},
"identityMap":{
   "email_lc_sha256":[
      {
         "id":"655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
         "id":"66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
   ]
},
```



>[!MORELIKETHIS]
>
>* [Se connecter à Azure Événement Hubs et activer des données à l&#39;aide d&#39;appels d&#39;API](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [Destination AWS Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [Types et catégories de destination](/help/rtcdp/destinations/destination-types.md)