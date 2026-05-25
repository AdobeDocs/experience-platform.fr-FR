---
title: setVar()
description: Définit une valeur que vous pouvez récupérer ultérieurement à l’aide de getVar().
exl-id: b73e1f1e-4675-4086-ac9c-96be549a8588
TQID: https://experienceleague.adobe.com/773o0s4qnuf3LGvdovgpm8OtSQI7jtWI61vua1sBMG0
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 209
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

>[!NOTE]
>
>Évitez d’utiliser des points (`.`) lors de la définition de noms de variable à l’aide de cette méthode. La méthode `getVar()` ne reconnaît pas les variables qui contiennent des périodes définies à l’aide de `setVar()`. Toutefois, `getVar()` _reconnaît_ les éléments de données qui utilisent des périodes lorsqu’ils sont définis dans l’interface utilisateur des balises.
