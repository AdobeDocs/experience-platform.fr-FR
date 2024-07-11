---
title: clickCollection
description: Ajustez les paramètres de collection des clics.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---


# `clickCollection`

La variable `clickCollection` contient plusieurs variables qui vous aident à contrôler les données de lien collectées automatiquement. Utilisez ces variables lorsque vous souhaitez inclure ou exclure des types de liens de la collecte de données.

Cela nécessite [`clickCollectionEnabled`](clickcollectionenabled.md) à activer.

Elle est prise en charge sur le SDK Web 2.25.0 ou version ultérieure.

Les variables suivantes sont disponibles dans la variable `clickCollection` objet :

* **`clickCollection.internalLinkEnabled`**: valeur booléenne qui détermine si les liens du domaine actif sont automatiquement suivis. Par exemple : `https://example.com/index.html` to `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: valeur booléenne qui détermine si la bibliothèque effectue le suivi des liens qualifiés de téléchargements en fonction de la variable [`downloadLinkQualifier`](downloadlinkqualifier.md) .
* **`clickCollection.externalLinkEnabled`**: valeur booléenne qui détermine si les liens vers des domaines externes sont automatiquement suivis. Par exemple : `https://example.com` to `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: valeur booléenne qui détermine si la bibliothèque attend jusqu’à la page suivante pour envoyer les données de suivi des liens. Lorsque la page suivante se charge, combinez les données de suivi des liens à l’événement de chargement de page. L’activation de cette option réduit le nombre d’événements que vous envoyez à Adobe. If `internalLinkEnabled` est désactivée, alors cette variable ne fait rien.
* **`clickCollection.sessionStorageEnabled`**: valeur booléenne qui détermine si les données de suivi des liens sont stockées dans l’enregistrement de session au lieu des variables locales. If `internalLinkEnabled` ou `eventGroupingEnabled` sont désactivées, alors cette variable ne fait rien.

  Adobe recommande vivement d’activer cette variable lorsque vous utilisez `eventGroupingEnabled`. If `eventGroupingEnabled` est activé pendant `sessionStorageEnabled` est désactivée, le fait de cliquer sur une nouvelle page entraîne la perte des données de suivi des liens, car elles ne sont pas conservées dans l’enregistrement de session. Bien qu’il soit acceptable de désactiver `sessionStorageEnabled` dans les applications d’une seule page, il n’est pas idéal pour les pages non SPA.
* **`filterClickDetails`**: fonction de rappel qui fournit des contrôles complets sur les données de suivi des liens que vous collectez. Vous pouvez utiliser cette fonction de rappel pour modifier, obscurcir ou interrompre l’envoi de données de suivi des liens. Ce rappel est utile lorsque vous souhaitez omettre des informations spécifiques, telles que des informations d’identification personnelle dans les liens.

## Cliquez sur les paramètres de collecte à l’aide de l’extension de balise SDK Web.

Sélectionnez la variable **[!UICONTROL Activer la collecte de données de clic]** , [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). L’activation de cette case à cocher affiche les options suivantes relatives à la collection de clics :

* [!UICONTROL Liens internes]
   * [!UICONTROL Activation du regroupement d’événements]
   * [!UICONTROL Activation du stockage de session]
* [!UICONTROL Liens externes]
* [!UICONTROL Liens de téléchargement]
* [!UICONTROL Filtrer les propriétés de clic]

1. Connexion à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Collecte de données] , puis cochez la case **[!UICONTROL Activer la collecte de données de clic]**.
1. Sélectionnez les paramètres de collection de clics souhaités.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

La variable [!UICONTROL Filtrer les propriétés de clic] callback ouvre un éditeur de code personnalisé qui vous permet d’insérer le code souhaité. Dans l’éditeur de code, vous avez accès aux variables suivantes :

* **`content.clickedElement`**: élément DOM sur lequel l’utilisateur a cliqué.
* **`content.pageName`**: nom de la page lorsque le clic s’est produit.
* **`content.linkName`**: nom du lien cliqué.
* **`content.linkRegion`**: région du lien sur lequel l’utilisateur a cliqué.
* **`content.linkType`**: type de lien (sortie, téléchargement ou autre).
* **`content.linkURL`**: URL de destination du lien cliqué.
* **`return true`**: quittez immédiatement le rappel avec les valeurs de variable actuelles.
* **`return false`**: quittez immédiatement le rappel et abandonnez la collecte des données.

Toute variable définie en dehors de `content` peuvent être utilisées, mais ne sont pas incluses dans la payload envoyée à Adobe.

## Cliquez sur Paramètres de collection à l’aide de la bibliothèque JavaScript SDK Web

Définissez les variables de votre choix dans le `clickCollection` lors de l’exécution de l’objet [`configure`](overview.md) . Si elle n’est pas définie, les paramètres par défaut de cet objet dépendent de la valeur de [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`: correspond à `clickCollectionEnabled`
* `downloadLinkEnabled`: correspond à `clickCollectionEnabled`
* `externalLinkEnabled`: correspond à `clickCollectionEnabled`
* `eventGroupingEnabled`: la valeur par défaut est `false`; doit être explicitement activé.
* `sessionStorageEnabled`: la valeur par défaut est `false`; doit être explicitement activé.
* `filterClickDetails`: ne contient pas de fonction ; doit être explicitement enregistré.

>[!TIP]
>Adobe recommande d’activer `eventGroupingEnabled`, car cela permet de réduire le nombre d’événements qui sont pris en compte dans l’utilisation contractuelle.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
