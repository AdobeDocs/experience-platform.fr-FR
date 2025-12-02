---
title: _moniteurs
description: Ajoutez des écouteurs d’événement pour déboguer votre implémentation de balise.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# `_monitors`

L’objet `_satellite._monitors` vous permet de créer des écouteurs d’événement et d’exécuter du code personnalisé lorsque la bibliothèque détecte une règle déclenchée. Son utilisation principale consiste à vous aider à déboguer votre implémentation pour vous assurer que les règles se déclenchent correctement.

>[!IMPORTANT]
>
>Cet objet est uniquement à des fins de débogage. Ne liez pas la logique de production à cet objet. La disponibilité des propriétés ou des noms dans cet objet peut être modifiée par Adobe à tout moment.

```ts
_satellite._monitors?: {
  ruleTriggered(event: { rule: Rule }): void;
  ruleCompleted(event: { rule: Rule }): void;
  ruleConditionFailed(event: { rule: Rule; condition: Condition }): void;
}[];
```

Vous pouvez écouter les types d’événements suivants :

## `ruleTriggered`

Cette fonction de rappel se déclenche lorsqu’un événement déclenche une règle avant que les conditions et actions de la règle ne soient traitées. Si cette fonction se déclenche, `ruleCompleted` ou `ruleConditionFailed` se déclenche peu de temps après (s’excluant mutuellement).

## `ruleCompleted`

La fonction de rappel `ruleCompleted` se déclenche après `ruleTriggered` lorsque les critères de condition de la règle réussissent et que toutes les actions de la règle sont exécutées.

## `ruleConditionFailed`

La fonction de rappel `ruleConditionFailed` se déclenche après `ruleTriggered` lorsqu’au moins une des conditions de la règle échoue.

## objet `Rule`

Chaque fonction de rappel expose un objet `Rule` qui fournit des informations sur la règle elle-même.

```ts
type Rule = {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}
```

| Nom | Type | Description |
|---|---|---|
| **`id`** | `string` | Identifiant unique de la règle. |
| **`name`** | `string` | Nom convivial de la règle. |
| **`events`** | `Event[]` | Tableau d’événements que vous avez configurés pour déclencher la règle. |
| **`conditions`** | `Condition[]` | Tableau de conditions que vous avez configurées pour déclencher la règle. |
| **`actions`** | `Action[]` | Tableau d’actions que vous avez configuré pour exécuter lorsque la règle est déclenchée. |

## Exemple

Ajoutez le fragment de code suivant à votre HTML dans la balise `<head>` avant d’appeler le chargeur de bibliothèque de balises :

```html
<script>
  window._satellite ??= {};
  window._satellite._monitors ??= [];
  window._satellite._monitors.push({
    ruleTriggered(event) { console.log('Rule triggered', event.rule);},
    ruleCompleted(event) { console.log('Rule completed', event.rule);},
    ruleConditionFailed(event) { console.log('Rule condition failed', event.rule, event.condition);}
  });
</script>
<script src="https://assets.adobedtm.com/.../launch-EN...js" async></script>
```

Comme la bibliothèque de balises n’est pas encore chargée à ce stade de la page, l’objet `_satellite` initial est créé et un tableau sur `_satellite._monitors` est initialisé. Le script ajoute ensuite un objet de moniteur à ce tableau.

Tenez compte des conseils suivants lorsque vous utilisez des moniteurs :

* Notez que ces messages de débogage utilisent `console.log` au lieu de [`_satellite.logger`](logger.md), car les hooks sont créés avant le chargement de la bibliothèque de balises.
* Bien que l’exemple de code inclue les trois fonctions de rappel , il ne s’agit pas de champs obligatoires. Vous ne pouvez inclure que les hooks souhaités lors du débogage des règles sur votre site.
* Plusieurs moniteurs sont autorisés, même pour les mêmes événements. Si vous utilisez plusieurs moniteurs pour un seul événement, l&#39;ordre d&#39;appel n&#39;est pas garanti.
* Veillez à créer `_monitors` _avant_ charger la bibliothèque de balises. Si vous créez ces points d’extension après le chargement de la bibliothèque, seules les règles qui se déclenchent à partir de ce moment sont interceptées.
