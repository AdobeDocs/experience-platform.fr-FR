---
keywords: Adresse IP, plage IP, liste autorisée, liste autorisée, Query Service, accès réseau
title: LISTE AUTORISÉE d’adresse IP pour Query Service
description: Cette page fournit des plages d’adresses IP mises à jour que vous pouvez ajouter à votre liste autorisée pour un accès sécurisé à Query Service.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: ac29d10d3774a736d1e54255508ba244ff72f278
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 4%

---

# Liste autorisée d’adresses IP {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe vous recommande de mettre cette page en signet et de la revoir tous les trois mois pour rechercher les dernières adresses IP. Adobe ne fournit pas de notification pour les nouvelles plages d’adresses IP.
> * Depuis le 15 octobre 2024, seules les nouvelles plages d’adresses IP sont valides pour l’accès à Query Service. Les adresses IP obsolètes ne fonctionnent plus. Veillez à ce que votre liste autorisée ne contienne que les nouvelles adresses IP afin d’éviter les interruptions de service.

## Vue d’ensemble {#overview}

Vous pouvez définir des contrôles d’accès réseau via votre pare-feu réseau. En spécifiant la plage d’adresses IP appropriée, vous pouvez autoriser le trafic pour l’accès à Query Service.

Dans le cadre des améliorations en cours, Adobe a mis à jour les plages d’adresses IP pour l’accès réseau à Query Service. Les adresses IP précédentes sont désormais obsolètes et seules les nouvelles adresses IP sont valides. Il est essentiel de mettre à jour votre liste autorisée pour inclure les nouvelles plages d’adresses IP suivantes afin de maintenir le service ininterrompu.

Adobe vous recommande d’ajouter les plages d’adresses IP suivantes spécifiques à une liste autorisée selon votre région. L’échec de l’ajout de ces plages d’adresses IP spécifiques à une région peut entraîner des erreurs ou des interruptions de service.

## VA7 : Clients des États-Unis et des États-Unis {#us-americas}

**Nouvelle adresse IP :** 4.152.211.251

## NLD2 : clients EMEA {#emea}

**Nouvelle adresse IP :** 108.141.12.47

## AUS5 : clients APAC {#apac}

**Nouvelle adresse IP :** 40.82.220.111

## CAN2 : clients canadiens {#can2}

**Nouvelle adresse IP :** 4.172.28.20

## GBR9 : clients britanniques {#gbr9}

**Nouvelle adresse IP :** 20.254.80.141

## Configuration des restrictions basées sur les adresses IP {#set-ip-restrictions}

Utilisez les [guides de l’API d’autorisation de Data Distiller](./auth-api/overview.md) pour configurer des restrictions basées sur les adresses IP. Ces restrictions basées sur les adresses IP garantissent que seuls les réseaux et les ordinateurs clients approuvés peuvent accéder aux données via SQL dans Adobe Experience Platform. Découvrez comment configurer, appliquer et surveiller les restrictions d’adresses IP pour respecter des normes de sécurité élevées, avec des fonctionnalités de suivi et d’alerte d’accès en temps réel.

* [Guide de démarrage](./auth-api/getting-started.md)
* [Guide du point de terminaison d’accès IP](./auth-api/ip-access.md)
* [Guide du point de fin de validation IP](./auth-api/validate.md)
