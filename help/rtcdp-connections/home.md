---
keywords: Experience Platform;accueil;rubriques populaires;collecte de données;lancement;sdk web
solution: Experience Platform
title: Présentation de Real-Time Customer Data Platform Connections
topic-legacy: overview
description: Découvrez les différentes technologies impliquées dans la collecte de données relatives aux expériences client dans Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: ht
source-wordcount: '472'
ht-degree: 100%

---

# Présentation de Real-Time Customer Data Platform Connections

Real-Time Customer Data Platform (RTCDP) Connections fournit un ensemble de technologies vous permettant de collecter des données d’expérience client à partir des sources côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network afin qu’elles soient enrichies, transformées et distribuées vers des destinations Adobe ou autres qu’Adobe en quelques secondes.

RTCDP Connections est pris en charge pour les sources côté client suivantes :

* Applications web
* Applications mobiles natives
* Applications OTT (over-the-top)

RTCDP Connections se concentre sur la capacité de découverte et l’accessibilité des jeux de données ingérés, ce qui comprend :

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html?lang=fr)
* [Balises](../tags/home.md)
* [Flux de données](../edge/datastreams/overview.md)
* [Transfert d’événement](../tags/ui/event-forwarding/overview.md)
* [SDK web Adobe Experience Platform](../edge/home.md)
* [ SDK Mobile Adobe Experience Platform](https://aep-sdks.gitbook.io/docs/)
* [Débogueur Adobe Experience Platform](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=fr)
* [Modèle de données d’expérience (XDM)](../xdm/home.md)
* [Adobe Experience Platform Identity Service](../identity-service/home.md)

Ce guide fournit une présentation générale de RTCDP Connections ainsi que la manière dont il procède pour envoyer des données aux produits Adobe Experience Cloud et aux applications autres qu’Adobe par Platform Edge Network.

## Balises, SDK Web et SDK Mobile

Le SDK Web de Platform et le SDK Mobile de Platform réduisent et compressent toutes les bibliothèques de produits d’Adobe dans un seul kit de développement pour les plateformes web et mobiles, respectivement. Ils peuvent être implémentés à l’aide de code brut ou en utilisant des [balises](../tags/home.md) via l’interface utilisateur de collecte de données.

La compression de ces bibliothèques accélère la collecte de données et consolide les opérations dans un flux unique, reliant les appareils côté client au réseau Platform Edge.

![Balises, SDK Web, SDK Mobile](./images/home/tags-sdks.png)

## Réseau et flux de données Platform Edge {#edge}

Le réseau Platform Edge est un réseau de serveurs distribué dans le monde entier. Rapide et fiable, il est capable de recevoir et de traiter des données à très grande échelle. Grâce aux balises, vous pouvez mettre en place des [flux de données](../edge/datastreams/overview.md) pour des produits comme Adobe Target, Adobe Audience Manager et Adobe Analytics. Ces configurations vous permettent d‘activer les produits en question côté serveur sans modifier le code côté client.

![Solutions de flux de données et d’Adobe](./images/home/adobe-solutions.png)

>[!NOTE]
>
>Pour une présentation détaillée du réseau Platform Edge, reportez-vous à [cette présentation interactive du produit](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Transfert d’événement

[Transfert d’événement](../tags/ui/event-forwarding/overview.md) peut exploiter n’importe quel flux de données Experience Platform, ce qui vous permet de transformer, d’enrichir et d’envoyer des données à n’importe quelle destination non Adobe avec une latence extrême faible et sans ajouter de code tiers à l’appareil client.

![Transfert d’événement](./images/home/event-forwarding.png)

>[!NOTE]
>
>Le transfert d’événement est une fonctionnalité payante uniquement incluse dans l’offre Real-Time Customer Data Platform Connections.

## Étapes suivantes

Ce document fournit une présentation détaillée de la manière dont RTCDP Connections fonctionne pour automatiser le processus d’envoi de vos données d’expérience client collectées à des produits Adobe et à des destinations tierces.

![Framework de collecte de données](./images/home/collection.png)

Pour plus d’informations sur le workflow général impliqué dans l’envoi des données d’événement via Edge Network, reportez-vous à la section [Présentation complète](./e2e.md).
