---
title: Présentation de la bibliothèque JavaScript Web SDK
description: Envoyez des données à Adobe Experience Platform Edge Network à l’aide de JavaScript.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 3%

---

# Présentation de la bibliothèque JavaScript Web SDK

**Adobe Experience Platform Web SDK** est une bibliothèque JavaScript côté client qui vous permet d’envoyer des données à Adobe Experience Platform Edge Network. Ce guide décrit le chemin d’implémentation de la bibliothèque JavaScript Web SDK (`alloy.js`), y compris les concepts de base, l’installation, la configuration et les commandes. Pour connaître l’extension de balise Web SDK dans l’interface utilisateur de collecte de données, reportez-vous à la section [Extension de balise Web SDK](/help/tags/extensions/client/web-sdk/overview.md).

Web SDK envoie les données indépendamment de la solution (XDM) à Experience Platform Edge Network, qui les mappe ensuite aux formats et destinations spécifiques à la solution et les envoie en temps réel.

## Experience Platform Edge Network {#edge-network}

Adobe Experience Platform Edge Network offre une collecte de données à faible latence, une informatique enfichable et une activation de données rapide sur tous les canaux adressables. Il propose un SDK consolidé unique pour les canaux web, mobiles et côté serveur, qui envoie des données à un domaine Adobe commun (`adobedc.net`) et reçoit une seule payload pour la diffusion des données et de l’expérience.

Côté serveur, une passerelle de périphérie unifiée et un framework de service de plateforme commune simplifient le déploiement de nouvelles fonctionnalités, tout en offrant les avantages suivants :

* réduire le délai de rentabilisation du client ;
* mettre fin à la nécessité d&#39;intégrations « ponctuelles »;
* amélioration des performances par rapport aux anciennes bibliothèques ;
* Diminution des coûts d&#39;exploitation ;
* l&#39;accélération de l&#39;innovation ;
* Création d’avantages concurrentiels durables pour les clients Adobe.

Un système de périphérie consolidé vous permet de gérer des campagnes publicitaires, marketing et de personnalisation sur tous les canaux. Il réduit le coût total de possession et prend en charge divers types de données, ce qui vous permet de mapper votre modèle de données pour l’utiliser avec plusieurs produits Experience Cloud.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliothèques remplacées par le SDK Web {#sdks}

Web SDK est une bibliothèque open source créée à partir de zéro pour intégrer les fonctionnalités des bibliothèques existantes. Elle résout les problèmes d’ordre de déclenchement des balises, d’incohérences de version et de gestion des dépendances, offrant ainsi un moyen de mettre en œuvre de nombreux produits Experience Cloud. Le SDK Web remplace la collecte de données pour les services suivants :

* Service d’identification des visiteurs Adobe Experience Platform (`Visitor.js`)
* Adobe Analytics `AppMeasurement.js`)
* Adobe Target `AT.js`)
* Adobe Audience Manager `DIL.js`)
* Adobe Media Analytics
* Adobe Advertising

Il introduit également un nouveau point d’entrée qui simplifie les requêtes HTTP aux solutions Adobe. Auparavant, plusieurs appels étaient nécessaires pour chaque bibliothèque de collecte de données. Désormais, un seul appel peut récupérer un identifiant, récupérer une expérience [!DNL Target], envoyer des données à [!DNL Audience Manager] et transmettre des données à Adobe Experience Platform.

## Migrer des bibliothèques existantes vers le SDK Web {#migrating-to-web-sdk}

Adobe offre un chemin de mise à niveau simplifié pour simplifier votre migration depuis l’une des bibliothèques existantes vers le SDK Web. Vous pouvez migrer chaque page de votre site web individuellement, sans avoir à migrer l’ensemble du site en une seule fois. Vous pouvez utiliser le SDK Web sur certaines pages tandis que les bibliothèques existantes restent sur d’autres, ce qui permet une transition progressive.
