---
title: Types d’événements pour les extensions web
description: Découvrez comment définir un module de bibliothèque relatif aux types d’événements pour une extension web dans Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 44%

---

# Types d’événements

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Un module Bibliothèque de type d’événement est conçu pour détecter lorsqu’une activité se produit, puis appeler une fonction pour déclencher une règle associée. L’événement détecté est personnalisable. Il peut détecter lorsqu’un utilisateur fait un certain geste, fait défiler rapidement ou interagit avec quelque chose ?

>[!NOTE]
>
>Ce document suppose que vous connaissez les modules de bibliothèque et leur intégration dans les extensions de balises. Consultez la présentation du [formatage du module de bibliothèque](./format.md) pour une introduction relative à son implémentation avant de revenir à ce guide.

`module.exports` acceptez les paramètres  `settings` et  `trigger` . Cela permet de personnaliser le type d’événement.

```js
module.exports = function(settings, trigger) { … };
```

| Paramètre | Description |
| --- | --- |
| `settings` | Objet contenant tous les paramètres configurés par l’utilisateur dans la vue du type d’événement. Vous avez le contrôle ultime sur ce qui va dans cet objet. |
| `trigger` | Fonction que le module doit appeler chaque fois que la règle doit être déclenchée. Il existe une relation un-à-un entre un objet `settings`, une fonction `trigger` et une règle. Cela signifie que la fonction de déclenchement que vous avez reçue pour une règle ne peut pas être utilisée pour déclencher une autre règle. |

>[!NOTE]
>
>La fonction exportée sera appelée une fois pour chaque règle configurée pour utiliser votre type d’événement.

En prenant comme exemple l’activité de cinq secondes qui s’écoule, après cinq secondes, l’activité a eu lieu et la règle se déclenche. Le module ressemblera à cet exemple.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

Si vous souhaitez que l’utilisateur Adobe Experience Platform puisse configurer la durée, vous avez la possibilité de saisir et d’enregistrer une durée dans l’objet settings. L’objet pourrait ressembler à ceci :

```js
{
  "duration": 25000
}
```

Pour fonctionner sur la durée définie par l’utilisateur, le module doit être mis à jour pour inclure cette durée.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## Transmission de données d’événement contextuelles

Lorsqu’une règle est déclenchée, il est souvent utile de fournir des détails supplémentaires sur l’événement qui s’est produit. Les utilisateurs qui créent des règles peuvent trouver ces informations utiles pour obtenir un certain comportement. Par exemple, si un spécialiste du marketing souhaite créer une règle dans laquelle une balise d’analyse est envoyée chaque fois que l’utilisateur balaie l’écran. L’extension doit fournir un type d’événement `swipe` afin que le marketeur puisse utiliser ce type d’événement pour déclencher la règle appropriée. En supposant que le spécialiste du marketing souhaite inclure l’angle auquel le glissement s’est produit sur la balise, cela serait difficile à faire sans fournir d’informations supplémentaires. Pour fournir des informations supplémentaires sur l’événement qui s’est produit, transmettez un objet lors de l’appel de la fonction `trigger`. Par exemple :

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

Le spécialiste marketing peut alors utiliser cette valeur sur une balise d’analyse en spécifiant la valeur `%event.swipeAngle%` dans un champ de texte. Il peut également accéder à `event.swipeAngle` à partir d’autres contextes (comme une action de code personnalisée). Il est possible d’inclure d’autres types d’informations d’événement facultatives qui peuvent être utiles à un marketeur de la même manière.

### [!DNL nativeEvent]

Si votre type d’événement est basé sur un événement natif (par exemple, si votre extension a fourni un type d’événement `click` ), il est recommandé de définir la propriété `nativeEvent` comme suit.

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

Cela peut s’avérer utile pour les spécialistes marketing qui tentent d’accéder à des informations provenant de l’événement natif, telles que les coordonnées du curseur.

### [!DNL element]

S’il existe une relation forte entre un élément et l’événement qui s’est produit, il est recommandé de définir la propriété `element` sur le noeud DOM de l’élément. Par exemple, si votre extension fournit un type d’événement `click` et que vous autorisez les spécialistes marketing à le configurer afin que la règle ne se déclenche que si un élément avec l’ID `herobanner` est sélectionné. Dans ce cas, si l’utilisateur sélectionne la bannière principale, il est recommandé d’appeler `trigger` et de définir `element` sur le noeud DOM de la bannière principale.

```js
trigger({
  element: element // the value would be the DOM node
});
```

## Respect de l’ordre des règles

Les balises dans Adobe Experience Platform permettent aux utilisateurs de classer des règles. Par exemple, un utilisateur peut créer deux règles qui utilisent toutes deux le type d’événement orientation-changement et pour personnaliser l’ordre dans lequel les règles se déclenchent. En supposant que l’utilisateur Adobe Experience Platform spécifie une valeur de commande `2` pour l’événement de changement d’orientation dans la règle A et une valeur de commande `1` pour l’événement de changement d’orientation dans la règle B. Cela indique que lorsque l’orientation change sur un appareil mobile, la règle B doit se déclencher avant la règle A (les règles dont les valeurs d’ordre sont inférieures se déclenchent en premier).

Comme mentionné précédemment, la fonction exportée dans notre module d’événement sera appelée une fois pour chaque règle configurée pour utiliser notre type d’événement. Chaque fois que la fonction exportée est appelée, elle transmet une fonction `trigger` unique liée à une règle spécifique. Dans le scénario qui vient d’être décrit, notre fonction exportée sera appelée une fois avec une fonction `trigger` liée à la règle B, puis une autre fois avec une fonction `trigger` liée à la règle A. La règle B est appelée en premier parce que l’utilisateur lui a donné une valeur d’ordre inférieure à la règle A. Lorsque notre module de bibliothèque détecte un changement d’orientation, il est important d’appeler les fonctions `trigger` dans l’ordre dans lequel elles ont été fournies au module de bibliothèque.

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
