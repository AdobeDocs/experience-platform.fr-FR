---
title: Présentation de lʼextension Core Event Forwarding
description: Découvrez lʼextension Core Event Forwarding dans Adobe Experience Platform.
feature: Event Forwarding
exl-id: b5ee4ccf-6fa5-4472-be04-782930f07e20
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 97%

---

# Présentation de lʼextension Core Event Forwarding

Lʼextension Core Event Forwarding fournit les événements, conditions et types de données par défaut pour les transferts dʼévénements dans Adobe Experience Platform.

Utilisez cette référence pour obtenir des informations sur les options disponibles lors de l’utilisation de cette extension pour créer une règle.

## Types de conditions de l’extension Core

Cette section décrit les types de conditions disponibles dans l’extension Core. Ces types de condition peuvent être utilisés avec le type de logique normal ou Exception.

### Custom code

Spécifiez un Custom Code qui doit exister comme condition de l’événement. Utilisez l’éditeur de code intégré pour saisir le code personnalisé. Le transfert d’événement dans Adobe Experience Platform prend en charge ES13.

1. Sélectionner **[!UICONTROL Open Editor]**.
1. Saisissez le Custom Code.
1. Sélectionner **[!UICONTROL Save]**.

Pour accéder à la valeur d’un élément de données dans le code personnalisé, utilisez la méthode `getDataElementValue`. Par exemple, pour récupérer la valeur d’un élément de données nommé `productName`, écrivez ce qui suit : 

```javascript
getDataElementValue('productName') 
```

#### objet ruleStash

Dans votre code personnalisé, vous pouvez également utiliser l’objet `ruleStash`.

```javascript
utils.logger.log(context.arc.ruleStash);
```

`ruleStash` est un objet qui collecte chaque résultat des modules d’action.

Chaque extension a son propre espace de noms. Par exemple, si votre extension porte le nom `send-beacon`, tous les résultats des actions `send-beacon` sont stockés sur l’espace de noms `ruleStash['send-beacon']`.

```javascript
utils.logger.log(context.arc.ruleStash['adobe-cloud-connector']);
```

L’espace de noms est unique pour chaque extension et a la valeur `undefined` au début.

L’espace de noms sera remplacé par le résultat renvoyé par chaque action. Il n’y a pas de magie dans l’espace de noms. Par exemple, si vous disposez d’une extension `transform` contenant deux actions : `generate-fullname` et `generate-fulladdress`, ajoutez les deux actions à une règle.

Si le résultat de l’action `generate-fullname` est `Firstname Lastname`, l’ensemble de règles s’affiche comme suit une fois l’action terminée :

