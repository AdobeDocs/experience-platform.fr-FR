---
title: Partage d’identité entre domaines
description: Maintenez la continuité des identités entre les domaines dont votre organisation est propriétaire afin d’améliorer la personnalisation et les rapports.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Partage d’identité entre domaines

Lorsque des visiteurs passent d’un domaine appartenant à votre organisation à un autre, chaque domaine conserve sa propre identité de visiteur par défaut. Sans transfert explicite, un visiteur qui clique sur l’un de vos domaines vers un autre est traité comme une nouvelle personne inconnue sur le site de destination. Ce type d’implémentation fragmente la création de rapports et redémarre la personnalisation.

Le partage d’identités interdomaines résout ce problème en ajoutant un paramètre de chaîne de requête `adobe_mc` à l’URL de destination lorsqu’un visiteur clique sur un lien ou est redirigé. Ce paramètre est associé à l’[Experience Cloud ID (ECID)](./overview.md) du visiteur, à l’identifiant de votre organisation et à une date et heure. Lorsque la page de destination se charge avec un paramètre de `adobe_mc` valide, Web SDK le lit automatiquement et applique l’identité transmise à sa première requête Edge Network, de sorte que les deux domaines partagent le même visiteur. Le paramètre `adobe_mc` expire au bout de cinq minutes. La page de destination doit donc se charger rapidement après la redirection.

Ce cas pratique couvre le partage d’identités entre sites web sur différents domaines. Si vous souhaitez transmettre l’identité d’une application mobile dans une page WebView ou web mobile, utilisez plutôt le partage d’identité [mobile à web](./mobile-to-web.md).

## Conditions préalables

Avant de commencer, assurez-vous que votre implémentation répond aux exigences suivantes :

* **Web SDK** : [Web SDK](/help/collection/js/js-overview.md) version **2.11.0 ou ultérieure** ou l’extension de balise Web SDK est installée sur les domaines source et de destination.
* **Configuration de correspondance** : tous les domaines participants utilisent le même [`orgId`](../js/commands/configure/orgid.md) lors de la configuration de Web SDK.
* **Contrôle d’URL** : votre code contrôle les liens ou les redirections entre les domaines afin que vous puissiez ajouter des paramètres de chaîne de requête à l’URL de destination.

## Implémenter le partage inter-domaines

Vous devez configurer le partage d’identité sur chaque domaine qui agit comme source dans une remise entre domaines. Si les visiteurs peuvent naviguer dans les deux directions entre deux domaines, configurez les deux domaines en tant que sources.

>[!BEGINTABS]

>[!TAB Bibliothèque ]

Utilisez la commande [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) pour ajouter le paramètre `adobe_mc` aux liens sortants. L’exemple suivant écoute les clics sur les éléments d’ancrage et ajoute une identité à tout lien pointant vers un domaine souhaité :

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to a domain you want to share identity with
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".example.com") && !url.hostname.endsWith(".example.org")) return;

  // Append the identity to the URL, then navigate
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    window.open(result.url, anchor.target || "_self");
  });
});
```

>[!TAB Extension de balise Web SDK]

Utilisez l’action [**[!UICONTROL Redirect with identity]**](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) pour ajouter le paramètre `adobe_mc` aux liens sortants. Vous pouvez créer une règle avec les conditions suivantes pour obtenir le comportement souhaité :

1. **Event** : définissez l’extension sur **[!UICONTROL Core]** et le type d’événement sur **[!UICONTROL Click]**. Sous **[!UICONTROL Elements matching the CSS selector]**, saisissez `a[href]`.
2. **Condition** : définissez l’extension sur **[!UICONTROL Core]** et le type de condition sur **[!UICONTROL Value Comparison]**. Définissez **[!UICONTROL Left Operand]** sur `%this.hostname%`, **[!UICONTROL Operator]** sur **[!UICONTROL Matches Regex]** et **[!UICONTROL Right Operand]** sur une expression régulière correspondant à vos domaines de destination (par exemple, `example\.com$|example\.org$`).
3. **Action** : définissez l’extension sur **[!UICONTROL Adobe Experience Platform Web SDK]** et le type d’action sur **[!UICONTROL Redirect with identity]**.

>[!ENDTABS]

## Recevoir une identité sur le domaine de destination

Aucun code supplémentaire n’est requis sur le domaine de destination. Lorsque le SDK Web est présent sur la page et que l’URL contient un paramètre de `adobe_mc` valide, le SDK extrait automatiquement l’ECID et l’applique au mappage d’identité du visiteur lors de sa première requête Edge Network.

Assurez-vous que le domaine de destination remplit les conditions suivantes :

* L’extension de balise Web SDK ou Web SDK est installée et configurée avec le même [`orgId`](../js/commands/configure/orgid.md) que le domaine source. Vous pouvez utiliser la bibliothèque JavaScript et l’extension de balise Web SDK de manière interchangeable entre les domaines, à condition qu’ils partagent le même `orgId`.
* La page charge et envoie sa première requête Edge Network dans les **cinq minutes** suivant la redirection, avant l’expiration du paramètre `adobe_mc` .
