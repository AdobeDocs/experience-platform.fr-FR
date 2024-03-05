---
title: contexte
description: Collecte automatique des données d’appareil, d’environnement ou de lieu.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 13%

---

# `context`

La variable `context` est un tableau de chaînes qui détermine ce que le SDK Web peut automatiquement collecter. Bien que ces données puissent offrir une grande valeur, l’omission de certaines de ces données peut s’avérer bénéfique afin que vous puissiez vous conformer à la politique de confidentialité de votre entreprise.

## Mots-clés de contexte et éléments XDM

Si vous incluez un mot-clé contextuel donné, le SDK Web renseigne automatiquement tous les éléments XDM associés. Si vous souhaitez omettre un élément XDM spécifique tout en en autorisant d’autres, vous pouvez effacer les valeurs à l’aide de la variable [`onBeforeEventSend`](onbeforeeventsend.md). Si vous envoyez plusieurs événements sur une page, le SDK Web inclut ces champs sur chaque `SendEvent` appelez .

### Web

La variable `"web"` Le mot-clé collecte des informations sur la page active.

| Dimension | Description | Chemin XDM | Exemple de valeur |
| --- | --- | --- | --- |
| Page URL (URL de la page) | URL de la page active. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL du référent | URL de la page précédemment visitée. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### Appareil

La variable `"device"` collecte des informations sur l’appareil de l’utilisateur.

| Dimension | Description | Chemin XDM | Exemple de valeur |
| --- | --- | --- | --- |
| Hauteur d’écran | Hauteur de l’écran en pixels. | `xdm.device.screenHeight` | `900` |
| Largeur d’écran | Largeur de l’écran en pixels. | `xdm.device.screenWidth` | `1440` |
| Orientation de l’écran | Orientation de l’écran. | `xdm.device.screenOrientation` | `landscape` ou `portrait`. |

{style="table-layout:auto"}

### Environnement

La variable `"environment"` Le mot-clé collecte des informations sur le navigateur de l’utilisateur.

| Dimension | Description | Chemin XDM | Exemple de valeur |
| --- | --- | --- | --- |
| Type d’environnement | Type d’environnement par lequel l’expérience est apparue. Le SDK Web définit toujours ce champ sur `browser`. | `xdm.environment.type` | `browser` |
| Hauteur de la fenêtre d’affichage | Hauteur de la zone de contenu du navigateur en pixels. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Largeur de la fenêtre d’affichage | Largeur de la zone de contenu du navigateur en pixels. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### Contexte de l’emplacement

La variable `"placeContext"` collecte des informations sur l’emplacement de l’utilisateur.

| Dimension | Description | Chemin XDM | Exemple de valeur |
| --- | --- | --- | --- |
| Heure locale | Horodatage local pour l’utilisateur final dans l’extension simplifiée [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) format. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Décalage du fuseau horaire local | Le nombre de minutes pendant lesquelles l’utilisateur est décalé par rapport à GMT. | `xdm.placeContext.localTimezoneOffset` | `360` |

{style="table-layout:auto"}

### Conseils client à forte entropie

La variable `"highEntropyUserAgentHints"` Le mot-clé collecte des informations détaillées sur l’appareil de l’utilisateur. Ces données sont incluses dans l’en-tête HTTP de la demande envoyée à Adobe. Une fois les données arrivées dans le réseau Edge, l’objet XDM renseigne son chemin d’accès XDM respectif. Si vous définissez le chemin XDM correspondant dans votre `sendEvent` , elle prévaut sur la valeur de l’en-tête HTTP.

Si vous utilisez des recherches d’appareils lors de la [configuration de votre flux de données](/help/datastreams/configure.md), les données peuvent être effacées au profit des valeurs de recherche de périphérique. Certains champs de conseil client et de recherche de périphérique ne peuvent pas exister dans le même accès.

| Dimension | Description | En-tête HTTP | Chemin XDM | Exemple de valeur |
| --- | --- | --- | --- | --- |
| Version du système d’exploitation | Version du système d’exploitation. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | |
| Architecture | Architecture du processeur sous-jacent. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | |
| Modèle d’appareil | Nom du périphérique utilisé. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | |
| Bitness | Nombre de bits pris en charge par l’architecture du processeur sous-jacente. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | |
| Fournisseur du navigateur | Société qui a créé le navigateur. Indicateur de faible entropie `Sec-CH-UA` collecte également cet élément. | `Sec-CH-UA-Full-Version-List` | | |
| Nom du navigateur | Le navigateur utilisé. Indicateur de faible entropie `Sec-CH-UA` collecte également cet élément. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | |
| Version du navigateur | Version significative du navigateur. Indicateur de faible entropie `Sec-CH-UA` collecte également cet élément. La version exacte du navigateur n’est pas collectée automatiquement. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | |

{style="table-layout:auto"}

## Collecte des informations contextuelles à l’aide de l’extension de balise SDK Web

Le paramètre d’informations contextuelles est une combinaison de boutons radio et de cases à cocher lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Chaque case à cocher correspond à un mot-clé contextuel.

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Faites défiler l’écran vers le bas jusqu’à [!UICONTROL Collecte de données] puis sélectionnez l’une des options suivantes : **[!UICONTROL Toutes les informations contextuelles par défaut]** ou **[!UICONTROL Informations contextuelles spécifiques]**.
1. Si vous sélectionnez **[!UICONTROL Informations contextuelles spécifiques]**, activez la case à cocher en regard de chaque élément d’informations contextuelles souhaité.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

## Collecte d’informations contextuelles à l’aide de la bibliothèque JavaScript SDK Web

Définissez la variable `context` tableau de chaînes lors de l’exécution de la variable `configure` . Si vous omettez cette propriété lors de la configuration du SDK, toutes les informations contextuelles, sauf `"highEntropyUserAgentHints"` est collectée par défaut. Définissez cette propriété si vous souhaitez collecter des indices client à forte entropie ou si vous souhaitez omettre d’autres informations contextuelles de la collecte de données. Les chaînes peuvent être incluses dans n’importe quel ordre.

>[!NOTE]
>
>Si vous souhaitez collecter toutes les informations contextuelles, y compris les conseils client à forte entropie, vous devez inclure chaque valeur dans la variable `context` chaîne de tableau. Par défaut `context` omises de valeur `highEntropyUserAgentHints`et si vous définissez la variable `context` , toutes les valeurs omises ne collectent pas de données.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
