---
title: Surveillance des hooks pour Adobe Experience Platform Web SDK
description: Découvrez comment utiliser les hooks de surveillance fournis par Adobe Experience Platform Web SDK pour déboguer votre implémentation et capturer les journaux Web SDK.
exl-id: 56633311-2f89-4024-8524-57d45c7d38f7
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 6%

---

# Surveillance des hooks pour Web SDK

Adobe Experience Platform Web SDK comprend des hooks de surveillance que vous pouvez utiliser pour surveiller divers événements système. Ces outils sont utiles pour développer vos propres outils de débogage et pour capturer les journaux Web SDK.

Web SDK déclenche les fonctions de surveillance que vous ayez ou non activé [débogage](commands/configure/debugenabled.md).

## `onInstanceCreated` {#onInstanceCreated}

Cette fonction de rappel est déclenchée lorsque vous avez réussi à créer une instance de Web SDK. Voir l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
onInstanceCreated(data) {
    // data.instanceName
    // data.instance
}
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance Web SDK est stockée. |
| `data.instance` | Fonction | Fonction d’instance utilisée pour appeler les commandes Web SDK. |

## `onInstanceConfigured` {#onInstanceConfigured}

Cette fonction de rappel est déclenchée par le SDK Web lorsque la commande [`configure`](commands/configure/overview.md) est résolue avec succès. Voir l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
 onInstanceConfigured(data) {
     // data.instanceName
     // data.config
 }
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance Web SDK est stockée. |
| `data.config` | Objet | Objet contenant la configuration que vous avez utilisée pour votre instance Web SDK. Il s’agit des options transmises à la commande [`configure`](commands/configure/overview.md) avec toutes les valeurs par défaut ajoutées. |

## `onBeforeCommand` {#onBeforeCommand}

Cette fonction de rappel est déclenchée par Web SDK avant l’exécution de toute autre commande. Vous pouvez utiliser cette fonction pour récupérer les options de configuration d’une commande spécifique. Voir l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

```js
onBeforeCommand(data) {
    // data.instanceName
    // data.commandName
    // data.options
}
```

| Paramètre | Type | Description |
|---------|----------|----------|
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance Web SDK est stockée. |
| `data.commandName` | Chaîne | Nom de la commande Web SDK devant laquelle cette fonction est exécutée. |
| `data.options` | Objet | Un objet contenant les options transmises à la commande Web SDK. |

## `onCommandResolved` {#onCommandResolved}

Cette fonction de rappel est déclenchée lors de la résolution des promesses de commande. Vous pouvez utiliser cette fonction pour afficher les options de commande et le résultat. Voir l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

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
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance Web SDK est stockée. |
| `data.commandName` | Chaîne | Nom de la commande Web SDK exécutée. |
| `data.options` | Objet | Un objet contenant les options transmises à la commande Web SDK. |
| `data.result` | Objet | Objet contenant le résultat de la commande Web SDK. |

## `onCommandRejected` {#onCommandRejected}

Cette fonction de rappel est déclenchée avant le rejet d’une promesse de commande et contient des informations sur la raison du rejet de la commande. Voir l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

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
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance Web SDK est stockée. |
| `data.commandName` | Chaîne | Nom de la commande Web SDK exécutée. |
| `data.options` | Objet | Un objet contenant les options transmises à la commande Web SDK. |
| `data.error` | Objet | Objet contenant le message d’erreur renvoyé par l’appel réseau du navigateur (`fetch` dans la plupart des cas), ainsi que la raison pour laquelle la commande a été refusée. |

## `onBeforeNetworkRequest` {#onBeforeNetworkRequest}

Cette fonction de rappel est déclenchée avant l’exécution d’une requête réseau. Voir l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

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
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance Web SDK est stockée. |
| `data.requestId` | Chaîne | `requestId` générée par Web SDK pour activer le débogage. |
| `data.url` | Chaîne | L’URL demandée. |
| `data.payload` | Objet | Objet payload de requête réseau qui sera converti au format JSON et envoyé dans le corps de la requête, par le biais d’une méthode `POST`. |

## `onNetworkResponse` {#onNetworkResponse}

Cette fonction de rappel est déclenchée lorsque le navigateur reçoit une réponse. Voir l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

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
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance Web SDK est stockée. |
| `data.requestId` | Chaîne | `requestId` générée par Web SDK pour activer le débogage. |
| `data.url` | Chaîne | L’URL demandée. |
| `data.payload` | Objet | Objet de payload qui sera converti au format JSON et envoyé dans le corps de la requête, par le biais d’une méthode `POST`. |
| `data.body` | Chaîne | Corps de réponse au format chaîne. |
| `data.parsedBody` | Objet | Objet contenant le corps de la réponse analysée. Si une erreur se produit lors de l’analyse du corps de la réponse, ce paramètre n’est pas défini. |
| `data.status` | Chaîne | Code de réponse au format entier. |
| `data.retriesAttempted` | Nombre entier | Nombre de reprises tentées lors de l’envoi de la requête. Zéro signifie que la requête a réussi au premier essai. |

