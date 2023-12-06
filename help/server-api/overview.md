---
title: Vue d’ensemble de l’API du serveur réseau Edge
description: Découvrez ce qu’est l’API du serveur réseau Edge et comment l’utiliser.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 9%

---


# Vue d’ensemble de l’API du serveur réseau Edge {#overview}

Adobe Experience Platform Edge Network offre un moyen optimisé aux clients d’interagir avec n’importe quel service Adobe Experience Cloud ou Adobe Experience Platform Edge.

La variable [!DNL Edge Network Server API] peut être utilisé pour divers cas d’utilisation de la collecte de données, de la personnalisation, de la publicité et du marketing. La variable [!DNL Server API] peut être utilisé sur les serveurs, [!DNL IoT] périphériques, des décodeurs et d’autres périphériques.

Depuis la variable [!DNL Server API] ne repose sur aucune bibliothèque à charger. Elle offre un moyen rapide d’interagir avec le réseau Adobe Experience Platform Edge et les solutions prises en charge.

Les avantages de [!DNL Server API] l’architecture comprend :

* Réduction du temps de chargement des pages
* Latence améliorée
* Collecte de données propriétaires
* Communication rationalisée côté serveur entre les services

La variable [!DNL Server API] prend en charge la collecte de données interactives et par lots, via deux points de terminaison dédiés :

1. Le point de terminaison interactif prend en charge la communication avec les services Adobe Experience Platform et Adobe Experience Cloud qui prennent en charge la segmentation avancée, la personnalisation et d’autres cas d’utilisation marketing.
2. Le point de terminaison de lot permet d’envoyer des requêtes par lot lorsque les données doivent être intégrées sans recevoir de réponse des applications en cours d’appel.

La variable [!DNL Server API] prend en charge le type de requêtes suivant :

* Demandes authentifiées via [Adobe Developer](https://developer.adobe.com/), à l’aide de la fonction `server.adobedc.net` point de terminaison .
* Requêtes non authentifiées via le `edge.adobedc.net` point de terminaison .

Cela permet des cas d’utilisation qui permettent une collecte sécurisée et authentifiée de données sensibles, conformément aux politiques de confidentialité de votre entreprise. En plus de l’authentification, l’API serveur prend en charge le marquage des flux de données afin d’accepter uniquement la communication authentifiée via l’API.

Regardez la vidéo ci-dessous pour une présentation simplifiée de l’API serveur.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
