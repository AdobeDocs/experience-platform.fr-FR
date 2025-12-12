---
title: Types d’actions pour les extensions web
description: Découvrez comment définir un module Bibliothèque de type action pour une extension de balise dans une propriété web.
exl-id: d4539132-a72c-40b0-84b6-50cbe3785d2d
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 94%

---

# Types d’actions pour les extensions web

Dans le contexte des balises de collecte de données, une action est exécutée après qu’un événement de règle s’est produit et que toutes les conditions ont réussi l’évaluation.

Par exemple, une extension peut fournir un type d’action « show support chat » qui peut afficher une boîte de dialogue de conversation d’assistance pour aider les utilisateurs qui ont du mal à payer leur commande.

Ce document explique comment définir des types d’action pour une extension web dans Adobe Experience Platform.

>[!IMPORTANT]
>
>Ce document couvre les types d’actions pour les extensions web. Si vous développez une extension Edge, reportez-vous au guide sur les [types d’action pour les extensions Edge](../edge/action-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions web. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Les types d’actions sont généralement les suivants :

1. Une [vue](./views.md) affichée dans l’interface utilisateur d’Experience Platform et l’interface utilisateur de la collecte de données, qui permet aux utilisateurs de modifier les paramètres de l’action.
2. Un module de bibliothèque émis dans la bibliothèque d’exécution de balise pour interpréter les paramètres et effectuer une action.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

Par exemple, pour rendre le message configurable par l’utilisateur d’Adobe Experience Platform, vous pouvez autoriser ce dernier à saisir et enregistrer un message dans l’objet settings. L’objet ressemble à ceci :

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

Un second argument doit ensuite être transmis à votre module contenant les informations contextuelles à propos de l’événement qui déclenche la règle. Ces informations peuvent être utiles dans certains cas et peuvent être consultées comme suit :

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
