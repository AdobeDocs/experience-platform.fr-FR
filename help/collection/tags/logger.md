---
title: logger
description: Affichez les informations dans la console du navigateur lors du débogage.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---

# `logger`

L’objet `_satellite.logger` contient des méthodes qui vous permettent de générer des messages de diagnostic ou d’information sur la console du navigateur lorsque le [débogage](../use-cases/debugging.md) est activé. Si le débogage n’est pas activé, tous les appels de méthode `logger` n’ont aucun effet.

Ces méthodes permettent aux développeurs, aux spécialistes du marketing technique et aux testeurs de voir facilement ce qui se déclenche dans une propriété de balise et quand. Comme ces messages de console s’affichent uniquement lorsque le débogage est activé, vous pouvez laisser les messages `logger` dans les déploiements en production sans affecter la console du navigateur des visiteurs de votre site.

```ts
readonly _satellite.logger: {
  debug(...args: unknown[]): void;
  log(...args: unknown[]): void;
  info(...args: unknown[]): void;
  warn(...args: unknown[]): void;
  error(...args: unknown[]): void;
}
```

>[!TIP]
>
>Les versions précédentes de l’objet de balise `_satellite.notify()` utilisées. La fonction `notify()` est abandonnée au profit de `_satellite.logger`.

## Méthodes

Toutes les méthodes `_satellite.logger` transitent par leur méthode de `console.*` JavaScript correspondante lorsque le débogage est activé. La plupart des arguments ou objets `console` sont pris en charge à l’aide de `_satellite.logger` :

| Méthode | Transfère vers | Utilisations recommandées |
|---|---|---|
| `_satellite.logger.debug()` | `console.debug()` | Diagnostics détaillés ; certains navigateurs peuvent nécessiter une journalisation détaillée pour l’afficher. |
| `_satellite.logger.log()` | `console.log()` | Messages généraux. |
| `_satellite.logger.info()` | `console.info()` | Événements informatifs de haut niveau. |
| `_satellite.logger.warn()` | `console.warn()` | Problèmes récupérables. L’entrée de la console est mise en surbrillance en jaune. |
| `_satellite.logger.error()` | `console.error()` | Échecs. L’entrée de la console est mise en surbrillance en rouge. Adobe recommande d’utiliser des objets `error` pour les piles. |

```js
// First enable debugging mode
_satellite.setDebug(true);

// Logs a debug message
_satellite.logger.debug('Verbose diagnostic event');

// Logs a generic message
_satellite.logger.log('Example');

// Logs an informational message with mixed arguments
_satellite.logger.info('Rule triggered', 42, { ruleId: 'R123' }, ['a', 'b']);

// Logs a warning message
_satellite.logger.warn('Data element does not contain a value');

// Logs an error message with stack
_satellite.logger.error(new Error('Required extension not found'));
```

## Sortie console

La bibliothèque ajoute le préfixe suivant dans tous les messages de sortie de la console :

* **🚀** : permet de détecter facilement les messages de console qui proviennent de votre implémentation de balises.
* **\[Origine\]** : nom de la règle, de l’action, de l’extension ou de l’élément de données d’où provient le journal. Si vous appelez une méthode d’enregistreur en dehors de votre implémentation (par exemple via la console du navigateur), `[Custom Script]` est utilisée.
* **Sortie du message** : sortie de message incluse lors de l’appel de la méthode .

>[!NOTE]
>
>Les jetons de formatage du navigateur tels que `%c`, `%s` et `%d` ne sont pas appliqués, car l’enregistreur applique le préfixe `🚀 [Origin]`.
