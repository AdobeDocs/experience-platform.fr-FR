---
title: personnalisation
description: Effectuez le rendu de différents contenus pour différents utilisateurs et utilisatrices, créant ainsi une expérience personnalisée pour eux.
exl-id: 4bd370c8-8d8d-469e-9666-b5b6d0e3a660
TQID: https://experienceleague.adobe.com/8i3XgBUE5aqnvgELSwmcfd4NBcLVf0QobRRiDa32hfM
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a075b2c1-7748-4328-b7f6-343aa314616a
  - id: a653cc2e-bc85-4353-a306-399e5b247978
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1282
ht-degree: 0%

---

# `personalization`

L’objet `personalization` configure quelles décisions de personnalisation (offres ou propositions) sont demandées et comment elles sont traitées dans la requête et la réponse. Elle s’avère particulièrement précieuse dans les implémentations Adobe Target ou Adobe Journey Optimizer, car elle est le moteur qui vous permet de personnaliser le contenu affiché par utilisateur.

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["hero-banner"],
    surfaces: ["web://example.com"],
    schemas: ["https://ns.adobe.com/personalization/dom-action"],
    sendDisplayEvent: true,
    sendDisplayNotifications: true,
    includePendingDisplayNotifications: true,
    defaultPersonalizationEnabled: false
  },
  renderDecisions: true,
  xdm: adobeDataLayer.getState(reference)
});
```

L’objet `personalization` contient les propriétés suivantes :

## `personalization.decisionScopes`

La propriété `decisionScopes` est un tableau de chaînes qui indique au SDK Web de récupérer et de renvoyer les décisions de personnalisation. Chaque élément du tableau identifie un emplacement, un contexte ou un emplacement logique où un contenu personnalisé est souhaité.

Cette propriété est utile lorsque vous souhaitez récupérer explicitement du contenu personnalisé pour des zones ou des composants spécifiques d’une page. Elle est particulièrement utile dans les applications d’une seule page qui peuvent nécessiter différents ensembles d’offres à mesure que la navigation ou la vue de l’utilisateur change. Vous pouvez également utiliser cette propriété pour optimiser les performances en récupérant uniquement les offres pour les éléments d’interface utilisateur pertinents pour l’utilisateur.

```js
personalization: {
  decisionScopes: ["hero-banner", "cart-offer"]
}
```

Dans Adobe Target, chaque portée de décision est mappée à une mbox ou à une activité. Dans Adobe Journey Optimizer, chaque portée de décision est mappée à des emplacements ou des campagnes de contenu web basés sur des décisions. Dans Offer Decisioning, les portées de décision mappent les offres ou propositions que le visiteur doit recevoir.

>[!TIP]
>
>Si vous souhaitez demander (ou bloquer) la portée globale, utilisez [`defaultPersonalizationEnabled`](#personalizationdefaultpersonalizationenabled) au lieu de la spécifier ici dans `decisionScopes`.

## `personalization.surfaces`

La propriété `surfaces` est un tableau de chaînes [URI de surface](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/channels/code-based-experience/configure-code-based-channel/code-based-surface#surface-uri) qui définissent manuellement le canal, l’appareil ou le contexte pour lequel la personnalisation est demandée. Ils vous permettent de faire la distinction entre différentes expériences digitales, telles que des domaines, des applications ou des plateformes d’appareils au sein de votre écosystème cross-canal. Par défaut, la bibliothèque déduit la surface par défaut de la page active. Vous pouvez utiliser cette propriété pour remplacer la surface déduite automatiquement pour la page active.

Cette propriété est utile lorsque vous souhaitez utiliser la personnalisation cross-canal et doit distinguer le fonctionnement de la personnalisation entre des canaux distincts. Il permet de créer des offres distinctes pour différents sites sous la même organisation Adobe Experience Platform.

```js
personalization: {
  surfaces: ["web://example.com", "web://support.example.com/contact"]
}
```

Cette propriété est utilisée de manière fondamentale avec Adobe Journey Optimizer, car elle correspond aux surfaces configurées dans les campagnes Journey Optimizer et la gestion des surfaces.

## `personalization.schemas`

La propriété `schemas` est un tableau de chaînes URI de schéma qui filtrent les types de contenu de personnalisation demandés à partir d’Edge Network. La définition de cette propriété limite la réponse que vous recevez d’Adobe pour inclure uniquement les offres correspondant aux définitions de type de contenu que vous spécifiez. Si cet attribut est omis, la bibliothèque demande les offres de tous les schémas disponibles pour les portées ou surfaces correspondantes.

Cette propriété permet d’optimiser la taille de la réponse et de s’assurer que votre site web ou votre application ne reçoit que les types d’offres qu’il peut gérer. Il s’avère également utile lorsqu’il est utilisé avec des applications d’une seule page qui effectuent le rendu du contenu personnalisé d’une manière spécifique (par exemple en utilisant uniquement des actions DOM ou uniquement des objets JSON).

```js
personalization: {
  schemas: [
    "https://ns.adobe.com/personalization/dom-action",
    "https://ns.adobe.com/personalization/html-content-item"
  ]
}
```

Les URI de schéma suivants sont pris en charge :

* **`https://ns.adobe.com/personalization/dom-action`** : offres qui sont des actions DOM directes, généralement générées par le compositeur d’expérience visuelle dans Adobe Target. Ils contiennent des instructions pour manipuler automatiquement les éléments de la page sans code supplémentaire. Il s’agit de la norme pour la personnalisation web générée automatiquement.
* **`https://ns.adobe.com/personalization/html-content-item`** : offres contenant des données brutes d’HTML diffusées sous forme de chaîne. Votre mise en œuvre insère généralement ce contenu à l’emplacement souhaité sur la page, ce qui vous donne plus de contrôle que les actions DOM. Généralement utilisé pour les bannières, les fragments de code ou le contenu modal.
* **`https://ns.adobe.com/personalization/json-content-item`** : offres formatées en tant qu’objet JSON. Utilisé le plus souvent dans les implémentations basées sur les API ou les front-ends qui attendent des données structurées au lieu des modifications d’HTML ou de DOM.
* **`https://ns.adobe.com/personalization/redirect-item`** : offres qui redirigent vers une autre URL. Permet d’orienter l’utilisateur vers une nouvelle page en fonction du ciblage ou de la logique de prise de décision, telle que les pages de destination ou les flux d’intégration.
* **`https://ns.adobe.com/personalization/ruleset-item`** : fournit un bloc de logique commerciale pour alimenter un moteur de règles côté client. Contient un ensemble de règles avec version définissant les conditions et conséquences logiques (si/alors la logique de personnalisation).
* **`https://ns.adobe.com/personalization/message/in-app`** : offres formatées spécifiquement pour les messages in-app de Adobe Journey Optimizer, généralement sous la forme de modaux, de bannières, de pop-ups ou de superpositions.
* **`https://ns.adobe.com/personalization/message/content-card`** : offres formatées spécifiquement pour les cartes de contenu Adobe Journey Optimizer, conçues pour les flux persistants ou de type boîte de réception dans les applications web ou mobiles.
* **`https://ns.adobe.com/personalization/message/native-alert`** : offres formatées spécifiquement pour les alertes natives Adobe Journey Optimizer, déclenchant des boîtes de dialogue de notification natives sur la plateforme.
* **`https://ns.adobe.com/personalization/measurement`** : utilisé pour effectuer le suivi des clics et des interactions sur les offres personnalisées. Ne contient pas de contenu pouvant être rendu.
* **`https://ns.adobe.com/personalization/eventHistoryOperation`** : schéma de modification de l’historique des événements d’un visiteur dans l’enregistrement local. Utilisé en interne par les SDK pour suivre les expériences qui ont été diffusées ou bloquées. Ne contient pas de contenu pouvant être rendu.
* **`https://ns.adobe.com/personalization/default-content-item`** : contenu de secours ou par défaut, généralement lorsqu&#39;aucune offre personnalisée n&#39;est éligible. Cela permet de s’assurer que les utilisateurs et utilisatrices non qualifiés reçoivent toujours le contenu, en préservant la cohérence de l’expérience.

