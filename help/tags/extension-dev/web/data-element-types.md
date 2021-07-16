---
title: Types d’éléments de données pour les extensions web
description: Découvrez comment définir un module de bibliothèque de type élément de données pour une extension de balise dans une propriété web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 70%

---

# Types d’éléments de données pour les extensions Edge

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

L’objectif d’un module de bibliothèque de type élément de données est de récupérer un élément de données. La méthode de cette récupération est personnalisable. Différents types d’éléments de données permettent aux utilisateurs de Adobe Experience Platform de récupérer des données à partir d’un stockage local, d’un cookie ou d’un élément DOM.

>[!IMPORTANT]
>
>Ce document fournit des informations sur les types d’éléments de données pour les extensions web. Si vous développez une extension Edge, reportez-vous au guide sur les [types d’éléments de données pour les extensions Edge](../edge/data-element-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions de balises. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Supposons que vous souhaitiez autoriser les utilisateurs à récupérer cette donnée dans un élément d’enregistrement local nommé `productName`. Votre module peut se présenter comme suit :

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

Si vous souhaitez que l’utilisateur Adobe Experience Platform puisse configurer le nom de l’élément d’enregistrement local, vous pouvez autoriser l’utilisateur à saisir un nom, puis enregistrer le nom dans l’objet `settings` . L’objet pourrait ressembler à ceci :

```js
{
  itemName: "campaignId"
}
```

Pour fonctionner avec le nom d’élément d’enregistrement local défini par l’utilisateur, votre module doit changer comme suit :

```js
module.exports = function(settings) {
  return localStorage.getItem(settings.itemName);
}
```

## Prise en charge de la valeur par défaut

Gardez à l’esprit que les utilisateurs ont la possibilité de configurer une valeur par défaut pour tout élément de données. Si votre module Bibliothèque d’éléments de données renvoie la valeur `undefined` ou `null`, il sera automatiquement remplacé par la valeur par défaut configurée par l’utilisateur pour l’élément de données.

## Données contextuelles de l’événement

Si l’élément de données est récupéré suite au déclenchement d’une règle (par exemple, les éléments de données sont utilisés dans les conditions et les actions de la règle), un second argument sera transmis à votre module, contenant des informations contextuelles concernant l’événement qui a déclenché la règle. Ces informations peuvent être utiles dans certains cas et peuvent être consultées comme suit :

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
