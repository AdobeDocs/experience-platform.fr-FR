---
title: Types d’actions pour les extensions Edge
description: Découvrez comment définir un module de bibliothèque de type action pour une extension de balise dans une propriété edge.
source-git-commit: 99780f64c8f09acea06e47ebf5cabc762e05cab2
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 45%

---

# Types d’actions pour les extensions Edge

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Dans une règle de balise, une action est exécutée une fois que les conditions de règle ont réussi l’évaluation. Les types d’actions sont fournis par des extensions et leurs effets sont entièrement définis par l’auteur de l’extension.

Par exemple, une extension peut fournir un type d’action « show support chat » qui peut afficher une boîte de dialogue de conversation d’assistance pour aider les utilisateurs qui ont du mal à payer leur commande.

Ce document explique comment définir des types d’action pour une extension Edge dans Adobe Experience Platform.

>[!IMPORTANT]
>
>Si vous développez une extension web, reportez-vous au guide sur les [types d’action pour les extensions web](../web/action-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions Edge. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Les types d’actions sont généralement les suivants :

1. Vue affichée dans l’interface utilisateur de la collecte de données qui permet aux utilisateurs de modifier les paramètres de l’action.
2. Module de bibliothèque émis dans la bibliothèque du runtime de balises pour interpréter les paramètres et effectuer une action.

Par exemple, un module permettant de transférer certaines données vers un point de terminaison tiers peut ressembler à ceci.

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

Si vous souhaitez que le point de terminaison soit configurable par l’utilisateur et permettre l’entrée et la persistance d’un point de terminaison dans l’objet settings du module, l’objet ressemblerait à cela.

```json
{
  "endpoint": "http://someendpoint.com"
}
```

Pour fonctionner sur le point d’entrée défini par l’utilisateur, votre module doit passer à l’exemple suivant.

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