## `onNetworkError` {#onNetworkError}

Cette fonction de rappel est déclenchée lorsque la requête réseau a échoué. Voir l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

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
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance Web SDK est stockée. |
| `data.requestId` | Chaîne | `requestId` générée par Web SDK pour activer le débogage. |
| `data.url` | Chaîne | L’URL demandée. |
| `data.payload` | Objet | Objet de payload qui sera converti au format JSON et envoyé dans le corps de la requête, par le biais d’une méthode `POST`. |
| `data.error` | Objet | Objet contenant le message d’erreur renvoyé par l’appel réseau du navigateur (`fetch` dans la plupart des cas), ainsi que la raison pour laquelle la commande a été refusée. |

## `onBeforeLog` {#onBeforeLog}

Cette fonction de rappel est déclenchée avant que Web SDK ne consigne quoi que ce soit dans la console. Voir l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

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
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance Web SDK est stockée. |
| `data.componentName` | Chaîne | Nom du composant qui a généré le message du journal. |
| `data.level` | Chaîne | Niveau de journalisation. Niveaux pris en charge : `log`, `info`, `warn`, `error`. |
| `data.arguments` | Tableau de chaînes | Arguments du message du journal. |


## `onContentRendering` {#onContentRendering}

Cette fonction de rappel est déclenchée par le composant `personalization` à différentes étapes du rendu. La payload peut varier en fonction du paramètre `status` . Voir l’exemple ci-dessous pour plus d’informations sur les paramètres de la fonction.

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
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance Web SDK est stockée. |
| `data.componentName` | Chaîne | Nom du composant qui a généré le message du journal. |
| `data.payload` | Objet | Objet de payload qui sera converti au format JSON et envoyé dans le corps de la requête, par le biais d’une méthode `POST`. |
| `data.status` | Chaîne | Le composant `personalization` informe le SDK Web de l’état du rendu.  Valeurs prises en charge : <ul><li>`rendering-started` : indique que le Web SDK est sur le point de rendre des propositions. Avant que le SDK Web ne commence à effectuer le rendu d&#39;une portée de décision ou d&#39;une vue, dans l&#39;objet `data`, vous pouvez voir les propositions qui sont sur le point d&#39;être effectuées par le composant `personalization` et le nom de la portée.</li><li>`no-offers` : indique qu&#39;aucune payload n&#39;a été reçue pour les paramètres demandés.</li> <li>`rendering-failed` : indique que Web SDK n’a pas réussi à effectuer le rendu d’une proposition.</li><li>`rendering-succeeded` : indique que le rendu est terminé pour une portée de décision.</li> <li>`rendering-redirect` : indique que Web SDK effectuera le rendu d’une proposition de redirection.</li></ul> |

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
| `data.instanceName` | Chaîne | Nom de la variable globale dans laquelle l’instance Web SDK est stockée. |
| `data.componentName` | Chaîne | Nom du composant qui a généré le message du journal. |
| `data.status` | Chaîne | Le composant `personalization` informe le SDK Web de l’état du rendu. Valeurs prises en charge : <ul><li>`hide-containers`</li><li>`show-containers`</ul> |

## Spécification des hooks de surveillance lors de l’utilisation du package NPM {#specify-monitoring-npm}

Si vous utilisez le Web SDK via le package [NPM](install/npm.md), vous pouvez spécifier des hooks de surveillance dans la fonction `createInstance` , comme illustré ci-dessous.

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

Pour capturer tous les événements Web SDK, vous devez définir les hooks de surveillance avant le chargement du code Web SDK sur votre page. Chaque méthode de surveillance capture un événement Web SDK.

Vous pouvez définir des hooks de surveillance *après* le chargement du code Web SDK sur votre page, mais les hooks déclenchés avant le chargement de la page ne seront *pas* capturés.

Lorsque vous définissez votre objet de hook de surveillance, il vous suffit de définir les méthodes pour lesquelles vous souhaitez définir une logique spéciale.
Par exemple, si vous vous souciez uniquement de `onContentRendering`, vous pouvez simplement définir cette méthode. Il n’est pas nécessaire d’utiliser tous les hooks de surveillance en même temps.

Vous pouvez définir plusieurs objets de hook de surveillance. Tous les objets avec la méthode donnée seront appelés lorsque l’événement correspondant sera déclenché.

>[!TIP]
>
>Vous trouverez ci-dessous un exemple de page avec tous les hooks de surveillance implémentés.

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
