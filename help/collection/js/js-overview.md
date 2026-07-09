---
title: Présentation de la bibliothèque JavaScript Web SDK
description: Envoyez des données à Adobe Experience Platform Edge Network à l’aide de JavaScript.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
TQID: https://experienceleague.adobe.com/9lk8ofZIQFzuYYl-BaT-c79H1yEmRps-ZuiLXm4mjPU
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: df80eeb1-8d72-467e-b0df-9d51c7d3a0a1
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2:
  - id: a075b2c1-7748-4328-b7f6-343aa314616a
  - id: a8b0238e-1d43-4679-a3b4-5ba1bad83baa
  - id: baaa0dd2-d27e-4921-aae3-7888623a5fa5
  - id: c814092e-2730-45e8-a12d-e084529f52cb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: d5ef99fa-df0c-4153-bf94-105ad0724167
  - id: d833d0ef-8ed5-4cff-a5e7-9f12abd02a31
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: eb9732ab-8232-4b21-bc4c-89de86dbe4d7
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
  - id: fc7979f3-56c3-43ca-9784-f1ea3dc69c4b
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: abc02dd6-664f-446a-9aaa-675bc0f2fe4a
  - id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
  - id: b64298cc-90cc-46b7-8917-ee391f1c7516
  - id: d2a6cbf4-df32-480f-909e-b42f66dcb9f0
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: e8a4c7eb-7254-4984-ac46-e651a57c7e39
  - id: ee602049-8a18-43df-9299-a689a025a371
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 2f54212d8592c5ebc45b847c5f8269ddddfeb622
workflow-type: tm+mt
source-wordcount: 445
ht-degree: 5%

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

Web SDK est une bibliothèque open source créée à partir de zéro pour intégrer les fonctionnalités des bibliothèques existantes. Elle résout les problèmes d’ordre de déclenchement des balises, d’incohérences de version et de gestion des dépendances, offrant ainsi un moyen d’implémenter de nombreux produits Experience Cloud. Le SDK Web remplace la collecte de données pour les services suivants :

* Service d’identification des visiteurs Adobe (`VisitorAPI.js`)
* Adobe Analytics `AppMeasurement.js`)
* Adobe Target `AT.js`)
* Adobe Audience Manager `DIL.js`)
* Adobe Media Analytics
* Adobe Advertising

Il introduit également un nouveau point d’entrée qui simplifie les requêtes HTTP aux solutions Adobe. Auparavant, plusieurs appels étaient nécessaires pour chaque bibliothèque de collecte de données. Désormais, un seul appel peut récupérer un identifiant, récupérer une expérience [!DNL Target], envoyer des données à [!DNL Audience Manager] et transmettre des données à Adobe Experience Platform.

## Migrer des bibliothèques existantes vers le SDK Web {#migrating-to-web-sdk}

Adobe offre un chemin de mise à niveau simplifié pour simplifier votre migration depuis l’une des bibliothèques existantes vers le SDK Web. Vous pouvez migrer chaque page de votre site web individuellement, sans avoir à migrer l’ensemble du site en une seule fois. Vous pouvez utiliser le SDK Web sur certaines pages tandis que les bibliothèques existantes restent sur d’autres, ce qui permet une transition progressive.
