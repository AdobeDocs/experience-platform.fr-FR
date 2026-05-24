---
title: Types d’actions pour les extensions Edge
description: Découvrez comment définir un module de bibliothèque de type action pour une extension de balise dans une propriété edge.
exl-id: c0b058aa-f0fe-4fd8-a873-018482c3e4db
TQID: https://experienceleague.adobe.com/qzGN76aYVBTkwpg5Kvl-itWtvOlecfyyN0mFkgff6So
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6id: b64298cc-90cc-46b7-8917-ee391f1c7516id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 344
ht-degree: 93%

---

# Types d’actions pour les extensions Edge

Dans une règle de balise, une action est exécutée après que les conditions de la règle ont satisfait à lʼévaluation. Les types dʼactions sont fournis par les extensions et leurs effets sont entièrement définis par lʼauteur de lʼextension.

Par exemple, une extension peut fournir un type d’action « show support chat » qui peut afficher une boîte de dialogue de conversation d’assistance pour aider les utilisateurs qui ont du mal à payer leur commande.

Ce document explique comment définir des types dʼaction pour une extension Edge dans Adobe Experience Platform.

>[!IMPORTANT]
>
>Si vous développez une extension web, reportez-vous au guide sur les [types d’action pour les extensions web](../web/action-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions Edge. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Les types d’actions sont généralement les suivants :

1. Une vue affichée dans l’interface utilisateur d’Experience Platform et l’interface utilisateur de la collecte de données qui permet aux utilisateurs de modifier les paramètres de l’action.
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
