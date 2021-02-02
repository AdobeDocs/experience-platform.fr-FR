---
keywords: Experience Platform ; accueil ; sujets populaires ; concentrateurs de Événement Azure ; concentrateurs de événements azurés ; concentrateurs de Événements ; concentrateurs de événements
solution: Experience Platform
title: Connecteur de concentrateurs de Événement Azure
topic: overview
description: La documentation ci-dessous fournit des informations sur la façon de connecter les concentrateurs de Événement Azure à la plate-forme à l'aide d'API ou de l'interface utilisateur.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 1%

---


# (bêta) Connecteur Azure Événement Hubs

>[!NOTE]
>
>Le connecteur Azure Événement Hubs est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../home.md#terms-and-conditions).

Adobe Experience Platform fournit une connectivité native pour les fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform] et [!DNL Azure]. Vous pouvez importer vos données de ces systèmes dans [!DNL Platform].

Les sources d’enregistrement Cloud peuvent importer vos propres données dans [!DNL Platform] sans avoir à télécharger, mettre en forme ou télécharger. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. [!DNL Platform] vous permet d’importer des données  [!DNL Azure Event Hubs] en temps réel.

## LISTE AUTORISÉE d&#39;adresse IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas d’adresses IP spécifiques à votre région à votre liste autorisée, des erreurs ou des performances risquent d’apparaître lors de l’utilisation de sources. Pour plus d&#39;informations, consultez la page [liste autorisée d&#39;adresse IP](../../ip-address-allow-list.md).

## Connecter [!DNL Azure Event Hubs] à [!DNL Platform]

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Azure Event Hubs] à [!DNL Platform] à l&#39;aide d&#39;API ou de l&#39;interface utilisateur :

### Utilisation des API

- [Création d&#39;un connecteur Azure Événement Hubs à l&#39;aide de l&#39;API Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Collecte de données en flux continu à l’aide de l’API du service de flux](../../tutorials/api/collect/streaming.md)

### Utilisation de l’interface utilisateur

- [Création d&#39;un connecteur source Azure Événement Hubs dans l&#39;interface utilisateur](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configuration d’un flux de données pour un connecteur d’enregistrement cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)