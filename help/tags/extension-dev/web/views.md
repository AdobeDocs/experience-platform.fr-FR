---
title: Vues dans les extensions web
description: 'Découvrez comment définir des vues pour les modules de bibliothèque dans vos extensions web Adobe Experience Platform '
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '2062'
ht-degree: 77%

---

# Vues dans les extensions web

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Chaque type d’événement, de condition, d’action ou d’élément de données peut fournir une vue permettant à un utilisateur de fournir des paramètres. L’extension peut également avoir une [vue de configuration d’extension](../configuration.md) de niveau supérieur permettant aux utilisateurs de fournir des paramètres globaux pour l’extension entière. Le processus de création d’une vue est identique pour tous les types de vues.

## Inclusion d’un type de document

Veillez à inclure une balise `doctype` dans votre fichier HTML. En règle générale, cela signifie que vous devez commencer votre fichier HTML avec les éléments suivants :

```xml
<!DOCTYPE html>
```

## Inclusion du script iframe de balises

Incluez le script iframe de balises dans le code HTML de votre vue :

```html
<script src="https://assets.adobedtm.com/activation/reactor/extensionbridge/extensionbridge.min.js"></script>
```

Ce script fournit une API de communication pour permettre à votre vue de communiquer avec l’application de balises.

## Inscription avec l’API de communication du pont d’extension

Une fois le script iframe chargé, vous devrez fournir certaines méthodes aux balises qu’il utilisera pour la communication. Appelez `window.extensionBridge.register` et transmettez-lui un objet comme suit :

```js
window.extensionBridge.register({
  init: function(info) {
    // Populate view with info.settings which will exist if the user is editing something
    // that was previously saved.
    if (info.settings) {
      document.getElementById('name').value = info.settings.name;
    }
  },
  validate: function() {
    // Return whether the view is valid.
    return document.getElementById('name').value.length > 0;
  },
  getSettings: function() {
    // Return user-provided settings.
    return {
      name: document.getElementById('name').value
    };
  }
});
```

Le contenu de chacune des méthodes devra être modifié en fonction de vos besoins de vue personnalisés.

### [!DNL init]

La méthode `init` sera appelée par des balises dès que la vue aura été chargée dans l’iframe. Un seul argument sera transmis (`info`) qui doit être un objet contenant les propriétés suivantes :

