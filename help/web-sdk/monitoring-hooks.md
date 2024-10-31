---
title: Surveillance des hooks pour le SDK Web Adobe Experience Platform
description: Découvrez comment utiliser les hooks de surveillance fournis par le SDK Web de Adobe Experience Platform pour déboguer votre mise en oeuvre et capturer les journaux du SDK Web.
source-git-commit: 3dacc991fd7760c1c358bec07aca83ffeb4f4f4d
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 6%

---


# Surveillance des hooks pour le SDK Web

Le SDK Web de Adobe Experience Platform comprend des hooks de surveillance que vous pouvez utiliser pour surveiller divers événements système. Ces outils sont utiles pour développer vos propres outils de débogage et pour capturer les journaux du SDK Web.

Le SDK Web déclenche les fonctions de surveillance que vous ayez activé ou non le [débogage](commands/configure/debugenabled.md).

## `onInstanceCreated` {#onInstanceCreated}

Cette fonction de rappel est déclenchée lorsque vous avez créé une instance SDK Web. Consultez l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
onInstanceCreated(data) {
    // data.instanceName
    // data.instance
}
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance du SDK Web est stockée. |
| `data.instance` | Fonction | Fonction d’instance utilisée pour appeler les commandes du SDK Web. |

## `onInstanceConfigured` {#onInstanceConfigured}

Cette fonction de rappel est déclenchée par le SDK Web lorsque la commande [`configure`](commands/configure/overview.md) est résolue. Consultez l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
 onInstanceConfigured(data) {
     // data.instanceName
     // data.config
 }
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance du SDK Web est stockée. |
| `data.config` | Objet | Objet contenant la configuration que vous avez utilisée pour votre instance de SDK Web. Il s’agit des options transmises à la commande [`configure`](commands/configure/overview.md) avec toutes les valeurs par défaut ajoutées. |

## `onBeforeCommand` {#onBeforeCommand}

Cette fonction de rappel est déclenchée par le SDK Web avant toute autre commande. Vous pouvez utiliser cette fonction pour récupérer les options de configuration d’une commande spécifique. Consultez l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
onBeforeCommand(data) {
    // data.instanceName
    // data.commandName
    // data.options
}
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance du SDK Web est stockée. |
| `data.commandName` | Chaîne | Nom de la commande du SDK Web devant laquelle cette fonction est exécutée. |
| `data.options` | Objet | Objet contenant les options transmises à la commande du SDK Web. |

## `onCommandResolved` {#onCommandResolved}

Cette fonction de rappel est déclenchée lors de la résolution des promesses de commande. Vous pouvez utiliser cette fonction pour afficher les options de commande et le résultat. Consultez l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
onCommandResolved(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.result
},
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance du SDK Web est stockée. |
| `data.commandName` | Chaîne | Nom de la commande SDK Web exécutée. |
| `data.options` | Objet | Objet contenant les options transmises à la commande du SDK Web. |
| `data.result` | Objet | Objet contenant le résultat de la commande SDK Web. |

## `onCommandRejected` {#onCommandRejected}

Cette fonction de rappel est déclenchée avant qu’une promesse de commande ne soit rejetée et contient des informations sur la raison pour laquelle la commande a été rejetée. Consultez l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
onCommandRejected(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.error
}
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance du SDK Web est stockée. |
| `data.commandName` | Chaîne | Nom de la commande SDK Web exécutée. |
| `data.options` | Objet | Objet contenant les options transmises à la commande du SDK Web. |
| `data.error` | Objet | Objet contenant le message d’erreur renvoyé par l’appel réseau du navigateur (`fetch` dans la plupart des cas), ainsi que la raison du rejet de la commande. |

## `onBeforeNetworkRequest` {#onBeforeNetworkRequest}

