---
title: LISTE AUTORISÉE d’adresses IP pour les destinations de stockage dans le cloud basées sur des fichiers
type: Documentation
description: Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre liste autorisée afin d’exporter en toute sécurité des données d’Experience Platform vers les destinations de stockage dans le cloud.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 1d8ba11b1043fa68bf3c0205e8cecc2de8910234
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 6%

---

# LISTE AUTORISÉE d’adresses IP pour les destinations de stockage dans le cloud basées sur des fichiers {#ip-address-allow-list-cloud-storage}

>[!IMPORTANT]
>
> * Adobe vous recommande de mettre cette page en signet et de la revoir tous les trois mois pour rechercher les dernières adresses IP. Adobe ne fournit pas de notification pour les nouvelles plages d’adresses IP.
> * Bien qu’Adobe prenne en charge les exportations de données vers les serveurs SFTP, les emplacements de stockage dans le cloud recommandés pour exporter des données sont [!DNL Amazon S3] et [!DNL Azure Blob].

## Applicabilité {#applicability}

Les informations de plage d’adresses IP de cette page s’appliquent aux connecteurs de stockage dans le cloud basés sur les fichiers suivants dans le catalogue des destinations :

* [[!UICONTROL Amazon S3]](./amazon-s3.md)
* [[!UICONTROL Google Cloud Storage]](google-cloud-storage.md)
* [SFTP](./sftp.md)

>[!IMPORTANT]
>
>Les plages d’adresses IP documentées sur cette page ne sont *pas* prises en charge pour les destinations de stockage dans le cloud basées sur les fichiers suivantes : [!UICONTROL Azure Blob], [!UICONTROL Azure Data Lake Storage Gen2] et [!UICONTROL Data Landing Zone].

## Vue d’ensemble {#overview}

Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre liste autorisée afin d’exporter en toute sécurité des données d’Experience Platform vers plusieurs destinations de stockage dans le cloud.

Vous pouvez définir des contrôles d’accès réseau via votre pare-feu réseau. En spécifiant la plage d’adresses IP appropriée, vous pouvez autoriser le trafic pour le service de transfert de données.

Adobe recommande d’ajouter les plages d’adresses IP suivantes à une liste autorisée avant d’utiliser les connexions de destination de stockage dans le cloud. Si vous n’ajoutez pas votre plage d’adresses IP spécifique à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation des connexions de destination de stockage dans le cloud.

## Requis pour tous les clients {#all-customers}

* `52.247.108.70`

## Clients américains {#us-customers}

* `52.252.71.64/29`

## Clients canadiens {#canada-customers}

* `20.220.135.16/29`

## Clients EMEA {#emea-customers}

* `51.137.8.208/29`

## Clients britanniques {#uk-customers}

* `20.26.133.96/29`

## Clients APAC {#apac-customers}

* `20.53.201.168/29`
