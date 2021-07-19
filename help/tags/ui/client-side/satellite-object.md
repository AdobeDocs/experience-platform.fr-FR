---
title: Référence d’objet satellite Balises
description: Découvrez lʼobjet _satellite côté client et les différentes fonctions quʼil offre dans Adobe Experience Platform.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 52%

---

# Balises Adobe Experience Platform Référence d’objet satellite

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Ce document sert de référence à l’objet `_satellite` côté client et aux différentes fonctions que vous pouvez exécuter avec celui-ci.

## `track`

**Code**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**Exemple**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` déclenche toutes les règles à l’aide du type d’événement Direct Call (Appel direct) qui a été configuré avec l’identifiant donné à partir de l’extension de balise Core. L’exemple ci-dessus déclenche toutes les règles à l’aide d’un type d’événement Direct Call (Appel direct) dans lequel l’identifiant configuré est `contact_submit`. Un objet facultatif contenant des informations connexes est également transmis. Vous pouvez accéder à l’objet de détail en saisissant `%event.detail%` dans un champ de texte d’une condition ou d’une action ou `event.detail` dans l’éditeur de code d’une condition ou d’une action Custom Code (Code personnalisé).

## `getVar`

**Code**

```javascript
_satellite.getVar(name: string) => *
```

**Exemple**

```javascript
var product = _satellite.getVar('product');
```

Dans l’exemple fourni, si un élément de données existe avec un nom correspondant, la valeur de l’élément de données est renvoyée. S’il n’existe aucun élément de données correspondant, il vérifie alors si une variable personnalisée avec un nom correspondant a été précédemment définie à l’aide de `_satellite.setVar()`. Si une variable personnalisée correspondante est trouvée, sa valeur va être renvoyée.

Notez que dans de nombreux champs de formulaire de l’interface utilisateur de la collecte de données, vous pouvez utiliser la syntaxe `%%` pour référencer des variables, ce qui réduit la nécessité d’appeler `_satellite.getVar()`. Par exemple, l’utilisation de %product% donne accès à la valeur de l’élément de données du produit ou de la variable personnalisée.

## `setVar`

**Code**

```javascript
_satellite.setVar(name: string, value: *)
```

**Exemple**

```javascript
_satellite.setVar('product', 'Circuit Pro');
```

`setVar()` définit une variable personnalisée avec un nom et une valeur donnés. Il est possible d’accéder ultérieurement à la valeur de la variable à l’aide de `_satellite.getVar()`.

Vous pouvez éventuellement définir plusieurs variables à la fois en transmettant un objet où les clés sont des noms de variable et où les valeurs sont les valeurs de variable correspondantes.

```javascript
_satellite.setVar({ 'product': 'Circuit Pro', 'category': 'hobby' });
```

## `getVisitorId`

**Code**

```javascript
_satellite.getVisitorId() => Object
```

**Exemple**

```javascript
var visitorIdInstance = _satellite.getVisitorId();
```

Si l’extension [!DNL Adobe Experience Cloud ID] est installée sur la propriété, cette méthode renvoie l’instance d’identifiant visiteur. Pour plus d’informations, consultez la [documentation du service Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr).

## `logger`

**Code**

```javascript
_satellite.logger.log(message: string)
```

```javascript
_satellite.logger.info(message: string)
```

```javascript
_satellite.logger.warn(message: string)
```

```javascript
_satellite.logger.error(message: string)
```

**Exemple**

```javascript
_satellite.logger.error('No product ID found.');
```

L’objet `logger` permet de consigner un message dans la console du navigateur. Le message ne s’affiche que si le débogage des balises est activé par l’utilisateur (en appelant `_satellite.setDebug(true)` ou en utilisant une extension de navigateur appropriée).

### Consignation des avertissements d’obsolescence

```javascript
_satellite.logger.deprecation(message: string)
```

**Exemple**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

Un avertissement s’affiche alors dans la console du navigateur. Le message s’affiche, que le débogage des balises soit activé ou non par l’utilisateur.

## `cookie`

**Code**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

```javascript
_satellite.cookie.get(name: string) => string
```

```javascript
_satellite.cookie.remove(name: string)
```

**Exemple**

```javascript
// Writing a cookie that expires in one week.
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

