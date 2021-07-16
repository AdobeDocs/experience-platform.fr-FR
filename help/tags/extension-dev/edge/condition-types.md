---
title: Types de conditions pour les extensions Edge
description: Découvrez comment définir un module de bibliothèque relatif aux types de conditions pour une extension Edge dans Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 63%

---

# Types de conditions pour les extensions Edge

>[!NOTE]
>
> Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Un module de bibliothèque de type condition évalue si un élément est vrai ou faux et renvoie une valeur booléenne.

>[!IMPORTANT]
>
>Ce document couvre les types de condition pour les extensions edge. Si vous développez une extension web, consultez le guide sur [les types de condition pour les extensions web](../web/condition-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions de balises. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Par exemple, si vous souhaitez évaluer si l’utilisateur se trouve sur l’hôte `example.com`, votre module peut ressembler à ceci.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

Si vous souhaitez que le nom d’hôte soit configurable par l’utilisateur pour autoriser la saisie d’un nom d’hôte et l’enregistrer dans l’objet settings, l’objet peut ressembler à cet exemple.

```js
{
  "hostname": "example.com"
}
```

Pour fonctionner sur le nom d’hôte défini par l’utilisateur, votre module doit changer de la façon suivante :

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith(settings.hostname);
};
```

## Résultat de la condition

Le résultat renvoyé par un module de condition peut être l’un des suivants :

1. Valeur booléenne (`true` ou `false`).
1. Une [promesse](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise) qui, une fois résolue, renvoie une valeur booléenne.

## Contexte du module Bibliothèque

Tous les modules de condition ont accès à une variable `context` fournie lors de l’appel du module. Vous pouvez en savoir plus [ici](./context.md).
