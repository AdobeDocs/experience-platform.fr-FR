---
title: subscribeRulesetItems
description: Abonnez-vous aux cartes de contenu pour une surface spécifique à l’aide de la commande subscribeRulesetItems .
source-git-commit: 01cba985e22e4673fb60721c810ac9cbee287386
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---


# `subscribeRulesetItems`

La commande `subscribeRulesetItems` vous permet de vous abonner à des propositions qui résultent d’ensembles de règles satisfaits. Pour ce faire, vous pouvez spécifier les surfaces et les schémas à filtrer et fournir une fonction de rappel.

Chaque fois que des jeux de règles sont évalués, la fonction de rappel reçoit un objet `result` avec un tableau de propositions à l’intérieur.

>[!IMPORTANT]
>
>La commande `subscribeRulesetItems` est le seul moyen d’obtenir des propositions provenant d’ensembles de règles, puisqu’elles ne sont pas renvoyées avec les résultats [`sendEvent`](sendevent/overview.md).

## Options de commande {#command-options}

Cette commande utilise un objet `options` avec les propriétés suivantes :

| Propriété | Type | Description |
| --- | --- | --- |
| `surfaces` | Tableau de chaînes | Une liste de surfaces. Les propositions ne sont reçues par la fonction de rappel que si elles correspondent à l&#39;une des surfaces fournies ici. |
| `schemas` | Tableau de chaînes | Liste de schémas. Les propositions ne sont reçues par la fonction de rappel que si elles correspondent à l’un des schémas fournis ici. |
| `callback` | Fonction | Fonction de rappel qui sera appelée lorsque les propositions résultent d’ensembles de règles satisfaits. La fonction de rappel reçoit deux paramètres lorsqu’elle est appelée : `result` et `collectEvent`. Pour plus d’informations, voir [Paramètres de rappel](#callback-parameters) . |

### Paramètres de rappel {#callback-parameters}

La fonction de rappel reçoit les deux paramètres décrits dans le tableau ci-dessous lorsqu’elle est appelée.

| Paramètre | Type | Description |
| --- | --- | --- |
| `result` | Objet | Cet objet contient un tableau `propositions`.  Ces propositions sont le résultat direct d&#39;ensembles de règles satisfaits. L’objet `result` est structuré de la même manière que l’ [objet result](command-responses.md) renvoyé par `sendEvent` à l’aide d’une clause `then`. |
| `collectEvent` | Fonction | Fonction pratique permettant d’envoyer des événements Edge Network pour effectuer le suivi des interactions, des affichages et d’autres événements. |

### Fonction `collectEvent` {#collectevent-function}

La fonction `collectEvent` est une fonction pratique que vous pouvez utiliser pour envoyer des événements Edge Network afin d’effectuer le suivi des interactions, des affichages et d’autres événements. Il accepte les deux paramètres décrits dans le tableau ci-dessous.

| Paramètre | Type | Description |
| --- | --- | --- |
| Type d’événement | Chaîne | Chaîne indiquant le type d’événement de proposition à émettre. Les types d’événements pris en charge sont `display`, `interact` ou `dismiss`. |
| `propositions` | Tableau | Tableau de propositions correspondant à l’événement. |

## Abonnez-vous aux cartes de contenu à l’aide de l’extension de balise SDK Web {#tag-extension}

Suivez les étapes ci-dessous pour vous abonner aux cartes de contenu par le biais de l’interface utilisateur Balises .

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Events], sélectionnez un événement existant ou créez-en un.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL SDK Web Adobe Experience Platform]** et définissez le **[!UICONTROL Type d’événement]** sur **[!UICONTROL Abonner les éléments d’ensemble de règles]**.
1. Sélectionnez les schémas et les surfaces pour lesquels vous souhaitez vous abonner aux cartes de contenu, dans la partie droite de l’écran.
1. Sélectionnez **[!UICONTROL Conserver les modifications]**, puis exécutez votre processus de publication.

## Abonnez-vous aux cartes de contenu à l’aide de la bibliothèque JavaScript SDK Web {#library}

L’exemple de code suivant s’abonne à la surface `web://mywebsite.com/#welcome` pour les cartes de contenu et utilise la méthode pratique `collectEvent` pour émettre des événements `display` pour toutes les propositions.

```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://mywebsite.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```
