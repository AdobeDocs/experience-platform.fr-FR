---
title: applyPropositions
description: Restituer des propositions qui ont déjà été rendues avec sendEvent.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# `applyPropositions`

La commande `applyPropositions` vous permet de rendre à nouveau des propositions qui ont déjà été rendues à l’aide de la commande [`sendEvent`](sendevent/overview.md). Cette commande est utile lorsque vous utilisez des applications monopages où des parties de la page sont rendues de nouveau, ce qui peut remplacer toutes les personnalisations déjà appliquées à la page.

Cette commande prend en charge les champs suivants :

* **Propositions** : tableau d’objets de proposition dont vous souhaitez effectuer à nouveau le rendu.
* **Nom de la vue** : nom de la vue dont le rendu doit être effectué. Les notifications d’affichage de ces décisions sont mises en cache et peuvent être incluses dans une commande de `sendEvent` ultérieure à l’aide de l’option `personalization.includeRenderedPropositions` .
* **Données Meta** : objet qui détermine la manière dont les offres HTML peuvent être appliquées. Il contient les propriétés suivantes :
   * Portée
   * Sélecteur
   * Type de l’action

>[!NOTE]
>
>La commande `applyPropositions` n’envoie pas automatiquement d’événements d’affichage. Si vous souhaitez enregistrer les affichages, utilisez la commande `sendEvent` décrite dans la section [Gérer les événements d’affichage](/help/collection/use-cases/personalization/display-events.md).

Exécutez la commande `applyPropositions` lors de l’appel de votre instance configurée de Web SDK. L’objet contenant les options de configuration prend en charge les champs suivants :

* **`propositions`** : tableau d’objets de proposition dont vous souhaitez effectuer à nouveau le rendu. Cet objet n’est généralement pas utilisé, car le champ `propositionScopes` détermine généralement les portées ou surfaces dont vous souhaitez effectuer à nouveau le rendu.
* **`metadata`** : détermine la manière dont les offres HTML sont appliquées. Il s’agit d’une carte où la clé est une portée ou une surface et où la valeur est un objet contenant les clés `selector` et `actionType`.
   * `selector` : chaîne contenant un sélecteur CSS de l’emplacement d’application d’HTML.
   * `actionType` : action à effectuer avec HTML. Les valeurs valides comprennent `setHtml`, `replaceHtml` et `appendHtml`.
* **`viewName`** : nom de la vue dont le rendu doit être effectué dans une application monopage. Les notifications d’affichage de ces décisions sont mises en cache et peuvent être incluses dans une commande de `sendEvent` ultérieure à l’aide de `personalization.includeRenderedPropositions`.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```

## Application de propositions à l’aide de l’extension de balise Web SDK

L’extension de balise Web SDK équivalente à cette commande est l’action [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md).
