---
keywords: Experience Platform;home;popular topics;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Connecteur de concentrateurs de Événement Azure
topic: overview
description: La documentation ci-dessous fournit des informations sur la façon de connecter les concentrateurs de Événement Azure à la plate-forme à l'aide d'API ou de l'interface utilisateur.
translation-type: tm+mt
source-git-commit: 7b92327cfeb2410baf313dd650f68cfeb6db36e6
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 1%

---


# (bêta) Connecteur Azure Événement Hubs

>[!NOTE]
>
>Le connecteur Azure Événement Hubs est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../home.md#terms-and-conditions) sources.

Adobe Experience Platform fournit une connectivité native aux fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform]et [!DNL Azure]. Vous pouvez importer vos données de ces systèmes dans [!DNL Platform].

Cloud storage sources can bring your own data into [!DNL Platform] without the need to download, format, or upload. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. [!DNL Platform] vous permet d’importer des données [!DNL Azure Event Hubs] en temps réel.

## LISTE AUTORISÉE d&#39;adresse IP

Les adresses IP suivantes doivent être ajoutées à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas d’adresses IP spécifiques à votre région à votre liste autorisée, des erreurs ou des performances risquent d’apparaître lors de l’utilisation de sources.

### Région est-américaine

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Région de l&#39;Europe occidentale

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australie-Est

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

## Se connecter [!DNL Azure Event Hubs] à [!DNL Platform]

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Azure Event Hubs] à [!DNL Platform] l’aide des API ou de l’interface utilisateur :

### Utilisation des API

- [Création d&#39;un connecteur Azure Événement Hubs à l&#39;aide de l&#39;API Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.](../../tutorials/api/explore/cloud-storage.md)
- [Collecte de données d’enregistrement Cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Création d&#39;un connecteur source Azure Événement Hubs dans l&#39;interface utilisateur](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configuration d’un flux de données pour un connecteur d’enregistrement cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)