---
title: track()
description: Déclenchez une règle d’appel direct.
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 2%

---

# `track()`

La méthode `_satellite.track()` permet de déclencher une règle [Direct call](/help/tags/extensions/client/core/overview.md#direct-call-event).

>[!IMPORTANT]
>
>Adobe considère `_satellite.track()` une **méthode d’implémentation héritée**. Bien qu’il soit toujours entièrement pris en charge, Adobe recommande vivement d’utiliser des méthodes d’implémentation plus modernes, telles que la [couche de données client Adobe](/help/tags/extensions/client/client-data-layer/overview.md), qui constitue l’approche recommandée pour les nouvelles implémentations.
>
>Si vous choisissez d’utiliser `_satellite.track()` sur votre site, **protégez chaque appel** afin que votre site ne soit pas étroitement lié à la bibliothèque de balises. Si elle n’est pas protégée, la suppression de la propriété de balise à l’avenir entraîne des erreurs dans toutes les références à l’objet `_satellite`.

```ts
_satellite.track(identifier: string, detail?: unknown ): void;
```

Lorsque vous appelez `_satellite.track()` à l’aide de l’identifiant configuré dans l’interface utilisateur des balises, cette règle est immédiatement déclenchée. L’appel de cette méthode agit uniquement comme événement de règle ; les conditions de la règle s’appliquent toujours avant d’exécuter les actions de la règle. Plusieurs règles d’appel direct peuvent utiliser le même identifiant, ce qui vous permet de déclencher toutes ces règles en même temps à l’aide d’un seul appel `_satellite.track()`. Chaque règle déclenchée vérifie toujours ses propres conditions avant d’effectuer une action, même si plusieurs règles partagent le même identifiant.

## Champs disponibles

La méthode `_satellite.track()` prend en charge deux arguments :

| Nom | Type | Obligatoire | Description |
|---|---|---|---|
| **`identifier`** | `string` | Oui | Identifiant de la règle d’appel direct. Cet identifiant est défini lors de la configuration de la règle dans l’interface utilisateur des balises. |
| **`detail`** | `unknown` | Non | Payload facultative contenant toutes les informations souhaitées. Lors de la configuration d’une règle, vous pouvez accéder à la payload à l’aide de `event.detail` (code personnalisé) ou de `%event.detail%` (champs de texte qui prennent en charge la notation des éléments de données). |

```js
// Trigger rules with the identifier 'example'
if (window._satellite?.track) {
  _satellite.track('example');
}

// Trigger a direct call rule with an optional payload that your tag rule can use
_satellite.track('contact_submit', { name: 'John Doe' });
// When configuring the rule, access the payload field using:
// event.detail.name (custom code block) or
// %event.detail.name% (data element)
```
