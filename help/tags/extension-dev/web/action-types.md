---
title: Types d’actions pour les extensions web
description: Découvrez comment définir un module de bibliothèque de type action pour une extension de balise dans une propriété web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 65%

---

# Types d’actions pour les extensions web

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Un module Bibliothèque de type action est conçu pour exécuter une action prédéfinie. Les effets de cette action ne dépendent que de vous. Voulez-vous envoyer une balise, présenter une offre, remercier l’utilisateur d’avoir visité un site, enregistrer un cookie ou ouvrir une discussion de support technique ?

>[!IMPORTANT]
>
>Ce document couvre les types d’actions pour les extensions web. Si vous développez une extension Edge, reportez-vous au guide sur les [types d’action pour les extensions Edge](../edge/action-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions de balises. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

Par exemple, pour rendre le message configurable par l’utilisateur Adobe Experience Platform, vous pouvez autoriser l’utilisateur à saisir et enregistrer un message dans l’objet settings. L’objet ressemble à ceci :

```json
{
  "message": "Thank you for being one of our VIP members!"
}
```

Pour pouvoir agir sur le message défini par l’utilisateur, votre module doit changer comme suit :

```js
module.exports = function(settings) {
  alert(settings.message);
}
```

## Données contextuelles de l’événement

Un second argument doit ensuite être transmis à votre module contenant les informations contextuelles sur l’événement qui déclenche la règle. Ces informations peuvent être utiles dans certains cas et peuvent être consultées comme suit :

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
