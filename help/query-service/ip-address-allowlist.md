---
keywords: adresse IP, plage d’adresses IP, liste autorisée,, Query Service, accès réseau
title: Adresse IP associée à Query Service
description: Cette page fournit des plages d’adresses IP mises à jour que vous pouvez ajouter à votre place sur la liste autorisée pour un accès sécurisé à Query Service.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
TQID: https://experienceleague.adobe.com/29vuxFP4lB-AJy1I68P2Cxtt6HzMgE8Azz0F-gUXgI4
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 314
ht-degree: 4%

---

# Liste autorisée d’adresses IP {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe vous recommande d’ajouter un signet à cette page et de la consulter tous les trois mois pour rechercher les dernières adresses IP. Adobe ne fournit pas de notification des nouvelles plages d’adresses IP.
> * Depuis le 15 octobre 2024, seules les nouvelles plages d’adresses IP sont valides pour l’accès à Query Service. Les adresses IP obsolètes ne fonctionnent plus. Assurez-vous que votre place sur la liste autorisée ne comprend que les nouvelles adresses IP afin d’éviter toute interruption de service.

## Vue d’ensemble {#overview}

Vous pouvez définir des contrôles d’accès réseau via votre pare-feu réseau. En spécifiant la plage d’adresses IP appropriée, vous pouvez autoriser le trafic pour l’accès à Query Service.

Dans le cadre des améliorations continues, Adobe a mis à jour les plages d’adresses IP pour l’accès réseau à Query Service. Les adresses IP précédentes sont désormais obsolètes et seules les nouvelles adresses IP sont valides. Il est essentiel de mettre à jour votre place sur la liste autorisée pour inclure les nouvelles plages d’adresses IP suivantes afin de maintenir un service ininterrompu.

Adobe vous recommande d’ajouter les plages d’adresses IP spécifiques à une région à un place sur la liste autorisée de données en fonction de votre région. L’échec de l’ajout de ces plages d’adresses IP spécifiques à une région peut entraîner des erreurs ou des perturbations du service.

## VA7 : Clients des États-Unis et de l&#39;Amérique {#us-americas}

**New IP:** 4.152.211.251

## NLD2 : clients EMEA {#emea}

**New IP:** 108.141.12.47

## AUS5 : clients APAC {#apac}

**New IP:** 40.82.220.111

## CAN2 : clients canadiens {#can2}

**New IP:** 4.172.28.20

## GBR9 : clients du Royaume-Uni {#gbr9}

**New IP:** 20.254.80.141

## Configurer des restrictions basées sur les adresses IP {#set-ip-restrictions}

Utilisez les [guides de l’API Data Distiller Authorization](./auth-api/overview.md) pour configurer des restrictions basées sur des adresses IP. Ces restrictions IP garantissent que seuls les réseaux et les ordinateurs clients approuvés peuvent accéder aux données via SQL dans Adobe Experience Platform. Découvrez comment configurer, appliquer et surveiller les restrictions IP afin de respecter des normes de sécurité élevées, avec des fonctionnalités de suivi d’accès et d’alerte en temps réel.

* [Guide de prise en main](./auth-api/getting-started.md)
* [Guide du point d’entrée d’accès IP](./auth-api/ip-access.md)
* [Guide du point d’entrée de validation IP](./auth-api/validate.md)
