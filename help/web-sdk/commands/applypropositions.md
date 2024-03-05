---
title: applyPropositions
description: Rendre les propositions qui ont déjà été générées avec sendEvent.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---


# `applyPropositions`

La variable `applyPropositions` permet de rendre à nouveau les propositions déjà générées à l’aide de la commande [`sendEvent`](sendevent/overview.md) . Cette commande est utile lorsque vous utilisez des applications d’une seule page dans lesquelles des parties de la page sont régénérées, ce qui peut remplacer toute personnalisation déjà appliquée à la page.

Cette commande prend en charge les champs suivants :

* **Propositions**: un tableau d’objets de proposition que vous souhaitez rendre à nouveau.
* **Nom de la vue**: nom de la vue à rendre. Les notifications d’affichage de ces décisions sont mises en cache et peuvent être incluses dans une `sendEvent` à l’aide de la commande `personalization.includePendingDisplayNotifications` .
* **Métadonnées**: objet qui détermine la manière dont les offres de HTML peuvent être appliquées. Il contient les propriétés suivantes :
   * Portée
   * Sélecteur
   * Type d’action

## Application de propositions à l’aide de l’extension de balise SDK Web

L’application de propositions est effectuée en tant qu’action au sein d’une règle dans l’interface des balises de collecte de données Adobe Experience Platform.

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez la variable [!UICONTROL Extension] du champ déroulant vers **[!UICONTROL SDK Web Adobe Experience Platform]**, puis définissez la variable [!UICONTROL Type d’action] to **[!UICONTROL Appliquer les propositions]**.
1. Définissez les champs de votre choix à droite.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre workflow de publication.

## Application de propositions à l’aide de la bibliothèque JavaScript SDK Web

Exécutez la variable `applyPropositions` lors de l’appel de votre instance configurée du SDK Web. L’objet contenant des options de configuration prend en charge les champs suivants :

* **`propositions`**: un tableau d’objets de proposition que vous souhaitez rendre à nouveau. Cet objet n’est généralement pas utilisé, comme `propositionScopes` détermine généralement les portées ou les surfaces que vous souhaitez restituer à nouveau.
* **`metadata`**: détermine la manière dont les offres de HTML sont appliquées. Il s’agit d’une carte où la clé est une portée ou une surface, et la valeur est un objet contenant les clés. `selector` et `actionType`.
   * `selector`: chaîne contenant un sélecteur CSS indiquant où appliquer le HTML.
   * `actionType`: action à effectuer avec le HTML. Les valeurs valides comprennent `setHtml`, `replaceHtml` et `appendHtml`.
* **`viewName`**: nom de la vue à afficher dans une application d’une seule page. Les notifications d’affichage de ces décisions sont mises en cache et peuvent être incluses dans une `sendEvent` à l’aide de `personalization.includePendingDisplayNotifications`.

```js
alloy("applyPropositiions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
