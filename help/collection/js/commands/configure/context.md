---
title: contexte
description: Collectez automatiquement les données relatives à l’appareil, à l’environnement ou à l’emplacement.
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 14%

---

# `context`

La propriété `context` est un tableau de chaînes qui détermine ce que le SDK Web peut collecter automatiquement. Bien que ces données puissent fournir une grande valeur, l’omission de certaines de ces données peut être bénéfique afin que vous puissiez vous conformer à la politique de confidentialité de votre organisation.

## Mots-clés de contexte et éléments XDM

Si vous incluez un mot-clé de contexte donné, le SDK Web renseigne automatiquement tous ses éléments XDM associés. Si vous souhaitez omettre un élément XDM spécifique tout en en autorisant d’autres, vous pouvez effacer les valeurs à l’aide de [`onBeforeEventSend`](onbeforeeventsend.md). Si vous envoyez plusieurs événements sur une page, le SDK Web inclut ces champs à chaque appel `SendEvent`.

### Web

Le mot-clé `"web"` collecte des informations sur la page active.

| Dimension | Description | Chemin XDM | Exemple de valeur |
| --- | --- | --- | --- |
| Page URL (URL de la page) | URL de la page active. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL du référent | URL de la page précédemment visitée. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

### Appareil

Le mot-clé `"device"` collecte des informations sur l’appareil de l’utilisateur.

| Dimension | Description | Chemin XDM | Exemple de valeur |
| --- | --- | --- | --- |
| Hauteur d’écran | Hauteur de l’écran en pixels. | `xdm.device.screenHeight` | `900` |
| Largeur d’écran | Largeur de l’écran en pixels. | `xdm.device.screenWidth` | `1440` |
| Orientation de l’écran | Orientation de l’écran. | `xdm.device.screenOrientation` | `landscape` ou `portrait`. |

### Environnement

Le mot-clé `"environment"` collecte des informations sur le navigateur de l’utilisateur.

| Dimension | Description | Chemin XDM | Exemple de valeur |
| --- | --- | --- | --- |
| Type d’environnement | Type d’environnement à travers lequel l’expérience a fait surface. Le SDK Web définit toujours ce champ sur `browser`. | `xdm.environment.type` | `browser` |
| Hauteur de la fenêtre d’affichage | Hauteur de la zone de contenu du navigateur en pixels. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Largeur de la fenêtre d’affichage | Largeur de la zone de contenu du navigateur en pixels. | `xdm.environment.browserDetails.viewportWidth` | `642` |

### Contexte de l’emplacement

Le mot-clé `"placeContext"` collecte des informations sur l’emplacement de l’utilisateur.

| Dimension | Description | Chemin XDM | Exemple de valeur |
| --- | --- | --- | --- |
| Heure locale | Horodatage local pour l’utilisateur final au format [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) étendu simplifié. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Décalage du fuseau horaire local | Nombre de minutes pendant lesquelles l’utilisateur ou l’utilisatrice est décalé par rapport au GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |
| Code pays | Code pays de l’utilisateur final. | `xdm.placeContext.geo.countryCode` | `US` |
| Province de l&#39;État | Code province de l’état de l’utilisateur final. | `xdm.placeContext.geo.stateProvince` | `CA` |
| Latitude | La latitude de l’emplacement de l’utilisateur final. | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| Longitude | Longitude de l’emplacement de l’utilisateur final. | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

### Date et heure

Le mot-clé `"timestamp"` collecte des informations sur la date et l’heure de l’événement. Ce contexte est toujours inclus et ne peut pas être supprimé.

