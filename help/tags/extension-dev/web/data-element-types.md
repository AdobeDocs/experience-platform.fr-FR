---
title: Types d’éléments de données pour les extensions web
description: Découvrez comment définir un module Bibliothèque de type élément de données pour une extension de balise dans une propriété web.
exl-id: 3aa79322-2237-492f-82ff-0ba4d4902f70
TQID: https://experienceleague.adobe.com/3-r4TB78yu-NQ1yxOHRjy8IO-NSWyPHCmmectAD5ib8
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dfc56824-e8b9-499e-85d4-21aedb507314id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: b64298cc-90cc-46b7-8917-ee391f1c7516id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: f6ff4d13-7b5c-4533-8556-95e76673d4cbid: f9a2105e-7a47-4e85-9193-31a519a2cb83
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 559
ht-degree: 96%

---

# Types d’éléments de données pour les extensions web

Dans les balises de la collecte de données, les éléments de données sont essentiellement des alias vers des éléments de données sur une page. Ces données se trouvent dans des paramètres de chaîne de requête, des cookies, des éléments DOM ou d’autres emplacements. Un élément de données peut être référencé par des règles et agit comme une abstraction pour l’accès à ces données.

Les types d’éléments de données sont fournis par les extensions et permettent aux utilisateurs de configurer des éléments de données pour accéder à des données d’une manière particulière. Par exemple, une extension peut fournir un type d’élément de données « élément d’enregistrement local » dans lequel l’utilisateur de peut spécifier un nom d’élément d’enregistrement local. Lorsque l’élément de données est référencé par une règle, l’extension peut rechercher la valeur de l’élément d’enregistrement local en utilisant le nom d’élément d’enregistrement local que l’utilisateur a fourni lors de la configuration de l’élément de données.

Ce document explique comment définir des types d’éléments de données pour une extension web dans Adobe Experience Platform.

>[!IMPORTANT]
>
>Si vous développez une extension Edge, reportez-vous au guide sur les [types d’éléments de données pour les extensions Edge](../edge/data-element-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions web. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Les types d’éléments de données sont généralement les suivants :

1. Une [vue](./views.md) affichée dans l’interface utilisateur d’Experience Platform et l’interface utilisateur de la collecte de données, qui permet aux utilisateurs de modifier les paramètres de l’élément de données.
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