| Propriété | Description |
| --- | --- |
| `settings` | Objet contenant les paramètres précédemment enregistrés à partir de cette vue. Si `settings` est `null`, cela indique que l’utilisateur crée les paramètres initiaux plutôt que de charger une version enregistrée. Si `settings` est un objet, vous devez l’utiliser pour remplir votre vue, car l’utilisateur choisit de modifier les paramètres précédemment conservés. |
| `extensionSettings` | Paramètres enregistrés dans la vue de configuration de l’extension. Cela peut s’avérer utile pour accéder aux paramètres d’extension dans les vues qui ne sont pas la vue de configuration de l’extension. Si la vue actuelle est la vue de configuration de l’extension, utilisez `settings`. |
| `propertySettings` | Objet contenant les paramètres de la propriété. Consultez le [guide d’objet Turbine](../turbine.md#property-settings) pour plus d’informations sur le contenu de cet objet. |
| `tokens` | Objet contenant des jetons API. Pour accéder aux API d’Adobe depuis la vue, vous devez généralement utiliser un jeton IMS sous `tokens.imsAccess`. Ce jeton ne sera disponible que pour les extensions développées par Adobe. Si vous êtes un employé d’Adobe représentant une extension créée par Adobe, veuillez [envoyer un email à l’équipe d’ingénierie de collecte de données](mailto:reactor@adobe.com) et indiquer le nom de l’extension afin que nous puissions l’ajouter à la liste autorisée. |
| `company` | Objet contenant une seule propriété, `orgId`, qui représente votre Adobe Experience Cloud ID (chaîne alphanumérique de 24 caractères). |
| `schema` | Objet au format [Schéma JSON](http://json-schema.org/). Cet objet provient du [manifeste d’extension](../manifest.md) et peut s’avérer utile pour valider votre formulaire. |

Votre vue doit utiliser ces informations pour générer et gérer son formulaire. Il est probable que vous n’aurez affaire qu’à `info.settings`, mais d’autres informations sont fournies en cas de besoin.

### [!DNL validate]

La méthode `validate` sera appelée une fois que l’utilisateur aura cliqué sur le bouton &quot;Enregistrer&quot;. Elle devrait renvoyer l’une des valeurs suivantes :

* Valeur booléenne indiquant si l’entrée de l’utilisateur est valide.
* Promesse qui sera résolue ultérieurement avec une valeur booléenne indiquant si l’entrée de l’utilisateur est valide.

C’est à vous en tant que développeur d’extensions de déterminer ce qui constitue une entrée valide, puisque votre module de bibliothèque agira sur cette entrée.

Si l’entrée de l’utilisateur n’est pas valide, veuillez l’indiquer dans votre vue afin que les utilisateurs sachent ce qui doit être corrigé.

### [!DNL getSettings]

La méthode `getSettings` sera appelée une fois que l’utilisateur aura cliqué sur le bouton &quot;Enregistrer&quot; et que la vue aura été validée. La fonction doit renvoyer l’une des valeurs suivantes :

* Objet contenant des paramètres basés sur l’entrée de l’utilisateur.
* Promesse qui sera résolue ultérieurement avec un objet contenant des paramètres basés sur l’entrée de l’utilisateur.

Cet objet settings sera ultérieurement émis dans la bibliothèque du runtime de balises. C’est vous qui décidez du contenu de cet objet. L’objet doit être sérialisable et désérialisable vers et depuis JSON. Les valeurs telles que les fonctions ou les instances [RegExp](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/RegExp) ne répondent pas à ces critères et ne sont donc pas autorisées.

## Exploitation des vues partagées

L’objet `window.extensionBridge` possède plusieurs méthodes qui vous permettent de tirer parti des vues existantes disponibles par le biais de balises afin que vous n’ayez pas à les reproduire dans votre vue. Les options disponibles sont les suivantes :

### [!DNL openCodeEditor]

```js
window.extensionBridge.openCodeEditor().then(function(code) { 
  console.log(code);
});
```

L’appel de cette méthode affiche un modal permettant à un utilisateur de modifier un extrait de code. Lorsque l’utilisateur a terminé de modifier le code, la promesse est résolue avec le code mis à jour. Si l’utilisateur ferme l’éditeur de code sans choisir d’enregistrer les modifications, la promesse ne sera jamais résolue. L’objet `options` doit être structuré comme suit :

| Propriété | Description |
| --- | --- |
| `code` | Code à afficher dans l’éditeur. Est généralement fourni lorsque l’utilisateur modifie du code existant. Si ce n’est pas le cas, l’éditeur de code sera vide à l’ouverture. |
| `language` | Langage du code qui sera modifié. Les options valides sont `javascript`, `html`, `css`, `json` et `plaintext`. En l’absence de valeur fournie, `javascript` est utilisé par défaut. |

### [!DNL openRegexTester]

```js
window.extensionBridge.openRegexTester().then(function(pattern) { 
  console.log(pattern);
});
```

L’appel de cette méthode affiche un mode permettant à un utilisateur de tester et de modifier un modèle d’expression régulière. Une fois que l’utilisateur a terminé de modifier l’expression régulière, la promesse sera résolue avec le modèle d’expression régulière mis à jour. Si l’utilisateur ferme le testeur regex sans choisir d’enregistrer les modifications, la promesse ne sera jamais résolue. L’objet `options` doit contenir les propriétés suivantes :

| Propriété | Description |
| --- | --- |
| `pattern` | Modèle d’expression régulière qui doit être utilisé comme valeur initiale du champ de modèle à l’intérieur du testeur. Est généralement fourni lorsque l’utilisateur modifie une expression régulière existante. Si ce n’est pas le cas, le champ de motif sera initialement vide. |
| `flags` | Les indicateurs d’expression régulière qui doivent être utilisés par le testeur. Par exemple, `gi` indique l’indicateur de correspondance globale et l’indicateur de casse ignorée. Ces indicateurs ne sont pas modifiables par l’utilisateur dans le testeur, mais sont utilisés pour illustrer les indicateurs spécifiques que l’extension utilisera lors de l’exécution de l’expression régulière. Dans le cas contraire, aucun indicateur ne sera utilisé dans le testeur. Voir [Documentation sur RegExp de MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) pour plus d’informations sur les indicateurs d’expression régulière.<br><br>Un scénario courant est une extension qui permet aux utilisateurs d’inverser la casse pour une expression régulière. Pour ce faire, l’extension fournit généralement une case à cocher dans sa vue d’extension qui, lorsqu’elle est cochée, active l’insensibilité à la casse (représentée par l’indicateur `i`). L’objet settings enregistré par la vue doit indiquer si la case à cocher a été cochée pour que le module Bibliothèque exécutant l’expression régulière sache s’il faut utiliser l’indicateur `i`. En outre, lorsque la vue d’extension souhaite ouvrir le testeur d’expression régulière, elle doit transmettre l’indicateur `i` si la case d’insensibilité à la casse est cochée. Cela permet à l’utilisateur de tester correctement l’expression régulière avec l’insensibilité à la casse activée. |

### [!DNL openDataElementSelector] {#open-data-element}

```js
window.extensionBridge.openDataElementSelector().then(function(dataElement) { 
  console.log(dataElement);
});
```

L’appel de cette méthode affiche un modal permettant à un utilisateur de sélectionner un élément de données. Lorsque l’utilisateur a fini de sélectionner un élément de données, la promesse est résolue avec le nom de l’élément de données sélectionné (par défaut, le nom est encadré de signes de pourcentage). Si l’utilisateur ferme le sélecteur d’éléments sans choisir d’enregistrer les modifications, la promesse ne sera jamais résolue.

L’objet `options` doit contenir une seule propriété booléenne, `tokenize`. Cette propriété indique si le nom de l’élément de données sélectionné doit être encadré de signes de pourcentage avant de résoudre la promesse. Consultez la section sur la [prise en charge des éléments de données](#supporting-data-elements) pour savoir pourquoi cela est utile. Cette option est définie par défaut sur `true`.

## Éléments de données pris en charge {#supporting-data-elements}

Vos vues comportent probablement des champs de formulaire dans lesquels les utilisateurs souhaitent exploiter des éléments de données. Par exemple, si votre vue comporte un champ de texte dans lequel l’utilisateur doit saisir un nom de produit, il peut ne pas être logique que l’utilisateur saisisse une valeur codée en dur dans le champ. L’utilisateur peut préférer que la valeur du champ soit dynamique (déterminée au moment de l’exécution), ce qui peut être fait en utilisant un élément de données.

Par exemple, supposons que nous créions une extension qui envoie une balise pour suivre une conversion. Supposons également que l’une des données que notre balise envoie est un nom de produit. Notre vue d’extension qui permet à l’utilisateur de configurer la balise aurait probablement un champ de texte pour le nom du produit. En règle générale, il ne serait pas très logique que l’utilisateur de Platform saisisse un nom de produit statique tel que « Calzone Oven XL », car le nom du produit dépend probablement de la page à partir de laquelle la balise sera envoyée. C’est un excellent exemple pour un élément de données.

Si un utilisateur souhaite utiliser l’élément de données `productname` comme valeur du nom du produit, il peut saisir le nom de l’élément de données encadré de signes de pourcentage (`%productname%`). Nous appelons le nom de l’élément de données encadré de signes de pourcentage un &quot;jeton d’élément de données&quot;. Ce concept est souvent familier aux utilisateurs de Platform. Votre extension, à son tour, enregistrerait le jeton d’élément de données dans l’objet `settings` qu’elle exporte. L’objet settings peut alors ressembler à ceci :

```js
{
  productName: '%productname%'
}
```

Au moment de l’exécution, avant de transmettre l’objet settings à votre module de bibliothèque, l’objet settings est analysé et tous les jetons d’élément de données sont remplacés par leurs valeurs respectives. Si, au moment de l’exécution, la valeur de l’élément de données `productname` était `Ceiling Medallion Pro 2000`, l’objet settings qui serait transmis à votre module de bibliothèque serait le suivant :

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Pour indiquer où il peut s’avérer utile pour les utilisateurs d’utiliser des éléments de données et pour en faciliter la saisie, il est vivement recommandé d’ajouter un bouton d’icône en regard de ces champs, comme indiqué ici :

![champ d’élément de données](../images/data-element-field.png)

Quand un utilisateur clique sur le bouton Suivant en regard du champ de texte, appelez `window.extensionBridge.openDataElementSelector` comme [indiqué ci-dessus](#open-data-element). Cette option affiche une liste des éléments de données de l’utilisateur dans laquelle l’utilisateur peut choisir plutôt que d’avoir à mémoriser le nom et à saisir les signes de pourcentage. Une fois que l’utilisateur a sélectionné un élément de données, vous recevrez le nom de l’élément de données sélectionné encadré des signes de pourcentage (sauf si vous avez défini l’option `tokenize` sur `false`). Nous vous encourageons à remplir ensuite le champ de texte avec le résultat.

### Remplacement des jetons d’élément de données

Comme décrit précédemment, si un objet settings persistant se composait des éléments suivants :

```js
{
  productName: '%productname%'
}
```

Et, au moment de l’exécution, la valeur de l’élément de données `productname` était `Ceiling Medallion Pro 2000`, alors l’objet settings transmis à votre module de bibliothèque serait le suivant :

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Chaque fois qu’une valeur rencontrée dans un objet settings est composée d’un signe de pourcentage, puis d’une chaîne, puis d’un signe de pourcentage, _et de rien d’autre_, elle est remplacée par la valeur de l’élément de données _sans modifier le type de la valeur de l’élément de données_.

Par exemple, si la valeur de `productname` au moment de l’exécution était à la place le nombre `538` (et non une chaîne), l’objet settings transmis à votre module de bibliothèque serait le suivant :

```js
{
  productName: 538
}
```

Veuillez noter que le résultat `538` est, ici, un nombre et non une chaîne. De même, si la valeur de l’élément de données au moment de l’exécution était une fonction (un cas d’utilisation rare mais possible), l’objet settings obtenu se présenterait comme suit :

```js
{
  productName: function() { … }
}
```

D’un autre côté, supposons que l’objet settings persistant se présentait comme suit :

```js
{
  productName: '%productname% - %modelnumber%'
}
```

Dans ce cas, dans la mesure où la valeur de `productName` est supérieure à un jeton d’élément de données unique, le résultat sera toujours une chaîne. Chaque jeton d’élément de données est remplacé par sa valeur respective après avoir été converti en chaîne. Si, au moment de l’exécution, la valeur de `productname` était `Ceiling Medallion Pro` (une chaîne) et `modelnumber` était `2000` (un nombre), l’objet settings obtenu transmis à votre module de bibliothèque serait :

```js
{
  productName: 'Ceiling Medallion Pro - 2000'
}
```

## Éviter la navigation

La communication entre la vue d’extension et l’interface utilisateur de collecte de données contenante dépend de l’absence de navigation dans la vue d’extension. Par conséquent, évitez d’ajouter quoi que ce soit à votre vue d’extension qui permette à l’utilisateur de quitter la page HTML de cette vue. Par exemple, si vous fournissez un lien dans votre vue d’extension, veillez à ce qu’il ouvre une nouvelle fenêtre de navigateur (généralement en ajoutant `target="_blank"` à la balise d’ancrage). Si vous choisissez d’utiliser un élément `form` dans votre vue d’extension, veillez à ce que le formulaire ne soit jamais envoyé. L’envoi du formulaire peut survenir par inadvertance si vous disposez d’un élément `button` dans le formulaire et ne parvenez pas à y ajouter `type="button"`. L’envoi d’un formulaire dans votre vue d’extension provoquerait l’actualisation du document HTML, générant une interruption de l’expérience utilisateur.
