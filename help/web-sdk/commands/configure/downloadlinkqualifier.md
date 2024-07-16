---
title: downloadLinkQualifier
description: Permet de déterminer comment le suivi automatique des liens qualifie les liens de téléchargement.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

Si vous activez le suivi automatique des liens à l’aide de [`clickCollectionEnabled`](clickcollectionenabled.md), la propriété `downloadLinkQualifier` permet de déterminer les critères pour qu’une URL soit considérée comme un lien de téléchargement.

Cette propriété est une chaîne regex. Si l’URL sur laquelle l’utilisateur a cliqué correspond à cette expression régulière, `xdm.web.webInteraction.type` est défini sur `"download"`. Les liens sont également immédiatement classés comme lien de téléchargement s’ils incluent un attribut d’HTML `download`. Si `clickCollectionEnabled` n’est pas activé, cette propriété ne fait rien.

## Télécharger le qualificateur de lien à l’aide de l’extension de balise du SDK Web

Activez la case à cocher **[!UICONTROL Activer la collecte de données de clic]** , puis saisissez le texte de votre choix sous **[!UICONTROL Télécharger le qualificateur de lien]** lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Faites défiler l’écran jusqu’à la section [!UICONTROL Collecte de données], puis cochez la case **[!UICONTROL Activer la collecte de données de clic]**.
1. Une fois activée, la zone de texte **[!UICONTROL Télécharger le qualificateur de lien]** s’affiche. Saisissez la valeur souhaitée. Des boutons sont également disponibles pour tester l’expression régulière et restaurer la valeur par défaut.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Télécharger le qualificateur de lien à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la chaîne `downloadLinkQualifier` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété, la valeur par défaut est la suivante :

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Si vous souhaitez utiliser différents critères pour qualifier les liens de téléchargement, définissez cette propriété sur la valeur regex souhaitée.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": true,
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```
