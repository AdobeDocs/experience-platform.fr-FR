---
title: downloadLinkQualifier
description: Permet de déterminer comment le suivi automatique des liens qualifie les liens de téléchargement.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

Si vous activez le suivi automatique des liens en utilisant [`clickCollectionEnabled`](clickcollectionenabled.md), la variable `downloadLinkQualifier` permet de déterminer les critères pour qu’une URL soit considérée comme un lien de téléchargement.

Cette propriété est une chaîne regex. Si l’URL sur laquelle l’utilisateur a cliqué correspond à cette expression régulière, `xdm.web.webInteraction.type` est défini sur `"download"`. Les liens sont également immédiatement classés comme lien de téléchargement s’ils incluent une `download` Attribut HTML. If `clickCollectionEnabled` n’est pas activée, cette propriété ne fait rien.

## Télécharger le qualificateur de lien à l’aide de l’extension de balise du SDK Web

Activez la variable **[!UICONTROL Activer la collecte de données de clic]** , puis saisissez le texte de votre choix sous **[!UICONTROL Qualificateur de lien de téléchargement]** when [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Collecte de données] , puis cochez la case **[!UICONTROL Activer la collecte de données de clic]**.
1. Une fois activée, la variable **[!UICONTROL Qualificateur de lien de téléchargement]** la zone de texte s’affiche. Saisissez la valeur souhaitée. Des boutons sont également disponibles pour tester l’expression régulière et restaurer la valeur par défaut.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Télécharger le qualificateur de lien à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la variable `downloadLinkQualifier` chaîne lors de l’exécution de la variable `configure` . Si vous omettez cette propriété, la valeur par défaut est la suivante :

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
