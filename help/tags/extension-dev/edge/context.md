---
title: Contexte dans les modules d’extension Edge
description: Découvrez l’objet Contexte ainsi que son rôle dans l’interaction avec les modules Bibliothèque dans les extensions de balises des propriétés Edge.
exl-id: 04e4e369-687e-4b46-9d24-18a97a218555
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 100%

---

# Contexte dans les modules d’extension Edge

Tous les modules de bibliothèque des extensions Edge reçoivent un objet `context` lorsqu’ils sont exécutés. Ce document couvre les propriétés fournies par l’objet `context` et le rôle qu’ils jouent dans les modules de bibliothèque.

## Adobe Request Context (arc)

La propriété `arc` est un objet qui fournit des informations sur l’événement déclenchant la règle. Les sections ci-dessous couvrent les différentes sous-propriétés contenues dans cet objet.

### [!DNL event]

L’objet `event` représente l’événement qui a déclenché la règle et contient les valeurs suivantes :

```js
logger.log(context.arc.event);
```

| Propriété | Description |
| --- | --- |
| `xdm` | Objet XDM de l’événement. |
| `data` | Couche de données personnalisée. |

### [!DNL request]

À ne pas confondre avec une requête de l’appareil client, `request` est un objet légèrement modifié qui provient d’Adobe Experience Platform Edge Network.

```js
logger.log(context.arc.request)
```

L’objet `request` présente deux propriétés de niveau supérieur : `body` et `head`. La propriété `body` contient des informations sur le modèle de données d’expérience (XDM) et peut être inspectée dans le débogueur Adobe Experience Platform lorsque vous accédez à **[!UICONTROL Launch]** et sélectionnez l’onglet **[!UICONTROL Edge Trace]**.

### [!DNL ruleStash] {#rulestash}

`ruleStash` est un objet qui collectera chaque résultat des modules d’action.

```js
logger.log(context.arc.ruleStash);
```

Chaque extension a son propre espace de noms. Par exemple, si votre extension porte le nom `send-beacon`, tous les résultats des actions `send-beacon` seront stockés sur l’espace de noms `ruleStash['send-beacon']`.

L’espace de noms est unique pour chaque extension et a la valeur `undefined` au début.

L’espace de noms est remplacé par le résultat renvoyé par chaque action. Par exemple, considérez une extension `transform` contenant deux actions : `generate-fullname` et `generate-fulladdress`. Ces deux actions sont ensuite ajoutées à une règle.

Si le résultat de l’action `generate-fullname` est `Firstname Lastname`, l’ensemble de règles s’affiche comme suit une fois l’action terminée :

```js
{
  transform: 'Firstname Lastname'
}
```

Si le résultat de l’action `generate-address` est `3900 Adobe Way`, l’ensemble de règles s’affiche comme suit une fois l’action terminée :

```js
{
  transform: '3900 Adobe Way'
}
```

Remarquez que « Firstname Lastname » n’existe plus dans l’ensemble de règles, parce que l’action `generate-address` l’a remplacé par une nouvelle valeur.

Si vous voulez que `ruleStash` stocke les résultats des deux actions dans l’espace de noms `transform`, vous pouvez écrire votre module d’action comme dans l’exemple suivant :

```js
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;

  if (!transformRuleStash) {
    transformRuleStash = {};
  }

  transformRuleStash.fullName = 'Firstname Lastname';

  return transformRuleStash;
}
```

La première fois que cette action est exécutée, `ruleStash` commence comme `undefined` et est donc initialisé en tant qu’objet vide. La prochaine fois que l’action sera exécutée, elle recevra `ruleStash` qui a été renvoyé lors de l’appel précédent de l’action. L’utilisation d’un objet en tant que `ruleStash` vous permet d’ajouter de nouvelles données sans perdre les données précédemment définies par d’autres actions de notre extension.

>[!NOTE]
>
>Lorsque vous utilisez cette stratégie, veillez à toujours renvoyer l’ensemble complet des règles d’extension qui y sont liées. En revanche, si vous renvoyez une seule valeur, la stratégie remplacera toutes les autres propriétés que vous auriez définies.

## Utilitaires

La propriété `utils` représente un objet qui fournit des utilitaires spécifiques à l’exécution des balises.

### [!DNL logger]

Lʼutilitaire `logger` vous permet de consigner les messages qui sʼafficheront pendant les sessions de débogage lors de lʼutilisation dʼ[Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob).

```js
context.utils.logger.error('Error!');
```

Le journal utilise les méthodes suivantes dans lesquelles `message` est le message que vous voulez enregistrer :

| Méthode | Description |
| --- | --- |
| `log(message)` | Consigne un message sur la console. |
| `info(message)` | Consigne un message d’information dans la console. |
| `warn(message)` | Consigne un message d’avertissement dans la console. |
| `error(message)` | Consigne un message d’erreur dans la console. |
| `debug(message)` | Consigne un message de débogage dans la console. Visible uniquement lorsque la journalisation `verbose` est activée dans la console du navigateur. |

### [!DNL fetch]

Cet utilitaire implémente l’interface [API de récupération](https://developer.mozilla.org/fr-FR/docs/Web/API/Fetch_API). Vous pouvez utiliser la fonction pour envoyer des requêtes à des points d’entrée tiers.

```js
context.utils.fetch('http://example.com/movies.json')
  .then(response => response.json())
```

### [!DNL getBuildInfo]

Cet utilitaire renvoie un objet contenant des informations sur la version actuelle de la bibliothèque d’exécution des balises.

```js
logger.log(context.utils.getBuildInfo().turbineBuildDate);
```

L’objet contient les valeurs suivantes :

| Propriété | Description |
| --- | --- |
| `turbineVersion` | Version de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) utilisée dans la bibliothèque actuelle. |
| `turbineBuildDate` | Date ISO 8601 de création de la version de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) utilisée dans le conteneur. |
| `buildDate` | Date ISO 8601 de la création de la bibliothèque actuelle. |
| `environment` | Environnement pour lequel cette bibliothèque a été créée. Les valeurs possibles sont les suivantes : `development`, `staging` et `production.` |

Voici un exemple d’objet `getBuildInfo` pour démontrer les valeurs qu’il renvoie :

```js
{
  turbineVersion: "1.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

### [!DNL getExtensionSettings]

Cette utilitaire renvoie l’objet `settings` qui a été enregistré pour la dernière fois à partir de la vue [configuration de l’extension](../configuration.md).

```js
logger.log(context.utils.getExtensionSettings());
```

### [!DNL getSettings]

Cet utilitaire renvoie l’objet `settings` qui a été enregistré pour la dernière fois à partir de la vue de module de bibliothèque correspondante.

```js
logger.log(context.utils.getSettings());
```

### [!DNL getRule]

Cet utilitaire renvoie un objet contenant des informations sur la règle qui déclenche le module.

```js
logger.log(context.utils.getRule());
```

L’objet contient les valeurs suivantes :

| Propriété | Description |
| --- | --- |
| `id` | Identifiant de règle. |
| `name` | Nom de la règle. |
