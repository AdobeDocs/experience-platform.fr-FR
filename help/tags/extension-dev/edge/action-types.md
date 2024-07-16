---
title: Types d’actions pour les extensions Edge
description: Découvrez comment définir un module de bibliothèque de type action pour une extension de balise dans une propriété edge.
exl-id: c0b058aa-f0fe-4fd8-a873-018482c3e4db
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 94%

---

# Types d’actions pour les extensions Edge

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Dans une règle de balise, une action est exécutée après que les conditions de la règle ont satisfait à lʼévaluation. Les types dʼactions sont fournis par les extensions et leurs effets sont entièrement définis par lʼauteur de lʼextension.

Par exemple, une extension peut fournir un type d’action « show support chat » qui peut afficher une boîte de dialogue de conversation d’assistance pour aider les utilisateurs qui ont du mal à payer leur commande.

Ce document explique comment définir des types dʼaction pour une extension Edge dans Adobe Experience Platform.

>[!IMPORTANT]
>
>Si vous développez une extension web, reportez-vous au guide sur les [types d’action pour les extensions web](../web/action-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions Edge. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Les types d’actions sont généralement les suivants :

1. Vue affichée dans l’interface utilisateur de l’Experience Platform et dans l’interface utilisateur de collecte de données qui permet aux utilisateurs de modifier les paramètres de l’action.
2. Un module de bibliothèque émis dans la bibliothèque d’exécution de balise pour interpréter les paramètres et effectuer une action.

Par exemple, un module permettant de transférer certaines données vers un point d’entrée tiers peut ressembler à ceci.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  return fetch('http://someendpoint.com', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

Si vous souhaitez que le point d’entrée soit configurable par l’utilisateur et permettre l’entrée et la persistance d’un point d’entrée dans l’objet settings du module, l’objet ressemblera à ce qui suit.

```json
{
  "endpoint": "http://someendpoint.com"
}
```

Pour pouvoir agir sur le point d’entrée défini par l’utilisateur, votre module doit être transformé de façon à correspondre à l’exemple qui suit.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  const  { endpoint } = settings;
  return fetch(endpoint, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

## Résultat de l’action

Le résultat renvoyé par un module d’action peut être n’importe quel résultat. Si l’action doit exécuter une tâche asynchrone, vous pouvez renvoyer une [promesse](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise) qui renvoie le résultat souhaité une fois qu’elle a été résolue.

Le résultat de l’action est stocké dans une clé `ruleStash` qui est mise à la disposition de tous les modules via le paramètre `context` (`context.arc.ruleStash`). Vous pouvez en savoir plus sur `ruleStash` [ici](./context.md#rulestash).
