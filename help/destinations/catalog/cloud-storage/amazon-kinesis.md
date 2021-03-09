---
keywords: Amazon Kinesis ; destination de la kinesis ; kinesis
title: Connexion Amazon
description: Créez une connexion sortante en temps réel vers votre enregistrement Kinesis Amazon pour diffuser les données de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 32cb198bcf2c142b50c4b7a60282f0c923be06b1
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 6%

---


# (Beta) [!DNL Amazon Kinesis] connexion

>[!IMPORTANT]
>
>La destination [!DNL Amazon Kinesis] dans Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

Le service [!DNL Kinesis Data Streams] de [!DNL Amazon Web Services] vous permet de collecter et de traiter de vastes flux d&#39;enregistrements de données en temps réel.

Vous pouvez créer une connexion sortante en temps réel à votre [!DNL Amazon Kinesis] enregistrement de diffusion de données à partir de Adobe Experience Platform.

* Pour plus d&#39;informations sur [!DNL Amazon Kinesis], consultez la [documentation Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Pour vous connecter à [!DNL Amazon Kinesis] par programmation, consultez le [didacticiel sur l&#39;API de destinations de diffusion en continu](../../api/streaming-destinations.md).
* Pour vous connecter à [!DNL Amazon Kinesis] à l&#39;aide de l&#39;interface utilisateur de la plate-forme, consultez les sections ci-dessous.

![Amazon dans l’interface utilisateur](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Cas d’utilisation {#use-cases}

En utilisant des destinations de diffusion en flux continu telles que [!DNL Amazon Kinesis], vous pouvez facilement intégrer des événements de segmentation à forte valeur ajoutée et des attributs de profil associés dans vos systèmes de choix.

Par exemple, une prospect a téléchargé un livre blanc qui les classe dans un segment &quot;forte propension à la conversion&quot;. En mappant le segment dans lequel la prospect se trouve sur la destination [!DNL Amazon Kinesis], vous recevriez ce événement dans [!DNL Amazon Kinesis]. Vous pouvez y appliquer une approche par soi-même et décrire la logique d&#39;entreprise en plus du événement, comme vous pensez qu&#39;elle fonctionne le mieux avec vos systèmes informatiques d&#39;entreprise.

## Type d&#39;exportation {#export-type}

**Basé sur**  le profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [ d’activation de ](../../ui/activate-destinations.md#select-attributes)destination.

## Connexion à la destination {#connect-destination}

Voir [Flux de travaux de destination des enregistrements cloud ](./workflow.md)pour savoir comment se connecter à vos destinations d’enregistrement cloud, y compris celles prises en charge par [!DNL Amazon].

Pour les destinations [!DNL Amazon Kinesis], saisissez les informations suivantes dans le processus de création de destination :

### Dans l’étape d’authentification {#authentication-step}

* **[!DNL Amazon Web Services]clé d&#39;accès et clé** secrète : Dans  [!DNL Amazon Web Services], générez une  `access key - secret access key` paire pour accorder l’accès à la plate-forme à votre  [!DNL Amazon Kinesis] compte. Pour en savoir plus, consultez la [documentation Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **region** : Indiquez la  [!DNL Amazon Web Services] région à laquelle diffuser les données.

![Champs d’entrée dans l’étape du compte](../../assets/catalog/cloud-storage/amazon-kinesis/account.png)

### Dans l’étape de configuration {#setup-step}

* **Nom** : Attribuez un nom à votre connexion.  [!DNL Amazon Kinesis]
* **Description** : Fournissez une description de votre connexion à  [!DNL Amazon Kinesis].
* **stream** : Indiquez le nom d’un flux de données existant dans votre  [!DNL Amazon Kinesis] compte. La plate-forme exportera les données vers ce flux.
* **[!UICONTROL Actions]** marketing : Les actions marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des actions marketing définies par Adobe ou créer votre propre action marketing. Pour plus d’informations sur les actions marketing, voir la page [Gouvernance des données dans Adobe Experience Platform](../../../data-governance/policies/overview.md). Pour plus d&#39;informations sur les actions marketing définies par l&#39;Adobe, consultez la [Présentation des stratégies d&#39;utilisation des données](../../../data-governance/policies/overview.md).

![Champs d’entrée dans l’étape d’authentification](../../assets/catalog/cloud-storage/amazon-kinesis/setup.png)

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](../../ui/activate-destinations.md).

## Données exportées {#exported-data}

Vos données [!DNL Experience Platform] exportées atterrissent dans [!DNL Amazon Kinesis] au format JSON. Par exemple, le événement ci-dessous contient l’attribut profil d’adresse électronique d’une audience qui s’est qualifiée pour un certain segment et a quitté un autre segment. Les identités de cette prospect sont ECID et email.

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
>* [Connexion à Amazon Kinesis et activation des données à l’aide de l’API du service de flux](../../api/streaming-destinations.md)
>* [Destination des centres de Événement Azure](./azure-event-hubs.md)
>* [Types et catégories de destination](../../destination-types.md)

