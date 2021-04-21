---
keywords: Experience Platform ; accueil ; rubriques populaires ; collecte de données ; lancement ; sdk Web
solution: Experience Platform
title: Présentation de la collecte de données
topic-legacy: overview
description: Découvrez les différentes technologies impliquées dans la collecte de données sur les expériences client à Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 6%

---

# Présentation de la collecte de données

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client à partir de sources côté client et de les envoyer au Adobe Experience Platform Edge Network où elles peuvent être enrichies, transformées et distribuées en secondes vers des destinations Adobes ou non Adobes.

La collecte de données est prise en charge pour les sources côté client suivantes :

* Applications Web
* Applications mobiles natives
* Applications OTT (over-the-top)

Les technologies de collecte de données fournies par l&#39;Experience Platform mettent l&#39;accent sur la découverte et l&#39;accessibilité des jeux de données assimilés. Ces technologies englobent les éléments suivants :

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Adobe Experience Platform Launch](https://adobe.com/go/launch_help_en)
* [SDK web Adobe Experience Platform](../edge/home.md)
* [Modèle de données d’expérience (XDM)](../xdm/home.md)

![](./images/Collection.png)

## Des mises en oeuvre plus simples et des performances plus rapides côté client

Les kits SDK Web et Mobile de Adobe Experience Platform s’effondrent et compressent toutes les bibliothèques de produits d’Adobe en un seul kit de développement pour les plates-formes Web ou mobiles. La compression de ces bibliothèques accélère la collecte de données et consolide les opérations dans un flux unique, des périphériques côté client au réseau Adobe Experience Platform Edge.

## Processus de basculement pour déployer la technologie de l&#39;Adobe

Platform Edge Network est un réseau de serveurs mondialement distribué, rapide et fiable, capable de recevoir et de traiter des données à une grande échelle. Grâce à Platform launch, vous pouvez configurer des configurations [edge](../edge/fundamentals/edge-configuration.md) pour des produits tels que Adobe Target, Adobe Audience Manager et Adobe Analytics, qui vous permettent d&#39;activer ces produits côté serveur sans modifier le code côté client.

![](./images/deploy.png)

## Transformer, enrichir et envoyer des données rapidement et en toute sécurité

[Adobe Experience Platform Launch Server ](https://experienceleague.adobe.com/docs/launch/using/server-side-info/server-side-overview.html) Sidecan peut appuyer sur n’importe quel flux de données de plateforme. Vous pouvez transformer, enrichir et envoyer des données vers une destination autre que l’Adobe avec une latence extrêmement faible sans ajouter de code tiers au périphérique client, ce qui permet une collecte et une distribution plus rapides et plus sécurisées des données.

![](./images/launch.png)
