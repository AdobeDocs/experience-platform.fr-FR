---
title: Référence dʼobjet satellite
description: Découvrez lʼobjet _satellite côté client et les différentes fonctions quʼil offre dans les balises.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 309f3cce82c5d6c7f10c08b05da6d9c6c44631b6
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 90%

---

# Référence d’objet satellite

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Ce document sert de référence à lʼobjet `_satellite` côté client et aux différentes fonctions que vous pouvez exécuter avec celui-ci.

## `track`

**Code**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**Exemple**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` déclenche toutes les règles à lʼaide du type dʼévénement Direct Call (Appel direct) qui a été configuré avec lʼidentifiant donné à partir de lʼextension de balise Core. L’exemple ci-dessus déclenche toutes les règles à l’aide d’un type d’événement Direct Call (Appel direct) dans lequel l’identifiant configuré est `contact_submit`. Un objet facultatif contenant des informations connexes est également transmis. Vous pouvez accéder à l’objet de détail en saisissant `%event.detail%` dans un champ de texte d’une condition ou d’une action ou `event.detail` dans l’éditeur de code d’une condition ou d’une action Custom Code (Code personnalisé).

## `getVar`

**Code**

```javascript
_satellite.getVar(name: string) => *
```

**Exemple**

```javascript
var product = _satellite.getVar('product');
```

Dans lʼexemple proposé, sʼil existe un élément de données avec un nom correspondant, la valeur de lʼélément de données sera renvoyée. S’il n’existe aucun élément de données correspondant, il vérifie alors si une variable personnalisée avec un nom correspondant a été précédemment définie à l’aide de `_satellite.setVar()`. Si une variable personnalisée correspondante est trouvée, sa valeur va être renvoyée.

>[!NOTE]
>
>Vous pouvez utiliser la syntaxe de pourcentage (`%`) pour référencer des variables pour de nombreux champs de formulaire dans votre mise en oeuvre de balise, ce qui réduit la nécessité d’appeler `_satellite.getVar()`. Par exemple, l’utilisation de `%product%` permet d’accéder à la valeur de l’élément de données du produit ou de la variable personnalisée.

Lorsqu’un événement déclenche une règle, vous pouvez transmettre l’objet `event` correspondant à la règle dans `_satellite.getVar()` comme suit :

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

## `setVar`

>[!NOTE]
>
>Le code `setVar` est entièrement distinct d’un élément de données spécifié dans les balises.

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

Si l’extension [!DNL Adobe Experience Cloud ID] est installée sur la propriété, cette méthode renvoie l’instance d’identifiant visiteur. Pour plus d’informations, consultez la [documentation du service Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr).

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

Lʼobjet `logger` permet de consigner un message dans la console du navigateur. Le message ne sʼaffiche que si le débogage de balises est activé par lʼutilisateur (en appelant `_satellite.setDebug(true)` ou en utilisant une extension de navigateur appropriée).

### Consignation des avertissements d’obsolescence

```javascript
_satellite.logger.deprecation(message: string)
```

**Exemple**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

Cette opération permet de consigner un message dʼavertissement dans la console du navigateur. Le message sʼaffiche et ce, que le débogage de balises soit activé ou non par lʼutilisateur.

## `cookie` {#cookie}

`_satellite.cookie` contient des fonctions permettant de lire et dʼécrire des cookies. C’est une copie exposée du js-cookie de bibliothèque tiers. Pour plus dʼinformations sur lʼutilisation avancée de cette bibliothèque, consultez la [documentation sur le js-cookie](https://www.npmjs.com/package/js-cookie#basic-usage).

### Configuration dʼun cookie {#cookie-set}

Pour configurer un cookie, utilisez `_satellite.cookie.set()`.

**Code**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

>[!NOTE]
>
>Dans l’ancienne méthode [`setCookie`](#setCookie) de définition des cookies, le troisième argument (facultatif) de cet appel de fonction était un entier qui indiquait le délai d’expiration du cookie en jours. Dans cette nouvelle méthode, un objet « attributes » est accepté comme troisième argument à la place. Pour définir une expiration pour un cookie à l’aide de la nouvelle méthode, vous devez fournir une propriété `expires` dans l’objet attributes et la définir sur la valeur souhaitée. Ceci est illustré dans lʼexemple ci-dessous.

**Exemple**

L’appel de fonction suivant écrit un cookie qui expire en une semaine.

```javascript
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

### Récupération d’un cookie {#cookie-get}

Pour récupérer un cookie, utilisez `_satellite.cookie.get()`.

**Code**

```javascript
_satellite.cookie.get(name: string) => string
```

**Exemple**

L’appel de fonction suivant lit un cookie précédemment configuré.

```javascript
var product = _satellite.cookie.get('product');
```

### Suppression d’un cookie {#cookie-remove}

Pour supprimer un cookie, utilisez `_satellite.cookie.remove()`.

**Code**

```javascript
_satellite.cookie.remove(name: string)
```

**Exemple**

L’appel de fonction suivant supprime un cookie précédemment configuré.

```javascript
_satellite.cookie.remove('product');
```

## `buildInfo`

**Code**

```javascript
_satellite.buildInfo
```

Cet objet contient des informations sur la création de la bibliothèque dʼexécution des balises actuelle. L’objet contient les propriétés suivantes :

### `turbineVersion`

Permet de fournir la version de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilisée dans la bibliothèque actuelle.

### `turbineBuildDate`

