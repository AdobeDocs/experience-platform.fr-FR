---
title: LISTE AUTORISÉE d’adresses IP pour les destinations de stockage dans le cloud basées sur des fichiers
type: Documentation
description: Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre liste autorisée pour exporter en toute sécurité des données d’Experience Platform vers des destinations d’espace de stockage.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 4ae7ff58d02b46f1b213bd382d3e98b3f63819e8
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 5%

---

# PLACE SUR LA LISTE AUTORISÉE d’adresse IP pour les destinations de stockage dans le cloud basées sur des fichiers {#ip-address-allow-list-cloud-storage}

>[!IMPORTANT]
>
> * Adobe vous recommande d’ajouter un signet à cette page et de la consulter tous les trois mois pour rechercher les dernières adresses IP. Adobe ne fournit pas de notification des nouvelles plages d’adresses IP.
> * Bien qu’Adobe prenne en charge les exportations de données vers des serveurs SFTP, les emplacements de stockage dans le cloud recommandés pour exporter les données sont [!DNL Amazon S3] et [!DNL Azure Blob].

## Applicabilité {#applicability}

Les informations sur la plage d’adresses IP de cette page s’appliquent aux connecteurs de stockage dans le cloud basés sur des fichiers suivants du catalogue des destinations :

* [[!UICONTROL Amazon S3]](./amazon-s3.md)
* [[!UICONTROL Google Cloud Storage]](google-cloud-storage.md)
* [SFTP](./sftp.md)

>[!IMPORTANT]
>
>Les plages d’adresses IP documentées sur cette page ne sont *pas* prises en charge pour les destinations d’espace de stockage dans le cloud basées sur des fichiers suivantes : [!UICONTROL Azure Blob], [!UICONTROL Azure Data Lake Storage Gen2], [!UICONTROL Data Landing Zone] et serveurs SFTP hébergés sur Microsoft Azure.

## Vue d’ensemble {#overview}

Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre place sur la liste autorisée pour exporter en toute sécurité des données d’Experience Platform vers plusieurs destinations d’espace de stockage.

Vous pouvez définir des contrôles d’accès réseau via votre pare-feu réseau. En spécifiant la plage d’adresses IP appropriée, vous pouvez autoriser le trafic pour le service de transfert de données.

Adobe vous recommande d’ajouter les plages d’adresses IP suivantes à un place sur la liste autorisée de données avant d’utiliser les connexions de destination de stockage dans le cloud. Si vous n’ajoutez pas votre plage d’adresses IP spécifique à une région à votre place sur la liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation des connexions de destination d’espace de stockage.

## Requis pour tous les clients {#all-customers}

* `52.247.108.70`

## Clients aux États-Unis utilisant AWS {#aws}

La plage d’adresses IP ci-dessous s’applique aux clients Experience Platform s’exécutant sur Amazon Web Services (AWS). Pour plus d’informations, consultez la [Présentation d’Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

>[!NOTE]
>
>Cette plage d’adresses IP n’est pas prise en charge pour les clients s’exécutant sur AWS qui utilisent des destinations basées sur des fichiers pour exporter des données vers Amazon S3.

* `66.117.18.0/24`

## Clients aux États-Unis {#us-customers}

* `52.252.71.64/29`

## Clients au Canada {#canada-customers}

* `20.220.135.16/29`

## Clients EMEA {#emea-customers}

* `51.137.8.208/29`

## Clients au Royaume-Uni {#uk-customers}

* `20.26.133.96/29`

## Clients APAC {#apac-customers}

* `20.53.201.168/29`
