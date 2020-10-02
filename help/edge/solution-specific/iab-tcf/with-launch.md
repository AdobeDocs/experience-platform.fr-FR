---
title: Utilisation d’IAB TCF 2.0 avec lancement
seo-title: Configuration du consentement IAB TCF 2.0 avec le lancement d’Adobe et le kit de développement Web Adobe Experience Platform
description: Découvrez comment configurer le consentement d’IAB TCF 2.0 avec le lancement d’Adobe et Adobe Experience Platform Web SDK
seo-description: Découvrez comment configurer le consentement d’IAB TCF 2.0 avec le lancement d’Adobe et Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 48cebe994b450b0dac5e6f256ab81827a7e8a0d5
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 0%

---


# Utilisation d’IAB TCF 2.0 avec Experience Platform Launch et de l’extension AEP Web SDK

Le Kit de développement logiciel Web Adobe Experience Platform (Adobe Experience Platform Web SDK) prend en charge Interactive Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0). Ce guide vous explique comment configurer une propriété Adobe Experience Platform Launch pour envoyer des informations de consentement IAB TCF 2.0 à l’Adobe à l’aide de l’extension AEP Web SDK Launch.

Si vous ne souhaitez pas utiliser d&#39;Experience Platform Launch, veuillez consulter le guide sur l&#39; [utilisation d&#39;IAB TCF 2.0 sans Experience Platform Launch](./without-launch.md).

## Prise en main

Pour utiliser IAB TCF 2.0 avec Experience Platform Launch et l&#39;extension AEP Web SDK, vous devez disposer d&#39;un schéma XDM et d&#39;un jeu de données. Si vous n&#39;avez défini aucune de ces options, consultez le guide [de début](../../getting-started/quick-start-with-launch.md) rapide du lancement du kitAdobe Experience Platform Web SDK avant de continuer.

En outre, ce guide vous demande de bien comprendre le SDK Web de Adobe Experience Platform. Pour une actualisation rapide, veuillez lire la présentation [du SDK Web](../../home.md) Adobe Experience Platform et la documentation sur les questions [](../../getting-started/web-sdk-faq.md) fréquentes.

## Définition du consentement par défaut

Dans la configuration de l&#39;extension, il existe un paramètre pour le consentement par défaut. Cela contrôle le comportement des clients qui n’ont pas de cookie de consentement. Si vous souhaitez mettre en file d’attente les Événements d’expérience pour les clients qui n’ont pas de cookie de consentement, définissez cette option sur `pending`.

>[!NOTE]
>
>Actuellement, il n’existe aucun moyen de définir cette variable de manière dynamique par le biais de l’extension Experience Platform Launch.

