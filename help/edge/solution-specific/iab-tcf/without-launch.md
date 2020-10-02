---
title: Utilisation d’IAB TCF 2.0 sans lancement
seo-title: Configuration du consentement IAB TCF 2.0 avec le SDK Web Adobe Experience Platform
description: Découvrez comment configurer le consentement IAB TCF 2.0 avec le SDK Web Adobe Experience Platform
seo-description: Découvrez comment configurer le consentement IAB TCF 2.0 avec le SDK Web Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 48cebe994b450b0dac5e6f256ab81827a7e8a0d5
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---


# Utilisation d’IAB TCF 2.0 avec l’extension Adobe Experience Platform Web SDK

Ce guide explique comment intégrer Interactive Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0) au Adobe Experience Platform Web SDK sans utiliser d’Experience Platform Launch. Pour un aperçu de l’intégration avec IAB TCF 2.0, consultez la [présentation](./overview.md). Pour un guide sur la façon de s&#39;intégrer à l&#39;Experience Platform Launch, lisez le guide [IAB TCF 2.0 pour Experience Platform Launch](./with-launch.md).

## Prise en main

Ce guide utilise l&#39; `__tcfapi` interface pour accéder aux renseignements sur le consentement. Il peut s’avérer plus facile pour vous d’intégrer directement votre fournisseur de gestion de cloud (CMP). Toutefois, les informations contenues dans ce guide peuvent encore être utiles car les CMP offrent généralement des fonctionnalités similaires à l’API TCF.

>[!NOTE]
>
>Ces exemples supposent que lorsque le code est exécuté, `window.__tcfapi` il est défini sur la page. Les CMP peuvent fournir un hook où vous pouvez exécuter ces fonctions lorsque l&#39; `__tcfapi` objet est prêt.

Pour utiliser IAB TCF 2.0 avec Experience Platform Launch et l’extension AEP Web SDK, vous devez disposer d’un schéma XDM. Si vous n&#39;avez défini aucune de ces options, début en consultant le guide [de début rapide JavaScript du kit](../../getting-started/quick-start-without-launch.md) Adobe Experience Platform Web SDK avant de continuer.

En outre, ce guide vous demande de bien comprendre le SDK Web de Adobe Experience Platform. Pour une actualisation rapide, veuillez lire la présentation [du SDK Web](../../home.md) Adobe Experience Platform et la documentation sur les questions [](../../getting-started/web-sdk-faq.md) fréquentes.

## Activation du consentement par défaut

Si vous souhaitez traiter tous les utilisateurs inconnus de la même manière, vous pouvez définir le consentement par défaut sur `pending`. Cette option met en file d’attente les Événements d’expérience jusqu’à ce que les préférences de consentement soient reçues.

Pour plus d&#39;informations sur le consentement par défaut, reportez-vous à la section [de consentement par](../../fundamentals/configuring-the-sdk.md#default-consent) défaut de la documentation de configuration du SDK Web de la plate-forme.

### Définition du consentement par défaut en fonction de `gdprApplies`

Certains CMP permettent de déterminer si le Règlement général sur la protection des données (RGPD) s&#39;applique au client. Si vous souhaitez obtenir le consentement des clients pour lesquels GDPR ne s’applique pas, vous pouvez utiliser l’ `gdprApplies` indicateur dans l’appel de l’API TCF.

L’exemple suivant illustre une façon de procéder :

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

Dans cet exemple, la `configure` commande est appelée une fois `tcData` obtenue à partir de l’API TCF. Si `gdprApplies` la valeur est true, le consentement par défaut est défini sur `pending`. Si `gdprApplies` la valeur est false, le consentement par défaut est défini sur `in`. Veillez à renseigner la `alloyConfiguration` variable avec votre configuration.

>[!NOTE]
>
>Lorsque le consentement par défaut est défini sur `in`, la `setConsent` commande peut toujours être utilisée pour enregistrer vos préférences de consentement des clients.

## Utilisation du événement setConsent

L’API TCF 2.0 de l’IAB fournit un événement pour le moment où le consentement est mis à jour par le client. Cela se produit lorsque le client définit initialement ses préférences et lorsque le client met à jour ses préférences.

L’exemple suivant illustre une façon de procéder :

```javascript
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

Ce bloc de code écoute le `useractioncomplete` événement, puis définit le consentement, en transmettant la chaîne de consentement et l&#39; `gdprApplies` indicateur. Si vous disposez d’identités personnalisées pour vos clients, veillez à renseigner la `identityMap` variable. Consultez le guide sur le consentement [](../../fundamentals/supporting-consent.md) à l&#39;appui pour plus d&#39;information sur l&#39;appel `setConsent`.

## Inclusion des informations de consentement dans sendEvent

Dans les schémas XDM, vous pouvez stocker les informations de préférence de consentement dans les Événements d’expérience. Il existe deux façons d’ajouter ces informations à chaque événement.

Tout d&#39;abord, vous pouvez fournir le schéma XDM approprié à chaque `sendEvent` appel. L’exemple suivant illustre une façon de procéder :

```javascript
var sendEventOptions = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    sendEventOptions.xdm.consentStrings = [{
      consentStandard: "IAB TCF"
      consentStandardVersion: "2.0"
      consentStringValue: tcData.tcString,
      gdprApplies: tcData.gdprApplies
    }];
    window.alloy("sendEvent", sendEventOptions);
  }
});
```

Cet exemple récupère les informations de consentement pour l’API TCF, puis envoie un événement avec les informations de consentement ajoutées au schéma XDM. Consultez le guide des événements [de](../../fundamentals/tracking-events.md) suivi pour comprendre ce qui doit figurer dans les `sendEvent` options de commande.

L’autre moyen d’ajouter les informations de consentement à chaque requête consiste à utiliser le rappel `onBeforeEventSend` . Pour plus d’informations sur la manière de procéder, consultez la section sur la [modification des événements globalement](../../fundamentals/tracking-events.md#modifying-events-globally) dans la documentation des événements de suivi.

## Étapes suivantes

Maintenant que vous avez appris à utiliser IAB TCF 2.0 avec l’extension Adobe Experience Platform Web SDK, vous pouvez également choisir de vous intégrer à d’autres solutions d’Adobe telles que Adobe Analytics ou la plateforme de données client en temps réel. Pour plus d’informations, consultez l’aperçu [du Cadre de transparence et de consentement](./overview.md) IAB 2.0.