Date ISO 8601 de création de la version de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilisée dans le conteneur.

### `buildDate`

Date ISO 8601 de la création de la bibliothèque actuelle.

Cet exemple illustre les valeurs d’objet :

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z"
}
```

## `environment`

Cet objet contient des informations sur l’environnement sur lequel la bibliothèque du runtime de balises active est déployée.

**Code**

```javascript
_satellite.environment
```

L’objet contient les propriétés suivantes :

```javascript
{
  id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
  stage: "development"
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant de l’environnement. |
| `stage` | Environnement pour lequel cette bibliothèque a été créée. Les valeurs possibles sont `development`, `staging` et `production`. |

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

`notify` consigne un message sur la console du navigateur. Le message ne sʼaffiche que si le débogage de balises est activé par lʼutilisateur (en appelant `_satellite.setDebug(true)` ou en utilisant une extension de navigateur appropriée).

Un niveau de journalisation facultatif peut être transmis, ce qui va affecter la stylisation et le filtrage du message enregistré. Les niveaux pris en charge sont les suivants :

3 - Messages d’information.

4 - Messages d’avertissement.

5 - Messages d’erreur.

Si vous ne fournissez pas de niveau de journalisation ou que vous transmettez une autre valeur de niveau, le message sera consigné en tant que message ordinaire.

## `setCookie` {#setCookie}

>[!IMPORTANT]
>
>Cette méthode a été abandonnée. Veuillez plutôt utiliser [`_satellite.cookie.set()`](#cookie-set).

**Code**

```javascript
_satellite.setCookie(name: string, value: string, days: number)
```

**Exemple**

```javascript
_satellite.setCookie('product', 'Circuit Pro', 3);
```

Cette opération configure un cookie dans le navigateur de lʼutilisateur. Le cookie persistera pendant le nombre de jours spécifié.

## `readCookie`

>[!IMPORTANT]
>
>Cette méthode a été abandonnée. Veuillez plutôt utiliser [`_satellite.cookie.get()`](#cookie-get).

**Code**

```javascript
_satellite.readCookie(name: string) => string
```

**Exemple**

```javascript
var product = _satellite.readCookie('product');
```

Cette opération lit un cookie à partir du navigateur de lʼutilisateur.

## `removeCookie`

>[!NOTE]
>
>Cette méthode a été abandonnée. Veuillez plutôt utiliser [`_satellite.cookie.remove()`](#cookie-remove).

**Code**

```javascript
_satellite.removeCookie(name: string)
```

**Exemple**

```javascript
_satellite.removeCookie('product');
```

Cette opération supprime un cookie du navigateur de lʼutilisateur.

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

Sur votre page web exécutant une bibliothèque de balises, ajoutez un fragment de code à votre code HTML. En règle générale, le code est inséré dans lʼélément `<head>` avant lʼélément `<script>` qui charge la bibliothèque de balises. Cela permet au moniteur de capturer les premiers événements système qui surviennent dans la bibliothèque de balises. Par exemple :

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

Dans le premier élément de script, puisque la bibliothèque de balises n’a pas encore été chargée, l’objet `_satellite` initial est créé et un tableau est initialisé sur `_satellite._monitors`. Le script ajoute ensuite un objet de moniteur à ce tableau. L’objet de moniteur peut spécifier les méthodes suivantes, qui seront ensuite appelées par la bibliothèque de balises :

### `ruleTriggered`

Cette fonction est appelée après qu’un événement déclenche une règle, mais avant que les conditions et actions de la règle ne soient traitées. L’objet d’événement transmis à `ruleTriggered` contient des informations sur la règle déclenchée.

### `ruleCompleted`

Cette fonction est appelée une fois qu’une règle a été entièrement traitée. En d’autres termes, l’événement est survenu, toutes les conditions ont été satisfaites et toutes les actions ont été exécutées. L’objet d&#39;événement transmis à `ruleCompleted` contient des informations sur la règle qui a été traitée.

### `ruleConditionFailed`

Cette fonction est appelée après le déclenchement d’une règle et l’échec de l’une de ses conditions. L’objet d’événement transmis à `ruleConditionFailed` contient des informations sur la règle déclenchée et la condition qui a échoué.

Si `ruleTriggered` est appelé, `ruleCompleted` ou `ruleConditionFailed` sera appelé peu de temps après.

>[!NOTE]
>
>Un moniteur n’a pas besoin de spécifier les trois méthodes (`ruleTriggered`, `ruleCompleted` et `ruleConditionFailed`). Les balises dans Adobe Experience Platform fonctionnent avec toutes les méthodes prises en charge fournies par le moniteur.

### Test du moniteur

L’exemple ci-dessus indique les trois méthodes du moniteur. Lorsqu’elles sont appelées, le moniteur déconnecte les informations pertinentes. Pour tester ce paramètre, configurez deux règles dans la bibliothèque de balises :

1. Une règle qui comporte un événement clics et une condition de navigateur qui est uniquement satisfaite si le navigateur est [!DNL Chrome].
1. Une règle qui comporte un événement clics et une condition de navigateur qui est uniquement satisfaite si le navigateur est [!DNL Firefox].

Si vous ouvrez la page dans [!DNL Chrome], ouvrez la console du navigateur et cliquez sur la page, afin que les éléments suivants apparaissent dans la console :

![](../../images/debug.png)

Il est possible d’ajouter des raccordements ou des informations supplémentaires à ces gestionnaires, si nécessaire.
