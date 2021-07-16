---
title: Types de conditions pour les extensions web
description: Découvrez comment définir un module de bibliothèque de type condition pour une extension de balise dans une propriété web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 86%

---

# Types de conditions pour les extensions web

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Un module de bibliothèque de type de condition a un seul objectif : évaluer si quelque chose est vrai ou faux. Ce qu’il évalue ne dépend que de vous.

>[!NOTE]
>
>Ce document couvre les types de conditions pour les extensions web. Si vous développez une extension Edge, reportez-vous au guide sur les [types de condition pour les extensions Edge](../edge/condition-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions de balises. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Par exemple, si vous souhaitez évaluer si l’utilisateur se trouve sur l’hôte `example.com`, votre module peut se présenter comme suit :

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

Maintenant, imaginez une situation où vous souhaitez rendre le nom d’hôte configurable par l’utilisateur Adobe Experience Platform Vous pouvez autoriser l’utilisateur à saisir un nom d’hôte, puis enregistrer ce dernier dans l’objet settings. L’objet pourrait ressembler à ceci :

```js
{
  "hostname": "example.com"
}
```

Pour fonctionner sur le nom d’hôte défini par l’utilisateur, votre module doit changer de la façon suivante :

```js
module.exports = function(settings) {
  return document.location.hostname === settings.hostname;
};
```

## Données contextuelles de l’événement

Un second argument qui contient des informations contextuelles concernant l’événement qui a déclenché la règle est transmis à votre module. Ces informations peuvent être utiles dans certains cas et peuvent être consultées comme suit :

```js
module.exports = function(settings, event) {
  // event contains information regarding the event that fired the rule
};
```

L’objet `event` doit contenir les propriétés suivantes :

| Propriété | Description |
| --- | --- |
| `$type` | Chaîne décrivant le nom de l’extension et le nom de l’événement, joints à l’aide d’un point. Par exemple : `youtube.play`. |
| `$rule` | Objet contenant des informations sur la règle en cours d’exécution. L’objet doit contenir les sous-propriétés suivantes :<ul><li>`id` : ID de la règle en cours d’exécution.</li><li>`name` : nom de la règle en cours d’exécution.</li></ul> |

L’extension fournissant le type d’événement qui a déclenché la règle peut éventuellement ajouter toute autre information utile à cet objet `event`.
