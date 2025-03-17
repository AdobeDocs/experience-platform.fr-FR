---
keywords: Adresses IP, plage d’adresses IP, destinations de liste autorisée placer sur la liste autorisée place sur la liste autorisée,,
title: Liste autorisée d’adresses IP pour les destinations en flux continu
type: Documentation
description: Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre liste autorisée de données pour exporter en toute sécurité des données d’Experience Platform vers votre point d’entrée de l’API HTTP REST, Amazon Kinesis ou votre instance Azure Event Hubs.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: ee4c42a2298c588590b1535524ed8f3dfe13b603
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 9%

---

# Liste autorisée d’adresses IP pour les destinations en flux continu {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe vous recommande d’ajouter un signet à cette page et de la consulter tous les trois mois pour rechercher les dernières adresses IP. Adobe ne fournit pas de notification des nouvelles plages d’adresses IP.
> * La liste des adresses IP documentée ici *ne s’applique pas* aux destinations que vous créez à l’aide de [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md).

## Vue d’ensemble {#overview}

Les plages d’adresses IP documentées ici s’appliquent aux destinations suivantes :

* [Destination de l’API HTTP](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

Le trafic sortant d’Experience Platform vers ces destinations passe toujours par les adresses IP répertoriées sur cette page.

Placer sur la liste autorisée Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre pour exporter en toute sécurité des données d’Experience Platform vers votre point d’entrée HTTP, votre [!DNL Amazon Kinesis] ou votre instance [!DNL Azure Event Hubs]. Cette fonctionnalité est particulièrement utile si votre point d’entrée HTTP se trouve derrière un pare-feu d’entreprise ou si les normes de sécurité et de conformité de votre entreprise exigent qu’une liste de plages d’adresses IP soit placée sur la liste autorisée.

Vous pouvez définir des contrôles d’accès réseau via votre pare-feu réseau. En spécifiant la plage d’adresses IP appropriée, vous pouvez autoriser le trafic pour le service de transfert de données.

Adobe vous recommande d’ajouter les plages d’adresses IP suivantes à un place sur la liste autorisée de données avant d’utiliser les destinations mentionnées ci-dessus sur cette page. Si vous n’ajoutez pas votre plage d’adresses IP spécifique à une région à votre place sur la liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de ces destinations de diffusion en streaming.

## VA7 : clients des États-Unis et des Amériques {#us-americas}

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
`20.22.83.112`
<!-- 
## VA6: US and Americas customers running on AWS {#aws}

The IP range below applies to Experience Platform customers running on Amazon Web Services (AWS). See the [Experience Platform Multi-Cloud overview](../../../landing/multi-cloud.md) for more information.

`66.117.18.0/24` -->

## NLD2 : clients EMEA {#emea}

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
`20.101.233.128`

## AUS5 : clients APAC {#apac}

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
`20.53.206.128`
`20.227.35.177`

## CAN2 : clients du Canada {#can}

`20.104.46.128/28`
`20.104.46.160/28`
`20.104.46.64/28`
`20.104.46.80/28`
`20.116.145.94`
`20.116.147.168`
`20.200.70.192/28`
`20.200.70.208/28`
`20.200.70.224/28`
`20.200.70.240/28`
`20.200.71.0/28`
`20.200.71.112/28`
`20.200.71.128/28`
`20.200.71.144/28`
`20.200.71.16/28`
`20.200.71.160/28`
`20.200.71.176/28`
`20.200.71.32/28`
`20.200.71.48/28`
`20.200.71.64/28`
`20.200.71.80/28`
`20.200.71.96/28`
`20.200.93.180`
`20.200.94.116`
`20.200.94.83`

## GBR9 : clients de la Grande-Bretagne {#gbr}

`20.254.3.48/28`
`20.254.4.0/28`
`20.26.128.247`
`20.254.1.128/28`
`20.254.2.32/28`
`20.26.64.208/28`
`20.254.2.208/28`
`20.254.3.176/28`
`20.254.4.64/28`
`20.254.3.32/28`
`20.254.3.144/28`
`20.26.64.240/28`
`20.254.4.16/28`
`20.254.3.240/28`
`20.26.65.0/28`
`20.254.4.32/28`
`20.254.3.112/28`
`20.254.4.96/28`
`20.108.202.84`
`20.108.119.100`
`20.254.2.128/28`
`20.26.131.71`
`20.26.130.226`
`20.26.64.112/28`
`20.254.3.192/28`