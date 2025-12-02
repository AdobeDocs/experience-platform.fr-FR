---
title: downloadLinkQualifier
description: Permet de déterminer comment le suivi automatique des liens qualifie les liens de téléchargement.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `downloadLinkQualifier`

Si vous activez le suivi automatique des liens à l’aide de [`clickCollectionEnabled`](clickcollectionenabled.md), la propriété `downloadLinkQualifier` permet de déterminer les critères selon lesquels une URL doit être considérée comme un lien de téléchargement.

Cette propriété est une chaîne RegEx. Si l’URL cliquée correspond à cette expression régulière, `xdm.web.webInteraction.type` est défini sur `"download"`. Les liens sont également immédiatement classés comme liens de téléchargement s’ils incluent un attribut HTML `download`. Si `clickCollectionEnabled` n’est pas activé, cette propriété n’a aucun effet.

Définissez la chaîne de `downloadLinkQualifier` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété, la valeur par défaut est la suivante :

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Si vous souhaitez utiliser différents critères pour qualifier les liens de téléchargement, définissez cette propriété sur la valeur RegEx souhaitée.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```

## Télécharger le qualificateur de lien à l’aide de l’extension de balise Web SDK

L’équivalent de l’extension de balise Web SDK de ce champ se trouve sous [Paramètres de configuration de la collecte de données](/help/tags/extensions/client/web-sdk/configure/data-collection.md#download-link-qualifier) lors de la configuration de l’extension de balise.
