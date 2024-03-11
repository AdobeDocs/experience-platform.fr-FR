---
title: Présentation du SDK (Web Software Development Kit) de Adobe Experience Platform
description: Découvrez comment utiliser le SDK Web de Adobe Experience Platform pour intégrer des fonctionnalités de Platform à votre site web.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 28%

---


# SDK Web Adobe Experience Platform {#overview}

>[!IMPORTANT]
>
>Fin avril 2024, le SDK Web de Adobe Experience Platform supprimera la prise en charge de toutes les versions d’Internet Explorer.

Le SDK (Web Software Development Kit) de Adobe Experience Platform est une bibliothèque JavaScript côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec ses services via Adobe Experience Platform Edge Network.

Adobe propose deux méthodes pour mettre en oeuvre le SDK Web :

* La variable [Extension de balise SDK Web](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Consultez le tutoriel sur la manière de [Mise en oeuvre de Adobe Experience Cloud avec le SDK Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr) pour plus d’informations.
* Mise en oeuvre manuelle à l’aide de la bibliothèque JavaScript du SDK Web.

Ce guide d’utilisation comprend des instructions sur l’interaction avec les solutions Experience Cloud par le biais de la bibliothèque JavaScript du SDK Web et de l’extension de balise, le cas échéant.

## Réseau Edge Experience Platform {#edge-network}

Le SDK Web Experience Platform fait partie d’un ensemble d’outils qui constituent le réseau Adobe Experience Platform Edge.

Le réseau Edge est constitué des composants suivants :

* **[SDK Web Experience Platform](#overview):** Une bibliothèque JavaScript et une extension de balise qui vous aident à simplifier le déploiement des technologies Adobe.
* **[SDK Mobile Experience Platform](https://developer.adobe.com/client-sdks/home/):** Extension du SDK mobile v5 qui permet d’utiliser la nouvelle méthodologie de déploiement.
* **[API du serveur réseau Edge](../server-api/overview.md):** Une API côté serveur que vous pouvez utiliser pour divers cas d’utilisation de la collecte de données, de la personnalisation, de la publicité et du marketing. L’API serveur peut être utilisée sur des serveurs, des périphériques IoT, des décodeurs et sur divers autres périphériques.

Le réseau Edge est un cadre pour la collecte de données à faible latence, l’informatique enfichable et l’activation rapide des données sur tous les canaux adressables. Il fournit un SDK consolidé unique pour chaque canal (web, mobile, côté serveur), qui envoie des données à un domaine d’Adobe commun (`adobedc.net`) et reçoit une seule payload pour la diffusion des données et de l’expérience.

Côté serveur, une passerelle de périphérie unifiée et une structure de service de plateforme commune facilitent le déploiement de nouvelles fonctionnalités dans cet environnement informatique en temps réel. Cette architecture :

* diminue le délai de rentabilisation du client ;
* met fin au besoin d’intégrations « point à point » ;
* améliore les performances par rapport aux anciennes bibliothèques ;
* réduit les coûts ;
* augmente la vitesse d’innovation ;
* crée des avantages concurrentiels durables pour les clients Adobe.

Un seul système de périphérie consolidé vous permet de gérer vos campagnes publicitaires, marketing ou de personnalisation sur tous les canaux en tant qu’expérience intégrée. Il permet également à l’Adobe de fournir des services dont le coût total de possession est inférieur pour les clients. Le système Edge est conçu pour accueillir la plupart des types de données, ce qui vous permet de mapper votre propre modèle de données à ingérer par plusieurs produits Experience Cloud.

## Vue d’ensemble des vidéos {#video}

Regardez la vidéo ci-dessous pour un aperçu de Adobe Experience Platform [!DNL Web SDK] et la variable [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliothèques remplacées par le SDK Web {#sdks}

Le SDK Web n’est pas seulement un wrapper des bibliothèques existantes. Il s&#39;agit d&#39;une nouvelle bibliothèque, écrite de toutes pièces pour incorporer les fonctionnalités des bibliothèques existantes. Son objectif est de mettre fin aux problèmes liés au déclenchement des balises dans le bon ordre, à l’incohérence avec les problèmes de contrôle de version des bibliothèques et à une meilleure gestion des dépendances. Il s’agit d’une nouvelle méthode d’implémentation, [open source](https://github.com/adobe/alloy), d’[!DNL Experience Cloud].

Le SDK Web de Platform remplace les SDK suivants :

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Outre une nouvelle bibliothèque, il existe un nouveau point d’entrée qui rationalise les requêtes HTTP vers les solutions Adobe. Avant : `Visitor.js` a envoyé un appel de blocage au service d’identification des visiteurs, puis `AT.js` a envoyé un appel à Adobe Target, `DIL.js` a envoyé un appel à Adobe Audience Manager, puis `AppMeasurement.js` a envoyé un appel à Adobe Analytics. Cette nouvelle bibliothèque et ce nouveau point d’entrée peuvent récupérer un identifiant ou une expérience [!DNL Target], envoyer les données à [!DNL Audience Manager] et les transmettre à Adobe Experience Platform grâce à un seul appel.

La vidéo suivante présente Adobe Experience Platform [!DNL Web SDK] et Adobe Experience Platform [!DNL Edge Network] en action. L’exemple vidéo utilise un appel unique à Adobe qui envoie les données à [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], et [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migrer des bibliothèques existantes vers le SDK Web {#migrating-to-web-sdk}

Pour simplifier votre migration depuis l’un des [bibliothèques existantes](#sdks) Adobe offre un chemin de mise à niveau simplifié vers le SDK Web. Ce chemin vous permet de migrer chaque page de votre site web vers le SDK Web sans avoir à migrer simultanément l’intégralité de votre site web. Vous pouvez utiliser le SDK Web sur une page donnée, alors que les bibliothèques existantes résident sur d’autres pages. Une fois que vous êtes prêt, vous pouvez également migrer ces pages.

### Migration de `AT.js` aux considérations relatives au SDK Web {#considerations}

Avant de migrer des pages qui utilisent `AT.js` dans le SDK Web, veillez à activer les options de configuration du SDK Web suivantes. Ces options garantissent que le profil du visiteur est conservé lors de la navigation à partir de pages avec `AT.js` aux pages utilisant le SDK Web.

* [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [`targetMigrationEnabled`](/help/web-sdk/commands/configure/targetmigrationenabled.md)


>[!IMPORTANT]
>
>Les fonctionnalités Target suivantes ne sont pas prises en charge lors de la migration d’at.js vers le SDK Web :
>
>* [Offres de redirection](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=fr)
>* [Prise en charge CNAME et inter-domaines](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Après la migration depuis `AT.js` sur le SDK Web, supprimez la `targetMigrationEnabled` de votre configuration.
