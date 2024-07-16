---
title: Vue d’ensemble de l’API du serveur réseau Edge
description: Découvrez ce qu’est l’API du serveur réseau Edge et comment l’utiliser.
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: 041a1782442df5f08bb52e4e450734a51c7781ea
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 9%

---

# Vue d’ensemble de l’API du serveur réseau Edge {#overview}

Adobe Experience Platform Edge Network offre un moyen optimisé aux clients d’interagir avec n’importe quel service Adobe Experience Cloud ou Adobe Experience Platform Edge.

Le [!DNL Edge Network Server API] peut être utilisé pour divers cas d’utilisation de la collecte de données, de la personnalisation, de la publicité et du marketing. Le [!DNL Server API] peut être utilisé sur les serveurs, les appareils [!DNL IoT], les décodeurs et sur divers autres appareils.

Étant donné que le [!DNL Server API] ne dépend d’aucune bibliothèque à charger, il offre un moyen rapide et éclair d’interagir avec l’Edge Network Adobe Experience Platform et les solutions prises en charge.

Les avantages de l’architecture [!DNL Server API] incluent :

* Réduction du temps de chargement des pages
* Latence améliorée
* Collecte de données propriétaires
* Communication rationalisée côté serveur entre les services

[!DNL Server API] prend en charge la collecte de données interactives et par lots, via deux points de terminaison dédiés :

1. Le point de terminaison interactif prend en charge la communication avec les services Adobe Experience Platform et Adobe Experience Cloud qui prennent en charge la segmentation avancée, la personnalisation et d’autres cas d’utilisation marketing.
2. Le point de terminaison de lot permet d’envoyer des requêtes par lot lorsque les données doivent être intégrées sans recevoir de réponse des applications en cours d’appel.

[!DNL Server API] prend en charge le type de requêtes suivant :

* Demandes authentifiées via [Adobe Developer](https://developer.adobe.com/) à l’aide du point de terminaison `server.adobedc.net`.
* Requêtes non authentifiées via le point de terminaison `edge.adobedc.net`.

Cela permet des cas d’utilisation qui permettent une collecte sécurisée et authentifiée de données sensibles, conformément aux politiques de confidentialité de votre entreprise. En plus de l’authentification, l’API serveur prend en charge le marquage des flux de données afin d’accepter uniquement la communication authentifiée via l’API.

Regardez la vidéo ci-dessous pour une présentation simplifiée de l’API serveur.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
