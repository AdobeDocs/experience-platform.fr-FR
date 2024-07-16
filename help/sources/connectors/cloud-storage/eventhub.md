---
title: Présentation du connecteur Source des centres d’événements Azure
description: Découvrez comment connecter Azure Event Hubs à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 12ddf87d594b7e25a0356cd419e990b262c1734e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 20%

---

# Source [!DNL Azure Event Hubs]

>[!IMPORTANT]
>
>La source [!DNL Azure Event Hubs] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Adobe Experience Platform fournit une connectivité native pour les fournisseurs cloud tels qu’AWS, [!DNL Google Cloud Platform] et [!DNL Azure]. Vous pouvez importer vos données de ces systèmes dans Platform.

Les sources de stockage dans le cloud peuvent introduire vos propres données dans Platform sans avoir à les télécharger, les formater ou les transférer. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. Platform vous permet d’importer des données depuis [!DNL Event Hubs] en temps réel.

## Mise à l’échelle avec [!DNL Event Hubs]

Le facteur d’échelle de votre instance [!DNL Event Hubs] doit être augmenté si vous devez ingérer des données à volume élevé, augmenter le parallélisme ou augmenter la vitesse de la plateforme d’ingestion.

### Entrer des données à volume supérieur

Actuellement, le volume maximal de données que vous pouvez importer de votre compte [!DNL Event Hubs] vers Platform est de 2 000 enregistrements par seconde. Pour augmenter et ingérer des données à volume supérieur, contactez votre représentant Adobe.

### Augmentation du parallélisme sur [!DNL Event Hubs] et Platform

Le parallèle fait référence à l’exécution simultanée des mêmes tâches sur plusieurs unités de traitement afin d’augmenter la vitesse et les performances. Vous pouvez augmenter le parallélisme du côté [!DNL Event Hubs] en augmentant la partition ou en acquérant plus d’unités de traitement pour votre compte [!DNL Event Hubs]. Pour plus d’informations, consultez ce [[!DNL Event Hubs] document sur la mise à l’échelle](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability).

Pour augmenter la vitesse d’ingestion du côté Platform, Platform doit augmenter le nombre de tâches dans le connecteur source à lire à partir de vos partitions [!DNL Event Hubs]. Une fois que vous avez augmenté le parallélisme du côté [!DNL Event Hubs], contactez votre représentant d’Adobe pour mettre à l’échelle les tâches de Platform en fonction de votre nouvelle partition. Actuellement, ce processus n’est pas automatisé.

## Utilisation d’un réseau virtuel pour se connecter à [!DNL Event Hubs] à Platform

Vous pouvez configurer un réseau virtuel pour connecter [!DNL Event Hubs] à Platform tout en activant vos mesures de pare-feu. Pour configurer un réseau virtuel, accédez à ce [[!DNL Event Hubs] document d’ensemble de règles réseau](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) et procédez comme suit :

* Sélectionnez **Essayer** dans le panneau API REST ;
* Authentifiez votre compte [!DNL Azure] à l’aide de vos informations d’identification dans le même navigateur.
* Sélectionnez l’espace de noms, le groupe de ressources et l’abonnement [!DNL Event Hubs] que vous souhaitez apporter à Platform, puis sélectionnez **RUN** ;
* Dans le corps JSON qui s’affiche, ajoutez le sous-réseau Platform suivant sous `virtualNetworkRules` dans `properties` :


>[!IMPORTANT]
>
>Vous devez effectuer une sauvegarde du corps JSON que vous recevez, avant de mettre à jour `virtualNetworkRules` avec le sous-réseau Platform, car il contient vos règles de filtrage IP existantes. Dans le cas contraire, les règles seront supprimées après l’appel .


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Consultez la liste ci-dessous pour différentes régions des sous-réseaux Platform :

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

Pour plus d’informations sur les ensembles de règles réseau, consultez le [[!DNL Event Hubs] document](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) suivant.

## Connecter [!DNL Event Hubs] à Platform

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Event Hubs] à Platform à l’aide d’API ou de l’interface utilisateur :

### Utiliser les API

* [Création d’une connexion source Event Hubs à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Collecter des données en continu à l’aide de l’API Flow Service](../../tutorials/api/collect/streaming.md)

### Utiliser l’interface utilisateur

* [Création d’une connexion source aux centres d’événements dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Configurer un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
