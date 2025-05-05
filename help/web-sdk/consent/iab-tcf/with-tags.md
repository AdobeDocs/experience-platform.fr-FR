---
title: Intégrer la prise en charge de l’IAB TCF 2.0 à l’aide des balises et de l’extension Experience Platform Web SDK
description: Découvrez comment configurer le consentement IAB TCF 2.0 avec les balises et l’extension Adobe Experience Platform Web SDK.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# Intégrer la prise en charge de l’IAB TCF 2.0 à l’aide des balises et de l’extension Experience Platform Web SDK

Adobe Experience Platform Web SDK prend en charge Interactive Advertising Bureau Transparency &amp; Consent Framework version 2.0 (IAB TCF 2.0). Ce guide explique comment configurer une propriété de balise pour envoyer des informations de consentement IAB TCF 2.0 à Adobe à l’aide de l’extension de balise Adobe Experience Platform Web SDK.

Si vous ne souhaitez pas utiliser de balises, reportez-vous au guide sur l’[utilisation d’IAB TCF 2.0 sans balises](./without-tags.md).

## Commencer

Pour utiliser IAB TCF 2.0 avec les balises et l’extension Experience Platform Web SDK, vous devez disposer d’un schéma XDM et d’un jeu de données.

En outre, ce guide nécessite une compréhension du fonctionnement de Adobe Experience Platform Web SDK. Pour une rapide mise à jour, veuillez lire la présentation de Adobe Experience Platform Web SDK [&#128279;](../../home.md) et la documentation [Questions fréquentes](../../faq.md).

## Définition du consentement par défaut

Dans la configuration de l’extension, il existe un paramètre pour le consentement par défaut. Cela contrôle le comportement des clients qui ne disposent pas d’un cookie de consentement. Si vous souhaitez mettre en file d’attente les événements d’expérience pour les clients qui ne disposent pas d’un cookie de consentement, définissez ce paramètre sur `pending`. Si vous souhaitez ignorer les événements d’expérience pour les clients qui ne disposent pas d’un cookie de consentement, définissez ce paramètre sur `out`. Vous pouvez également utiliser un élément de données pour définir de manière dynamique la valeur de consentement par défaut. Voir [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) pour plus d’informations.

## Mise à jour du profil avec les informations de consentement {#consent-code-1}

Pour appeler l’action [`setConsent`](/help/web-sdk/commands/setconsent.md) lorsque les préférences de consentement de vos clients ont changé, créez une règle de balise. Commencez par ajouter un nouvel événement et choisissez le type d’événement « Code personnalisé » de l’extension Core.

Utilisez l’exemple de code suivant pour votre nouvel événement :

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Ce code personnalisé effectue deux opérations :

* Définit deux éléments de données, l’un avec la chaîne de consentement et l’autre avec l’indicateur `gdprApplies`. Cela s’avère utile ultérieurement lors du remplissage de l’action « Définir le consentement ».

* Déclenche la règle lorsque les préférences de consentement ont été modifiées. L’action « Définir le consentement » doit être utilisée chaque fois que les préférences de consentement ont changé. Ajoutez une action « Définir le consentement » dans l’extension et remplissez le formulaire comme suit :

* Standard : « IAB TCF »
* Version : « 2.0 »
* Valeur : « %IAB TCF Consent String% »
* RGPD : « %IAB TCF Consent GDPR% »

![IAB Set Consent Action](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>Vous ne pouvez pas choisir ces éléments de données à l’aide du sélecteur d’éléments de données, car ils ont été créés via du code personnalisé. Vous devez saisir le nom de l’élément de données avec les signes de pourcentage. Ce code met à jour le profil de votre client avec ses nouvelles préférences de consentement chaque fois qu’il les modifie. En outre, le serveur renvoie une valeur de cookie, ce qui peut empêcher Adobe Experience Platform Web SDK d’enregistrer les événements d’expérience.

## Création d’un élément de données XDM pour les événements d’expérience

La chaîne de consentement doit être incluse dans l’événement d’expérience XDM. Pour ce faire, utilisez l’élément de données Objet XDM . Commencez par créer un élément de données d’objet XDM ou utilisez-en un que vous avez déjà créé pour envoyer des événements. Si vous avez ajouté le groupe de champs de schéma Confidentialité des événements d’expérience à votre schéma, vous devez disposer d’une clé `consentStrings` dans l’objet XDM.

1. Sélectionnez **[!UICONTROL consentStrings]**.

1. Choisissez **[!UICONTROL Fournir des éléments individuels]** puis sélectionnez **[!UICONTROL Ajouter un élément]**.

1. Développez l’en-tête **[!UICONTROL consentString]**, développez le premier élément, puis renseignez les valeurs suivantes :

* `consentStandard` : IAB TCF
* `consentStandardVersion` : 2.0
* `consentStringValue` : %IAB TCF Chaîne de consentement%
* `gdprApplies` : %IAB TCF Consent GDPR%

>[!IMPORTANT]
>
>Vous ne pouvez pas choisir ces éléments de données à l’aide du sélecteur d’éléments de données, car ils ont été créés via du code personnalisé. Vous devez saisir le nom de l’élément de données avec les signes de pourcentage.

## Envoi d’un événement d’expérience initial avec des informations de consentement IAB TCF 2.0

Si l’événement d’expérience initial sur la page est déclenché avec un événement de chargement de page, la chaîne de consentement peut ne pas encore avoir été chargée. Cette règle est destinée à remplacer votre événement de chargement de page actuel. Pour vous assurer que les informations de consentement sont chargées en premier, créez une règle et ajoutez le code suivant en tant qu’événement de code personnalisé :

```javascript
// Wait for window.__tcfapi to be defined, then trigger when there is a consent string
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF GDPR Applies", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn"t defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Ce code est identique au code personnalisé précédent, sauf que les événements `useractioncomplete` et `tcloaded` sont gérés ensemble. Le [code personnalisé précédent](#consent-code-1) ne se déclenche que lorsque le client choisit ses préférences pour la première fois. Ce code se déclenche également lorsque le client a déjà choisi ses préférences. Par exemple, lors du deuxième chargement de la page.

Ajoutez une action « Envoyer l’événement » à partir de l’extension Experience Platform Web SDK. Dans le champ XDM , choisissez l’élément de données XDM que vous avez créé dans la section précédente.

## Envoi d’autres événements avec les informations de consentement IAB TCF 2.0

Lorsque des événements sont déclenchés après l’événement d’expérience initial, les deux éléments de données sont toujours définis et peuvent être utilisés pour envoyer les informations de consentement IAB. Utilisez le même élément de données XDM pour envoyer des événements futurs. Les informations de l’IAB TCF 2.0 sont incluses.

## Étapes suivantes

Maintenant que vous avez appris à utiliser IAB TCF 2.0 avec l’extension Experience Platform Web SDK, vous pouvez également choisir de l’intégrer à d’autres solutions Adobe telles qu’Adobe Analytics ou Adobe Real-Time Customer Data Platform. Pour plus d’informations, consultez la présentation du [Cadre de transparence et de consentement 2.0 de l’IAB](./overview.md).
