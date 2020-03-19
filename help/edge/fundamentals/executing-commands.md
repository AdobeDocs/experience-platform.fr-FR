---
title: Exécution des commandes
seo-title: Exécution des commandes du SDK Web d’Adobe Experience Platform
description: Découvrez comment exécuter les commandes du SDK Web Experience Platform
seo-description: Découvrez comment exécuter les commandes du SDK Web Experience Platform
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Bêta) Exécution des commandes

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Une fois le code de base mis en oeuvre sur votre page Web, vous pouvez commencer à exécuter des commandes à l’aide du SDK. Il n&#39;est pas nécessaire d&#39;attendre que le fichier externe \(`alloy.js`\) soit chargé à partir du serveur avant d&#39;exécuter les commandes. Si le SDK n’est pas terminé, les commandes sont mises en file d’attente et traitées par le SDK dès que possible.

Les commandes sont exécutées à l’aide de la syntaxe suivante.

```javascript
alloy("commandName", options);
```

Le `commandName` code indique au SDK ce qu’il doit faire, tandis `options` que les paramètres et données que vous souhaitez transmettre dans une commande sont les suivants : Comme les options disponibles dépendent de la commande, veuillez consulter la documentation pour plus de détails sur chaque commande.

## Une note sur les promesses

[Les promesses](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) sont fondamentales pour la manière dont le SDK communique avec le code de votre page Web. Une promesse est une structure de programmation commune et n&#39;est pas spécifique à ce SDK ni même à JavaScript. Une promesse agit comme un proxy pour une valeur inconnue lors de la création de la promesse. Une fois la valeur connue, la promesse est &quot;résolue&quot; avec la valeur. Les fonctions de gestionnaire peuvent être associées à une promesse, de sorte que vous puissiez être averti lorsque la promesse a été résolue ou lorsqu’une erreur s’est produite lors du processus de résolution de la promesse. Pour en savoir plus sur les promesses, veuillez lire [ce tutoriel](https://javascript.info/promise-basics) ou toute autre ressource sur le Web.

## Gestion des réussites ou des échecs

Chaque fois qu&#39;une commande est exécutée, une promesse est renvoyée. La promesse représente l&#39;achèvement éventuel du commandement. Dans l’exemple ci-dessous, vous pouvez utiliser `then` et `catch` des méthodes pour déterminer le moment où la commande a réussi ou échoué.

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Si savoir quand la commande réussit n&#39;est pas important pour vous, vous pouvez supprimer l&#39; `then` appel.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

De même, si savoir quand la commande échoue n&#39;est pas important pour vous, vous pouvez supprimer l&#39; `catch` appel.

```javascript
alloy("commandName", options)
  .then(function(value) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

## Suppression des erreurs

Si la promesse est rejetée et que vous n’avez pas ajouté d’ `catch` appel, l’erreur &quot;bulle vers le haut&quot; est consignée dans la console de développement de votre navigateur, que la journalisation soit activée ou non dans le SDK Web d’Adobe Experience Platform. Si cela vous préoccupe, vous pouvez définir l’option de `suppressErrors` configuration sur `true` comme indiqué dans [Configuration du SDK](configuring-the-sdk.md).
