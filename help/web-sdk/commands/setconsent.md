---
title: setConsent
description: Utilisé sur chaque page pour suivre le consentement de l’utilisateur.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---

# setConsent

La variable `setConsent` indique au SDK Web s’il doit envoyer des données (inclusion), ignorer des données (exclusion) ou utiliser [`defaultConsent`](configure/defaultconsent.md) (consentement inconnu).

Le SDK Web prend en charge les normes suivantes :

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: les normes 1.0 et 2.0 sont prises en charge.
* **[Structure de transparence et de consentement de l’IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: si vous utilisez cette norme, le profil client en temps réel du visiteur est mis à jour avec les informations de consentement si votre mise en oeuvre est correctement configurée :
   1. Le schéma de profil individuel XDM contient la variable [Groupe de champs de consentement du TCF 2.0 de l’IAB](/help/xdm/field-groups/profile/iab.md).
   1. Le schéma Événement d’expérience contient la variable [Groupe de champs de consentement du TCF 2.0 de l’IAB](/help/xdm/field-groups/event/iab.md).
   1. Vous incluez les informations de consentement IAB dans l’événement [Objet XDM](sendevent/xdm.md). Le SDK Web n’inclut pas automatiquement les informations de consentement lors de l’envoi de données d’événement.

Après avoir utilisé cette commande, le SDK Web écrit les préférences de l’utilisateur dans un cookie. La prochaine fois que l’utilisateur charge votre site web dans le navigateur, le SDK récupère ces préférences persistantes pour déterminer si des événements peuvent être envoyés à Adobe.

Adobe vous recommande de stocker les préférences de boîte de dialogue de consentement séparément de celles du consentement du SDK Web. Le SDK Web ne permet pas de récupérer le consentement. Pour vous assurer que les préférences de l’utilisateur restent synchronisées avec le SDK, vous pouvez appeler la fonction `setConsent` à chaque chargement de page. Le SDK Web effectue uniquement un appel au serveur lorsque le consentement est modifié.

## Définition du consentement à l’aide de l’extension de balise SDK Web

La définition du consentement est effectuée en tant qu’action dans une règle dans l’interface des balises de collecte de données Adobe Experience Platform.

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez la variable [!UICONTROL Extension] du champ déroulant vers **[!UICONTROL SDK Web Adobe Experience Platform]**, puis définissez la variable [!UICONTROL Type d’action] to **[!UICONTROL Définition du consentement]**.
1. Définissez les champs de votre choix à droite, y compris **[!UICONTROL Standard]** et **[!UICONTROL Consentement général]**.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre workflow de publication.

Vous pouvez inclure plusieurs objets de consentement dans cette action.

## Définition du consentement à l’aide de la bibliothèque JavaScript du SDK Web

Exécutez la variable `setConsent` lors de l’appel de votre instance configurée du SDK Web. Vous pouvez inclure les objets suivants dans cette commande :

* **`consent[]`**: un tableau de `consent` objets. L’objet de consentement est formaté différemment selon la norme et la version que vous choisissez.
* **`identityMap`**: objet contrôlant la manière dont un ECID est généré et les informations de consentement des identifiants sont liées. Adobe recommande d’inclure cet objet lors de la `setConsent` est exécuté avant d’autres commandes, telles que [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: objet qui contient [remplacements de la configuration du flux de données](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0 standard `consent` objet

* **`standard`**: la norme de consentement que vous choisissez. Définissez cette propriété sur `"Adobe"` pour la norme Adobe 2.0.
* **`version`**: chaîne représentant la version de la norme de consentement. Définissez cette propriété sur `"2.0"` pour la norme Adobe 2.0.
* **`value`**: objet contenant des valeurs de consentement.
   * **`value.collect.val`**: valeur de consentement. Les valeurs valides sont `"y"` (inclusion) et `"n"` (exclusion).
   * **`value.metadata.time`**: date et heure auxquelles l’utilisateur a défini la valeur de consentement.

```js
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "collect": {
        "val": "y"
      },
      "metadata": {
        "time": "YYYY-03-17T15:48:42-07:00"
      }
    }
  }]
});
```

>[!TAB IAB TCF 2.0]

### Norme IAB TCF 2.0 `consent` objet

* **`standard`**: la norme de consentement que vous choisissez. Définissez cette propriété sur `"IAB TCF"` pour la norme IAB TCF 2.0.
* **`version`**: chaîne représentant la version de la norme de consentement. Définissez cette propriété sur `"2.0"` pour la norme IAB TCF 2.0.
* **`value`**: chaîne contenant la valeur de consentement.
* **`gdprApplies`**: valeur booléenne qui détermine si le RGPD s’applique à cette valeur de consentement. Sa valeur par défaut est `true`.
* **`gdprContainsPersonalData`**: valeur booléenne qui détermine si les données d’événement associées à cet utilisateur contiennent des données personnelles. Sa valeur par défaut est `false`.

```js
alloy("setConsent", {
  consent: [{
    "standard": "IAB TCF",
    "version": "2.0",
    "value": "CO052l-O052l-DGAMBFRACBgAIBAAAAABIYgEawAQEagAAAA",
    "gdprApplies": true,
    "gdprContainsPersonalData": true
  }]
});
```

>[!TAB Adobe 1.0]

### Adobe 1.0 standard `consent` objet

* **`standard`**: la norme de consentement que vous choisissez. Définissez cette propriété sur `"Adobe"` pour la norme Adobe 1.0.
* **`version`**: chaîne représentant la version de la norme de consentement. Définissez cette propriété sur `"1.0"` pour la norme Adobe 1.0.
* **`value.general`**: valeur de consentement. Les valeurs valides sont `"in"` (inclusion) et `"out"` (exclusion).

```js
// Set consent using the Adobe 1.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "1.0",
    "value": {
      "general": "in"
    }
  }]
});
```

>[!ENDTABS]