Cette fonction de rappel est déclenchée avant l’exécution d’une requête réseau. Consultez l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
onBeforeNetworkRequest(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
}
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance du SDK Web est stockée. |
| `data.requestId` | Chaîne | `requestId` généré par le SDK Web pour activer le débogage. |
| `data.url` | Chaîne | URL demandée. |
| `data.payload` | Objet | Objet de payload de requête réseau qui sera converti au format JSON et envoyé dans le corps de la requête, via une méthode `POST`. |

## `onNetworkResponse` {#onNetworkResponse}

Cette fonction de rappel est déclenchée lorsque le navigateur reçoit une réponse. Consultez l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
onNetworkResponse(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.body
    // data.parsedBody
    // data.status
    // data.retriesAttempted
}
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance du SDK Web est stockée. |
| `data.requestId` | Chaîne | `requestId` généré par le SDK Web pour activer le débogage. |
| `data.url` | Chaîne | URL demandée. |
| `data.payload` | Objet | Objet de payload qui sera converti au format JSON et envoyé dans le corps de la requête, via une méthode `POST`. |
| `data.body` | Chaîne | Corps de la réponse au format chaîne. |
| `data.parsedBody` | Objet | Objet contenant le corps de la réponse analysée. Si une erreur se produit lors de l’analyse du corps de la réponse, ce paramètre n’est pas défini. |
| `data.status` | Chaîne | Le code de réponse au format entier. |
| `data.retriesAttempted` | Nombre entier | Nombre de tentatives lors de l’envoi de la requête. Zéro signifie que la requête a réussi au premier essai. |

## `onNetworkError` {#onNetworkError}

Cette fonction de rappel est déclenchée en cas d’échec de la requête réseau. Consultez l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
onNetworkError(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.error
},
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance du SDK Web est stockée. |
| `data.requestId` | Chaîne | `requestId` généré par le SDK Web pour activer le débogage. |
| `data.url` | Chaîne | URL demandée. |
| `data.payload` | Objet | Objet de payload qui sera converti au format JSON et envoyé dans le corps de la requête, via une méthode `POST`. |
| `data.error` | Objet | Objet contenant le message d’erreur renvoyé par l’appel réseau du navigateur (`fetch` dans la plupart des cas), ainsi que la raison du rejet de la commande. |

## `onBeforeLog` {#onBeforeLog}

Cette fonction de rappel est déclenchée avant que le SDK Web ne consigne quoi que ce soit dans la console. Consultez l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
onBeforeLog(data) {
    // data.instanceName
    // data.componentName
    // data.level
    // data.arguments
}
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance du SDK Web est stockée. |
| `data.componentName` | Chaîne | Nom du composant qui a généré le message du journal. |
| `data.level` | Chaîne | Le niveau de journalisation. Niveaux pris en charge : `log`, `info`, `warn`, `error`. |
| `data.arguments` | Tableau de chaînes | Arguments du message du journal. |


## `onContentRendering` {#onContentRendering}

Cette fonction de rappel est déclenchée par le composant `personalization` à différentes étapes de rendu. La charge utile peut varier, selon le paramètre `status` . Consultez l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
 onContentRendering(data) {
     // data.instanceName
     // data.componentName
     // data.payload
     // data.status
}
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance du SDK Web est stockée. |
| `data.componentName` | Chaîne | Nom du composant qui a généré le message du journal. |
| `data.payload` | Objet | Objet de payload qui sera converti au format JSON et envoyé dans le corps de la requête, via une méthode `POST`. |
| `data.status` | Chaîne | Le composant `personalization` informe le SDK Web de l’état du rendu.  Valeurs prises en charge : <ul><li>`rendering-started` : indique que le SDK Web est sur le point d’effectuer le rendu des propositions. Avant que le SDK Web ne commence à effectuer le rendu d’une portée de décision ou d’une vue, dans l’objet `data`, vous pouvez voir les propositions sur le point d’être générées par le composant `personalization` et le nom de la portée.</li><li>`no-offers` : indique qu’aucune charge utile n’a été reçue pour les paramètres demandés.</li> <li>`rendering-failed` : indique que le SDK Web n’a pas pu effectuer le rendu d’une proposition.</li><li>`rendering-succeeded` : indique que le rendu est terminé pour une portée de décision.</li> <li>`rendering-redirect` : indique que le SDK Web va effectuer le rendu d’une proposition de redirection.</li></ul> |

