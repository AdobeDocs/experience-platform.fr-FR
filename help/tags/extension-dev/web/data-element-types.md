---
title: Types d’éléments de données pour les extensions web
description: Découvrez comment définir un module Bibliothèque de type élément de données pour une extension de balise dans une propriété web.
exl-id: 3aa79322-2237-492f-82ff-0ba4d4902f70
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 96%

---

# Types d’éléments de données pour les extensions web

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Dans les balises de la collecte de données, les éléments de données sont essentiellement des alias vers des éléments de données sur une page. Ces données se trouvent dans des paramètres de chaîne de requête, des cookies, des éléments DOM ou d’autres emplacements. Un élément de données peut être référencé par des règles et agit comme une abstraction pour l’accès à ces données.

Les types d’éléments de données sont fournis par les extensions et permettent aux utilisateurs de configurer des éléments de données pour accéder à des données d’une manière particulière. Par exemple, une extension peut fournir un type d’élément de données « élément d’enregistrement local » dans lequel l’utilisateur de peut spécifier un nom d’élément d’enregistrement local. Lorsque l’élément de données est référencé par une règle, l’extension peut rechercher la valeur de l’élément d’enregistrement local en utilisant le nom d’élément d’enregistrement local que l’utilisateur a fourni lors de la configuration de l’élément de données.

Ce document explique comment définir des types d’éléments de données pour une extension web dans Adobe Experience Platform.

>[!IMPORTANT]
>
>Si vous développez une extension Edge, reportez-vous au guide sur les [types d’éléments de données pour les extensions Edge](../edge/data-element-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions web. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Les types d’éléments de données sont généralement les suivants :

1. Une [vue](./views.md) affichée dans l’interface utilisateur Experience Platform et l’interface utilisateur de collecte de données qui permet aux utilisateurs de modifier les paramètres de l’élément de données.
2. Un module de bibliothèque émis dans la bibliothèque d’exécution de balise pour interpréter les paramètres et récupérer des éléments de données.

Supposons que vous souhaitiez autoriser les utilisateurs à récupérer cette donnée dans un élément d’enregistrement local nommé `productName`. Votre module peut se présenter comme suit :

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

Si vous souhaitez que le nom de l’élément de stockage local soit configurable par l’utilisateur d’Adobe Experience Platform, vous pouvez autoriser l’utilisateur à saisir un nom puis à l’enregistrer dans l’objet `settings`. L’objet pourrait ressembler à ceci :

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