Pour plus d’informations sur le consentement par défaut, reportez-vous à la section [de consentement par](../../fundamentals/configuring-the-sdk.md#default-consent) défaut de la documentation de configuration du SDK.

## Mise à jour du Profil avec les informations de consentement {#consent-code-1}

Pour appeler l’ `setConsent` action lorsque les préférences de consentement de vos clients ont changé, vous devez créer une nouvelle règle d’Experience Platform Launch. Début en ajoutant un nouveau événement et en choisissant le type d&#39;événement &quot;Code personnalisé&quot; de l&#39;extension Core.

Utilisez l’exemple de code suivant pour votre nouveau événement :

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

* Définit deux éléments de données, l’un avec la chaîne de consentement et l’autre avec l’ `gdprApplies` indicateur. Cela s’avère utile ultérieurement lors de l’exécution de l’action &quot;Définir le consentement&quot;.

* Déclenche la règle lorsque les préférences de consentement ont changé. L’action &quot;Définir le consentement&quot; doit être utilisée chaque fois que les préférences de consentement ont changé. ajoutez une action &quot;Définir le consentement&quot; dans l’extension et remplissez le formulaire comme suit :

* Standard : &quot;IAB TCF&quot;
* Version : &quot;2.0&quot;
* Valeur : &quot;%IAB TCF Consent String%&quot;
* GDPR s&#39;applique : &quot;%IAB TCF Consent GDPR%&quot;

![Action de consentement du jeu IAB](../../../assets/iab_set_consent_action.png)

>[!IMPORTANT]
>
>Vous ne pouvez pas choisir ces éléments de données à l’aide du sélecteur d’éléments de données, car ils ont été créés à l’aide d’un code personnalisé. Vous devez saisir le nom de l’élément de données avec les signes de pourcentage. Ce code met à jour le profil de votre client avec ses nouvelles préférences de consentement chaque fois qu’il change. De plus, le serveur renvoie une valeur de cookie, ce qui peut empêcher le Adobe Experience Platform Web SDK d’enregistrer des Événements d’expérience.

## Création d’un élément de données XDM pour les Événements d’expérience

La chaîne de consentement doit être incluse dans le Événement d’expérience XDM. Pour ce faire, utilisez l’élément de données Objet XDM. Début en créant un nouvel élément de données d’objet XDM ou en utilisant un élément déjà créé pour l’envoi de événements. Si vous avez ajouté le mixin Confidentialité d’Experience Événement à votre schéma, vous devez disposer d’une `consentStrings` clé dans l’objet XDM.

1. Sélectionnez **[!UICONTROL consentStrings]**.

1. Choisissez **[!UICONTROL Fournir des éléments]** individuels et sélectionnez **[!UICONTROL Ajouter un élément]**.

1. Développez l’en-tête **[!UICONTROL consentString]** , puis développez le premier élément, puis renseignez les valeurs suivantes :

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`: %IAB Chaîne de consentement TCF%
* `gdprApplies`: %IAB TCF Consentement GDPR%

>[!IMPORTANT]
>
>Vous ne pouvez pas choisir ces éléments de données à l’aide du sélecteur d’éléments de données, car ils ont été créés à l’aide d’un code personnalisé. Vous devez saisir le nom de l’élément de données avec les signes de pourcentage.

## Envoi d’un premier Événement d’expérience avec des informations de consentement IAB TCF 2.0

Si le Événement d’expérience initial sur la page est déclenché avec un événement de chargement de page, il se peut que la chaîne de consentement n’ait pas encore été chargée. Cette règle est destinée à remplacer le événement de chargement de page actuel. Pour vous assurer que les informations de consentement sont chargées en premier, créez une règle et ajoutez le code suivant en tant que événement de code personnalisé :

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

Ce code est identique au code personnalisé précédent, sauf que les deux `useractioncomplete` `tcloaded` événements et les deux sont gérés. Le code [personnalisé](#consent-code-1) précédent ne se déclenche que lorsque le client choisit ses préférences pour la première fois. Ce code se déclenche également lorsque le client a déjà choisi ses préférences. Par exemple, au second chargement de page.

ajoutez une action &quot;Envoyer le Événement&quot; à partir de l’extension Adobe Experience Platform Web SDK. Dans le champ XDM, choisissez l’élément de données XDM que vous avez créé dans la section précédente.

## Envoi d’autres événements avec des informations de consentement IAB TCF 2.0

Lorsque des événements sont déclenchés après le Événement d’expérience initial, les deux éléments de données sont toujours définis et peuvent être utilisés pour envoyer les informations de consentement IAB. Utilisez le même élément de données XDM pour envoyer des événements futurs. Les informations du CCI TCF 2.0 sont incluses.

## Étapes suivantes

Maintenant que vous avez appris à utiliser IAB TCF 2.0 avec l’extension Adobe Experience Platform Web SDK, vous pouvez également choisir de vous intégrer à d’autres solutions d’Adobe telles que Adobe Analytics ou la plateforme de données client en temps réel. Pour plus d’informations, consultez l’aperçu [du Cadre de transparence et de consentement](./overview.md) IAB 2.0.
