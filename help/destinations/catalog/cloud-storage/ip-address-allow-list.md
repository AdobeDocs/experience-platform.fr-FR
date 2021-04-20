---
keywords: Adresse IP, plage d’adresses IP, destinations de liste autorisée, liste autorisée
title: 'LISTE AUTORISÉE d’adresses IP pour les destinations d’enregistrement cloud '
type: Documentation
description: Cette page fournit des plages d'adresses IP que vous pouvez ajouter à votre liste autorisée, afin d'exporter en toute sécurité des données de l'Experience Platform vers votre serveur SFTP, Amazon S3 ou votre enregistrement Azure Blob.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
translation-type: tm+mt
source-git-commit: ac62ebcc7b00a96f718a3c39725bcf21ce3d56cf
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# LISTE AUTORISÉE d&#39;adresse IP pour les destinations d&#39;enregistrement cloud {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe vous recommande de mettre cette page en signet et de la consulter de nouveau tous les trois mois afin de rechercher les adresses IP les plus récentes. Adobe ne fournit pas de notification sur les nouvelles plages d’adresses IP.
> * Bien que l’Adobe prenne en charge les exportations de données vers les serveurs SFTP, les emplacements d’enregistrement de cloud recommandés pour exporter les données sont [!DNL Amazon S3] et [!DNL Azure Blob].


## Présentation {#overview}

Cette page fournit des plages d&#39;adresses IP que vous pouvez ajouter à votre liste autorisée, pour exporter en toute sécurité des données de l&#39;Experience Platform vers votre enregistrement [serveur SFTP](./sftp.md), [Amazon S3](./amazon-s3.md) ou [Blob Azure](./azure-blob.md).

Vous pouvez définir des contrôles d&#39;accès réseau via votre pare-feu réseau. En spécifiant la plage d’adresses IP appropriée, vous pouvez autoriser le trafic pour le service de transfert de données.

Adobe vous recommande d’ajouter les plages d’adresses IP suivantes à une liste autorisée avant d’utiliser les connexions de destination d’enregistrement cloud. Si vous n’ajoutez pas votre plage d’adresses IP spécifique à votre région à votre liste autorisée, des erreurs ou des performances risquent d’apparaître lors de l’utilisation des connexions de destination d’enregistrement cloud.

## Obligatoire pour tous les clients

* `52.247.108.70`

## Clients américains

* `52.252.71.64/29`

## Clients EMEA

* `51.137.8.208/29`

## Clients APAC

* `20.53.201.168/29`
