---
title: Destinations SFTP de liste autorisée d’adresses IP
type: Documentation
description: Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre liste autorisée afin d’exporter en toute sécurité des données d’Experience Platform vers votre serveur SFTP.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 3d870975593313062d796601f0e19a0a3aec7854
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 17%

---

# Liste autorisée d’adresses IP pour les destinations SFTP {#ip-address-allow-list-sftp}

>[!IMPORTANT]
>
> * Adobe vous recommande de mettre cette page en signet et de la revoir tous les trois mois pour rechercher les dernières adresses IP. Adobe ne fournit pas de notification pour les nouvelles plages d’adresses IP.
> * Bien qu’Adobe prenne en charge les exportations de données vers les serveurs SFTP, les emplacements de stockage dans le cloud recommandés pour exporter des données sont les suivants : [!DNL Amazon S3] et [!DNL Azure Blob].

## Vue d’ensemble {#overview}

Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre liste autorisée pour exporter en toute sécurité des données de l’Experience Platform vers votre [Serveur SFTP](./sftp.md).

Vous pouvez définir des contrôles d’accès réseau via votre pare-feu réseau. En spécifiant la plage d’adresses IP appropriée, vous pouvez autoriser le trafic pour le service de transfert de données.

Adobe recommande d’ajouter les plages d’adresses IP suivantes à une liste autorisée avant d’utiliser les connexions de destination de stockage dans le cloud. Si vous n’ajoutez pas votre plage d’adresses IP spécifique à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation des connexions de destination de stockage dans le cloud.

## Requis pour tous les clients

* `52.247.108.70`

## Clients américains

* `52.252.71.64/29`

## Clients EMEA

* `51.137.8.208/29`

## Clients APAC

* `20.53.201.168/29`
