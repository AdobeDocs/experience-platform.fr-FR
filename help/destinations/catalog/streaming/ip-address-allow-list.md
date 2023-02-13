---
keywords: Adresse IP, plage IP, destinations de liste autorisée, liste autorisée, liste autorisée des destinations de diffusion en continu
title: Liste autorisée d’adresses IP pour les destinations en flux continu
type: Documentation
description: Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre liste autorisée afin d’exporter en toute sécurité des données d’Experience Platform vers votre point de terminaison API REST HTTP, Amazon Kinesis ou votre instance Azure Event Hubs.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: 4d71e246c8ce92cbdae4d248568cf32ab44ac82a
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 15%

---

# Liste autorisée d’adresses IP pour les destinations en flux continu {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe vous recommande de mettre cette page en signet et de la revoir tous les trois mois pour rechercher les dernières adresses IP. Adobe ne fournit pas de notification pour les nouvelles plages d’adresses IP.
> * La liste des adresses IP documentée ici *ne fait pas* s’appliquent à toutes les destinations que vous créez à l’aide de [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md).


## Présentation {#overview}

Les plages d’adresses IP documentées ici s’appliquent aux destinations suivantes :

* [Destination de l’API HTTP](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

Le trafic sortant de l’Experience Platform vers ces destinations passe toujours par les adresses IP répertoriées sur cette page.

Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre liste autorisée pour exporter en toute sécurité des données d’Experience Platform vers votre point d’entrée HTTP, [!DNL Amazon Kinesis]ou [!DNL Azure Event Hubs] instance. Cette fonctionnalité est particulièrement utile si votre point de terminaison HTTP se trouve derrière un pare-feu d’entreprise ou si les normes de sécurité et de conformité de votre entreprise nécessitent qu’une liste de plages d’adresses IP soit placée sur la liste autorisée.

Vous pouvez définir des contrôles d’accès réseau via votre pare-feu réseau. En spécifiant la plage d’adresses IP appropriée, vous pouvez autoriser le trafic pour le service de transfert de données.

Adobe vous recommande d’ajouter les plages d’adresses IP suivantes à une liste autorisée avant de travailler avec les destinations mentionnées ci-dessus sur cette page. Si vous ne parvenez pas à ajouter votre plage d’adresses IP spécifique à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation de ces destinations de diffusion en continu.

## VA7 : Clients américains et américains {#us-americas}

`20.186.185.239`
`40.70.154.136/29`
`52.254.106.160/28`
`52.254.106.176/28`
`52.254.105.192/28`
`20.186.185.181`
`52.254.107.64/28`
`52.254.107.80/28`
`52.254.106.144/28`
`52.254.106.0/28`
`52.254.107.16/28`
`52.254.107.32/28`
`52.254.106.224/28`
`20.186.185.227`
`52.254.106.192/28`
`52.254.107.128/28`
`52.254.106.208/28`
`52.254.106.240/28`
`52.254.107.0/28`
`52.254.107.144/28`

## NLD2 : Clients EMEA {#emea}

`40.74.4.160/28`
`40.74.6.128/28`
`40.74.7.128/28`
`40.74.4.176/28`
`51.144.184.248/29`
`40.74.7.208/28`
`52.142.236.87`
`20.50.23.153`
`20.101.246.9`
`40.74.4.144/28`
`40.74.7.160/28`
`40.74.3.176/28`
`40.74.6.144/28`
`40.74.6.80/28`
`40.74.5.128/28`
`40.74.7.144/28`
`40.74.7.176/28`
`40.74.6.96/28`
`40.74.6.112/28`
`51.105.144.1`
`40.74.7.192/28`
`51.105.144.81`
`51.124.70.4`

## AUS5 : Clients APAC {#apac}

`20.43.104.80/28`
`20.43.104.16/28`
`20.43.104.128/28`
`20.40.188.166`
`20.40.191.224/28`
`20.43.104.176/28`
`20.43.104.0/28`
`20.43.105.0/28`
`20.43.105.48/28`
`20.40.191.240/28`
`20.43.104.192/28`
`20.40.188.227`
`20.40.188.194`
`20.43.104.144/28`
`20.43.104.160/28`
`20.43.104.96/28`
`20.43.105.32/28`
`20.43.104.112/28`
`20.43.105.16/28`
`20.43.104.48/28`
`20.40.191.96/28`
`20.43.104.32/28`
`20.43.104.64/28`