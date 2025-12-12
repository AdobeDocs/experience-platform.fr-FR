---
title: Modules partagés pour l’extension Adobe Analytics
description: Découvrez les modules de bibliothèque partagés fournis par lʼextension de balise Adobe Analytics dans Adobe Experience Platform.
exl-id: f1d7cb2b-0058-46f9-983c-079079e06057
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 100%

---

# Modules partagés pour l’extension Adobe Analytics

L’[extension Adobe Analytics](./overview.md) fournit deux [modules partagés différents](../../../extension-dev/web/shared.md) que vous pouvez intégrer à votre application d’expérience. Ces modules sont traités dans les sections ci-dessous.

## [!DNL get-tracker]

Avant d’envoyer des balises, Adobe Analytics doit initialiser l’objet de suivi. Le processus d’initialisation commence par le chargement de [AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=fr), suivi par la création d’un objet de suivi.

Vous pouvez accéder à l’objet de suivi après son initialisation complète en utilisant le module partagé `get-tracker` comme suit :

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

getTracker().then(function(tracker) {
  // Use tracker in some way
});
```

### Vérification de l’installation d’Adobe Analytics

Il est possible qu’Adobe Analytics n’ait pas été installé ou inclus dans la même bibliothèque de balise que votre extension. C’est pourquoi il est vivement recommandé de vérifier si tel est le cas dans votre code et de gérer cette situation de manière appropriée. Le code JavaScript suivant est un exemple d’implémentation de cette méthode :

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

if (getTracker) {
  getTracker().then(function(tracker) {
    // Use tracker in some way
  });
} else {
  turbine.logger.error("The Adobe Analytics extension is required for Extension XYZ to function properly.");
}
```

Si le `getTracker` est `undefined`, l’extension Adobe Analytics n’existe pas dans la bibliothèque de balises. Vous pouvez personnaliser le message consigné afin de refléter précisément les fonctionnalités qui risquent d’être perdues si Adobe Analytics n’est pas installé.


## [!DNL augment-tracker]

Une fois l’objet de suivi initialisé, l’étape suivante du processus est l’augmentation. Cette étape donne à votre extension la possibilité d’augmenter le suivi avec tout ce qui est nécessaire avant que des variables aient été appliquées à partir de la configuration de l’extension Adobe Analytics ou avant que des balises aient été envoyées.

En outre, votre extension a la possibilité de suspendre le processus d’initialisation de l’outil de suivi pendant que votre extension effectue toute tâche asynchrone propre, telle que la récupération de données ou de JavaScript à partir d’un serveur.

Vous pouvez implémenter le module `augment-tracker` de la manière suivante :

```js
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  // Augment tracker in some way
});
```

La fonction transmise à `augmentTracker()` sera appelée dès que la phase d’augmentation du processus d’initialisation de l’outil de suivi sera atteinte.

Si votre extension doit terminer une tâche asynchrone avant d’augmenter le suivi, vous pouvez renvoyer une promesse à partir de votre fonction comme suit :

```js
var Promise = require('@adobe/reactor-promise');
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  return new Promise(function(resolve) {
    // Augment the tracker object, then call resolve()
  });
});
```

En renvoyant une promesse, votre extension signale à Adobe Analytics qu’il doit interrompre le processus d’initialisation du suivi jusqu’à ce que la promesse soit résolue.

>[!WARNING]
>
>Soyez prudent lors de la suspension du processus d’initialisation du suivi, car cela peut retarder l’envoi des balises et, donc, générer des données non collectées (par exemple, si l’utilisateur quitte la page avant que la balise ne soit envoyée).
