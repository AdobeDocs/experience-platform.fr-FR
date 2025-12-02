---
title: clickCollection
description: Ajustez les paramètres de collection de clics.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# `clickCollection`

L’objet `clickCollection` contient plusieurs variables qui vous aident à contrôler les données de lien collectées automatiquement. Utilisez ces variables lorsque vous souhaitez inclure ou exclure des types de liens de la collecte de données. Il est pris en charge dans les versions 2.25.0 ou ultérieures de Web SDK.

Cette variable nécessite tous les éléments suivants :

* [`clickCollectionEnabled`](clickcollectionenabled.md) doit être activé.
* Si vous utilisez `clickCollection.filterClickDetails`, l’[`onBeforeLinkClickSend`](onbeforelinkclicksend.md) de méthode obsolète doit être vide.
* La payload de l’événement doit contenir une valeur dans `xdm.web.webPageDetails.name` à un moment donné au cours de la visite du visiteur.

Si votre implémentation ne répond pas à toutes les exigences ci-dessus, alors cet objet n’a aucune incidence.

Les propriétés suivantes sont disponibles dans l’objet `clickCollection` :

| Propriété | Type | Description |
| --- | --- | --- |
| **`internalLinkEnabled`** | `boolean` | Détermine si les liens dans le domaine actuel sont automatiquement suivis. Par exemple, `https://example.com/index.html` à `https://example.com/product.html` serait considéré comme un lien interne. |
| **`downloadLinkEnabled`** | `boolean` | Détermine si la bibliothèque effectue le suivi des liens qui sont considérés comme des téléchargements en fonction de la propriété [`downloadLinkQualifier`](downloadlinkqualifier.md). |
| **`externalLinkEnabled`** | `boolean` | Détermine si les liens vers des domaines externes sont automatiquement suivis. Par exemple, `https://example.com` à `https://example.net` serait considéré comme un lien externe. |
| **`eventGroupingEnabled`** | `boolean` | Détermine si la bibliothèque attend l’événement « page vue » suivant pour envoyer les données de suivi des liens. La bibliothèque considère un événement comme une « page vue » lorsque les éléments suivants sont inclus dans la payload :<ul><li>`xdm.web.webPageDetails.name` contient une valeur de chaîne</li><li>`xdm.web.webPageDetails.pageViews.value` est supérieur à `0`</li></ul>Lorsque l’événement « page vue » se charge, la bibliothèque combine les données de suivi des liens stockées avec le reste des données de cet événement. L’activation de cette option réduit le nombre total d’événements que vous envoyez à Adobe. Si `internalLinkEnabled` est désactivé, cette variable n’a aucun effet. |
| **`sessionStorageEnabled`** | `boolean` | Détermine si les données de suivi des liens sont stockées dans le stockage de session au lieu de variables locales. Si `internalLinkEnabled` ou `eventGroupingEnabled` sont désactivés, cette variable n’a aucun effet.<br>Adobe recommande vivement d’activer cette variable lors de l’utilisation de `eventGroupingEnabled` en dehors des applications monopages. Si `eventGroupingEnabled` est activé alors que `sessionStorageEnabled` est désactivé, cliquer sur une nouvelle page entraîne la perte des données de suivi des liens, car elles ne sont pas conservées dans le stockage de la session. Étant donné que les applications monopages n’accèdent généralement pas à une nouvelle page, le stockage de session n’est pas nécessaire pour les pages SPA. |
| **`filterClickDetails`** | `function` | Fonction de rappel qui fournit des contrôles complets sur les données de suivi des liens que vous collectez. Vous pouvez utiliser cette fonction de rappel pour modifier, obscurcir ou abandonner l’envoi des données de suivi des liens. Ce rappel est utile lorsque vous souhaitez omettre des informations spécifiques, telles que des informations d’identification personnelle dans les liens. |

Si vous ne définissez pas cet objet dans la commande [`configure`](overview.md), les paramètres par défaut de cet objet dépendent de la valeur de [`clickCollectionEnabled`](clickcollectionenabled.md) :

* `internalLinkEnabled` : Correspond à `clickCollectionEnabled`
* `downloadLinkEnabled` : Correspond à `clickCollectionEnabled`
* `externalLinkEnabled` : Correspond à `clickCollectionEnabled`
* `eventGroupingEnabled` : la valeur par défaut est `false` ; doit être explicitement activé
* `sessionStorageEnabled` : la valeur par défaut est `false` ; doit être explicitement activé
* `filterClickDetails` : ne contient pas de fonction ; doit être explicitement enregistré

>[!TIP]
>
>Adobe recommande d’activer les `eventGroupingEnabled` lorsque `internalLinkEnabled` est activé, car cela réduit le nombre d’événements qui sont pris en compte dans l’utilisation contractuelle.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true,
    filterClickDetails: function(content) {
      // If the link is a clickable telephone number, anonymize it
      if(content.linkUrl?.includes("tel:")) {
        content.linkName = content.linkUrl = "Phone number";
      }
      // If the link is an email address, anonymize it
      if(content.linkUrl?.includes("mailto:")) {
        content.linkName = content.linkUrl = "Email address";
      }
    }
  }
});
```

## Configuration de la collecte des clics pour l’extension de balises Web SDK

Ces paramètres peuvent être configurés dans l’extension de balise Web SDK à l’aide des [&#x200B; Paramètres de configuration de la collecte de données &#x200B;](/help/tags/extensions/client/web-sdk/configure/data-collection.md).
