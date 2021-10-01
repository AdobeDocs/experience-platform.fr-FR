---
keywords: Experience Platform;accueil;rubriques populaires;collecte de données;launch;sdk web
solution: Experience Platform
title: Présentation de la collecte de données
topic-legacy: overview
description: Découvrez les différentes technologies impliquées dans la collecte de données relatives aux expériences client dans Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: f61a845b915df3d803085fbf528e014c8acd9dbd
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 100%

---

# Présentation de la collecte de données

Adobe Experience Platform fournit un ensemble de technologies qui vous permettent de collecter des données d’expérience client à partir de sources côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network afin qu’elles soient enrichies, transformées et distribuées vers des destinations Adobe ou autres qu’Adobe en quelques secondes.

La collecte de données est prise en charge pour les sources côté client suivantes :

* Applications web
* Applications mobiles natives
* Applications OTT (over-the-top)

Les technologies de collecte de données fournies par Experience Platform se concentrent sur le référencement et l’accessibilité des jeux de données ingérés. Ces technologies englobent les éléments suivants :

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html?lang=fr)
* [Balises](../tags/home.md)
* [Transfert d’événement](../tags/ui/event-forwarding/overview.md)
* [SDK web Adobe Experience Platform](../edge/home.md)
* [Modèle de données d’expérience (XDM)](../xdm/home.md)

![](./images/Collection.png)

## Implémentations facilitées, performances côté client accélérées

Les SDK web et mobile d’Adobe Experience Platform réduisent et compressent toutes les bibliothèques des produits Adobe en un seul kit de développement pour les plateformes web ou mobiles. La compression de ces bibliothèques accélère la collecte de données et consolide les opérations dans un flux unique, reliant les appareils côté client à Adobe Experience Platform Edge Network.

## Processus de basculement afin de déployer la technologie Adobe {#edge}

Platform Edge Network est un réseau de serveurs distribué dans le monde entier. Rapide et fiable, il est capable de recevoir et de traiter des données à très grande échelle. Grâce aux balises, vous pouvez mettre en place des [flux de données](../edge/fundamentals/datastreams.md) pour des produits comme Adobe Target, Adobe Audience Manager et Adobe Analytics. Ces configurations vous permettent d‘activer les produits en question côté serveur sans modifier le code côté client.

![](./images/deploy.png)

>[!NOTE]
>
>Pour une présentation détaillée de Platform Edge Network, reportez-vous à [cette présentation interactive du produit](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Transformation, enrichissement et envoi de données de manière rapide et sécurisée

[Le transfert d’événement dans Adobe Experience Platform](../tags/ui/event-forwarding/overview.md) peut exploiter n’importe quel flux de données Platform. Vous pouvez transformer, enrichir et envoyer des données vers une destination autre qu’Adobe avec une latence extrêmement faible, et ce, sans ajouter de code tiers au périphérique client. Ainsi, les données sont collectées et distribuées de manière plus rapide et plus sécurisée.

![](./images/launch.png)
