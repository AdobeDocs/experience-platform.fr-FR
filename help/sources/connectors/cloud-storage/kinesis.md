---
title: Présentation du connecteur Source Amazon Kinesis
description: Découvrez comment connecter Amazon Kinesis à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 13%

---

# Source [!DNL Amazon Kinesis]

>[!IMPORTANT]
>
>- La source [!DNL Amazon Kinesis] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time CDP Ultimate.
>
>- Vous pouvez désormais utiliser la source [!DNL Amazon Kinesis] lors de l’exécution de Adobe Experience Platform sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).


Adobe Experience Platform fournit une connectivité native aux fournisseurs de cloud tels qu’AWS, [!DNL Google Cloud Platform] et [!DNL Azure]. Vous pouvez importer vos données de ces systèmes dans [!DNL Experience Platform].

Les sources de stockage dans le cloud peuvent introduire vos propres données dans [!DNL Experience Platform] sans avoir à les télécharger, les formater ou les transférer. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. [!DNL Experience Platform] vous permet d’importer des données de [!DNL Amazon Kinesis] en temps réel.

>[!NOTE]
>
>Le facteur d’échelle de [!DNL Kinesis] doit être augmenté si vous devez ingérer des données à volume élevé. Actuellement, le volume maximal de données que vous pouvez importer depuis votre compte [!DNL Kinesis] vers Experience Platform est de 4 000 enregistrements par seconde. Pour effectuer une mise à l’échelle et ingérer des données à volume plus élevé, contactez votre représentant Adobe.

## Conditions préalables

La section suivante fournit des informations supplémentaires sur la configuration préalable requise avant de pouvoir créer une connexion source [!DNL Kinesis].

### Configurer la politique d’accès

Un flux de [!DNL Kinesis] nécessite les autorisations suivantes pour créer une connexion source :

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Ces autorisations sont organisées via la console [!DNL Kinesis] et sont vérifiées par Experience Platform une fois que vous avez saisi vos informations d’identification et sélectionné votre flux de données.

L’exemple ci-dessous affiche les droits d’accès minimum requis pour créer une connexion source [!DNL Kinesis].

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
| `kinesis:GetRecords` | Action requise pour obtenir des enregistrements à partir d&#39;un décalage ou d&#39;un identifiant de partition spécifique. |
| `kinesis:DescribeStream` | Une action qui renvoie des informations concernant le flux, y compris la carte des partitions, nécessaire pour générer un identifiant de partition. |
| `kinesis:ListStreams` | Action requise pour répertorier les flux disponibles que vous pouvez sélectionner dans l’interface utilisateur. |

Pour plus d’informations sur le contrôle de l’accès pour les flux de données [!DNL Kinesis], consultez le [[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html) suivant.

### Configurer le type d’itérateur

[!DNL Kinesis] prend en charge les types d’itérateur suivants pour vous permettre de spécifier l’ordre de lecture de vos données :

| Type d’itérateur | Description |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Les données sont lues à partir d&#39;une position identifiée par un numéro de séquence spécifique. |
| `AFTER_SEQUENCE_NUMBER` | Les données sont lues à partir d&#39;une position identifiée par un numéro de séquence spécifique. |
| `AT_TIMESTAMP` | Les données sont lues à partir d’une position identifiée par un horodatage spécifique. |
| `TRIM_HORIZON` | Les données sont lues à partir de l’enregistrement de données le plus ancien. |
| `LATEST` | Les données sont lues à partir de l’enregistrement de données le plus récent. |

Actuellement, une source d’interface utilisateur [!DNL Kinesis] ne prend en charge que les `TRIM_HORIZON`, tandis que l’API prend en charge les modes `TRIM_HORIZON` et `LATEST` comme modes d’obtention de données. La valeur d’itérateur par défaut utilisée par Experience Platform pour la source de [!DNL Kinesis] est `TRIM_HORIZON`.

Pour plus d’informations sur les types d’itérateur, consultez le [[!DNL Kinesis] document](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax) suivant.

## Connexion de [!DNL Amazon Kinesis] à [!DNL Experience Platform]

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Amazon Kinesis] à [!DNL Experience Platform] à l’aide d’API ou de l’interface utilisateur :

### Utiliser les API

- [Créer une connexion source Amazon Kinesis à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Collecter des données en continu à l’aide de l’API Flow Service](../../tutorials/api/collect/streaming.md)

### Utiliser l’interface utilisateur

- [Créer une connexion source Amazon Kinesis dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configurer un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
