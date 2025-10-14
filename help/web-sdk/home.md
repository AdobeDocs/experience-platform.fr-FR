---
title: Présentation Du Kit De Développement Logiciel Web Adobe Experience Platform (SDK)
description: Découvrez comment utiliser Adobe Experience Platform Web SDK pour intégrer les fonctionnalités d’Experience Platform à votre site web.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 5%

---

# SDK Web Adobe Experience Platform {#overview}

Adobe Experience Platform Web SDK est une bibliothèque JavaScript côté client qui permet aux clients Adobe Experience Cloud d’interagir avec ses services via Adobe Experience Platform Edge Network.

Vous pouvez implémenter le SDK Web de deux manières :

* L’extension de balise [Web SDK](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Pour plus d’informations, consultez le tutoriel sur la [implémentation de Adobe Experience Cloud avec Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr).
* Implémentation manuelle à l’aide de la [bibliothèque JavaScript Web SDK](install/library.md).

Ce guide comprend des instructions pour interagir avec les solutions Experience Cloud à l’aide de la bibliothèque JavaScript Web SDK et de l’extension de balise.

## Experience Platform Edge Network {#edge-network}



Experience Platform Web SDK fait partie d’Adobe Experience Platform Edge Network, qui comprend :

* **[Experience Platform Web SDK](#overview)** : bibliothèque JavaScript et extension de balise pour simplifier le déploiement de la technologie Adobe.
* **[Experience Platform Mobile SDK &#x200B;](https://developer.adobe.com/client-sdks/home/)** : une extension du SDK Mobile v5 pour la nouvelle méthodologie de déploiement.
* **[API Edge Network &#x200B;](https://developer.adobe.com/data-collection-apis/docs/api/)** : API côté serveur pour la collecte de données, la personnalisation, la publicité et les cas d’utilisation marketing. Vous pouvez l’utiliser sur des serveurs, des appareils IoT, des décodeurs et d’autres appareils.

Edge Network offre une collecte de données à faible latence, une informatique enfichable et une activation de données rapide sur tous les canaux adressables. Il propose un SDK consolidé unique pour les canaux web, mobiles et côté serveur, qui envoie des données à un domaine Adobe commun (`adobedc.net`) et reçoit une seule payload pour la diffusion des données et de l’expérience.

Côté serveur, une passerelle de périphérie unifiée et un framework de service de plateforme commune simplifient le déploiement de nouvelles fonctionnalités, tout en offrant les avantages suivants :

* réduire le délai de rentabilisation du client ;
* mettre fin à la nécessité d&#39;intégrations « ponctuelles »;
* amélioration des performances par rapport aux anciennes bibliothèques ;
* Diminution des coûts d&#39;exploitation ;
* l&#39;accélération de l&#39;innovation ;
* Création d’avantages concurrentiels durables pour les clients Adobe.

Un système de périphérie consolidé vous permet de gérer des campagnes publicitaires, marketing et de personnalisation sur tous les canaux. Il réduit le coût total de possession et prend en charge divers types de données, ce qui vous permet de mapper votre modèle de données pour l’utiliser avec plusieurs produits Experience Cloud.

## Vue d’ensemble des vidéos {#video}

Regardez la vidéo ci-dessous pour un aperçu de la [!DNL Web SDK] Adobe Experience Platform et du [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/37259?quality=12&learn=on&captions=fre_fr)

## Bibliothèques remplacées par le SDK Web {#sdks}

Web SDK est une nouvelle bibliothèque open source créée à partir de zéro pour intégrer les fonctionnalités des bibliothèques existantes. Elle résout les problèmes liés à l’ordre de déclenchement des balises, aux incohérences de version et à la gestion des dépendances, offrant ainsi une nouvelle méthode [open source](https://github.com/adobe/alloy) d’implémentation de la [!DNL Experience Cloud].

Le Web SDK remplace :

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Il introduit également un nouveau point d’entrée qui simplifie les requêtes HTTP aux solutions Adobe. Auparavant, plusieurs appels étaient nécessaires pour `Visitor.js`, `AT.js`, `DIL.js` et `AppMeasurement.js`. Désormais, un seul appel peut récupérer un identifiant, récupérer une expérience [!DNL Target], envoyer des données à [!DNL Audience Manager] et transmettre des données à Adobe Experience Platform.

Regardez la vidéo ci-dessous pour voir les [!DNL Web SDK] et les [!DNL Edge Network] de Adobe Experience Platform en action, à l’aide d’un seul appel pour envoyer des données à [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] et [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/3413665?captions=fre_fr)

## Migrer des bibliothèques existantes vers le SDK Web {#migrating-to-web-sdk}

Adobe offre un chemin de mise à niveau simplifié pour simplifier votre migration depuis l’une des [&#x200B; bibliothèques existantes &#x200B;](#sdks) vers Web SDK. Vous pouvez migrer chaque page de votre site web individuellement, sans avoir à migrer l’ensemble du site en une seule fois. Vous pouvez utiliser le SDK Web sur certaines pages tandis que les bibliothèques existantes restent sur d’autres, ce qui permet une transition progressive.

### Considérations relatives à la migration de `AT.js` vers Web SDK {#considerations}

Avant de migrer des pages à l’aide de `AT.js` vers Web SDK, activez les options de configuration de Web SDK suivantes pour vous assurer que le profil du visiteur est conservé lors de la navigation entre les pages.

* [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [`targetMigrationEnabled`](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>Les fonctionnalités de Target suivantes ne sont pas prises en charge lors de la migration de `at.js` vers Web SDK :
>
>* [Offres de redirection](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=fr)
>* [Prise en charge CNAME et inter-domaines](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html?lang=fr)

Après la migration de `AT.js` vers Web SDK, supprimez l’option `targetMigrationEnabled` de votre configuration.
