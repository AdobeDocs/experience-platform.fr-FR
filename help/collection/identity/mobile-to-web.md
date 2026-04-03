---
title: Partage d’identité entre des applications mobiles et des vues web/web mobiles
description: Transmettez l’identité d’une application mobile dans du contenu web mobile ou un WebView afin que la création de rapports et la personnalisation puissent continuer dans le contexte web.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Partage d’identité entre des applications mobiles et des vues web/web mobiles

Lorsqu’un visiteur passe d’une application mobile à une page WebView ou web mobile, l’application et les contextes web conservent chacun leur propre identité. Sans transfert explicite, l’expérience web traite le visiteur comme une nouvelle personne inconnue, ce qui fragmente le reporting et redémarre la personnalisation.

Le partage d’identités mobile à web résout ce problème en transmettant l’[Experience Cloud ID (ECID)](./overview.md) du visiteur de l’application mobile à la destination web via un paramètre de chaîne de requête `adobe_mc`. Le paramètre est associé à l’ECID, à l’ID d’organisation Experience Cloud et à une date et heure. Lorsque la destination web se charge avec un paramètre de `adobe_mc` valide, le SDK Web le lit automatiquement et applique l’identité transmise à sa première requête Edge Network, de sorte que les deux contextes partagent le même visiteur.

Utilisez ce modèle lorsque votre application mobile ouvre une page WebView ou web mobile contrôlée par votre organisation et que vous souhaitez que l’activité de l’application et l’activité web restent liées au même visiteur. Si votre objectif est la continuité d’identité entre les sites web de différents domaines, utilisez plutôt le [partage inter-domaines](cross-domain-sharing.md).

## Conditions préalables

Avant de commencer, assurez-vous que votre implémentation répond aux exigences suivantes :

* **Application mobile** : SDK mobile Adobe Experience Platform avec l’extension [Identity for Edge Network](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/) version **1.1.0 ou ultérieure** (iOS et Android).
* **Destination web** : la version [Web SDK](/help/collection/js/js-overview.md) **2.11.0 ou ultérieure** ou l’extension de balise Web SDK.
* **Contrôle d’URL** : votre code contrôle l’URL que l’application transmet à WebView ou au navigateur afin que vous puissiez y ajouter des paramètres de chaîne de requête.
* **Configuration de correspondance** : le même ID d’organisation Experience Cloud est configuré dans les implémentations mobile et web.

## Récupérer l’identité à partir de l’application mobile {#retrieve-identity}

Utilisez l’API [`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables) de l’extension Identity for Edge Network pour récupérer l’identité du visiteur sous forme de chaîne de requête. Vous pouvez ensuite ajouter cette chaîne à l’URL avant d’ouvrir WebView ou le navigateur.

La chaîne renvoyée contient les paramètres codés en URL suivants :

| Paramètre | Description |
| --- | --- |
| `MCID` | Experience Cloud ID (ECID). |
| `MCORGID` | L’identifiant de votre organisation Experience Cloud. Ce paramètre doit correspondre à l’organisation configurée dans le SDK Web sur la page de destination. |
| `TS` | Date et heure. La destination doit recevoir cette valeur dans les **cinq minutes** ou la remise est refusée. |

Les exemples de code suivants montrent à quoi pourrait ressembler une remise dans votre application mobile :

>[!BEGINTABS]

>[!TAB Swift (iOS)]

```swift
Identity.getUrlVariables { (urlVariables, error) in
    if let error = error {
        // Handle the error
        return
    }

    guard let urlVariables = urlVariables else { return }

    // Construct the full URL by appending the identity query string
    if let url = URL(string: "https://example.com/webapp?\(urlVariables)") {
        // Open the URL in a WebView or browser
        let request = URLRequest(url: url)
        webView.load(request)
    }
}
```

>[!TAB Kotlin (Android)]

```kotlin
Identity.getUrlVariables { urlVariables ->
    if (urlVariables != null) {
        // Construct the full URL by appending the identity query string
        val url = "https://example.com/webapp?$urlVariables"

        // Open the URL in a WebView or browser
        webView.loadUrl(url)
    }
}
```

>[!ENDTABS]

## Recevoir une identité côté web {#receive-identity}

Aucun code supplémentaire n’est requis sur la destination web. Lorsque le SDK Web est présent sur la page et que l’URL contient un paramètre de `adobe_mc` valide, le SDK extrait automatiquement l’ECID et l’applique au mappage d’identité du visiteur lors de la première requête Edge Network.

Si la destination web utilise l’extension de balise Web SDK et que vous devez rediriger le visiteur vers une autre page tout en préservant l’identité, utilisez l’action [Rediriger avec identité](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) pour transférer le paramètre `adobe_mc` vers la page suivante.

>[!NOTE]
>
>Le paramètre `adobe_mc` expire après **cinq minutes**. Assurez-vous que la destination web charge et envoie rapidement sa première requête Edge Network après l’ouverture de l’URL.
