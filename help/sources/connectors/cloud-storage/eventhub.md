---
keywords: Experience Platform;accueil;rubriques les plus consultées;centres d’événements Azure;centres d’événements Azure;centres d’événements;centres d’événements
solution: Experience Platform
title: Présentation du connecteur source Azure Event Hub
topic-legacy: overview
description: Découvrez comment connecter Azure Event Hubs à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: cda9ca9c560b1af2147c00ea4e89dff09b7428ba
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 7%

---


# [!DNL Azure Event Hubs] connector

Adobe Experience Platform fournit une connectivité native pour les fournisseurs cloud tels qu’AWS, [!DNL Google Cloud Platform], et [!DNL Azure]. Vous pouvez importer vos données de ces systèmes dans Platform.

Les sources de stockage dans le cloud peuvent introduire vos propres données dans Platform sans avoir à les télécharger, les formater ou les transférer. Les données ingérées peuvent être formatées sous la forme XDM JSON, XDM Parquet ou délimitées. Chaque étape du processus est intégrée dans le workflow Sources . Platform vous permet d’importer des données depuis [!DNL Event Hubs] en temps réel.

## Utiliser un réseau virtuel pour se connecter à [!DNL Event Hubs] vers Platform

Vous pouvez configurer un réseau virtuel pour vous connecter. [!DNL Event Hubs] à Platform lorsque vos mesures de pare-feu sont activées. Pour configurer un réseau virtuel, procédez comme suit : [[!DNL Event Hubs] document d’ensemble de règles réseau](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) puis sélectionnez **Essayez** dans le panneau API REST. Ensuite, authentifiez votre [!DNL Azure] à l’aide de vos informations d’identification, puis sélectionnez [!DNL Event Hubs] espace de noms, groupe de ressources et abonnement que vous souhaitez apporter à Platform.

Une fois la configuration effectuée, mettez à jour la variable **corps de requête** avec le JSON correspondant à votre région réseau, dans la liste ci-dessous :

>[!TIP]
>
>Vous devez sauvegarder vos règles de filtrage IP de pare-feu existantes, car elles seront supprimées après cet appel.

### VA7 : Amérique du Nord

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

### NLD2 : Europe

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### AUS5 : Australie

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5_network_10_21_116_0_22/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

Voir ce qui suit : [[!DNL Event Hubs] document](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set) pour plus d’informations sur les ensembles de règles réseau.

## Connexion [!DNL Event Hubs] vers Platform

La documentation ci-dessous fournit des informations sur la connexion. [!DNL Event Hubs] vers Platform à l’aide d’API ou de l’interface utilisateur :

### Utilisation des API

- [Création d’une connexion source Event Hubs à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Collecte de données en continu à l’aide de l’API Flow Service](../../tutorials/api/collect/streaming.md)

### Utilisation de l’interface utilisateur

- [Création d’une connexion source aux centres d’événements dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configuration d’un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
