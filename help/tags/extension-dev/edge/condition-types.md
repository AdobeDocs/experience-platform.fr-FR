---
title: Types de conditions pour les extensions Edge
description: Découvrez comment définir un module de bibliothèque relatif aux types de conditions pour une extension Edge dans Adobe Experience Platform.
exl-id: fe13420e-ffa7-49d6-92c4-965ebd9d7390
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 94%

---

# Types de conditions pour les extensions Edge

>[!NOTE]
>
> Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Dans une règle de balise, une condition est évaluée suite à l’apparition d’un événement. Toutes les conditions doivent renvoyer la valeur vraie pour que la règle continue son traitement. Les types de conditions sont fournis par les extensions et évaluent si un élément est vrai ou faux, renvoyant une valeur booléenne.

Par exemple, une extension peut fournir un type de condition « viewport contains » dans lequel l’utilisateur peut spécifier un sélecteur CSS. Lorsque la condition est évaluée sur le site web du client, l’extension peut trouver des éléments correspondant au sélecteur CSS et renvoyer si la fenêtre d’affichage de l’utilisateur contient l’un d’entre eux.

Ce document explique comment définir des types de conditions pour une extension Edge dans Adobe Experience Platform.

>[!IMPORTANT]
>
>Si vous développez une extension web, consultez le guide sur [les types de condition pour les extensions web](../web/condition-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions Edge. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Les types de conditions se composent généralement des éléments suivants :

1. Vue affichée dans l’interface utilisateur de l’Experience Platform et dans l’interface utilisateur de collecte de données qui permet aux utilisateurs de modifier les paramètres de la condition.
2. Un module de bibliothèque émis dans la bibliothèque d’exécution de balise pour interpréter les paramètres et évaluer une condition.

Par exemple, si vous souhaitez évaluer si l’utilisateur se trouve sur l’hôte `example.com`, votre module pourra ressembler à ceci.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

Si vous souhaitez que le nom d’hôte soit configurable par l’utilisateur pour autoriser la saisie d’un nom d’hôte et l’enregistrer dans l’objet Paramètres, l’objet peut ressembler à cet exemple.

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
