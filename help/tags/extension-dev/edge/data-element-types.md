---
title: Types dʼéléments de données pour les extensions Edge
description: Découvrez comment définir un module de bibliothèque de type élément de données pour une extension de balise dans une propriété Edge.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 46%

---

# Types d’éléments de données dans les extensions Edge

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Un module de bibliothèque de type élément de données récupère un élément de données. L’auteur du module détermine la manière dont cet élément de données est récupéré. Par exemple, vous pouvez utiliser un type d’élément de données pour permettre aux utilisateurs de Adobe Experience Platform de récupérer un élément de données de la couche XDM ou de leur couche de données personnalisée.

>[!IMPORTANT]
>
>Ce document couvre les types d’éléments de données pour les extensions Edge. Si vous développez une extension web, reportez-vous au guide sur les [types d’éléments de données pour les extensions web](../web/data-element-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions de balises. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Si vous souhaitez permettre aux utilisateurs de récupérer une donnée de la couche de données personnalisée, votre module peut ressembler à cet exemple.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Si vous souhaitez que les données renvoyées pour la couche de données puissent être configurées par l’utilisateur de Adobe Experience Platform, vous pouvez autoriser l’utilisateur à saisir un nom clé, puis enregistrer le nom dans l’objet `settings`. L&#39;objet pourrait ressembler à ceci.

```js
{
  keyName: "campaignId"
}
```

Pour fonctionner avec le nom d’élément d’enregistrement local défini par l’utilisateur, votre module doit changer comme suit :

```js
module.exports = (context) => {
  const data = context.arc.event.data;
  return data[keyName];
};
```

## Contexte du module Bibliothèque

Tous les modules d’éléments de données ont accès à une variable `context` fournie lors de l’appel du module. Vous pouvez en savoir plus [ici](./context.md).
