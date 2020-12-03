---
keywords: Amazon Kinesis;kinesis destination;kinesis
title: Destination Amazon
seo-title: Destination Amazon
description: Créez une connexion sortante en temps réel vers votre enregistrement Kinesis Amazon pour diffuser les données de Adobe Experience Platform.
seo-description: Créez une connexion sortante en temps réel vers votre enregistrement Kinesis Amazon pour diffuser les données de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 7484e64d0d359f40ef242dfc9d2d1704018a8ed6
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 7%

---


# (bêta) [!DNL Amazon Kinesis] destination


>[!IMPORTANT]
>
>La [!DNL Amazon Kinesis] destination en temps réel du CDP est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

Le [!DNL Kinesis Data Streams] service de [!DNL Amazon Web Services] vous permet de collecter et de traiter des flux importants d&#39;enregistrements de données en temps réel.

Vous pouvez créer une connexion sortante en temps réel vers votre [!DNL Amazon Kinesis] enregistrement pour diffuser des données à partir de Adobe Experience Platform.

* Pour plus d’informations sur [!DNL Amazon Kinesis]Amazon, consultez la documentation [](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Pour vous connecter à [!DNL Amazon Kinesis] l’aide d’appels d’API, consultez le didacticiel [sur l’API](../../api/streaming-destinations.md)de destinations de diffusion en continu.
* Pour vous connecter à [!DNL Amazon Kinesis] l’aide de l’interface utilisateur CDP en temps réel, consultez les sections ci-dessous.

![Amazon dans l’interface utilisateur](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)


## Cas d’utilisation {#use-cases}

En utilisant des destinations de diffusion en flux continu, telles que [!DNL Amazon Kinesis], vous pouvez facilement intégrer des événements de segmentation à forte valeur ajoutée et des attributs de profil associés dans vos systèmes de choix.

Par exemple, une prospect a téléchargé un livre blanc qui les classe dans un segment &quot;forte propension à la conversion&quot;. En mappant le segment dans lequel la prospect arrive à la [!DNL Amazon Kinesis] destination, vous recevrez ce événement dans [!DNL Amazon Kinesis]. Vous pouvez y appliquer une approche par soi-même et décrire la logique d&#39;entreprise en plus du événement, comme vous pensez qu&#39;elle fonctionne le mieux avec vos systèmes informatiques d&#39;entreprise.

## Type d’exportation {#export-type}

**Basé sur** le profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [d’activation de](../../ui/activate-destinations.md#select-attributes)destination.

## Connexion à la destination {#connect-destination}

See [Cloud storage destinations workflow ](./workflow.md)for instructions on how to connect to your cloud storage destinations, including those supported by [!DNL Amazon].

For [!DNL Amazon Kinesis] destinations, enter the following information in the create destination workflow:

### Dans l’étape d’authentification {#authentication-step}

* **[!DNL Amazon Web Services]clé d&#39;accès et clé** secrète : Dans [!DNL Amazon Web Services], générez une `access key - secret access key` paire pour accorder un accès CDP en temps réel à votre [!DNL Amazon Kinesis] compte. Pour en savoir plus, consultez la documentation [sur les services Web](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon.
* **region**: Indiquez la [!DNL Amazon Web Services] région à laquelle diffuser les données.

![Champs d’entrée dans l’étape du compte](../../assets/catalog/cloud-storage/amazon-kinesis/account.png)

### Dans l’étape de configuration {#setup-step}

* **Nom**: Attribuez un nom à votre connexion. [!DNL Amazon Kinesis]
* **Description**: Fournissez une description de votre connexion à [!DNL Amazon Kinesis].
* **stream**: Indiquez le nom d’un flux de données existant dans votre [!DNL Amazon Kinesis] compte. Le CDP en temps réel exportera les données dans ce flux.

![Champs d’entrée dans l’étape d’authentification](../../assets/catalog/cloud-storage/amazon-kinesis/setup.png)

<!--

>[!IMPORTANT]
>
>Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](../../ui/activate-destinations.md).

## Données exportées {#exported-data}

Vos données [!DNL Experience Platform] exportées s’affichent [!DNL Amazon Kinesis] au format JSON. Par exemple, le événement ci-dessous contient l’attribut profil d’adresse électronique d’une audience qui s’est qualifiée pour un certain segment et a quitté un autre segment. Les identités de cette prospect sont ECID et email.

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
>* [Se connecter à Amazon Kinesis et activer des données à l’aide d’appels d’API](../../api/streaming-destinations.md)
>* [Destination des centres de Événement Azure](./azure-event-hubs.md)
>* [Types et catégories de destination](../../destination-types.md)

