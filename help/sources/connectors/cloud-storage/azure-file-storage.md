---
keywords: Experience Platform;home;popular topics;Azure File Storage;azure file storage
solution: Experience Platform
title: Connecteur d'Enregistrement de fichiers Azure
topic: overview
description: La documentation ci-dessous fournit des informations sur la façon de connecter Azure File Enregistrement à Platform à l'aide d'API ou de l'interface utilisateur.
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# (Bêta) Connecteur d&#39;Enregistrement de fichier Azure

>[!NOTE]
>
>Le connecteur d&#39;Enregistrement de fichiers Azure est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../home.md#terms-and-conditions) sources.

Adobe Experience Platform fournit une connectivité native aux fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform]et [!DNL Azure]vous permet d’importer vos données à partir de ces systèmes.

Cloud storage sources can bring your own data into [!DNL Platform] without the need to download, format, or upload. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. [!DNL Platform] vous permet d’importer des données à partir de [!DNL Azure File Storage] lots.

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

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Azure File Storage] à [!DNL Platform] l’aide des API ou de l’interface utilisateur :

## Se connecter [!DNL Azure File Storage] à [!DNL Platform] l’aide des API

- [Création d&#39;un connecteur d&#39;Enregistrement de fichiers Azure à l&#39;aide de l&#39;API Flow Service](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.](../../tutorials/api/explore/cloud-storage.md)
- [Collecte de données d’enregistrement Cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

## Se connecter [!DNL Azure File Storage] à [!DNL Platform] l’aide de l’interface utilisateur

- [Création d&#39;un connecteur source d&#39;Enregistrement de fichiers Azure dans l&#39;interface utilisateur](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [Configuration d’un flux de données pour un connecteur d’enregistrement cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)