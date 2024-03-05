---
title: defaultConsent
description: Définissez la méthode de collecte du consentement par défaut.
source-git-commit: b9db136a9077e3420bfeb44ae45e7d72c322acbb
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# `defaultConsent`

La variable `defaultConsent` détermine la manière dont vous gérez le consentement pour la collecte de données avant d’appeler la méthode [`setConsent`](../setconsent.md) . Cette propriété est utile lorsque vous ne souhaitez pas collecter accidentellement des données d’individus résidant dans des zones où le consentement est requis avant de collecter des données.

Cette propriété accepte trois valeurs :

* **Dans**: la collecte des données se poursuit normalement, jusqu’à ce que l’utilisateur se désinscrive.
* **Out**: les données sont définitivement ignorées jusqu’à ce que l’utilisateur se connecte.
* **En attente**: les données sont stockées localement jusqu’à ce que l’utilisateur choisisse d’utiliser la variable [`setConsent`](../setconsent.md) . Les données ne persistent pas entre les chargements de page.

Si un visiteur ne figure pas dans la compétence du Règlement général sur la protection des données (RGPD), le consentement par défaut peut être défini sur `in`. Le consentement par défaut des visiteurs se trouvant dans la juridiction du RGPD peut être défini sur `pending`. Votre plateforme de gestion du consentement (CMP) peut détecter la région du client et fournir l’indicateur `gdprApplies` à IAB TCF 2.0. Cet indicateur peut être utilisé pour définir le consentement par défaut.

## Définition du consentement par défaut à l’aide de l’extension de balise SDK Web

Sélectionnez un bouton radio sous **[!UICONTROL Consentement par défaut]** when [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Privacy] , puis sélectionnez la **[!UICONTROL Consentement par défaut]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Définition du consentement par défaut à l’aide de la bibliothèque JavaScript du SDK Web

Définissez la variable `defaultConsent` de chaîne au niveau de consentement souhaité lors de l’exécution de la propriété `configure` . Cette propriété est sensible à la casse et ne prend en charge que les trois valeurs suivantes : `"in"`, `"out"`, et `"pending"`. Si vous tentez d’utiliser une autre valeur, la bibliothèque renvoie une erreur.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
