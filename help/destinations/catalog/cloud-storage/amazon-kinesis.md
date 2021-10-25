---
keywords: Amazon Kinesis ; destination Kinesis ; kinesis
title: Connexion Amazon
description: Créez une connexion sortante en temps réel à votre stockage Amazon Kinesis pour diffuser des données à partir de Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 3%

---

# (Bêta) [!DNL Amazon Kinesis] connexion

## Présentation {#overview}

>[!IMPORTANT]
>
>Le [!DNL Amazon Kinesis] dans Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

Le [!DNL Kinesis Data Streams] service par [!DNL Amazon Web Services] vous permet de collecter et de traiter des flux importants de données en temps réel.

Vous pouvez créer une connexion sortante en temps réel vers votre [!DNL Amazon Kinesis] pour diffuser des données à partir de Adobe Experience Platform.

* Pour plus d’informations sur [!DNL Amazon Kinesis], consultez la section [Documentation Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Pour vous connecter à [!DNL Amazon Kinesis] par programme, consultez la section [Didacticiel sur l’API des destinations en flux continu](../../api/streaming-destinations.md).
* Pour vous connecter à [!DNL Amazon Kinesis] à l’aide de l’interface utilisateur de la plate-forme, consultez les sections ci-dessous.

![Amazon Kinesis dans l&#39;interface utilisateur](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Cas d’utilisation {#use-cases}

En utilisant des destinations de diffusion telles que [!DNL Amazon Kinesis], vous pouvez facilement insérer des événements de segmentation de grande valeur et des attributs de profil associés dans vos systèmes de votre choix.

Par exemple, un prospect a téléchargé un livre blanc qui les qualifie en un segment de &quot;forte propension à convertir&quot;. En mappant le segment dans lequel le prospect tombe sur le [!DNL Amazon Kinesis] destination, vous recevriez cet événement dans [!DNL Amazon Kinesis]. Vous pouvez alors utiliser une approche &quot;bricolage&quot; et décrire la logique métier en plus de l&#39;événement, comme vous pensez qu&#39;elle fonctionnerait mieux avec vos systèmes informatiques d&#39;entreprise.

## Type d’exportation {#export-type}

**Basé sur le profil** - vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités (par exemple : adresse e-mail, numéro de téléphone, nom de famille), comme choisi dans l’écran des attributs sélectionnés de la [workflow d’activation du public](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Obligatoire [!DNL Amazon Kinesis] autorisations {#required-kinesis-permission}

Pour connecter et exporter des données vers votre [!DNL Amazon Kinesis] , l’Experience Platform a besoin d’autorisations pour les actions suivantes :

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Ces autorisations sont organisées par le biais de la [!DNL Kinesis] et sont contrôlés par Platform une fois que vous avez configuré votre destination Kinesis dans l&#39;interface utilisateur de Platform.

L’exemple ci-dessous affiche les droits d’accès minimum requis pour exporter les données vers un [!DNL Kinesis] destination.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `kinesis:ListStreams` | Action répertoriant vos flux de données Kinesis Amazon. |
| `kinesis:PutRecord` | Action qui écrit un enregistrement de données unique dans un flux de données Kinesis. |
| `kinesis:PutRecords` | Action qui écrit plusieurs enregistrements de données dans un flux de données Kinesis en un seul appel. |

Pour plus d’informations sur le contrôle de l’accès pour [!DNL Kinesis] flux de données, lisez ce qui suit : [[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Se connecter à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans la section [didacticiel sur la configuration de destination](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

En [configuration](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!DNL Amazon Web Services]clé d&#39;accès et clé secrète**: Entrée [!DNL Amazon Web Services], générez une `access key - secret access key` pour accorder l’accès à votre plate-forme [!DNL Amazon Kinesis] compte. Pour en savoir plus, consultez la page [Documentation de Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **région**: Indiquez laquelle [!DNL Amazon Web Services] pour diffuser les données vers.
* **Nom**: Fournissez un nom pour votre connexion à [!DNL Amazon Kinesis]
* **Description**: Fournissez une description de votre connexion à [!DNL Amazon Kinesis].
* **flux**: Indiquez le nom d’un flux de données existant dans votre [!DNL Amazon Kinesis] compte. La plate-forme exportera les données vers ce flux.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activer les segments vers cette destination {#activate}

Voir [Activer les données d’audience vers les destinations d’exportation de profil de diffusion en continu](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Votre exportation [!DNL Experience Platform] les données atterrissent dans [!DNL Amazon Kinesis] au format JSON. Par exemple, l’événement ci-dessous contient l’attribut de profil d’adresse électronique d’un public qui s’est qualifié pour un certain segment et a quitté un autre segment. Les identités de ce prospect sont ECID et e-mail.

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
>* [Connexion à Amazon Kinesis et activation de données à l’aide de l’API Flow Service](../../api/streaming-destinations.md)
>* [Destination Azure Event Hubs](./azure-event-hubs.md)
>* [Types et catégories de destination](../../destination-types.md)