## `onContentHiding` {#onContentHiding}

Cette fonction de rappel est déclenchée lorsqu’un style de masquage préalable est appliqué ou supprimé.

```js
onContentHiding(data) {
    // data.instanceName
    // data.componentName
    // data.status
}
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance du SDK Web est stockée. |
| `data.componentName` | Chaîne | Nom du composant qui a généré le message du journal. |
| `data.status` | Chaîne | Le composant `personalization` informe le SDK Web de l’état du rendu. Valeurs prises en charge : <ul><li>`hide-containers`</li><li>`show-containers`</ul> |

## Comment spécifier des hooks de surveillance lors de l’utilisation du package NPM {#specify-monitoris-npm}

Si vous utilisez le SDK Web via le [package NPM](install/npm.md), vous pouvez spécifier des hooks de surveillance dans la fonction `createInstasnce`, comme illustré ci-dessous.

```js
var monitor = {
  onBeforeCommand(data) {
    console.log(data);
  },
  ...
};
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy", monitors: [monitor] });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

## Exemple {#example}

Le SDK Web recherche un tableau d’objets dans une variable globale appelée `__alloyMonitors`.

Pour capturer tous les événements du SDK Web, vous devez définir vos hooks de surveillance avant que le code du SDK Web ne soit chargé sur votre page. Chaque méthode de surveillance capture un événement SDK Web.

Vous pouvez définir des hooks de surveillance *après le chargement du code du SDK Web* sur votre page, mais tous les hooks qui ont été déclenchés avant le chargement de la page seront *non* capturés.

Lorsque vous définissez votre objet de point d’extension de surveillance, il vous suffit de définir les méthodes pour lesquelles vous souhaitez définir une logique spéciale.
Par exemple, si vous vous souciez uniquement de `onContentRendering`, vous pouvez simplement définir cette méthode. Vous n’avez pas besoin d’utiliser tous les hooks de surveillance à la fois.

Vous pouvez définir plusieurs objets de point d’extension de surveillance. Tous les objets avec la méthode donnée sont appelés lorsque l’événement correspondant est déclenché.

>[!TIP]
>
>Voir ci-dessous un exemple de page avec tous les hooks de surveillance implémentés.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window.__alloyMonitors = window.__alloyMonitors || [];
    window.__alloyMonitors.push({
      onInstanceCreated(data) {
        // data.instanceName
        // data.instance
      },
      onInstanceConfigured(data) {
        // data.instanceName
        // data.config
      },
      onBeforeCommand(data) {
        // data.instanceName
        // data.commandName
        // data.options
      },
      // Added in version 2.4.0
      onCommandResolved(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.result
      },
      // Added in version 2.4.0
      onCommandRejected(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.error
      },
      onBeforeNetworkRequest(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
      },
      onNetworkResponse(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.body
        // data.parsedBody
        // data.status
        // data.retriesAttempted
      },
      onNetworkError(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.error
      },
      onBeforeLog(data) {
        // data.instanceName
        // data.componentName
        // data.level
        // data.arguments
      }
      onContentRendering(data) {
        // data.instanceName
        // data.componentName
        // data.payload
        // data.status
      },
      onContentHiding(data) {
        // data.instanceName
        // data.componentName
        // data.status
      }
    });
  </script>
  <script>
      !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
      []).push(o),n[o]=function(){var u=arguments;return new Promise(
      function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
      (window,["alloy"]);
    </script>
    <script src="alloy.js" async></script>
</head>
<body>
  <h1>Monitor Test</h1>
</body>
</html>
```
