---
title: Types dʼéléments de données pour les extensions Edge
description: Découvrez comment définir un module de bibliothèque de type élément de données pour une extension de balise dans une propriété Edge.
exl-id: ddbc3912-1c25-4d21-bde8-e40e583b4278
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 94%

---

# Types d’éléments de données dans les extensions Edge

Dans les balises, les éléments de données sont des alias de données sur une page web ou mobile, quel que soit l’emplacement de ces données dans l’événement reçu par le serveur. Un élément de données peut être référencé par des règles et agit comme une abstraction pour l’accès à ces données. À l’avenir, lors du changement d’emplacement des données (notamment en cas de modification de la clé de l’événement contenant la valeur), un seul élément de données pourra être reconfiguré tandis que toutes les règles référençant cet élément de données pourront rester inchangées.

Les types d’éléments de données sont fournis par les extensions. L’auteur de l’extension détermine la manière dont cet élément de données est récupéré. Par exemple, vous pouvez utiliser un type d’élément de données pour permettre aux utilisateurs d’Adobe Experience Platform de récupérer un élément de données de la couche XDM ou de leur couche de données personnalisée.

Ce document explique comment définir des types d’éléments de données pour une extension Edge dans Adobe Experience Platform.

>[!IMPORTANT]
>
>Si vous développez une extension web, reportez-vous au guide sur les [types d’éléments de données pour les extensions web](../web/data-element-types.md) à la place.
>
>Ce document suppose également que vous connaissez les modules de bibliothèque et leur intégration dans les extensions Edge. Si vous avez besoin d’une introduction, consultez la présentation sur le [formatage des modules de bibliothèque](./format.md) avant de revenir à ce guide.

Les types d’éléments de données sont généralement les suivants :

1. Une vue affichée dans l’interface utilisateur d’Experience Platform et l’interface utilisateur de la collecte de données qui permet aux utilisateurs de modifier les paramètres de l’élément de données.
2. Un module de bibliothèque émis dans la bibliothèque d’exécution de balise pour interpréter les paramètres et récupérer des éléments de données.

Si vous souhaitez permettre aux utilisateurs de récupérer un élément de donnée de la couche de données personnalisée, votre module peut ressembler à cet exemple.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Si vous souhaitez que les données renvoyées pour la couche de données puissent être configurées par lʼutilisateur dʼAdobe Experience Platform, vous pouvez autoriser lʼutilisateur à saisir un nom clé puis à enregistrer le nom dans lʼobjet `settings`. Lʼobjet pourrait ressembler à ceci.

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
