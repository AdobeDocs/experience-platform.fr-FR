---
title: Exécuter les commandes du SDK Web Adobe Experience Platform
description: Découvrez comment exécuter les commandes du SDK Web d’Experience Platform
keywords: Exécuter les commandes ; commandName ; Promises ; getLibraryInfo ; objets response ; consentement ;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 70%

---


# Exécuter les commandes

Une fois le code de base implémenté sur votre page web, vous pouvez commencer à exécuter des commandes à l’aide du SDK. Il n’est pas nécessaire d’attendre que le fichier externe (alliage.js) soit chargé à partir du serveur avant d’exécuter les commandes. Si le chargement du SDK n’est pas terminé, les commandes sont mises en file d’attente et traitées dès que possible par le SDK.

Les commandes sont exécutées à l’aide de la syntaxe ci-après.

```javascript
alloy("commandName", options);
```

`commandName` indique au SDK ce qu’il doit faire, tandis que `options` sont les paramètres et données que vous souhaitez transmettre dans une commande. Comme les options disponibles dépendent de la commande, veuillez consulter la documentation pour plus de détails sur chaque commande.

## Remarque sur les promesses

Les [promesses](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/Promise) sont fondamentales pour la communication du SDK avec le code de votre page web. Une promesse est une structure de programmation commune et n’est pas spécifique à ce SDK ni même à JavaScript. Elle agit comme un proxy pour une valeur inconnue lors de la création de la promesse. Une fois la valeur connue, la promesse est « résolue » avec la valeur. Des fonctions de gestionnaire peuvent être associées à une promesse, de sorte que vous puissiez être averti lorsque la promesse a été résolue ou lorsqu’une erreur s’est produite lors du processus de résolution de la promesse. Pour en savoir plus sur les promesses, veuillez lire [ce tutoriel](https://javascript.info/promise-basics) ou toute autre ressource sur le web.

## Gestion des succès ou des échecs {#handling-success-or-failure}

Chaque fois qu’une commande est exécutée, une promesse est renvoyée. La promesse représente l’achèvement éventuel de la commande. Dans l’exemple ci-dessous, vous pouvez utiliser les méthodes `then` et `catch` pour déterminer le moment où la commande a réussi ou échoué.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

S’il n’est pas important pour vous de savoir quand la commande réussit ou échoue, vous pouvez supprimer l’appel `then`.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

De même, si savoir quand la commande échoue n’est pas important pour vous, vous pouvez supprimer l’appel `catch`.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### Objets de réponse

Toutes les promesses renvoyées par les commandes sont résolues avec un objet `result`. L’objet result contient des données en fonction de la commande et du consentement de l’utilisateur. Par exemple, les informations de bibliothèque sont transmises sous la forme d’une propriété de l’objet result dans la commande suivante.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(results.libraryInfo.version);
  });
```

### Consentement

Si l&#39;utilisateur n&#39;a pas donné son consentement à une fin particulière, la promesse sera toujours résolue ; toutefois, l’objet response ne contiendra que les informations qui peuvent être fournies dans le contexte de ce à quoi l’utilisateur a consenti.