## `personalization.sendDisplayEvent`

La propriété `sendDisplayEvent` est une valeur booléenne qui détermine si un événement de notification d’affichage est automatiquement envoyé à Edge Network immédiatement après le rendu du contenu personnalisé sur la page. Si cet attribut est omis, sa valeur par défaut est `true`. Définissez cette variable sur `false` si vous ne souhaitez pas indiquer que du contenu personnalisé a été rendu pour le suivi des impressions.

Le cas d’utilisation le plus courant pour définir cette variable sur `false` est lorsque vous prévoyez d’envoyer une autre commande ailleurs dans votre implémentation qui signale un événement d’affichage. Certaines implémentations comportent à la fois des événements d’impression et d’analyse. Cette propriété vous permet de contrôler entièrement les commandes d’`sendEvent` qui incrémentent les impressions.

```js
personalization: {
  sendDisplayEvent: true
}
```

>[!NOTE]
>
>Les versions précédentes de Web SDK (versions 2.12.0 et antérieures) utilisent `sendDisplayNotifications` à la place.

## `personalization.includePendingDisplayNotifications`

La propriété `includePendingDisplayNotifications` est une valeur booléenne qui contrôle si des notifications d’affichage en attente sont regroupées dans l’appel `sendEvent` actuel. Les notifications d’affichage en attente sont des impressions de contenu personnalisé qui ont été générées mais pas encore signalées à Edge Network en tant qu’événement d’affichage. Cette propriété est utile lors de l’utilisation d’applications d’une seule page, car le rendu du contenu personnalisé et les appels de `sendEvent` peuvent être asynchrones les uns des autres.

