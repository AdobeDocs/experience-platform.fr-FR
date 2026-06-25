---
title: Variable sans Turbine
description: Découvrez l’objet turbine, une variable libre qui fournit des informations et des utilitaires spécifiques à l’exécution de balise d’Adobe Experience Platform.
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
TQID: https://experienceleague.adobe.com/8cXvf8-9uz6WBnifdRmP4dsInqW1DnI2jDFWW9BdauQ
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 74579d9ca311b241313a3d89b564f217cd3476c7
workflow-type: tm+mt
source-wordcount: 587
ht-degree: 94%

---

# Variable sans Turbine

L’objet `turbine` est une « variable libre » dans la portée des modules de bibliothèque de votre extension. Il fournit des informations et des utilitaires spécifiques à l’exécution de balise Adobe Experience Platform et est toujours disponible pour les modules de bibliothèque sans utiliser `require()`.

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` est un objet contenant des informations de version sur la bibliothèque actuelle dʼexécution des balises.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z"
}
```

| Propriété | Description |
| --- | --- |
| `turbineVersion` | Version de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilisée dans la bibliothèque actuelle. |
| `turbineBuildDate` | Date [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) à laquelle la version de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilisée à l’intérieur du conteneur a été créée. |
| `buildDate` | Date ISO 8601 de la création de la bibliothèque actuelle. |

{style="table-layout:auto"}

## `environment`

```js
console.log(turbine.environment.stage);
```

`turbine.environment` est un objet contenant des informations sur l’environnement sur lequel la bibliothèque est déployée.

```js
{
    id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
    stage: "development"
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant de l’environnement. |
| `stage` | Environnement pour lequel cette bibliothèque a été créée. Les valeurs possibles sont les suivantes : `development`, `staging` et `production`. |

{style="table-layout:auto"}

## `debugEnabled`

Valeur booléenne indiquant si le débogage des balises est actuellement activé.

Si vous essayez simplement de consigner des messages, il est peu probable que vous ayez besoin d’utiliser cette fonctionnalité. Au lieu de cela, consignez toujours les messages à lʼaide de `turbine.logger` afin de vous assurer quʼils ne sont imprimés sur la console que lorsque le débogage des balises est activé.

## `getDataElementValue`

```js
console.log(turbine.getDataElementValue(dataElementName));
```

Renvoie la valeur d’un élément de données.

## `getExtensionSettings` {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

Renvoie l’objet settings qui a été enregistré pour la dernière fois à partir de la vue [configuration de l’extension](./configuration.md).

Veuillez noter que les valeurs des objets settings renvoyés peuvent provenir d’éléments de données. Par conséquent, l’appel de `getExtensionSettings()` à des moments différents peut donner des résultats différents si les valeurs des éléments de données ont changé. Pour obtenir les valeurs les plus récentes, patientez aussi longtemps que possible avant dʼappeler `getExtensionSettings()`.

## `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

La propriété [hostedLibFiles](./manifest.md) peut être définie dans le manifeste dʼextension afin dʼhéberger divers fichiers avec la bibliothèque dʼexécution des balises. Ce module renvoie l’URL d’hébergement du fichier de bibliothèque donné.

## `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Récupère un module qui a été partagé depuis une autre extension. Si aucun module correspondant n’est trouvé, `undefined` est renvoyé. Voir [Implémentation de modules partagés](./web/shared.md) pour plus d’informations sur les modules partagés.

## `logger`

```js
turbine.logger.error('Error!');
```

Lʼutilitaire de journalisation est utilisé pour consigner les messages dans la console. Les messages s’affichent uniquement dans la console si le débogage est activé par l’utilisateur. La méthode recommandée pour activer le débogage consiste à utiliser [&#128279;](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob). Lʼutilisateur peut également exécuter la commande suivante `_satellite.setDebug(true)` dans la console de développeur du navigateur. La journalisation utilise les méthodes suivantes :

* `logger.log(message: string)` : consigne un message sur la console.
* `logger.info(message: string)` : consigne un message d’information dans la console.
* `logger.warn(message: string)` : consigne un message d’avertissement dans la console.
* `logger.error(message: string)` : consigne un message d’erreur dans la console.
* `logger.debug(message: string)` : consigne un message de débogage dans la console. (Visible uniquement lorsque la journalisation `verbose` est activée dans la console du navigateur.)
* `logger.deprecation(message: string)` : consigne un message d’avertissement dans la console, que le débogage des balises soit activé ou non par l’utilisateur.

## `onDebugChanged`

En transmettant une fonction de rappel dans `turbine.onDebugChanged`, les balises appellent votre rappel chaque fois que le débogage est activé/désactivé. Les balises transmettent une valeur booléenne à la fonction de rappel, qui est vraie si le débogage a été activé ou fausse si le débogage a été désactivé.

Si vous essayez simplement de consigner des messages, il est peu probable que vous ayez besoin d’utiliser cette fonctionnalité. Au lieu de cela, consignez toujours les messages à lʼaide de `turbine.logger` et les balises feront en sorte que vos messages ne soient imprimés sur la console que lorsque le débogage des balises sera activé.

## `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Un objet contenant les paramètres suivants définis par lʼutilisateur pour la propriété de la bibliothèque dʼexécution des balises actuelle :

* `propertySettings.domains: Array<String>`

  Tableau de domaines couverts par la propriété.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

  Les développeurs d’extensions ne doivent pas se préoccuper de ce paramètre.
