---
title: personnalisation
description: Effectuez le rendu de différents contenus pour différents utilisateurs et utilisatrices, créant ainsi une expérience personnalisée pour eux.
exl-id: 4bd370c8-8d8d-469e-9666-b5b6d0e3a660
source-git-commit: 54cd49bc1e6f23e3fb6d539274ea16d36ea21386
workflow-type: tm+mt
source-wordcount: '1244'
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

La propriété `surfaces` est un tableau de chaînes [URI de surface](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based-experience/configure-code-based-channel/code-based-surface#surface-uri) qui définissent manuellement le canal, l’appareil ou le contexte pour lequel la personnalisation est demandée. Ils vous permettent de faire la distinction entre différentes expériences digitales, telles que des domaines, des applications ou des plateformes d’appareils au sein de votre écosystème cross-canal. Par défaut, la bibliothèque déduit la surface par défaut de la page active. Vous pouvez utiliser cette propriété pour remplacer la surface déduite automatiquement pour la page active.

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
