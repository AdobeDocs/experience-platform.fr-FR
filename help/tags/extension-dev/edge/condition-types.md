---
title: Types de conditions pour les extensions Edge
description: Découvrez comment définir un module de bibliothèque relatif aux types de conditions pour une extension Edge dans Adobe Experience Platform.
exl-id: fe13420e-ffa7-49d6-92c4-965ebd9d7390
TQID: https://experienceleague.adobe.com/SPttAK4vfKt3bF9Dg07AANrWe1koxAhCYU1Y3aLGPrQ
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6id: b64298cc-90cc-46b7-8917-ee391f1c7516id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 369
ht-degree: 94%

---

# Types de conditions pour les extensions Edge

Dans une règle de balise, une condition est évaluée suite à l’apparition d’un événement. Toutes les conditions doivent renvoyer la valeur vraie pour que la règle continue son traitement. Les types de conditions sont fournis par les extensions et évaluent si un élément est vrai ou faux, renvoyant une valeur booléenne.

Par exemple, une extension peut fournir un type de condition « viewport contains » dans lequel l’utilisateur peut spécifier un sélecteur CSS. Lorsque la condition est évaluée sur le site web du client, l’extension peut trouver des éléments correspondant au sélecteur CSS et renvoyer si la fenêtre d’affichage de l’utilisateur contient l’un d’entre eux.

Ce document explique comment définir des types de conditions pour une extension Edge dans Adobe Experience Platform.

>[!IMPORTANT]
>
>Si vous développez une extension web, consultez le guide sur [les types de condition pour les extensions web](../web/condition-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions Edge. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Les types de conditions se composent généralement des éléments suivants :

1. Une vue affichée dans l’interface utilisateur d’Experience Platform et l’interface utilisateur de la collecte de données qui permet aux utilisateurs de modifier les paramètres de la condition.
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
