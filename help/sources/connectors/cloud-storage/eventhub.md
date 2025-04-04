---
title: Présentation Du Connecteur Source Azure Event Hubs
description: Découvrez comment connecter Azure Event Hubs à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 9%

---

# Source [!DNL Azure Event Hubs]

>[!IMPORTANT]
>
>* La source [!DNL Azure Event Hubs] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time CDP Ultimate.
>
>* Vous pouvez désormais utiliser la source [!DNL Azure Event Hubs] lors de l’exécution de Adobe Experience Platform sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).

Adobe Experience Platform fournit une connectivité native aux fournisseurs de cloud tels qu’AWS, [!DNL Google Cloud Platform] et [!DNL Azure]. Vous pouvez importer vos données de ces systèmes dans Experience Platform.

Les sources de stockage dans le cloud peuvent importer vos propres données dans Experience Platform sans avoir à les télécharger, les formater ou les charger. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. Experience Platform vous permet d’importer des données de [!DNL Event Hubs] en temps réel.

## Mise à l’échelle avec [!DNL Event Hubs]

Le facteur d’échelle de votre instance [!DNL Event Hubs] doit être augmenté si vous devez ingérer des données de volume élevé, augmenter le parallélisme ou augmenter la vitesse de l’ingestion sur Experience Platform.

### Entrée de données à volume plus élevé

Actuellement, le volume maximal de données que vous pouvez importer depuis votre compte [!DNL Event Hubs] vers Experience Platform est de 2 000 enregistrements par seconde. Pour effectuer une mise à l’échelle et ingérer des données à volume plus élevé, contactez votre représentant Adobe.

### Augmentation du parallélisme sur [!DNL Event Hubs] et Experience Platform

Le parallélisme désigne l&#39;exécution simultanée des mêmes tâches sur plusieurs unités de traitement afin d&#39;augmenter la vitesse et les performances. Vous pouvez augmenter le parallélisme du côté [!DNL Event Hubs] en augmentant la partition ou en acquérant davantage d’unités de traitement pour votre compte [!DNL Event Hubs]. Voir ce [[!DNL Event Hubs] document sur la mise à l’échelle](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) pour plus d’informations.

Pour augmenter le taux d’ingestion du côté d’Experience Platform, Experience Platform doit augmenter le nombre de tâches dans le connecteur source à lire à partir de vos partitions [!DNL Event Hubs]. Une fois que le parallélisme a augmenté du côté [!DNL Event Hubs], contactez votre représentant Adobe pour dimensionner les tâches Experience Platform en fonction de votre nouvelle partition. Actuellement, ce processus n’est pas automatisé.

## Utiliser un réseau virtuel pour se connecter à [!DNL Event Hubs] à Experience Platform

Vous pouvez configurer un réseau virtuel pour [!DNL Event Hubs] connecter à Experience Platform tout en activant vos mesures de pare-feu. Pour configurer un réseau virtuel, accédez à ce [[!DNL Event Hubs] document sur l’ensemble de règles réseau](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) et procédez comme suit :

* Sélectionnez **Essayer** dans le panneau API REST ;
* Authentifiez votre compte [!DNL Azure] à l’aide de vos informations d’identification dans le même navigateur ;
* Sélectionnez l’espace de noms de [!DNL Event Hubs], le groupe de ressources et l’abonnement que vous souhaitez importer dans Experience Platform, puis sélectionnez **EXÉCUTER**;
* Dans le corps JSON qui s’affiche, ajoutez le sous-réseau Experience Platform suivant sous `virtualNetworkRules` dans `properties` :


>[!IMPORTANT]
>
>Vous devez effectuer une sauvegarde du corps JSON que vous recevez avant de mettre à jour `virtualNetworkRules` avec le sous-réseau Experience Platform, car il contient vos règles de filtrage IP existantes. Sinon, les règles seront supprimées après l’appel.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Consultez la liste ci-dessous pour connaître les différentes régions des sous-réseaux Experience Platform :

### VA7 : Amérique du Nord

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### NLD2 : Europe

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2-vnet/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### AUS5 : Australie

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5-vnet/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

Consultez le [[!DNL Event Hubs] document](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) suivant pour plus d’informations sur les ensembles de règles réseau.

## Connexion de [!DNL Event Hubs] à Experience Platform

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Event Hubs] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

### Utiliser les API

* [Créer une connexion source Event Hubs à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Collecter des données en continu à l’aide de l’API Flow Service](../../tutorials/api/collect/streaming.md)

### Utiliser l’interface utilisateur

* [Créer une connexion source Event Hubs dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Configurer un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
