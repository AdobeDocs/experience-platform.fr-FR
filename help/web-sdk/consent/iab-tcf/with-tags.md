---
title: Intégration de la prise en charge du TCF 2.0 de l’IAB à l’aide de balises et de l’extension du SDK Web Platform
description: Découvrez comment configurer le consentement du TCF 2.0 de l’IAB avec les balises et l’extension du SDK Web Adobe Experience Platform.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# Intégrer la prise en charge du TCF 2.0 de l’IAB à l’aide de balises et de l’extension du SDK Web Platform

Le SDK Web de Adobe Experience Platform prend en charge la version 2.0 de Interactive Advertising Bureau Transparency &amp; Consent Framework (IAB TCF 2.0). Ce guide vous explique comment configurer une propriété de balise pour envoyer des informations de consentement IAB TCF 2.0 à Adobe à l’aide de l’extension de balise du SDK Web Adobe Experience Platform.

Si vous ne souhaitez pas utiliser de balises, reportez-vous au guide sur l’ [utilisation de IAB TCF 2.0 sans balises](./without-tags.md).

## Commencer

Pour utiliser IAB TCF 2.0 avec des balises et l’extension SDK Web Platform, vous devez disposer d’un schéma XDM et d’un jeu de données disponibles.

En outre, ce guide nécessite une compréhension pratique du SDK Web de Adobe Experience Platform. Pour une actualisation rapide, consultez la [présentation du SDK Web de Adobe Experience Platform](../../home.md) et la documentation [Forum aux questions](../../faq.md) .

## Définition du consentement par défaut

Dans la configuration de l’extension, il existe un paramètre pour le consentement par défaut. Cela contrôle le comportement des clients qui n’ont pas de cookie de consentement. Si vous souhaitez mettre en file d’attente les événements d’expérience pour les clients qui n’ont pas de cookie de consentement, définissez-le sur `pending`. Si vous souhaitez ignorer les événements d’expérience pour les clients qui n’ont pas de cookie de consentement, définissez-le sur `out`. Vous pouvez également utiliser un élément de données pour définir dynamiquement la valeur de consentement par défaut. Voir [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) pour plus d’informations.

## Mise à jour du profil avec les informations de consentement {#consent-code-1}

Pour appeler l’action [`setConsent`](/help/web-sdk/commands/setconsent.md) lorsque les préférences de consentement de vos clients ont changé, créez une règle de balise. Commencez par ajouter un nouvel événement et sélectionnez le type d’événement &quot;Code personnalisé&quot; de l’extension Core.

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

* Définit deux éléments de données, l’un avec la chaîne de consentement et l’autre avec l’indicateur `gdprApplies`. Cela s’avérera utile ultérieurement lors du remplissage de l’action &quot;Définir le consentement&quot;.

* Déclenche la règle lorsque les préférences de consentement ont changé. L’action &quot;Définir le consentement&quot; doit être utilisée chaque fois que les préférences de consentement ont changé. Ajoutez une action &quot;Définir le consentement&quot; dans l’extension et remplissez le formulaire comme suit :

* Standard : &quot;IAB TCF&quot;
* Version : &quot;2.0&quot;
* Valeur : &quot;%IAB TCF Consent String%&quot;
* Le RGPD s’applique : &quot;%IAB TCF Consent RGPD%&quot;

![Action de consentement du jeu IAB](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>Vous ne pouvez pas choisir ces éléments de données à l’aide du sélecteur d’éléments de données, car ils ont été créés par le biais d’un code personnalisé. Vous devez saisir le nom de l’élément de données avec les signes de pourcentage. Ce code met à jour le profil de votre client avec ses nouvelles préférences de consentement chaque fois qu’il change. En outre, le serveur renvoie une valeur de cookie, ce qui peut empêcher le SDK Web de Adobe Experience Platform d’enregistrer des événements d’expérience.

## Création d’un élément de données XDM pour les événements d’expérience

La chaîne de consentement doit être incluse dans l’événement d’expérience XDM. Pour ce faire, utilisez l’élément de données Objet XDM . Commencez par créer un élément de données d’objet XDM ou utilisez-en un que vous avez déjà créé pour envoyer des événements. Si vous avez ajouté le groupe de champs Confidentialité des événements d’expérience à votre schéma, vous devez disposer d’une clé `consentStrings` dans l’objet XDM.

1. Sélectionnez **[!UICONTROL consentStrings]**.

1. Sélectionnez **[!UICONTROL Fournir des éléments individuels]** et sélectionnez **[!UICONTROL Ajouter un élément]**.

1. Développez l’en-tête **[!UICONTROL consentString]**, développez le premier élément, puis renseignez les valeurs suivantes :

* `consentStandard` : IAB TCF
* `consentStandardVersion` : 2.0
* `consentStringValue` : %IAB TCF Consent String%
* `gdprApplies` : %consentement du TCF de l’IAB RGPD%

>[!IMPORTANT]
>
>Vous ne pouvez pas choisir ces éléments de données à l’aide du sélecteur d’éléments de données, car ils ont été créés par le biais d’un code personnalisé. Vous devez saisir le nom de l’élément de données avec les signes de pourcentage.

## Envoi d’un événement d’expérience initial avec des informations de consentement du TCF 2.0 de l’IAB

Si l’événement d’expérience initial sur la page est déclenché avec un événement de chargement de page, la chaîne de consentement n’a peut-être pas encore été chargée. Cette règle est destinée à remplacer l’événement de chargement de page actuel. Pour vous assurer que les informations de consentement sont chargées en premier, créez une règle et ajoutez le code suivant en tant qu’événement de code personnalisé :

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

Ce code est identique au code personnalisé précédent, sauf que les événements `useractioncomplete` et `tcloaded` sont gérés. Le [code personnalisé précédent](#consent-code-1) ne se déclenche que lorsque le client choisit ses préférences pour la première fois. Ce code se déclenche également lorsque le client a déjà choisi ses préférences. Par exemple, au second chargement de la page.

Ajoutez une action &quot;Envoyer l’événement&quot; à partir de l’extension SDK Web Platform. Dans le champ XDM, sélectionnez l’élément de données XDM que vous avez créé dans la section précédente.

## Envoi d’autres événements avec des informations de consentement du TCF 2.0 de l’IAB

Lorsque des événements sont déclenchés après l’événement d’expérience initial, les deux éléments de données sont toujours définis et peuvent être utilisés pour envoyer les informations de consentement de l’IAB. Utilisez le même élément de données XDM pour envoyer des événements futurs. Les informations IAB TCF 2.0 sont incluses.

## Étapes suivantes

Maintenant que vous avez appris à utiliser IAB TCF 2.0 avec l’extension SDK Web Platform, vous pouvez également choisir d’intégrer avec d’autres solutions Adobe telles qu’Adobe Analytics ou Adobe Real-Time Customer Data Platform. Pour plus d’informations, consultez la [présentation de Transparency &amp; Consent Framework 2.0 de l’IAB](./overview.md) .
