---
title: clickCollection
description: Ajustez les paramètres de collection des clics.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# `clickCollection`

L’objet `clickCollection` contient plusieurs variables qui vous aident à contrôler les données de lien collectées automatiquement. Utilisez ces variables lorsque vous souhaitez inclure ou exclure des types de liens de la collecte de données.

[`clickCollectionEnabled`](clickcollectionenabled.md) doit être activé.

Elle est prise en charge sur le SDK Web 2.25.0 ou version ultérieure.

Les variables suivantes sont disponibles dans l’objet `clickCollection` :

* **`clickCollection.internalLinkEnabled`** : valeur booléenne qui détermine si les liens du domaine actuel sont automatiquement suivis. Par exemple, `https://example.com/index.html` à `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`** : valeur booléenne qui détermine si la bibliothèque effectue le suivi des liens qualifiés de téléchargements en fonction de la propriété [`downloadLinkQualifier`](downloadlinkqualifier.md).
* **`clickCollection.externalLinkEnabled`** : valeur booléenne qui détermine si les liens vers des domaines externes sont automatiquement suivis. Par exemple, `https://example.com` à `https://example.net`.
* **`clickCollection.eventGroupingEnabled`** : valeur booléenne qui détermine si la bibliothèque attend jusqu’à la page suivante pour envoyer les données de suivi des liens. Lorsque la page suivante se charge, combinez les données de suivi des liens à l’événement de chargement de page. L’activation de cette option réduit le nombre d’événements que vous envoyez à Adobe. Si `internalLinkEnabled` est désactivé, cette variable ne fait rien.
* **`clickCollection.sessionStorageEnabled`** : valeur booléenne qui détermine si les données de suivi des liens sont stockées dans l’enregistrement de session au lieu des variables locales. Si `internalLinkEnabled` ou `eventGroupingEnabled` sont désactivés, cette variable ne fait rien.

  Adobe recommande vivement d’activer cette variable lors de l’utilisation de `eventGroupingEnabled` en dehors des applications d’une seule page. Si `eventGroupingEnabled` est activé alors que `sessionStorageEnabled` est désactivé, cliquer sur une nouvelle page entraîne la perte des données de suivi des liens, car elles ne sont pas conservées dans l’enregistrement de session. Comme les applications d’une seule page ne naviguent généralement pas vers une nouvelle page, le stockage de session n’est pas nécessaire pour SPA pages.
* **`filterClickDetails`** : fonction de rappel qui fournit des contrôles complets sur les données de suivi des liens que vous collectez. Vous pouvez utiliser cette fonction de rappel pour modifier, obscurcir ou interrompre l’envoi de données de suivi des liens. Ce rappel est utile lorsque vous souhaitez omettre des informations spécifiques, telles que des informations d’identification personnelle dans les liens.

## Cliquez sur les paramètres de collecte à l’aide de l’extension de balise SDK Web.

Sélectionnez l’une des options suivantes lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) :

* [!UICONTROL Collecter les liens internes]
   * [!UICONTROL Options de regroupement d’événements] :
      * [!UICONTROL Aucun regroupement d’événements]
      * [!UICONTROL Groupement d’événements à l’aide de l’enregistrement de session]
      * [!UICONTROL Groupement d’événements à l’aide d’un objet local]
* [!UICONTROL Collecter des liens externes]
* [!UICONTROL Collect download links]
* [!UICONTROL Propriétés de clic du filtre]

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Faites défiler l’écran jusqu’à la section [!UICONTROL Collecte de données], puis sélectionnez les paramètres de collecte de clics de votre choix.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

Le rappel [!UICONTROL Propriétés de clic de filtre] ouvre un éditeur de code personnalisé qui vous permet d’insérer le code souhaité. Dans l’éditeur de code, vous avez accès aux variables suivantes :

* **`content.clickedElement`** : élément DOM sur lequel l’utilisateur a cliqué.
* **`content.pageName`** : nom de la page lorsque le clic s’est produit.
* **`content.linkName`** : nom du lien cliqué.
* **`content.linkRegion`** : région du lien sur lequel l’utilisateur a cliqué.
* **`content.linkType`** : type de lien (sortie, téléchargement ou autre).
* **`content.linkURL`** : URL de destination du lien cliqué.
* **`return true`** : Quittez immédiatement le rappel avec les valeurs de variable actuelles.
* **`return false`** : Quittez immédiatement le rappel et abandonnez la collecte de données.

Toutes les variables définies en dehors de `content` peuvent être utilisées, mais ne sont pas incluses dans la payload envoyée à Adobe.

## Cliquez sur Paramètres de collection à l’aide de la bibliothèque JavaScript SDK Web

Définissez les variables souhaitées dans l’objet `clickCollection` lors de l’exécution de la commande [`configure`](overview.md). Si elle n’est pas définie, les paramètres par défaut de cet objet dépendent de la valeur de [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled` : correspond à `clickCollectionEnabled`
* `downloadLinkEnabled` : correspond à `clickCollectionEnabled`
* `externalLinkEnabled` : correspond à `clickCollectionEnabled`
* `eventGroupingEnabled` : la valeur par défaut est `false` ; doit être explicitement activée
* `sessionStorageEnabled` : la valeur par défaut est `false` ; doit être explicitement activée
* `filterClickDetails` : ne contient pas de fonction ; doit être explicitement enregistré

>[!TIP]
>Adobe recommande d’activer `eventGroupingEnabled` lorsque `internalLinkEnabled` est activé, car cela réduit le nombre d’événements qui sont pris en compte dans l’utilisation contractuelle.

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
