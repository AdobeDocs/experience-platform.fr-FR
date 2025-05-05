---
title: Intégrer la prise en charge d’IAB TCF 2.0 à l’aide de Adobe Experience Platform Web SDK
description: Découvrez comment configurer la prise en charge de l’IAB TCF 2.0 pour votre site web sans utiliser de balises.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# Intégrer la prise en charge d’IAB TCF 2.0 à Experience Platform Web SDK

Ce guide explique comment intégrer Interactive Advertising Bureau Transparency &amp; Consent Framework version 2.0 (IAB TCF 2.0) à Adobe Experience Platform Web SDK sans utiliser de balises. Pour une présentation de l’intégration à IAB TCF 2.0, lisez la [présentation](./overview.md). Pour obtenir un guide sur l’intégration aux balises, consultez le guide [IAB TCF 2.0 pour les balises](./with-tags.md).

## Commencer

Ce guide utilise l’interface `__tcfapi` pour accéder aux informations de consentement. Il peut être plus facile pour vous d’intégrer directement à votre fournisseur de gestion cloud (CMP). Toutefois, les informations contenues dans ce guide peuvent s’avérer utiles, car les CMP offrent généralement des fonctionnalités similaires à l’API TCF.

>[!NOTE]
>
>Ces exemples supposent que lorsque le code est exécuté, `window.__tcfapi` est défini sur la page. Les CMP peuvent fournir un hook dans lequel vous pouvez exécuter ces fonctions lorsque l’objet `__tcfapi` est prêt.

Pour utiliser IAB TCF 2.0 avec les balises et l’extension Adobe Experience Platform Web SDK, vous devez disposer d’un schéma XDM. Si vous n’avez configuré aucune de ces options, commencez par afficher cette page avant de continuer.

En outre, ce guide nécessite une compréhension du fonctionnement de Adobe Experience Platform Web SDK. Pour une rapide mise à jour, veuillez lire la présentation de Adobe Experience Platform Web SDK [&#128279;](../../home.md) et la documentation [Questions fréquentes](../../faq.md).

## Activer le consentement par défaut

Si vous souhaitez traiter tous les utilisateurs inconnus de la même manière, vous pouvez définir [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) sur `pending` ou `out`. Cette option met les événements d’expérience en file d’attente ou les ignore jusqu’à ce que les préférences de consentement soient reçues.

### Définition du consentement par défaut en fonction de `gdprApplies`

Certaines CMP permettent de déterminer si le Règlement général sur la protection des données (RGPD) s’applique au client. Si vous souhaitez supposer le consentement des clients pour lesquels le RGPD ne s’applique pas, vous pouvez utiliser l’indicateur `gdprApplies` dans l’appel API TCF.

L’exemple suivant illustre une méthode pour ce faire :

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

Dans cet exemple, la commande `configure` est appelée après l’obtention du `tcData` à partir de l’API TCF. Si `gdprApplies` est vrai, le consentement par défaut est défini sur `pending`. Si `gdprApplies` est faux, le consentement par défaut est défini sur `in`. Veillez à renseigner la variable `alloyConfiguration` avec votre configuration.

>[!NOTE]
>
>Lorsque le consentement par défaut est défini sur `in`, la commande `setConsent` peut toujours être utilisée pour enregistrer les préférences de consentement de vos clients.

## Utilisation de l’événement setConsent

L’API IAB TCF 2.0 fournit un événement pour le moment où le consentement est mis à jour par le client. Cela se produit lorsque le client définit initialement ses préférences et lorsqu’il les met à jour.

L’exemple suivant illustre une méthode pour ce faire :

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

Ce bloc de code écoute l’événement de `useractioncomplete`, puis définit le consentement en transmettant la chaîne de consentement et l’indicateur de `gdprApplies`. Si vous disposez d’identités personnalisées pour vos clients, veillez à renseigner la variable `identityMap` . Pour plus d’informations, consultez le guide sur [setConsent](../../../web-sdk/commands/setconsent.md).

## Inclusion des informations de consentement dans sendEvent

Dans les schémas XDM, vous pouvez stocker les informations de préférence de consentement des événements d’expérience. Il existe deux manières d’ajouter ces informations à chaque événement.

Tout d’abord, vous pouvez fournir le schéma XDM approprié à chaque appel `sendEvent`. L’exemple suivant illustre une méthode pour ce faire :

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

Cet exemple récupère les informations de consentement pour l’API TCF, puis envoie un événement avec les informations de consentement ajoutées au schéma XDM.

L’autre façon d’ajouter les informations de consentement à chaque requête consiste à utiliser le rappel [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md).

## Étapes suivantes

Maintenant que vous avez appris à utiliser IAB TCF 2.0 avec l’extension Experience Platform Web SDK, vous pouvez également choisir de l’intégrer à d’autres solutions Adobe telles qu’Adobe Analytics ou Adobe Real-Time Customer Data Platform. Pour plus d’informations, consultez la présentation du [Cadre de transparence et de consentement 2.0 de l’IAB](./overview.md).
