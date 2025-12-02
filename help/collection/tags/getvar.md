---
title: getVar()
description: Renvoie la valeur d’un élément de données ou une valeur définie à l’aide de setVar().
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---

# `getVar()`

La méthode `_satellite.getVar()` renvoie la valeur actuelle d’un [élément de données](/help/tags/ui/managing-resources/data-elements.md) ou une valeur définie à l’aide de [`_satellite.setVar()`](setvar.md). Si un élément de données et une valeur de `setVar()` partagent le même nom, l’élément de données est prioritaire. Si vous appelez un identifiant de chaîne qui n’existe pas encore, la méthode renvoie `undefined`. L’évaluation est synchrone.

```js
_satellite.getVar(name: string, event?: unknown) => unknown
```

La valeur renvoyée et le type dépendent du type d’élément de données que vous référencez. Par exemple, si vous appelez `getVar()` qui récupère une variable de chaîne, le type renvoyé est `string`. Si vous appelez `getVar()` qui renvoie un élément de données de variable Web SDK, le type renvoyé est une `object` contenant toutes les propriétés définies dans cette variable.

```js
// Retrieves the value in the `Example` data element
_satellite.getVar('Example');

// Execute custom logic depending on the numeric value in the `cartTotal` data element
const cartValue = Number(_satellite.getVar('cartTotal'));
if (cartValue > 100) {
  _satellite.logger.info('Purchase larger than $100 detected');
}

// Some data elements like Web SDK variables support deeply nested properties
const pageName = _satellite.getVar('Data layer')?.web?.webPageDetails?.name;
if (!pageName) {
  _satellite.logger.warn('Page name is not set');
}

// Custom code data elements support a second argument
// Works in a Launch custom code block where `event` is provided by the rule engine.
const rule = _satellite.getVar('Return event rule', event);
```

## Champs disponibles

La méthode `getVar()` prend en charge deux arguments. La plupart des cas d’utilisation n’incluent pas le deuxième argument facultatif.

| Nom | Type | Obligatoire | Description |
| --- | --- | --- | --- |
| **`name`** | `string` | Oui | Nom de l’élément de données à récupérer. Les noms des éléments de données respectent la casse. |
| **`event`** | `object` | Non | Contexte de l&#39;événement à partir de la règle de déclenchement. Utilisé uniquement dans des cas d’utilisation avancés par des éléments de données utilisant des [code personnalisé](/help/tags/ui/managing-resources/data-elements.md#custom-code) ou des extensions personnalisées. Lorsqu’une règle est déclenchée par un événement (tel qu’un clic, un envoi de formulaire ou une répartition JavaScript personnalisée), l’objet d’événement associé est inclus ici. Les éléments de données peuvent utiliser ces informations pour renvoyer des valeurs contextuelles, telles que les détails ou les propriétés de l’élément sur lequel l’utilisateur a cliqué, à partir d’un événement personnalisé. |
