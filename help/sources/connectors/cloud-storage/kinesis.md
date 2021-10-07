---
keywords: Experience Platform;accueil;rubriques les plus consultées;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Présentation d’Amazon Kinesis Source Connector
topic-legacy: overview
description: Découvrez comment connecter Amazon Kinesis à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 481f72c5c630f6dbcbbfd3eee11c91787e780f3f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# [!DNL Amazon Kinesis] connector

Adobe Experience Platform fournit une connectivité native pour les fournisseurs cloud tels qu’AWS, [!DNL Google Cloud Platform] et [!DNL Azure]. Vous pouvez importer vos données de ces systèmes dans [!DNL Platform].

Les sources de stockage dans le cloud peuvent importer vos propres données dans [!DNL Platform] sans avoir à les télécharger, les formater ou les charger. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le workflow Sources . [!DNL Platform] vous permet d’importer des données  [!DNL Amazon Kinesis] en temps réel.

## Conditions préalables

La section suivante fournit des informations supplémentaires sur la configuration de prérequis requise pour pouvoir créer une connexion source [!DNL Kinesis].

### Configuration de la stratégie d’accès

Un flux [!DNL Kinesis] nécessite les autorisations suivantes pour créer une connexion source :

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Ces autorisations sont organisées via la console [!DNL Kinesis] et sont vérifiées par Platform une fois que vous avez saisi vos informations d’identification et sélectionné votre flux de données.

L’exemple ci-dessous illustre les droits d’accès minimum requis pour créer une connexion source [!DNL Kinesis].

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:GetShardIterator",
                "kinesis:GetRecords",
                "kinesis:DescribeStream",
                "kinesis:ListStreams"
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
| `kinesis:GetShardIterator` | Action requise pour parcourir les enregistrements. |
| `kinesis:GetRecords` | Action requise pour obtenir des enregistrements à partir d’un décalage ou d’un identifiant de partage spécifique. |
| `kinesis:DescribeStream` | Action qui renvoie des informations concernant le flux, y compris la carte partagée, nécessaire pour générer un identifiant partagé. |
| `kinesis:ListStreams` | Action requise pour répertorier les flux disponibles que vous pouvez sélectionner dans l’interface utilisateur. |

Pour plus d’informations sur le contrôle de l’accès aux flux de données [!DNL Kinesis], consultez le [[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html) suivant.

### Configuration du type d’itérateur

[!DNL Kinesis] prend en charge les types d’itérateur suivants pour vous permettre de spécifier l’ordre de lecture de vos données :

| Type d’itérateur | Description |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Les données sont lues à partir d’une position identifiée par un numéro de séquence spécifique. |
| `AFTER_SEQUENCE_NUMBER` | Les données sont lues en commençant après la position identifiée par un numéro de séquence spécifique. |
| `AT_TIMESTAMP` | Les données sont lues à partir d’une position identifiée par un horodatage spécifique. |
| `TRIM_HORIZON` | Les données sont lues à partir de l’enregistrement de données le plus ancien. |
| `LATEST` | Les données sont lues à partir de l’enregistrement de données le plus récent. |

Une source d’interface utilisateur [!DNL Kinesis] ne prend actuellement en charge que `TRIM_HORIZON`, tandis que l’API prend en charge les modes `TRIM_HORIZON` et `LATEST` pour obtenir des données. La valeur d’itérateur par défaut utilisée par Platform pour la source [!DNL Kinesis] est `TRIM_HORIZON`.

Pour plus d’informations sur les types d’itérateur, voir le [[!DNL Kinesis] document](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax) suivant.

## Connectez [!DNL Amazon Kinesis] à [!DNL Platform]

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Amazon Kinesis] à [!DNL Platform] à l’aide des API ou de l’interface utilisateur :

### Utilisation des API

- [Création d’une connexion source Kinesis Amazon à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Collecte de données en continu à l’aide de l’API Flow Service](../../tutorials/api/collect/streaming.md)

### Utilisation de l’interface utilisateur

- [Création d’une connexion source Amazon Kinesis dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configuration d’un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
