---
title: subscribeRulesetItems
description: Abonnez-vous aux cartes de contenu pour une surface spécifique à l’aide de la commande subscribeRulesetItems .
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 4%

---

# `subscribeRulesetItems`

La commande `subscribeRulesetItems` vous permet de vous abonner à des propositions qui sont le résultat d’ensembles de règles satisfaits. Pour ce faire, spécifiez les surfaces et les schémas en fonction desquels filtrer et fournissez une fonction de rappel.

Chaque fois que des ensembles de règles sont évalués, la fonction de rappel reçoit un objet `result` contenant un tableau de propositions.

>[!IMPORTANT]
>
>La commande `subscribeRulesetItems` est la seule façon d’obtenir des propositions provenant d’ensembles de règles, puisqu’elles ne sont pas renvoyées avec des résultats [`sendEvent`](sendevent/overview.md).


```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://example.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```

Le code ci-dessus s’abonne à la surface `web://example.com/#welcome` pour les cartes de contenu et utilise la méthode pratique `collectEvent` pour émettre des événements `display` pour toutes les propositions.

## Options de la commande {#command-options}

Cette commande prend un objet `options` avec les propriétés suivantes :

| Propriété | Type | Description |
| --- | --- | --- |
| `surfaces` | Tableau de chaînes | Une liste de surfaces. Les propositions ne sont reçues par la fonction de rappel que si elles correspondent à l’une des surfaces fournies ici. |
| `schemas` | Tableau de chaînes | Une liste de schémas. Les propositions ne sont reçues par la fonction de rappel que si elles correspondent à l’un des schémas fournis ici. |
| `callback` | Fonction | Une fonction de rappel qui sera appelée lorsque les propositions sont le résultat de jeux de règles satisfaits. La fonction de rappel reçoit deux paramètres lorsqu’elle est appelée : `result` et `collectEvent`. Voir [paramètres de rappel](#callback-parameters) pour plus d’informations. |

### Paramètres de rappel {#callback-parameters}

Lorsqu’elle est appelée, la fonction de rappel reçoit les deux paramètres décrits dans le tableau ci-dessous.

| Paramètre | Type | Description |
| --- | --- | --- |
| `result` | Objet | Cet objet contient un tableau `propositions`.  Ces propositions sont le résultat direct d’ensembles de règles satisfaits. L’objet `result` est structuré de la même manière que l’objet [result](command-responses.md) renvoyé par `sendEvent` à l’aide d’une clause `then`. |
| `collectEvent` | Fonction | Fonction pratique que vous pouvez utiliser pour envoyer des événements Edge Network afin de suivre les interactions, les affichages et d’autres événements. |

### Fonction `collectEvent` {#collectevent-function}

La fonction `collectEvent` est une fonction pratique que vous pouvez utiliser pour envoyer des événements Edge Network afin de suivre les interactions, les affichages et d’autres événements. Il accepte les deux paramètres décrits dans le tableau ci-dessous.

| Paramètre | Type | Description |
| --- | --- | --- |
| Type d’événement | Chaîne | Chaîne indiquant le type d’événement de proposition à émettre. Les types d’événements pris en charge sont `display`, `interact` ou `dismiss`. |
| `propositions` | Tableau | Tableau de propositions correspondant à l’événement. |

## Abonnement aux cartes de contenu à l’aide de l’extension de balise Web SDK

L’extension de balise Web SDK équivalente aux réponses de commande est une règle qui s’abonne à l’événement [**[!UICONTROL Subscribe ruleset items]**](/help/tags/extensions/client/web-sdk/event-types.md#subscribe-ruleset-items). L’événement vous permet de fournir les schémas et surfaces souhaités.
