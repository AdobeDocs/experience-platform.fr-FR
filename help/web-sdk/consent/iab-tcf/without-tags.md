---
title: Intégration de la prise en charge du TCF 2.0 de l’IAB à l’aide du SDK Web de Adobe Experience Platform
description: Découvrez comment configurer la prise en charge du TCF 2.0 de l’IAB pour votre site web sans utiliser de balises.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Intégration de la prise en charge du TCF 2.0 de l’IAB au SDK Web de Platform

Ce guide explique comment intégrer la version 2.0 (IAB TCF 2.0) du Interactive Advertising Bureau Transparency &amp; Consent Framework avec le SDK Web de Adobe Experience Platform sans utiliser de balises. Pour un aperçu de l’intégration à IAB TCF 2.0, lisez la [présentation](./overview.md). Pour un guide sur l’intégration aux balises, consultez le [guide IAB TCF 2.0 pour les balises](./with-tags.md).

## Commencer

Ce guide utilise l’interface `__tcfapi` pour accéder aux informations de consentement. Il peut être plus facile d’intégrer directement votre fournisseur de gestion du cloud (CMP). Toutefois, les informations contenues dans ce guide peuvent être utiles, car les CMP offrent généralement des fonctionnalités similaires à l’API TCF.

>[!NOTE]
>
>Ces exemples supposent qu’au moment de l’exécution du code, `window.__tcfapi` est défini sur la page. Les CMP peuvent fournir un crochet où vous pouvez exécuter ces fonctions lorsque l’objet `__tcfapi` est prêt.

Pour utiliser IAB TCF 2.0 avec des balises et l’extension SDK Web Adobe Experience Platform, vous devez disposer d’un schéma XDM disponible. Si vous n’avez défini aucune de ces options, commencez par afficher cette page avant de continuer.

En outre, ce guide nécessite une compréhension pratique du SDK Web de Adobe Experience Platform. Pour une actualisation rapide, consultez la [présentation du SDK Web de Adobe Experience Platform](../../home.md) et la documentation [Forum aux questions](../../faq.md) .

## Activation du consentement par défaut

Si vous souhaitez traiter tous les utilisateurs inconnus de la même manière, vous pouvez définir [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) sur `pending` ou `out`. Cette file d’attente ou ignore les événements d’expérience jusqu’à ce que les préférences de consentement soient reçues.

### Définition du consentement par défaut basé sur `gdprApplies`

Certaines CMP permettent de déterminer si le Règlement général sur la protection des données (RGPD) s’applique au client. Si vous souhaitez obtenir le consentement des clients pour lesquels le RGPD ne s’applique pas, vous pouvez utiliser l’indicateur `gdprApplies` dans l’appel de l’API TCF.

L’exemple suivant illustre une méthode :

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

Dans cet exemple, la commande `configure` est appelée une fois que `tcData` a été obtenu à partir de l’API TCF. Si `gdprApplies` est vrai, le consentement par défaut est défini sur `pending`. Si `gdprApplies` a la valeur false, le consentement par défaut est défini sur `in`. Veillez à renseigner la variable `alloyConfiguration` avec votre configuration.

>[!NOTE]
>
>Lorsque le consentement par défaut est défini sur `in`, la commande `setConsent` peut toujours être utilisée pour enregistrer les préférences de consentement de vos clients.

## Utilisation de l’événement setConsent

L’API IAB TCF 2.0 fournit un événement pour lorsque le consentement est mis à jour par le client. Cela se produit lorsque le client définit initialement ses préférences et lorsque le client met à jour ses préférences.

L’exemple suivant illustre une méthode :

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

Ce bloc de code écoute l’événement `useractioncomplete`, puis définit le consentement, en transmettant la chaîne de consentement et l’indicateur `gdprApplies`. Si vous disposez d’identités personnalisées pour vos clients, veillez à renseigner la variable `identityMap`. Pour plus d’informations, consultez le guide sur [setConsent](../../../web-sdk/commands/setconsent.md) .

## Inclusion des informations de consentement dans sendEvent

Dans les schémas XDM, vous pouvez stocker les informations de préférences de consentement des événements d’expérience. Il existe deux manières d’ajouter ces informations à chaque événement.

Tout d’abord, vous pouvez fournir le schéma XDM approprié à chaque appel `sendEvent`. L’exemple suivant illustre une méthode :

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

L’autre manière d’ajouter les informations de consentement à chaque requête consiste à utiliser le rappel [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md).

## Étapes suivantes

Maintenant que vous avez appris à utiliser IAB TCF 2.0 avec l’extension SDK Web Platform, vous pouvez également choisir d’intégrer avec d’autres solutions Adobe telles qu’Adobe Analytics ou Adobe Real-Time Customer Data Platform. Pour plus d’informations, consultez la [présentation de Transparency &amp; Consent Framework 2.0 de l’IAB](./overview.md) .
