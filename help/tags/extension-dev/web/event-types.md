---
title: Types d’événements pour les extensions web
description: Découvrez comment définir un module de bibliothèque relatif aux types d’événements pour une extension web dans Adobe Experience Platform.
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 97%

---

# Types d’événement pour les extensions web

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Dans une règle de balise, un événement est une activité qui doit se produire pour qu’une règle se déclenche. Par exemple, une extension web peut fournir un type d’événement « mouvement » qui surveille un certain mouvement de souris ou de toucher. Une fois le mouvement effectué, la logique de l’événement déclenche la règle.

Un module Bibliothèque de type d’événement est conçu pour détecter lorsqu’une activité se produit, puis appeler une fonction pour déclencher une règle associée. L’événement détecté est personnalisable. Il peut par exemple détecter un certain mouvement de la part d’un utilisateur, un défilement rapide ou une interaction avec quelque chose.

Ce document explique comment définir des types d’événements pour une extension web dans Adobe Experience Platform.

>[!NOTE]
>
>Ce document suppose que vous connaissez les modules de bibliothèque et leur intégration dans les extensions web. Consultez la présentation du [formatage du module de bibliothèque](./format.md) pour une introduction relative à son implémentation avant de revenir à ce guide.

Les types d’événements sont définis par des extensions et se composent généralement des éléments suivants :

1. [view](./views.md) affiché dans l’interface utilisateur de l’Experience Platform et dans l’interface utilisateur de collecte de données qui permet aux utilisateurs de modifier les paramètres de l’événement.
2. Un module de bibliothèque émis dans la bibliothèque d’exécution de balise pour interpréter les paramètres et surveiller l’apparition d’une certaine activité.

`module.exports` acceptez les paramètres `settings` et `trigger`. Cela permet de personnaliser le type d’événement.

```js
module.exports = function(settings, trigger) { … };
```

| Paramètre | Description |
| --- | --- |
| `settings` | Objet contenant tous les paramètres configurés par l’utilisateur dans la vue du type d’événement. Vous avez le contrôle ultime sur ce qui va dans cet objet. |
| `trigger` | Fonction que le module doit appeler chaque fois que la règle doit être déclenchée. Il existe une relation de type « un à un » entre un objet `settings`, une fonction `trigger` et une règle. En d’autres termes, la fonction de déclenchement que vous avez reçue pour une règle ne peut pas être utilisée pour déclencher une autre règle. |

>[!NOTE]
>
>La fonction exportée sera appelée une fois pour chaque règle configurée pour utiliser votre type d’événement.

En prenant comme exemple l’activité de cinq secondes qui s’écoule, après cinq secondes, l’activité a eu lieu et la règle se déclenche. Le module ressemblera à cet exemple.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

Si vous souhaitez que l’utilisateur Adobe Experience Platform puisse configurer la durée, il est nécessaire d’ajouter la possibilité de saisir et d’enregistrer une durée à l’objet settings. L’objet pourrait ressembler à ceci :

```js
{
  "duration": 25000
}
```

Pour fonctionner selon la durée définie par l’utilisateur, notre module devrait être modifié pour devenir ceci :

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## Transmission de données d’événement contextuelles

Lorsqu’une règle est déclenchée, il est souvent utile de fournir des détails supplémentaires sur l’événement qui s’est produit. Les utilisateurs qui créent des règles peuvent trouver ces informations utiles pour obtenir un certain comportement. Supposons, par exemple, qu’un spécialiste marketing souhaite créer une règle dans laquelle une balise d’analyse est envoyée chaque fois que l’utilisateur balaie l’écran. L’extension doit fournir un type d’événement `swipe` afin que le spécialiste marketing puisse utiliser ce type d’événement pour déclencher la règle appropriée. En supposant que le spécialiste du marketing souhaite inclure l’angle auquel le glissement s’est produit sur la balise, cela serait difficile à faire sans fournir d’informations supplémentaires. Pour fournir des informations supplémentaires sur l’événement qui s’est produit, transmettez un objet lors de l’appel de la fonction `trigger`. Par exemple :

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

Le spécialiste marketing peut alors utiliser cette valeur sur une balise d’analyse en spécifiant la valeur `%event.swipeAngle%` dans un champ de texte. Il peut également accéder à `event.swipeAngle` à partir d’autres contextes (comme une action de code personnalisée). Il est possible d’inclure d’autres types d’informations d’événement facultatives qui peuvent être utiles à un spécialiste du marketing de la même manière.

### [!DNL nativeEvent]

Si votre type d’événement est basé sur un événement natif (par exemple, si votre extension a fourni un type d’événement `click`), nous vous recommandons de définir la propriété `nativeEvent` comme suit :

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

Cela peut s’avérer utile pour les spécialistes marketing qui tentent d’accéder à des informations provenant de l’événement natif, telles que les coordonnées du curseur.

### [!DNL element]

S’il existe une relation forte entre un élément et l’événement qui s’est produit, il est recommandé de définir la propriété `element` sur le nœud DOM de l’élément. Supposons, par exemple, que votre extension fournisse un type d’événement `click` et que vous autorisiez les spécialistes du marketing à le configurer afin que la règle ne se déclenche que si un élément avec l’identifiant de `herobanner` est sélectionné. Dans ce cas, si l’utilisateur sélectionne la bannière principale, il est recommandé d’appeler `trigger` et de définir `element` sur le nœud DOM de la bannière principale.

```js
trigger({
  element: element // the value would be the DOM node
});
```

## Respect de l’ordre des règles

Les balises permettent aux utilisateurs de trier les règles. Par exemple, un utilisateur peut créer deux règles qui utilisent toutes les deux le type d’événement de changement d’orientation et personnaliser l’ordre dans lequel les règles se déclenchent. Supposons que l’utilisateur d’Adobe Experience Platform spécifie une valeur d’ordre de `2` pour l’événement de modification d’orientation dans la règle A et une valeur d’ordre de `1` pour l’événement de modification d’orientation dans la règle B. Ces valeurs indiquent que lorsque l’orientation change sur un appareil mobile, la règle B doit se déclencher avant la règle A (les règles avec les plus petites valeurs d’ordre se déclenchent en premier).

Comme mentionné précédemment, la fonction exportée dans notre module d’événement sera appelée une fois pour chaque règle configurée pour utiliser notre type d’événement. Chaque fois que la fonction exportée est appelée, elle transmet une fonction `trigger` unique liée à une règle spécifique. Dans le scénario qui vient d’être décrit, notre fonction exportée sera appelée une fois avec une fonction `trigger` liée à la règle B, puis une autre fois avec une fonction `trigger` liée à la règle A. La règle B est appelée en premier parce que l’utilisateur lui a donné une valeur d’ordre inférieure à la règle A. Lorsque notre module de bibliothèque détecte une modification d’orientation, il est important d’appeler les fonctions `trigger` dans l’ordre dans lequel elles ont été fournies au module de bibliothèque.

Dans l’exemple de code ci-dessous, notez que lorsqu’un changement d’orientation est détecté, les fonctions de déclenchement sont appelées dans l’ordre selon lequel elles ont été fournies à notre fonction exportée :

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  triggers.forEach(function(trigger) {
    trigger();
  });
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

Cela permet de s’assurer que l’ordre spécifié par l’utilisateur est conservé.

Une implémentation incorrecte serait celle qui appelle les fonctions de déclenchement dans un ordre différent :

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  for (var i = triggers.length - 1; i >= 0; i--) {
    triggers[i]();
  }
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

Les pratiques de programmation naturelle maintiennent généralement l’ordre adéquat, mais il est important de connaître les implications et de les développer en conséquence.
