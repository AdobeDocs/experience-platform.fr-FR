---
keywords: Experience Platform ; accueil ; sujets populaires ; Amazon ; amazon kinesis ; Kinesis ; kinesis
solution: Experience Platform
title: Présentation du connecteur source Amazon
topic-legacy: overview
description: Découvrez comment connecter Amazon Kinesis à Adobe Experience Platform à à l’aide des API ou de l’interface utilisateur.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
translation-type: tm+mt
source-git-commit: af11bc966889be54fc27e02f3eee321519cef88f
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---

# [!DNL Amazon Kinesis] connecteur

Adobe Experience Platform fournit une connectivité native pour les fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform] et [!DNL Azure]. Vous pouvez importer vos données de ces systèmes dans [!DNL Platform].

Les sources d’enregistrement Cloud peuvent importer vos propres données dans [!DNL Platform] sans avoir à télécharger, mettre en forme ou télécharger. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. [!DNL Platform] vous permet d’importer des données  [!DNL Amazon Kinesis] en temps réel.

## LISTE AUTORISÉE d&#39;adresse IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas d’adresses IP spécifiques à votre région à votre liste autorisée, des erreurs ou des performances risquent d’apparaître lors de l’utilisation de sources. Pour plus d&#39;informations, consultez la page [liste autorisée d&#39;adresse IP](../../ip-address-allow-list.md).

## Conditions préalables

La section suivante fournit des informations supplémentaires sur la configuration de prérequis requise avant de pouvoir créer une connexion source [!DNL Kinesis].

### Configuration de la stratégie d’accès

Un flux [!DNL Kinesis] nécessite les autorisations suivantes pour créer une connexion source :

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Ces autorisations sont organisées via la console [!DNL Kinesis] et sont vérifiées par Platform une fois que vous avez saisi vos informations d’identification et sélectionné votre flux de données.

L&#39;exemple ci-dessous présente les droits d&#39;accès minimaux requis pour créer une connexion source [!DNL Kinesis].

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
| `kinesis:GetRecords` | Action requise pour obtenir des enregistrements à partir d’un décalage ou d’un ID partagé spécifique. |
| `kinesis:DescribeStream` | Action qui renvoie des informations concernant le flux, y compris le mappage partagé, nécessaire pour générer un identifiant partagé. |
| `kinesis:ListStreams` | Action requise pour liste des flux disponibles que vous pouvez sélectionner dans l’interface utilisateur. |

Pour plus d&#39;informations sur le contrôle de l&#39;accès aux flux de données [!DNL Kinesis], consultez le [[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html) suivant.

### Configurer le type d&#39;itérateur

[!DNL Kinesis] prend en charge les types d&#39;itérateur suivants pour vous permettre de spécifier l&#39;ordre de lecture de vos données :

| Type d&#39;itérateur | Description |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Les données sont lues à partir d’une position identifiée par un numéro de séquence spécifique. |
| `AFTER_SEQUENCE_NUMBER` | Les données sont lues en commençant après la position identifiée par un numéro de séquence spécifique. |
| `AT_TIMESTAMP` | Les données sont lues à partir d’une position identifiée par un horodatage spécifique. |
| `TRIM_HORIZON` | Les données sont lues à partir du plus ancien enregistrement de données. |
| `LATEST` | Les données sont lues à partir de l’enregistrement de données le plus récent. |

Une source d&#39;interface utilisateur [!DNL Kinesis] ne prend actuellement en charge que `TRIM_HORIZON`, tandis que l&#39;API prend en charge à la fois `TRIM_HORIZON` et `LATEST` en tant que modes pour obtenir des données. La valeur d&#39;itérateur par défaut utilisée par Platform pour la source [!DNL Kinesis] est `TRIM_HORIZON`.

Pour plus d&#39;informations sur les types d&#39;itérateur, consultez le [[!DNL Kinesis] document](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax) suivant.

## Connecter [!DNL Amazon Kinesis] à [!DNL Platform]

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Amazon Kinesis] à [!DNL Platform] à l&#39;aide d&#39;API ou de l&#39;interface utilisateur :

### Utilisation des API

- [Création d’une connexion source Amazon à l’aide de l’API du service de flux](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Collecte de données en flux continu à l’aide de l’API du service de flux](../../tutorials/api/collect/streaming.md)

### Utilisation de l’interface utilisateur

- [Création d’une connexion source Amazon dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configuration d’un flux de données pour une connexion d’enregistrement cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
