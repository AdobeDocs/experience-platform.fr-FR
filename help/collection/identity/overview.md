---
title: Identité dans la collecte de données
description: Découvrez comment la collecte de données utilise les ECID, les identifiants PRINCIPAUX, la persistance propriétaire et l’identityMap dans les implémentations web.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Identité dans la collecte de données

La collecte de données Adobe utilise des signaux d’identité pour reconnaître les visiteurs récurrents et transporter du contexte entre les expériences. Lorsqu’un visiteur atteint votre site, Edge Network génère un Experience Cloud ID (ECID) et le conserve dans un cookie propriétaire. Cet ECID est l’identifiant d’appareil principal utilisé dans les applications Adobe Experience Cloud et constitue la base sur laquelle s’appuient les analyses, la personnalisation et l’activation des audiences. Dans votre mise en œuvre, vous pouvez accéder à l’ECID du visiteur côté client via la commande [`getIdentity`](/help/collection/js/commands/getidentity.md). Au niveau du flux de données, vous pouvez utiliser [Préparation des données pour la collecte de données](/help/datastreams/data-prep.md) pour mapper l’ECID dans un champ XDM personnalisé avant qu’il n’atteigne les services en aval.

L’ECID identifie un appareil et non une personne. Pour lier l’activité à une personne connue, vous pouvez envoyer des identifiants supplémentaires, tels qu’un identifiant CRM ou un e-mail haché, ainsi que l’ECID à l’aide de l’[`identityMap`](./identity-map.md) XDM. Adobe recommande de définir un espace de noms au niveau de la personne comme [identité principale](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) chaque fois qu’il est disponible.

En plus de l’ECID par défaut, la collecte de données prend en charge des signaux d’identité supplémentaires en fonction de votre implémentation :

* **Identifiants d’appareils propriétaires (FPID)** : identifiants d’appareils que vous générez et gérez sur l’infrastructure que vous contrôlez. Edge Network utilise un FPID pour [amorcer l’ECID](./fpid.md), ce qui vous permet d’accroître la persistance des cookies sur les propriétés détenues lorsque les restrictions du navigateur raccourcissent la durée de vie des cookies gérés par Adobe.
* **CORE IDs** : identifiant distinct, basé sur demdex, qui participe aux workflows d’identité tiers lorsque des cookies tiers sont disponibles. L’identifiant CORE est distinct de l’ECID et peut être récupéré via [`getIdentity`](/help/collection/js/commands/getidentity.md). Pour plus d’informations sur la façon dont les contextes d’identité propriétaires et tiers fonctionnent ensemble, voir [Prise en charge des identités unifiées](./unified-identity-support.md).

Si vous effectuez une mise à niveau à partir de l’API visiteur ou que vous réconciliez un comportement d’identité antérieur, consultez [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md) de migrer les cookies AMCV existants.

## Collection propriétaire et tierce {#first-party-and-third-party-collection}

Le SDK Web définit toujours l’identité [cookies](https://experienceleague.adobe.com/fr/docs/core-services/interface/data-collection/cookies/web-sdk) (tels que les cookies `kndctr_`) comme des cookies propriétaires sur votre domaine, quel que soit le point d’entrée qui reçoit la demande de collecte de données. Le point d’entrée de collecte (le domaine vers lequel votre implémentation envoie des données) est un choix distinct qui affecte la manière dont les navigateurs et les politiques réseau traitent la requête elle-même.

**Collecte propriétaire** achemine les demandes de collecte de données par le biais d’un domaine contrôlé par votre organisation (par exemple, `data.example.com`) à l’aide d’un CNAME qui pointe vers Adobe Edge Network. Comme la requête reste sur votre domaine, elle est moins susceptible d’être bloquée par des bloqueurs de publicités ou des restrictions réseau du navigateur. La collecte propriétaire est également un prérequis pour la définition des [identifiants d’appareil propriétaires](./fpid.md) à partir de votre propre infrastructure de serveur, ce qui constitue la stratégie d’identité la plus durable disponible. Adobe recommande d’utiliser le [programme de certificat géré par Adobe](https://experienceleague.adobe.com/fr/docs/core-services/interface/data-collection/adobe-managed-cert) pour configurer la collecte propriétaire pour votre implémentation.

**Collection tierce** envoie directement les requêtes à une [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) appartenant à Adobe (telle que `example.data.adobedc.net`). Bien que les cookies d’identité soient toujours définis comme propriétaires sur votre domaine, la requête elle-même est envoyée à un domaine tiers, que certains navigateurs et bloqueurs de publicités peuvent restreindre.

## Choisir le modèle d’identité approprié {#choose-your-path}

* **Renforcer la persistance de l’identité sur les propriétés détenues** : utilisez [identifiants d’appareil propriétaires](./fpid.md) lorsque les restrictions du navigateur raccourcissent la durée de vie des cookies et que vous avez besoin d’une continuité plus forte pour les analyses et la personnalisation sur les sites que vous contrôlez.
* **Transférer l’identité d’une application vers le web mobile** : utilisez le [partage d’identité mobile vers le web](./mobile-to-web.md) lorsque le visiteur commence dans votre application mobile et continue dans une page web mobile ou WebView.
* **Maintenir la continuité de l’identité entre vos domaines** : utilisez le [partage inter-domaines](./cross-domain-sharing.md) lorsque des visiteurs passent d’une propriété web appartenant à votre organisation à une autre et que vous souhaitez une personnalisation et des rapports cohérents.
* **Combiner la persistance propriétaire avec l’activation tierce** : utilisez [Prise en charge des identités unifiées](./unified-identity-support.md) lorsque vous avez besoin d’une identification propriétaire durable avec des flux d’activation tiers pris en charge.
* **Envoyer des identifiants au niveau de la personne** : utilisez [`identityMap`](./identity-map.md) pour envoyer des identifiants CRM, des e-mails hachés et d’autres identifiants au niveau de la personne avec l’ECID afin que les services en aval puissent regrouper l’activité avec une personne connue.
* **Comprendre comment le consentement affecte l’identité** : lisez [Consentement et identité](./consent.md) pour savoir comment `defaultConsent` et `setConsent` contrôler le moment où le SDK Web génère un ECID, définit les cookies et envoie les données.

Pour obtenir de l’aide sur le diagnostic des problèmes d’identité tels que le gonflement des visiteurs, les incohérences ECID ou les problèmes FPID, voir [Dépannage d’identité](./troubleshooting.md).