```javascript
// Reading a previously set cookie.
var product = _satellite.cookie.get('product');
```

```javascript
// Removing a previously set cookie.
_satellite.cookie.remove('product');
```

Il s’agit d’un utilitaire permettant de lire et d’écrire des cookies. Il s’agit d’une copie exposée du cookie-js de bibliothèque tiers. Pour une utilisation plus poussée, consultez la [documentation sur l’utilisation de js-cookie](https://www.npmjs.com/package/js-cookie#basic-usage) (lien externe).

## `buildInfo`

**Code**

```javascript
_satellite.buildInfo
```

Cet objet contient des informations sur la version de la bibliothèque du runtime de balises active. L’objet contient les propriétés suivantes :

### `turbineVersion`

Ceci fournit la version [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilisée dans la bibliothèque actuelle.

### `turbineBuildDate`

Date ISO 8601 de création de la version de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilisée dans le conteneur.

### `buildDate`

Date ISO 8601 de la création de la bibliothèque actuelle.

### `environment`

Environnement pour lequel cette bibliothèque a été créée. Les valeurs possibles sont les suivantes :

* Développement
* Évaluation
* production

Cet exemple illustre les valeurs d’objet :

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

## `notify`

>[!NOTE]
>
>Cette méthode a été abandonnée. Veuillez plutôt utiliser `_satellite.logger.log()`.

**Code**

```javascript
_satellite.notify(message: string[, level: number])
```

**Exemple**

```javascript
_satellite.notify('Hello world!');
```

`notify` consigne un message dans la console du navigateur. Le message ne s’affiche que si le débogage des balises est activé par l’utilisateur (en appelant `_satellite.setDebug(true)` ou en utilisant une extension de navigateur appropriée).

Un niveau de journalisation facultatif peut être transmis, ce qui affecte le style et le filtrage du message enregistré. Les niveaux pris en charge sont les suivants :

3 - Messages d’information.

4 - Messages d’avertissement.

5 - Messages d’erreur.

Si vous ne fournissez pas de niveau de journalisation ou que vous transmettez une autre valeur de niveau, le message sera consigné en tant que message ordinaire.

## `setCookie`

>[!NOTE]
>
>Cette méthode a été abandonnée. Veuillez plutôt utiliser `_satellite.cookie.set()`.

**Code**

```javascript
_satellite.setCookie(name: string, value: string, days: number)
```

**Exemple**

```javascript
_satellite.setCookie('product', 'Circuit Pro', 3);
```

Cela définit un cookie dans le navigateur de l’utilisateur. Le cookie persistera pendant le nombre de jours spécifié.

## `readCookie`

>[!NOTE]
>
>Cette méthode a été abandonnée. Veuillez plutôt utiliser `_satellite.cookie.get()`.

**Code**

```javascript
_satellite.readCookie(name: string) => string
```

**Exemple**

```javascript
var product = _satellite.readCookie('product');
```

Ceci lit un cookie à partir du navigateur de l’utilisateur.

## `removeCookie`

>[!NOTE]
>
>Cette méthode a été abandonnée. Veuillez plutôt utiliser `_satellite.cookie.remove()`.

**Code**

```javascript
_satellite.removeCookie(name: string)
```

**Exemple**

```javascript
_satellite.removeCookie('product');
```

Cela supprime un cookie du navigateur de l’utilisateur.

## Fonctions de débogage

Les fonctions suivantes ne doivent pas être accessibles à partir du code de production. Elles sont uniquement destinées à des fins de débogage et changeront au fil du temps, selon les besoins.

### `container`

**Code**

```javascript
_satellite._container
```

**Exemple**

>[!IMPORTANT]
>
>Cette fonction ne doit pas être accessible à partir du code de production. Elle est uniquement destinée à des fins de débogage et changera au fil du temps, selon les besoins.

### `monitor`

**Code**

```javascript
_satellite._monitors
```

**Exemple**

>[!IMPORTANT]
>
>Cette fonction ne doit pas être accessible à partir du code de production. Elle est uniquement destinée à des fins de débogage et changera au fil du temps, selon les besoins.

**Exemple**

Sur votre page web exécutant une bibliothèque de balises, ajoutez un fragment de code à votre code HTML. En règle générale, le code est inséré dans l’élément `<head>` avant l’élément `<script>` qui charge la bibliothèque de balises. Cela permet au moniteur de capturer les premiers événements système qui se produisent dans la bibliothèque de balises. Par exemple :

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window._satellite = window._satellite || {};
    window._satellite._monitors = window._satellite._monitors || [];
    window._satellite._monitors.push({
      ruleTriggered: function (event) {
        console.log(
          'rule triggered',
          event.rule
        );
      },
      ruleCompleted: function (event) {
        console.log(
          'rule completed',
          event.rule
        );
      },
      ruleConditionFailed: function (event) {
        console.log(
          'rule condition failed',
          event.rule,
          event.condition
        );
      }
    });
  </script>
  <script src="//assets.adobedtm.com/launch-EN5bfa516febde4b22b3e7c6f96f6b439f.min.js"
          async></script>
</head>
<body>
  <h1>Click me!</h1>
</body>
</html>
```

Dans le premier élément de script, puisque la bibliothèque de balises n’a pas encore été chargée, l’objet `_satellite` initial est créé et un tableau sur `_satellite._monitors` est initialisé. Le script ajoute ensuite un objet de moniteur à ce tableau. L’objet monitor peut spécifier les méthodes suivantes qui seront ensuite appelées par la bibliothèque de balises :

### `ruleTriggered`

Cette fonction est appelée après qu’un événement déclenche une règle, mais avant que les conditions et actions de la règle ne soient traitées. L’objet d’événement transmis à `ruleTriggered` contient des informations sur la règle déclenchée.

### `ruleCompleted`

Cette fonction est appelée une fois qu’une règle a été entièrement traitée. En d’autres termes, l’événement s’est produit, toutes les conditions ont été remplies et toutes les actions ont été exécutées. L’objet d’événement transmis à `ruleCompleted` contient des informations sur la règle qui a été complétée.

### `ruleConditionFailed`

Cette fonction est appelée après le déclenchement d’une règle et l’échec de l’une de ses conditions. L’objet d’événement transmis à `ruleConditionFailed` contient des informations sur la règle déclenchée et la condition qui a échoué.

Si `ruleTriggered` est appelé, `ruleCompleted` ou `ruleConditionFailed` sera appelé peu de temps après.

>[!NOTE]
>
>Un moniteur n’a pas besoin de spécifier les trois méthodes (`ruleTriggered`, `ruleCompleted` et `ruleConditionFailed`). Les balises dans Adobe Experience Platform fonctionnent avec toutes les méthodes prises en charge fournies par le moniteur.

### Test du moniteur

L’exemple ci-dessus indique les trois méthodes du moniteur. Lorsqu’elles sont appelées, le moniteur déconnecte les informations pertinentes. Pour le tester, configurez deux règles dans la bibliothèque de balises :

1. Une règle qui comporte un événement clics et une condition de navigateur qui est uniquement satisfaite si le navigateur est [!DNL Chrome].
1. Une règle qui comporte un événement clics et une condition de navigateur qui est uniquement satisfaite si le navigateur est [!DNL Firefox].

Si vous ouvrez la page dans [!DNL Chrome], ouvrez la console du navigateur et cliquez sur la page, afin que les éléments suivants apparaissent dans la console :

![](../../images/debug.png)

Des hooks supplémentaires ou des informations supplémentaires peuvent être ajoutés à ces gestionnaires si nécessaire.
