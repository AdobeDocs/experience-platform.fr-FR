---
title: clickCollectionEnabled
description: Découvrez comment configurer le SDK Web pour déterminer si les données de clic sur les liens sont automatiquement collectées.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# `clickCollectionEnabled`

La propriété `clickCollectionEnabled` est une valeur booléenne qui détermine si le SDK Web collecte automatiquement les données de lien. Si vous ne définissez pas cette variable, sa valeur par défaut est `true`, ce qui signifie que les données de suivi des liens sont automatiquement collectées par défaut. La définition de cette propriété sur `false` est utile lorsque vous préférez effectuer le suivi manuel des données de lien.

Lorsque `clickCollectionEnabled` est activé, les éléments XDM suivants sont automatiquement renseignés avec des données :

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Les liens internes, les liens de téléchargement et les liens de sortie sont automatiquement suivis par défaut lorsque cette valeur booléenne est activée. Si vous souhaitez plus de contrôle sur le suivi automatique des liens, Adobe recommande d’utiliser l’objet [`clickCollection`](clickcollection.md).

## Logique de suivi des liens automatique

Le SDK Web effectue le suivi de tous les clics sur les éléments d’HTML `<a>` et `<area>` s’il n’a pas d’attribut `onClick`. Les clics sont capturés avec un écouteur d’événement de clic [capture](https://www.w3.org/TR/uievents/#capture-phase) joint au document. Lorsqu’un utilisateur clique sur un lien valide, la logique suivante est exécutée dans l’ordre :

1. Si le lien correspond à des critères basés sur des valeurs dans [`downloadLinkQualifier`](downloadlinkqualifier.md), ou si le lien contient un attribut d’HTML `download`, `xdm.web.webInteraction.type` est défini sur `"download"` (si `clickCollection.downloadLinkEnabled` est activé).
1. Si le domaine cible du lien diffère du `window.location.hostname` actif, `xdm.web.webInteraction.type` est défini sur `"exit"` (si `clickCollection.exitLinkEnabled` est activé).
1. Si le lien ne remplit pas les critères pour `"download"` ou `"exit"`, `xdm.web.webInteraction.type` est défini sur `"other"`.

Dans tous les cas, `xdm.web.webInteraction.name` est défini sur l’étiquette de texte du lien et `xdm.web.webInteraction.URL` sur l’URL de destination du lien. Si vous souhaitez également définir le nom du lien sur l’URL, vous pouvez remplacer ce champ XDM à l’aide du rappel `filterClickDetails` dans l’objet `clickCollection`.

## Activation du suivi automatique des liens à l’aide de l’extension de balise SDK Web {#tag-extension}

Cette variable est automatiquement gérée par l’extension de balise ; vous n’avez pas besoin de la définir explicitement. Si l’un des éléments suivants est sélectionné lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md), les données de suivi des liens applicables sont collectées :

* [!UICONTROL Collecter les clics sur les liens internes]
* [!UICONTROL Collecter les clics sur les liens externes]
* [!UICONTROL Collecter les clics sur les liens de téléchargement]

Voir [`clickCollection`](clickcollection.md) pour plus d’informations.

## Activation du suivi automatique des liens à l’aide de la bibliothèque JavaScript du SDK Web {#library}

Définissez la valeur booléenne `clickCollectionEnabled` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration du SDK Web, elle est définie par défaut sur `true`. Définissez cette valeur sur `false` si vous préférez définir `xdm.web.webInteraction.type` et `xdm.web.webInteraction.value` manuellement.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
