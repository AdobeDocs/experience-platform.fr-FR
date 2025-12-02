---
title: edgeBasePath
description: Chemin de base du point d’entrée utilisé pour interagir avec les services Adobe.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 1fa7b48f99948a5252635dc1a8c5142fea5df57b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# `edgeBasePath`

La propriété `edgeBasePath` modifie le chemin de destination lorsque vous interagissez avec les services Adobe. Adobe peut vous demander de modifier cette variable si vous participez à des programmes alpha ou bêta pour la collecte de données. La plupart des organisations n’ont pas besoin de définir ou de modifier cette propriété.

Définissez le champ de texte `edgeBasePath` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété, la valeur par défaut est `ee`. Adobe recommande d’omettre cette propriété de la plupart des configurations.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```

## Chemin de base Edge utilisant l’extension de balise Web SDK

L’équivalent de l’extension de balise Web SDK de ce champ se trouve sous [Paramètres de configuration avancés](/help/tags/extensions/client/web-sdk/configure/advanced-settings.md) lors de la configuration de l’extension de balise.
