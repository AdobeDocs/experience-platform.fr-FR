---
keywords: Adresses IP, plage d’adresses IP, destinations de liste autorisée placer sur la liste autorisée place sur la liste autorisée,,
title: Liste autorisée d’adresses IP pour les destinations en flux continu
type: Documentation
description: Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre liste autorisée de données pour exporter en toute sécurité des données d’Experience Platform vers votre point d’entrée de l’API HTTP REST ou votre instance Amazon Kinesis.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: 6d59d0555dda124acfd16483e11c2899ff5c846e
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 5%

---


# PLACE SUR LA LISTE AUTORISÉE d’adresse IP pour les destinations basées sur les API de streaming {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe vous recommande d’ajouter un signet à cette page et de la consulter tous les trois mois pour rechercher les dernières adresses IP. Adobe ne fournit pas de notification des nouvelles plages d’adresses IP.

## Vue d’ensemble {#overview}

Les plages d’adresses IP documentées sur cette page s’appliquent aux destinations suivantes :

* [Destinations d’entreprise avancées](../../destination-types.md#advanced-enterprise-destinations) : [destination d’API HTTP](./http-destination.md) et [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [Destinations d’exportation d’audiences en flux continu](../../destination-types.md#streaming-destinations) telles que [Audience en temps réel Pega CDH](/help/destinations/catalog/personalization/pega-v2.md), intégrations basées sur les API avec [Salesforce Marketing Cloud](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) et [Oracle Eloqua](/help/destinations/catalog/email-marketing/oracle-eloqua-api.md)
* Destinations publiques ou privées créées via [Destination SDK](../../destination-sdk/getting-started.md)

>[!IMPORTANT]
>
>Les plages d’adresses IP documentées sur cette page ne sont *pas* prises en charge pour les destinations [!DNL Azure Event Hubs] et les destinations basées sur les API de streaming hébergées sur Microsoft Azure.


Le trafic sortant d’Experience Platform vers ces destinations passe toujours par les adresses IP répertoriées sur cette page.

Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre place sur la liste autorisée pour exporter en toute sécurité des données d’Experience Platform vers les destinations répertoriées ci-dessus. Cette fonctionnalité est particulièrement utile si votre point d’entrée HTTP se trouve derrière un pare-feu d’entreprise ou si les normes de sécurité et de conformité de votre entreprise exigent qu’une liste de plages d’adresses IP soit placée sur la liste autorisée.

Vous pouvez définir des contrôles d’accès réseau via votre pare-feu réseau. En spécifiant la plage d’adresses IP appropriée, vous pouvez autoriser le trafic pour le service de transfert de données.

## Quand placer sur la liste autorisée les adresses IP sur cette page {#when-to-allowlist}

Si votre politique d’organisation exige que vous ajoutiez des adresses IP pour le trafic entrant, vous devez ajouter les plages d’adresses IP des catégories suivantes à votre placer sur la liste autorisée place sur la liste autorisée avant d’utiliser les destinations mentionnées ci-dessus sur cette page :

1. Toutes les [ adresses IP globales ](#global)
2. Outre les adresses IP globales, ajoutez les adresses IP correspondant à la région dans laquelle vous avez reçu les privilèges d’accès, à partir de la liste située plus bas sur la page. Si vous n’ajoutez pas votre plage d’adresses IP spécifique à une région à votre place sur la liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de ces destinations de diffusion en streaming.

## Adresses IP globales {#global}

* `3.209.222.108`
* `3.211.230.204`
* `35.169.227.49`
* `66.117.18.133`
* `66.117.18.134`
* `66.117.18.135`

Outre ces adresses IP globales, vous devez également placer sur la liste autorisée les adresses IP de la région dans laquelle votre organisation est approvisionnée à partir de la liste ci-dessous.

## VA7 : clients des États-Unis et des Amériques {#us-americas}

* `4.152.211.251`
* `20.22.83.112`
* `20.186.185.181`
* `20.186.185.227`
* `20.186.185.239`
* `40.70.154.136/29`
* `52.254.105.192/28`
* `52.254.106.0/28`
* `52.254.106.144/28`
* `52.254.106.160/28`
* `52.254.106.176/28`
* `52.254.106.192/28`
* `52.254.106.208/28`
* `52.254.106.224/28`
* `52.254.106.240/28`
* `52.254.107.0/28`
* `52.254.107.16/28`
* `52.254.107.32/28`
* `52.254.107.64/28`
* `52.254.107.80/28`
* `52.254.107.128/28`
* `52.254.107.144/28`

## VA6 : clients des États-Unis et des Amériques utilisant AWS {#aws}

La plage d’adresses IP ci-dessous s’applique aux clients Experience Platform s’exécutant sur Amazon Web Services (AWS). Pour plus d’informations, consultez la [Présentation d’Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

* `3.209.222.108`
* `3.211.230.204`
* `35.169.227.49`
* `66.117.18.133`
* `66.117.18.134`
* `66.117.18.135`

## NLD2 : clients EMEA {#emea}

* `20.50.23.153`
* `20.101.246.9`
* `40.74.3.176/28`
* `40.74.4.144/28`
* `40.74.4.160/28`
* `40.74.4.176/28`
* `40.74.5.128/28`
* `40.74.6.80/28`
* `40.74.6.96/28`
* `40.74.6.112/28`
* `40.74.6.128/28`
* `40.74.6.144/28`
* `40.74.7.128/28`
* `40.74.7.144/28`
* `40.74.7.160/28`
* `40.74.7.176/28`
* `40.74.7.192/28`
* `40.74.7.208/28`
* `51.105.144.1`
* `51.105.144.81`
* `51.124.70.4`
* `51.144.184.248/29`
* `52.142.236.87`
* `108.141.12.47`

## AUS5 : clients APAC {#apac}

* `20.40.188.166`
* `20.40.188.194`
* `20.40.188.227`
* `20.40.191.96/28`
* `20.40.191.224/28`
* `20.40.191.240/28`
* `20.43.104.0/28`
* `20.43.104.16/28`
* `20.43.104.32/28`
* `20.43.104.48/28`
* `20.43.104.64/28`
* `20.43.104.80/28`
* `20.43.104.96/28`
* `20.43.104.112/28`
* `20.43.104.128/28`
* `20.43.104.144/28`
* `20.43.104.160/28`
* `20.43.104.176/28`
* `20.43.104.192/28`
* `20.43.105.0/28`
* `20.43.105.16/28`
* `20.43.105.32/28`
* `20.43.105.48/28`
* `20.227.35.177`
* `20.53.206.128`

## CAN2 : clients du Canada {#can}

* `20.104.46.64/28`
* `20.104.46.80/28`
* `20.104.46.128/28`
* `20.104.46.160/28`
* `20.116.145.94`
* `20.116.147.168`
* `20.200.70.192/28`
* `20.200.70.208/28`
* `20.200.70.224/28`
* `20.200.70.240/28`
* `20.200.71.0/28`
* `20.200.71.16/28`
* `20.200.71.32/28`
* `20.200.71.48/28`
* `20.200.71.64/28`
* `20.200.71.80/28`
* `20.200.71.96/28`
* `20.200.71.112/28`
* `20.200.71.128/28`
* `20.200.71.144/28`
* `20.200.71.160/28`
* `20.200.71.176/28`
* `20.200.93.180`
* `20.200.94.83`
* `20.200.94.116`

## GBR9 : clients de la Grande-Bretagne {#gbr}

* `20.26.64.112/28`
* `20.26.64.208/28`
* `20.26.64.240/28`
* `20.26.65.0/28`
* `20.26.128.247`
* `20.26.130.226`
* `20.26.131.71`
* `20.108.119.100`
* `20.108.202.84`
* `20.254.1.128/28`
* `20.254.2.32/28`
* `20.254.2.128/28`
* `20.254.2.208/28`
* `20.254.3.32/28`
* `20.254.3.48/28`
* `20.254.3.112/28`
* `20.254.3.144/28`
* `20.254.3.176/28`
* `20.254.3.192/28`
* `20.254.3.240/28`
* `20.254.4.0/28`
* `20.254.4.16/28`
* `20.254.4.32/28`
* `20.254.4.64/28`
* `20.254.4.96/28`

## IND2 : clients de l’Inde {#india}

* `4.188.4.11`
* `4.188.4.99`
* `4.188.4.138`
* `4.188.4.154`
* `4.188.4.167`
* `4.213.40.145`
* `4.224.74.0/28`
* `4.224.74.64/28`
* `4.224.74.80/28`
* `4.224.74.96/28`
* `20.244.74.112/28`
* `20.244.77.0/28`
* `20.244.77.16/28`
* `20.244.77.160/28`
* `20.244.77.208/28`
* `20.244.78.0/28`
* `20.244.78.208/28`
* `20.244.79.0/28`
* `20.244.79.16/28`
* `20.244.79.48/28`
* `20.244.79.80/28`
* `20.244.79.128/28`
* `20.244.79.144/28`
* `20.244.79.192/28`
* `20.244.79.208/28`
* `20.244.79.224/28`

