---
title: setVar()
description: Définit une valeur que vous pouvez récupérer ultérieurement à l’aide de getVar().
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# `setVar()`

La méthode `_satellite.setVar()` vous permet de définir une ou plusieurs paires nom/valeur personnalisées qui peuvent ensuite être référencées par [`_satellite.getVar()`](getvar.md).

```ts
// Set a single name/value pair
_satellite.setVar(name: string, value: unknown): void

// Set multiple name/value pairs at once
_satellite.setVar(vars: { [name: string]: unknown }): void;
```

>[!IMPORTANT]
>
>Bien que la méthode `getVar()` puisse récupérer à la fois les éléments de données et les valeurs définis par `setVar()`, ces deux types d’entités sont distincts. L’utilisation de `setVar()` pour définir une valeur portant le même nom qu’un élément de données dans l’interface utilisateur des balises ne la remplace pas.

## Persistance et portée

`setVar()` valeurs ne sont actives que dans la mémoire de la page :

* **Page actuelle uniquement** : les valeurs persistent jusqu’à ce que la page soit déchargée. Dans les applications d’une seule page, elles persistent jusqu’à un rechargement complet ou vous les remplacez/effacez.
* **Pas d’enregistrement du navigateur** : rien n’est écrit dans les cookies, l’enregistrement local ou l’enregistrement de session.

## Valeurs de référence définies à l’aide de `setVar()`

Vous pouvez récupérer des valeurs dans du code personnalisé à l’aide de `getVar()` :

```js
// Set a custom variable using setVar()
_satellite.setVar('Ad location','Banner advertisement');

// Returns the string 'Banner advertisement'
_satellite.getVar('Ad location');
```

Vous pouvez également référencer ces variables dans l’interface utilisateur des balises dans les champs qui prennent en charge la notation des éléments de données :

```text
%Ad location%
```

>[!NOTE]
>
>Si une valeur définie à l’aide de `setVar()` utilise le même nom qu’un élément de données et que vous référencez ce nom dans la notation de l’élément de données, l’élément de données est prioritaire.

## Exemples

```js
// Set a single name/value pair
_satellite.setVar('product', 'Circuit Pro');

// Set multiple name/value pairs at once (same as calling setVar() three times)
_satellite.setVar({ 'title': 'Blinding Light', 'category': 'Game', 'genre': 'Tower defense' });

// Retrieve each value
_satellite.getVar('title'); // Blinding Light
_satellite.getVar('category'); // Game
_satellite.getVar('genre'); // Tower defense
```
