---
title: Intégration de la prise en charge d’IAB TCF 2.0 à l’aide du SDK Web Adobe Experience Platform
description: Découvrez comment configurer la prise en charge d’IAB TCF 2.0 pour votre site Web sans utiliser Adobe Experience Platform Launch.
seo-description: Découvrez comment configurer le consentement IAB TCF 2.0 avec le SDK Web Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---


# Intégration de la prise en charge d’IAB TCF 2.0 avec Platform Web SDK

Ce guide explique comment intégrer Interactive Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0) avec Adobe Experience Platform Web SDK sans utiliser d’Experience Platform Launch. Pour un aperçu de l&#39;intégration avec IAB TCF 2.0, consultez la [présentation](./overview.md). Pour un guide sur la façon de s&#39;intégrer à l&#39;Experience Platform Launch, consultez le [guide de l&#39;IAB TCF 2.0 pour Experience Platform Launch](./with-launch.md).

## Prise en main

Ce guide utilise l&#39;interface `__tcfapi` pour accéder aux informations de consentement. Il peut s’avérer plus facile pour vous d’intégrer directement votre fournisseur de gestion de cloud (CMP). Toutefois, les informations contenues dans ce guide peuvent encore être utiles car les CMP offrent généralement des fonctionnalités similaires à l’API TCF.

>[!NOTE]
>
>Ces exemples supposent que lorsque le code est exécuté, `window.__tcfapi` est défini sur la page. Les CMP peuvent fournir un hook permettant d&#39;exécuter ces fonctions lorsque l&#39;objet `__tcfapi` est prêt.

Pour utiliser IAB TCF 2.0 avec Experience Platform Launch et l’extension Adobe Experience Platform Web SDK, vous devez disposer d’un schéma XDM. Si vous n&#39;avez défini aucune de ces options, débuts en affichant cette page avant de continuer.

En outre, ce guide vous demande de bien comprendre le SDK Web de Adobe Experience Platform. Pour une actualisation rapide, consultez la [présentation du SDK Web de Adobe Experience Platform](../../home.md) et la [documentation sur les questions fréquentes](../../web-sdk-faq.md).

## Activation du consentement par défaut

Si vous souhaitez traiter tous les utilisateurs inconnus de la même manière, vous pouvez définir le consentement par défaut sur `pending`. Cette option met en file d’attente les Événements d’expérience jusqu’à ce que les préférences de consentement soient reçues.

Pour plus d&#39;informations sur le consentement par défaut, consultez la section [consentement par défaut](../../fundamentals/configuring-the-sdk.md#default-consent) de la documentation de configuration du SDK Web de la plate-forme.

### Définition du consentement par défaut basé sur `gdprApplies`

Certains CMP permettent de déterminer si le Règlement général sur la protection des données (RGPD) s&#39;applique au client. Si vous souhaitez obtenir le consentement des clients pour lesquels GDPR ne s’applique pas, vous pouvez utiliser l’indicateur `gdprApplies` dans l’appel de l’API TCF.

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

Dans cet exemple, la commande `configure` est appelée une fois que `tcData` a été obtenu à partir de l’API TCF. Si `gdprApplies` a la valeur true, le consentement par défaut est défini sur `pending`. Si `gdprApplies` a la valeur false, le consentement par défaut est défini sur `in`. Veillez à renseigner la variable `alloyConfiguration` avec votre configuration.

>[!NOTE]
>
>Lorsque le consentement par défaut est défini sur `in`, la commande `setConsent` peut toujours être utilisée pour enregistrer les préférences de consentement de vos clients.

## Utilisation du événement setConsent

L’API IAB TCF 2.0 fournit un événement pour le moment où le consentement est mis à jour par le client. Cela se produit lorsque le client définit initialement ses préférences et lorsque le client met à jour ses préférences.

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

Ce bloc de code écoute le événement `useractioncomplete`, puis définit le consentement, en transmettant la chaîne de consentement et l&#39;indicateur `gdprApplies`. Si vous disposez d’identités personnalisées pour vos clients, veillez à renseigner la variable `identityMap`. Pour plus d&#39;informations sur l&#39;appel à `setConsent`, consultez le guide sur [le consentement à l&#39;appui](../../consent/supporting-consent.md).

## Inclusion des informations de consentement dans sendEvent

Dans les schémas XDM, vous pouvez stocker les informations de préférence de consentement dans les Événements d’expérience. Il existe deux façons d’ajouter ces informations à chaque événement.

Tout d&#39;abord, vous pouvez fournir le schéma XDM approprié à chaque appel `sendEvent`. L’exemple suivant illustre une façon de procéder :

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

Cet exemple récupère les informations de consentement pour l’API TCF, puis envoie un événement avec les informations de consentement ajoutées au schéma XDM. Consultez le guide [événements de suivi](../../fundamentals/tracking-events.md) pour comprendre ce qui doit figurer dans les options de commande `sendEvent`.

L&#39;autre moyen d&#39;ajouter les informations de consentement à chaque requête consiste à utiliser le rappel `onBeforeEventSend`. Pour plus d’informations sur la manière de procéder, consultez la section [Modification des événements globalement](../../fundamentals/tracking-events.md#modifying-events-globally) dans la documentation des événements de suivi.

## Étapes suivantes

Maintenant que vous avez appris à utiliser IAB TCF 2.0 avec l&#39;extension Platform Web SDK, vous pouvez également choisir de vous intégrer à d&#39;autres solutions d&#39;Adobe telles que Adobe Analytics ou la plate-forme de données client en temps réel. Pour plus d&#39;informations, consultez la [présentation du Cadre de transparence et de consentement IAB 2.0](./overview.md).