La valeur par défaut de cette propriété est `false`. Définissez cette propriété sur `true` si vous souhaitez traiter par lots et vider toutes les notifications d’affichage en attente afin que leurs impressions soient enregistrées avec précision. L’implémentation synchrone, telle que les sites web traditionnels, n’a généralement pas besoin de définir cette propriété.

```js
personalization: {
  includePendingDisplayNotifications: true
}
```

## `personalization.defaultPersonalizationEnabled`

La propriété `defaultPersonalizationEnabled` `__view__` est une valeur booléenne qui vous donne un contrôle explicite sur la manière dont le SDK Web demande la portée et la surface de personnalisation par défaut à l’échelle de la page pour cette commande de `sendEvent`. Par défaut, lors de la première commande de `sendEvent` après le chargement d’une page, Web SDK demande des offres pour la portée de personnalisation par défaut à l’échelle de la page et les surfaces associées. Les commandes `sendEvent` suivantes ne demandent pas de personnalisation par défaut. Vous pouvez utiliser cette propriété pour remplacer ce comportement. Elle s’avère utile dans les implémentations d’applications monopages où vous pouvez demander à nouveau la personnalisation par défaut lorsque l’utilisateur parcourt votre site. Vous pouvez également utiliser cette propriété lorsque vous souhaitez _uniquement_ envoyer un événement d’affichage sans dupliquer la récupération des offres.

```js
personalization: {
  defaultPersonalizationEnabled: false
}
```

Cette propriété utilise la logique suivante en fonction de la manière dont elle est définie :

* **Non défini** : demandez une personnalisation par défaut lorsqu’elle n’a pas encore été demandée. La personnalisation par défaut est généralement demandée la première `sendEvent` après le chargement d’une page, puis n’est pas demandée à nouveau lors des appels de `sendEvent` suivants sur la même page. La définition de cette propriété remplace ce comportement.
* **`true`** : demande explicitement la portée de la page et la surface par défaut, même si cette commande de `sendEvent` n’est pas la première après le chargement d’une page. Les moments idéaux pour définir cette propriété sur `true` sont lorsque vous devez forcer une demande de personnalisation par défaut, comme dans les scénarios d’application d’une seule page.
* **`false`** : supprimer explicitement la requête pour l’étendue de la page et la surface par défaut, même si cette commande de `sendEvent` est la première après le chargement d’une page. Les moments idéaux pour définir cette propriété sur `false` sont lorsque vous souhaitez qu’une commande `sendEvent` donnée ne demande pas de nouvelles offres et envoie simplement des données à Analytics ou un événement d’affichage.

## Composants Personalization utilisant l’extension de balise Web SDK

L’équivalent de l’extension de balise Web SDK de cette propriété est la section [**[!UICONTROL Personalization]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) lors de la configuration d’une action « [!UICONTROL Send event] ».
