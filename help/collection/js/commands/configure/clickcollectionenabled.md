---
title: clickCollectionEnabled
description: Découvrez comment configurer Web SDK pour déterminer si les données relatives aux clics sur les liens sont automatiquement collectées.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: 364b9adc406f732ea5ba450730397c4ce1bf03cf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# `clickCollectionEnabled`

La propriété `clickCollectionEnabled` est une valeur booléenne qui détermine si le SDK Web collecte automatiquement les données de lien. Si vous ne définissez pas cette variable, sa valeur par défaut est `true`, ce qui signifie que les données de suivi des liens sont automatiquement collectées par défaut. La définition de cette propriété sur `false` est utile dans les cas où vous préférez effectuer le suivi manuel des données de lien.

Lorsque `clickCollectionEnabled` est activé, les éléments XDM suivants sont automatiquement renseignés avec des données :

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Les liens internes, les liens de téléchargement et les liens de sortie sont tous automatiquement suivis par défaut lorsque cette valeur booléenne est activée. Pour mieux contrôler le suivi automatique des liens, Adobe recommande d’utiliser l’objet [`clickCollection`](clickcollection.md) .

## Logique de tracking automatique des liens

Le SDK Web suit tous les clics sur les éléments `<a>` et `<area>` d’HTML s’il ne dispose pas d’un attribut `onClick`. Les clics sont capturés à l’aide d’un écouteur d’événement de clic [capture](https://www.w3.org/TR/uievents/#capture-phase) joint au document. Lorsqu’un utilisateur clique sur un lien valide, la logique suivante est exécutée dans l’ordre :

1. Si le lien correspond à des critères basés sur des valeurs dans [`downloadLinkQualifier`](downloadlinkqualifier.md), ou s’il contient un attribut HTML `download`, `xdm.web.webInteraction.type` est défini sur `"download"` (si `clickCollection.downloadLinkEnabled` est activé).
1. Si le domaine cible du lien diffère du `window.location.hostname` actuel, `xdm.web.webInteraction.type` est défini sur `"exit"` (si `clickCollection.exitLinkEnabled` est activé).
1. Si le lien ne répond aux critères d’aucune des options `"download"` ou `"exit"`, `xdm.web.webInteraction.type` est défini sur `"other"`.

Dans tous les cas, `xdm.web.webInteraction.name` est défini sur le libellé du texte du lien et `xdm.web.webInteraction.URL` sur l’URL de destination du lien. Si vous souhaitez également définir le nom du lien sur l’URL, vous pouvez remplacer ce champ XDM à l’aide du rappel `filterClickDetails` dans l’objet `clickCollection` .

Définissez la valeur booléenne `clickCollectionEnabled` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration de Web SDK, elle est définie par défaut sur `true`. Définissez cette valeur sur `false` si vous préférez définir `xdm.web.webInteraction.type` et `xdm.web.webInteraction.value` manuellement.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```

## Prise en charge des éléments de [!DNL Shadow DOM] ouverts

Web SDK prend en charge le suivi automatique des clics pour les liens à l’intérieur des éléments **Shadow DOM** ouverts.

De nombreux sites web modernes utilisent des [composants web](https://developer.mozilla.org/en-US/docs/Web/Web_Components) pour créer des éléments d’interface utilisateur réutilisables et encapsulés. Ces composants utilisent souvent une technologie appelée [**Shadow DOM**](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM) pour séparer leur structure interne et leurs styles du reste de la page.

Il existe deux types de Shadow DOM :

* **Open Shadow DOM :** la structure interne est accessible pour JavaScript s’exécutant sur la page. D’autres scripts peuvent interagir avec le contenu du composant ou l’inspecter.
* **DOM fantôme fermé :** la structure interne est masquée du JavaScript en dehors du composant, ce qui la rend inaccessible pour le suivi ou la manipulation.

Web SDK effectue automatiquement le suivi des clics sur les éléments `<a>` et `<area>` dans les **éléments Shadow DOM**, comme pour les liens dans le document principal. Ce suivi permet de s’assurer que les clics sur les liens dans les composants web à l’aide de [!DNL Shadow DOM] ouverts sont inclus dans vos données d’analyse. Les clics à l’intérieur **des DOM fantômes fermés** ne sont pas suivis, car leur structure interne est masquée du code JavaScript fonctionnant en dehors du composant.

## Activer ou désactiver la collecte des clics pour l’extension de balise Web SDK

Consultez [Paramètres de configuration de la collecte de données](/help/tags/extensions/client/web-sdk/configure/data-collection.md) dans la documentation de l’extension Web SDK pour savoir comment effectuer ces actions à l’aide de balises.