```js
{
  transform: 'Firstname Lastname`
}
```

Si le résultat de l’action `generate-address` est `3900 Adobe Way`, l’ensemble de règles s’affiche comme suit une fois l’action terminée :

```js
{
  transform: '3900 Adobe Way`
}
```

Remarquez que `Firstname Lastname` n’existe plus dans l’ensemble de règles. En effet, l’action `generate-address` l’a remplacée par l’adresse.

Si vous souhaitez stocker les résultats des deux actions dans l’espace de noms `transform` de `ruleStash`, vous pouvez écrire votre module d’action comme dans l’exemple suivant :

```javascript
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;
  if (!transformRuleStash) {
    transformRuleStash = {};
  }
  transformRuleStash.fullName = 'Firstname Lastname';
  return transformRuleStash;
}
```

Lors de la première exécution de cette action, `ruleStash` est `undefined` et est initialisé avec un objet vide. La prochaine fois que l’action est exécutée, `ruleStash` est renvoyée par l’action lorsqu’elle a été précédemment appelée. L’utilisation d’un objet en tant que `ruleStash` vous permet d’ajouter de nouvelles données sans perdre les données précédemment définies par d’autres actions de l’extension.

Dans ce cas, vous devez veiller à toujours renvoyer l’ensemble intégral des règles d’extension. Si vous ne renvoyez qu’une valeur (5, par exemple), l’ensemble des règles se présente comme suit :

```js
{
  transform: 5
}
```

### Value Comparison (Comparaison de valeurs) {#value-comparison}

Compare deux valeurs afin de déterminer si cette condition renvoie true (vrai).

Si vous disposez d’une règle avec plusieurs conditions, il est possible que cette condition renvoie true (vrai), mais que la règle ne se déclenche toujours pas, car les autres conditions sont considérées comme false (faux) ou l’une des exceptions est considérée comme true (vrai).

1. Donnez une valeur.
1. Sélectionnez l’opérateur. Pour plus d’informations, reportez-vous à la liste des opérateurs de comparaison de valeurs ci-dessous.
1. Donnez une autre valeur pour la comparaison.

Les opérateurs de comparaison de valeurs suivants sont disponibles :

**Equal :** la condition renvoie true (vrai) si les deux valeurs sont égales à l’aide d’une comparaison non stricte (dans JavaScript, l’opérateur ==). Les valeurs peuvent être de n’importe quel type. Lorsque vous saisissez un mot tel que _true_ (vrai), _false_ (faux), _null_ (nul) ou _undefined_ (non défini) dans un champ de valeur, le mot est comparé en tant que chaîne et n’est pas converti vers son équivalent JavaScript.

**Does Not Equal** (N’est pas égal à) : la condition renvoie true (vrai) si les deux valeurs ne sont pas égales à l’aide d’une comparaison non stricte (dans JavaScript, l’opérateur !=). Les valeurs peuvent être de n’importe quel type. Lorsque vous saisissez un mot tel que _true_ (vrai), _false_ (faux), _null_ (nul) ou _undefined_ (non défini) dans un champ de valeur, le mot est comparé en tant que chaîne et n’est pas converti vers son équivalent JavaScript.

**Contains :** la condition renvoie true (vrai) si la première valeur contient la seconde valeur. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie false (faux).

**Does Not Contain :** la condition renvoie true (vrai) si la première valeur ne contient pas la seconde valeur. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition va renvoyer true (vrai).

**Starts With :** la condition renvoie true (vrai) si la première valeur commence par la seconde valeur. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie false (faux).

**Does Not Start With :** la condition renvoie true (vrai) si la première valeur ne commence pas par la seconde valeur. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie true (vrai).

**Ends With :** la condition renvoie true (vrai) si la première valeur termine par la seconde valeur. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie false (faux).

**Does Not End With :** la condition renvoie true (vrai) si la première valeur ne se termine pas par la seconde valeur. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie true (vrai).

**Matches Regex :** la condition renvoie true (vrai) si la première valeur correspond à l’expression régulière. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie false (faux).

**Does Not Match Regex :** la condition renvoie true (vrai) si la première valeur ne correspond pas à l’expression régulière. Les nombres sont convertis en chaînes. Pour toute autre valeur qu’un nombre ou une chaîne, la condition renvoie true (vrai).

**Is Less Than :** la condition renvoie true (vrai) si la première valeur est inférieure à la seconde valeur. Les chaînes représentant des nombres sont converties en nombres. Pour toute autre valeur qu’un nombre ou une chaîne convertible, la condition renvoie false (faux).

**Is Less Than Or Equal To :** la condition renvoie true (vrai) si la première valeur est inférieure ou égale à la seconde valeur. Les chaînes représentant des nombres sont converties en nombres. Pour toute autre valeur qu’un nombre ou une chaîne convertible, la condition renvoie false (faux).

**Is Greater Than :** la condition renvoie true (vrai) si la première valeur est supérieure à la seconde valeur. Les chaînes représentant des nombres sont converties en nombres. Pour toute autre valeur qu’un nombre ou une chaîne convertible, la condition renvoie false (faux).

**Is Greater Than Or Equal To :** la condition renvoie true (vrai) si la première valeur est supérieure ou égale à la seconde valeur. Les chaînes représentant des nombres sont converties en nombres. Pour toute autre valeur qu’un nombre ou une chaîne convertible, la condition renvoie false (faux).

**Is True :** la condition renvoie true (vrai) si la valeur est une valeur booléenne dont la valeur est true (vrai). La valeur fournie n’est pas convertie en valeur booléenne s’il s’agit d’un autre type. Pour toute autre valeur qu’une valeur booléenne dont la valeur est true (vrai), la condition renvoie false (faux).

**Is Truthy :** la condition renvoie true (vrai) si la valeur est true (vrai) après avoir été convertie en valeur booléenne. Voir la [documentation sur la condition Truthy de MDN](https://developer.mozilla.org/fr-FR/docs/Glossaire/Truthy) pour des exemples de valeurs « truthy ».

**Is False :** la condition renvoie true (vrai) si la valeur est une valeur booléenne dont la valeur est false (faux). La valeur fournie n’est pas convertie en valeur booléenne s’il s’agit d’un autre type. Pour toute autre valeur qu’une valeur booléenne dont la valeur est false (faux), la condition renvoie false (faux).

**Is Falsy :** la condition renvoie true (vrai) si la valeur est false (faux) après avoir été convertie en valeur booléenne. Voir la [documentation sur la condition Falsy de MDN](https://developer.mozilla.org/fr-FR/docs/Glossaire/Falsy) pour des exemples de valeurs « falsy ».



## Types d’actions de l’extension Core

Cette section décrit les types d’actions disponibles dans l’extension Core.

### Custom Code

Fournissez le code qui s’exécute une fois que l’événement est déclenché et que les conditions sont évaluées. Le transfert d’événement dans Adobe Experience Platform prend en charge ES13.

1. Nommez le code d’action.
1. Sélectionner **[!UICONTROL Open Editor]**.
1. Modifiez le code, puis cliquez sur **[!UICONTROL Save]**.

Pour accéder à la valeur d’un élément de données dans le code personnalisé, utilisez la méthode `getDataElementValue`. Par exemple, pour récupérer la valeur d’un élément de données nommé `productName`, écrivez ce qui suit : 

```javascript
getDataElementValue('productName') 
```

Les actions de transfert dʼévénement sʼexécutent de manière séquentielle. Il est également possible que le code personnalisé dans une action renvoie une valeur pouvant être utilisée dans une action ultérieure. La valeur renvoyée peut provenir du code de cette action ou du corps de réponse d’un appel effectué vers une source externe. Pour référencer les données d’une action précédemment exécutée dans une seule règle où l’extension Core est utilisée, créez un élément de données de type `Path` et utilisez le chemin suivant pour référencer la valeur d’une variable appelée `productCategory` définie dans le code personnalisé de l’extension Core :

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## Types d’éléments de données de l’extension Core

Les types d’éléments de données sont déterminés par l’extension. Les types qui peuvent être créés ne sont pas limités.

Les sections suivantes décrivent les types d’éléments de données disponibles dans l’extension Core. D’autres extensions utilisent d’autres types d’éléments de données.

### Custom code

Il est possible d’entrer du code JavaScript personnalisé dans l’interface utilisateur en cliquant sur **[!UICONTROL Open Editor]** et en insérant le code dans la fenêtre de l’éditeur.

Une instruction de retour est nécessaire dans la fenêtre de l’éditeur afin d’indiquer quelle valeur doit être utilisée en tant que valeur de l’élément de données. Si aucune instruction de retour n’est incluse ou si la valeur `null` ou `undefined` est renvoyée, la valeur par défaut de l’élément de données reflète `null` ou `undefined`.

Pour accéder à la valeur d’un élément de données dans le code personnalisé, utilisez la méthode `getDataElementValue`. Par exemple, pour récupérer la valeur d’un élément de données nommé `productName`, écrivez ce qui suit : 

```javascript
getDataElementValue('productName') 
```

**Exemple :**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### Chemin

Un chemin vers une paire clé-valeur sur un événement envoyé à Adobe Experience Platform Edge Network peut être référencé à l’aide du type d’élément de données Path.

Pour référencer l’objet entier d’un événement, saisissez le chemin `arc`. L’acronyme `arc` désigne Adobe Resource Context et représente le chemin de niveau supérieur pour un événement envoyé à Adobe Experience Platform Edge Network.

Par exemple, étant donné que l’appel `interact` du client vers Edge Network a la demande suivante, comme vue depuis la console du navigateur :

```javascript
"events": [ 
        { 
             "xdm": { 
                    "page": { 
                            "btnHover": false, 
                            "pageName": "We Travel Home Page", 
                            "siteSection": "Landing Page" 
                     }] 
```

Pour entrer un chemin référençant `pageName`, saisissez ce qui suit dans le champ de chemin :

```javascript
arc.event.xdm.page.pageName 
```

>[!NOTE]
>
>Lʼappel `interact` du client possède `events`, mais pour le transfert dʼévénements, vous avez besoin de `event`. La raison en est que la fonctionnalité de transfert dʼévénements inspecte chaque événement individuellement, et non en tant que lot de plusieurs événements, comme indiqué sur le client.
