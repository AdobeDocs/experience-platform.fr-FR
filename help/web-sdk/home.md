---
title: Présentation du SDK (Web Software Development Kit) de Adobe Experience Platform
description: Découvrez comment utiliser le SDK Web de Adobe Experience Platform pour intégrer des fonctionnalités de Platform à votre site web.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 2bf9c7ada9fd223df92b5cc9b1415f20705c2042
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 5%

---

# SDK Web Adobe Experience Platform {#overview}

Le SDK Web de Adobe Experience Platform est une bibliothèque JavaScript côté client qui permet aux clients Adobe Experience Cloud d’interagir avec ses services via l’Edge Network Adobe Experience Platform.

Vous pouvez mettre en oeuvre le SDK Web de deux manières :

* L’ [extension de balise SDK Web](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Pour plus d’informations, consultez le tutoriel sur la [mise en oeuvre de Adobe Experience Cloud avec le SDK Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr) .
* Mise en oeuvre manuelle à l’aide de la [ bibliothèque JavaScript SDK Web](install/library.md).

Ce guide comprend des instructions pour interagir avec les solutions Experience Cloud à l’aide de la bibliothèque JavaScript SDK Web et de l’extension de balise.

## Edge Network Experience Platform {#edge-network}



Le SDK Web Experience Platform fait partie de l’Edge Network Adobe Experience Platform, qui comprend :

* **[SDK Web Experience Platform](#overview)** : bibliothèque JavaScript et extension de balise pour simplifier le déploiement de la technologie Adobe.
* **[SDK mobile Experience Platform](https://developer.adobe.com/client-sdks/home/)** : extension du SDK mobile v5 pour la nouvelle méthodologie de déploiement.
* **[API Edge Network](../server-api/overview.md)** : API côté serveur pour la collecte de données, la personnalisation, la publicité et les cas d’utilisation marketing. Vous pouvez l’utiliser sur des serveurs, des périphériques IoT, des décodeurs et d’autres périphériques.

L’Edge Network fournit une collecte de données à faible latence, un calcul enfichable et une activation rapide des données sur tous les canaux adressables. Il offre un SDK consolidé unique pour les canaux web, mobiles et côté serveur, en envoyant des données à un domaine d’Adobe commun (`adobedc.net`) et en recevant une charge utile unique pour la diffusion des données et de l’expérience.

Côté serveur, une passerelle Edge unifiée et une structure de service de plateforme commune simplifient le déploiement de nouvelles fonctionnalités, tout en offrant les avantages suivants :

* Réduire le temps de valorisation des clients ;
* mettre fin à la nécessité d&#39;intégrations &quot;ponctuelles&quot;;
* Amélioration des performances par rapport aux anciennes bibliothèques ;
* la diminution des coûts d&#39;exploitation;
* Accélérer l&#39;innovation;
* Créer des avantages concurrentiels durables pour les clients Adobes.

Un système de périphérie consolidé vous permet de gérer des campagnes publicitaires, marketing et de personnalisation sur tous les canaux. Il réduit le coût total de propriété et prend en charge différents types de données, ce qui vous permet de mapper votre modèle de données pour l’utiliser avec plusieurs produits Experience Cloud.

## Vue d’ensemble des vidéos {#video}

Regardez la vidéo ci-dessous pour un aperçu de Adobe Experience Platform [!DNL Web SDK] et de [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliothèques remplacées par le SDK Web {#sdks}

Le SDK Web est une nouvelle bibliothèque Open Source entièrement conçue pour intégrer les fonctionnalités des bibliothèques existantes. Elle résout les problèmes liés à l’ordre de déclenchement des balises, aux incohérences de version et à la gestion des dépendances, en offrant une nouvelle méthode [open source](https://github.com/adobe/alloy) pour mettre en oeuvre [!DNL Experience Cloud].

Le SDK Web remplace :

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Il introduit également un nouveau point de terminaison qui rationalise les requêtes HTTP pour Adobe des solutions. Auparavant, plusieurs appels étaient nécessaires pour `Visitor.js`, `AT.js`, `DIL.js` et `AppMeasurement.js`. Désormais, un seul appel peut récupérer un identifiant, récupérer une expérience [!DNL Target], envoyer des données à [!DNL Audience Manager] et transmettre des données à Adobe Experience Platform.

Regardez la vidéo ci-dessous pour voir Adobe Experience Platform [!DNL Web SDK] et [!DNL Edge Network] en action, à l’aide d’un seul appel pour envoyer des données à [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] et [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migrer des bibliothèques existantes vers le SDK Web {#migrating-to-web-sdk}

Adobe offre un chemin de mise à niveau simplifié pour simplifier la migration de l’une des [bibliothèques existantes](#sdks) vers le SDK Web. Vous pouvez migrer chaque page de votre site web individuellement, sans avoir à migrer simultanément l’ensemble du site. Vous pouvez utiliser le SDK Web sur certaines pages, tandis que les bibliothèques existantes restent sur d’autres, ce qui permet une transition progressive.

### Considérations relatives à la migration de `AT.js` vers le SDK Web {#considerations}

Avant de migrer des pages à l’aide de `AT.js` vers le SDK Web, activez les options de configuration du SDK Web suivantes pour vous assurer que le profil du visiteur est conservé lors de la navigation entre les pages.

* [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [`targetMigrationEnabled`](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>Les fonctionnalités Target suivantes ne sont pas prises en charge lors de la migration de `at.js` vers le SDK Web :
>
>* [Offres de redirection](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=fr)
>* [Prise en charge CNAME et inter-domaines](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Après la migration de `AT.js` vers le SDK Web, supprimez l’option `targetMigrationEnabled` de votre configuration.
