---
keywords: Adresse IP, plage IP, liste autorisée, liste autorisée
title: LISTE AUTORISÉE d’adresse IP pour Query Service
description: Cette page fournit des plages d’adresses IP que vous pouvez ajouter à votre liste autorisée.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 18%

---

# Liste autorisée d’adresses IP {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe vous recommande de mettre cette page en signet et de la revoir tous les trois mois pour rechercher les dernières adresses IP. Adobe ne fournit pas de notification pour les nouvelles plages d’adresses IP.
> * Bien qu’Adobe prenne en charge les exportations de données vers les serveurs SFTP, les emplacements de stockage dans le cloud recommandés pour exporter des données sont les suivants : [!DNL Amazon S3] et [!DNL Azure Blob].

## Vue d’ensemble {#overview}

Cette page fournit des adresses IP que vous pouvez ajouter à votre liste autorisée afin d’exporter en toute sécurité des données de l’Experience Platform vers votre [Serveur SFTP](../destinations/catalog/cloud-storage/sftp.md).

Vous pouvez définir des contrôles d’accès réseau via votre pare-feu réseau. En spécifiant la plage d’adresses IP appropriée, vous pouvez autoriser le trafic pour le service de transfert de données.

Adobe vous recommande d’ajouter les plages d’adresses IP suivantes à une liste autorisée en fonction de votre région. Si vous n’ajoutez pas votre plage d’adresses IP spécifique à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire.

## VA7 : clients des États-Unis et des Amériques {#us-americas}

* 52.138.119.167

## NLD2 : clients EMEA {#emea}

* 51.124.70.4

## AUS5 : clients APAC {#apac}

* 20.193.36.37

## CAN2 : clients canadiens {#can2}

* 20.104.5.248