| Dimension | Description | Chemin XDM | Exemple de valeur |
| --- | --- | --- | --- |
| Date et heure de l’événement | Date et heure UTC de l’utilisateur final au format [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) étendu simplifié. | `xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |

### Détails d’implémentation

Le mot-clé `implementationDetails` collecte des informations sur la version de SDK utilisée pour collecter l’événement.

| Dimension | Description | Chemin XDM | Exemple de valeur |
| --- | --- | --- | --- |
| Nom | Identifiant du kit de développement logiciel (SDK). Ce champ utilise un URI pour améliorer l’unicité entre les identifiants fournis par différentes bibliothèques de logiciels. | `xdm.implementationDetails.name` | Lorsque la bibliothèque autonome est utilisée, la valeur est `https://ns.adobe.com/experience/alloy`. Lorsque la bibliothèque est utilisée dans le cadre de l’extension de balise, la valeur est `https://ns.adobe.com/experience/alloy+reactor`. |
| Version | Version du kit de développement logiciel (SDK). | `xdm.implementationDetails.version` | Lorsque la bibliothèque autonome est utilisée, la valeur correspond à la version de la bibliothèque. Lorsque la bibliothèque est utilisée dans le cadre de l’extension de balise, la valeur est la version de la bibliothèque et la version de l’extension de balise jointes à une `+`. Par exemple, si la version de la bibliothèque est `2.1.0` et que la version de l’extension de balise est `2.1.3`, la valeur est `2.1.0+2.1.3`. |
| Environnement | Environnement dans lequel les données ont été collectées. Ce champ est toujours défini sur `browser` lors de l’utilisation de la bibliothèque JavaScript. | `xdm.implementationDetails.environment` | `browser` |

### Indications du client à entropie élevée {#high-entropy-client-hints}

Le mot-clé `"highEntropyUserAgentHints"` collecte des informations détaillées sur l’appareil de l’utilisateur. Ces données sont incluses dans l’en-tête HTTP de la requête envoyée à Adobe. Une fois les données arrivées au réseau Edge, l’objet XDM renseigne son chemin XDM respectif. Si vous définissez le chemin XDM correspondant dans votre appel `sendEvent`, il est prioritaire sur la valeur de l’en-tête HTTP.

Si vous utilisez les recherches d’appareil lors de la [configuration de votre flux de données](/help/datastreams/configure.md), les données peuvent être effacées au profit des valeurs de recherche d’appareil. Certains champs d’indications du client et champs de recherche de l’appareil ne peuvent pas exister dans le même accès.

| Propriété | Description | En-tête HTTP | Chemin XDM | Exemple |
| --- | --- | --- | --- | --- |
| Version du système d’exploitation | Version du système d’exploitation. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` |
| Architecture | Architecture CPU sous-jacente. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` |
| Modèle d’appareil | Nom de l’appareil utilisé. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` |
| Bitness | Nombre de bits pris en charge par l’architecture CPU sous-jacente. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` |
| Fournisseur du navigateur | Société qui a créé le navigateur. L’indice à faible entropie `Sec-CH-UA` collecte également cet élément. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` |
| Nom du navigateur | Le navigateur utilisé. L’indice à faible entropie `Sec-CH-UA` collecte également cet élément. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` |
| Version du navigateur | Version significative du navigateur. L’indice à faible entropie `Sec-CH-UA` collecte également cet élément. La version exacte du navigateur n’est pas collectée automatiquement. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` |

Voir [ Indications du client de l’agent utilisateur](/help/collection/use-cases/client-hints.md) pour plus d’informations.

Définissez le tableau `context` de chaînes lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration du SDK, toutes les informations contextuelles, à l’exception de `"highEntropyUserAgentHints"`, sont collectées par défaut. Définissez cette propriété si vous souhaitez collecter des indications du client à entropie élevée ou si vous souhaitez omettre d’autres informations contextuelles de la collecte de données. Les chaînes peuvent être incluses dans n’importe quel ordre.

>[!NOTE]
>
>Si vous souhaitez collecter toutes les informations contextuelles, y compris les indications du client à entropie élevée, vous devez inclure chaque valeur dans la chaîne du tableau `context`. La valeur de `context` par défaut omet les `highEntropyUserAgentHints`, et si vous définissez la propriété `context` , les valeurs omises ne collectent pas de données.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```

## Collecter des informations contextuelles à l’aide de l’extension de balise Web SDK

Voir [Paramètres contextuels](/help/tags/extensions/client/web-sdk/configure/data-collection.md#context-settings) sous Paramètres de configuration de la collecte de données dans la documentation de l’extension de balise Web SDK.
