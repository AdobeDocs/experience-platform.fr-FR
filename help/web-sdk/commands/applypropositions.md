---
title: applyPropositions
description: Rendre les propositions qui ont déjà été générées avec sendEvent.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# `applyPropositions`

La commande `applyPropositions` vous permet de rendre à nouveau les propositions déjà rendues à l’aide de la commande [`sendEvent`](sendevent/overview.md). Cette commande est utile lorsque vous utilisez des applications d’une seule page dans lesquelles des parties de la page sont régénérées, ce qui peut remplacer toute personnalisation déjà appliquée à la page.

Cette commande prend en charge les champs suivants :

* **Propositions** : un tableau d’objets de proposition que vous souhaitez rendre à nouveau.
* **Nom de la vue** : nom de la vue à afficher. Les notifications d’affichage de ces décisions sont mises en cache et peuvent être incluses dans une commande `sendEvent` ultérieure à l’aide de l’option `personalization.includePendingDisplayNotifications` .
* **Métadonnées** : objet qui détermine la manière dont les offres d’HTML peuvent être appliquées. Il contient les propriétés suivantes :
   * Portée
   * Sélecteur
   * Type d’action

## Application de propositions à l’aide de l’extension de balise SDK Web

L’application de propositions est effectuée en tant qu’action au sein d’une règle dans l’interface des balises de collecte de données Adobe Experience Platform.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez une action.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL SDK Web Adobe Experience Platform]** et définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Appliquer les propositions]**.
1. Définissez les champs de votre choix à droite.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre processus de publication.

## Application de propositions à l’aide de la bibliothèque JavaScript SDK Web

Exécutez la commande `applyPropositions` lors de l’appel de votre instance configurée du SDK Web. L’objet contenant des options de configuration prend en charge les champs suivants :

* **`propositions`** : un tableau d’objets de proposition que vous souhaitez rendre à nouveau. Cet objet n’est généralement pas utilisé, car le champ `propositionScopes` détermine généralement les portées ou les surfaces que vous souhaitez rendre à nouveau.
* **`metadata`** : détermine la manière dont les offres d’HTML sont appliquées. Il s’agit d’une carte où la clé est une portée ou une surface, et la valeur est un objet contenant les clés `selector` et `actionType`.
   * `selector` : chaîne contenant un sélecteur CSS indiquant où appliquer l’HTML.
   * `actionType` : action à effectuer avec l’HTML. Les valeurs valides sont `setHtml`, `replaceHtml` et `appendHtml`.
* **`viewName`** : nom de la vue à afficher dans une application d’une seule page. Les notifications d’affichage de ces décisions sont mises en cache et peuvent être incluses dans une commande `sendEvent` suivante à l’aide de `personalization.includePendingDisplayNotifications`.

```js
alloy("applyPropositiions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
