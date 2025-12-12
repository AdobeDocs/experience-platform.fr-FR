---
title: Types de conditions pour les extensions web
description: Découvrez comment définir un module de bibliothèque de types de conditions pour une extension de balise dans une propriété web.
exl-id: db504455-858b-4ac8-aa42-de516b0f1d5a
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 95%

---

# Types de conditions pour les extensions web

Dans le contexte d’une règle, une condition est évaluée une fois qu’un événement s’est produit. Toutes les conditions doivent renvoyer la valeur vraie pour que la règle continue son traitement. Une exception survient lorsque les utilisateurs placent explicitement des conditions dans un compartiment « exception », auquel cas toutes les conditions du compartiment doivent renvoyer la valeur false pour que la règle puisse continuer le traitement.

Par exemple, une extension peut fournir un type de condition « viewport contains » dans lequel l’utilisateur peut spécifier un sélecteur CSS. Lorsque la condition est évaluée sur le site web du client, l’extension peut trouver des éléments correspondant au sélecteur CSS et renvoyer si la fenêtre d’affichage de l’utilisateur contient l’un d’entre eux.

Ce document explique comment définir des types de conditions pour une extension web dans Adobe Experience Platform.

>[!NOTE]
>
>Si vous développez une extension Edge, reportez-vous au guide sur les [types de condition pour les extensions Edge](../edge/condition-types.md) à la place.
>
>Ce document suppose que vous connaissez les modules de bibliothèque et leur intégration dans les extensions web. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Les types de conditions se composent généralement des éléments suivants :

1. Une [vue](./views.md) affichée dans l’interface utilisateur d’Experience Platform et l’interface utilisateur de la collecte de données, qui permet aux utilisateurs de modifier les paramètres de la condition.
2. Un module de bibliothèque émis dans la bibliothèque d’exécution de balise pour interpréter les paramètres et évaluer une condition.

Un module de bibliothèque de type de condition a un seul objectif : évaluer si quelque chose est vrai ou faux. Ce qu’il évalue ne dépend que de vous.

Par exemple, si vous souhaitez évaluer si l’utilisateur se trouve sur l’hôte `example.com`, votre module peut se présenter comme suit :

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

Maintenant, imaginez une situation où vous souhaitez rendre le nom d’hôte configurable par l’utilisateur Adobe Experience Platform Vous pouvez autoriser l’utilisateur à saisir un nom d’hôte, puis enregistrer ce dernier dans l’objet settings. L’objet pourrait ressembler à ceci :

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
