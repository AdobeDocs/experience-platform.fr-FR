---
title: Destination Amazon Kinesis
seo-title: Destination Amazon Kinesis
description: Créez une connexion sortante en temps réel vers votre enregistrement Amazon Kinesis pour diffuser des données à partir d’Adobe Experience Platform.
seo-description: Créez une connexion sortante en temps réel vers votre enregistrement Amazon Kinesis pour diffuser des données à partir d’Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 5%

---


# Destination Amazon Kinesis

## Aperçu {#overview}

Le [!DNL Kinesis Data Streams] service d&#39;Amazon Web Services vous permet de collecter et de traiter des flux importants d&#39;enregistrements de données en temps réel.

Vous pouvez créer une connexion sortante en temps réel vers votre [!DNL Amazon Kinesis] enregistrement pour diffuser des données à partir d’Adobe Experience Platform.

* Pour plus d’informations sur [!DNL Amazon Kinesis]Amazon, voir la documentation [](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)Amazon.
* Pour vous connecter à [!DNL Amazon Kinesis] l’aide d’appels d’API, consultez le didacticiel [sur l’API]de destinations de diffusion en continu.
* Pour vous connecter à [!DNL Amazon Kinesis] l’aide de l’interface utilisateur CDP en temps réel d’Adobe, reportez-vous aux sections ci-dessous.

![Amazon Kinesis dans l’interface utilisateur](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## Cas d’utilisation {#use-cases}

En utilisant des destinations de diffusion en flux continu telles qu’Amazon Kinesis, vous pouvez facilement intégrer des événements de segmentation à forte valeur ajoutée et des attributs de profil associés dans vos systèmes de votre choix.

Par exemple, une prospect a téléchargé un livre blanc qui les classe dans un segment &quot;forte propension à la conversion&quot;. En mappant le segment dans lequel la prospect se trouve sur la destination Amazon Kinesis, vous recevriez ce événement dans Amazon Kinesis. Vous pouvez y appliquer une approche par soi-même et décrire la logique d&#39;entreprise en plus du événement, comme vous pensez qu&#39;elle fonctionne le mieux avec vos systèmes informatiques d&#39;entreprise.

## Connexion à la destination {#connect-destination}

See [Cloud storage destinations workflow ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)for instructions on how to connect to your cloud storage destinations, including those supported by [!DNL Amazon].

For [!DNL Amazon Kinesis] destinations, enter the following information in the create destination workflow:

### Dans l’étape Compte {#account-step}

* **Clé d’accès et clé** secrète Amazon Web Services : Dans [!DNL Amazon Web Services], générez une paire de clés d’accès secrètes pour accorder à Adobe un accès CDP en temps réel à votre [!DNL Amazon Kinesis] compte. Pour en savoir plus, consultez la documentation [sur les services Web](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon.
* **region**: Indiquez la [!DNL Amazon Web Services] région à laquelle diffuser les données.

![Champs d’entrée dans l’étape du compte](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### Dans l’étape d’authentification {#authentication-step}

* **Nom**: Attribuez un nom à votre connexion. [!DNL Amazon Kinesis]
* **Description**: Fournissez une description de votre connexion à [!DNL Amazon Kinesis].
* **stream**: Indiquez le nom de votre flux de données existant dans votre [!DNL Amazon Kinesis] compte. Adobe Real-time CDP exportera les données dans ce flux.

![Champs d’entrée dans l’étape d’authentification](/help/rtcdp/destinations/assets/aws-kinesis-authentication-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](/help/rtcdp/destinations/activate-destinations.md).

## Données exportées {#exported-data}

Vos données de plateforme d’expérience exportées s’affichent [!DNL Amazon Kinesis] au format JSON. Par exemple, un événement contenant l’identité de courriel haché d’une audience qui a quitté un certain segment peut ressembler à ceci :

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
>* Didacticiel sur l’API Amazon Kinesis
>* [Destination des centres de Événement Azure](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [Types et catégories de destination](/help/rtcdp/destinations/destination-types.md)

