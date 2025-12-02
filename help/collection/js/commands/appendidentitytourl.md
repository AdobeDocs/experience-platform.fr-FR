---
title: appendIdentityToUrl
description: Diffusez des expériences personnalisées plus précisément entre les applications, le web et les domaines.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `appendIdentityToUrl`

La commande `appendIdentityToUrl` vous permet d’ajouter un identifiant utilisateur à l’URL sous la forme d’une chaîne de requête. Cette action vous permet de transférer l’identité d’un visiteur ou d’une visiteuse entre les domaines, ce qui empêche le décompte de visiteurs en double pour les jeux de données qui incluent les deux domaines ou canaux. Il est disponible dans les versions 2.11.0 ou ultérieures de Web SDK.

La chaîne de requête générée et ajoutée à l’URL est `adobe_mc`. Si le SDK Web ne trouve pas d’ECID, il appelle le point d’entrée `/acquire` pour en générer un.

>[!NOTE]
>
>Si le consentement n’a pas été fourni, l’URL de cette méthode est renvoyée sans modification. Cette commande s’exécute immédiatement ; elle n’attend pas une mise à jour du consentement.

Exécutez la commande `appendIdentityToUrl` avec une URL comme paramètre. La méthode renvoie une URL avec l’identifiant ajouté sous la forme d’une chaîne de requête.

```js
alloy("appendIdentityToUrl",
  {
    url: document.location.href
  }
);
```

Vous pouvez ajouter un écouteur d’événement pour tous les clics reçus sur la page et vérifier si l’URL correspond aux domaines souhaités. Si c’est le cas, ajoutez l’identité à l’URL et redirigez l’utilisateur.

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to the desired domain
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".adobe.com") && !url.hostname.endsWith(".behance.com")) return;

  // Append the identity to the URL, then direct the user to the URL
  event.preventDefault();
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => { window.open(result.url, anchor.target || "_self"); });
});
```

Cette commande prend en charge l’objet [`edgeConfigOverrides`](configure/edgeconfigoverrides.md).

## Objet de réponse

Lors de la [gestion des réponses](command-responses.md) avec cette commande, l’objet de réponse contient **`url`**, la nouvelle URL avec des informations d’identité ajoutées comme paramètre de chaîne de requête.

## Ajout d’une identité à une URL à l’aide de l’extension de balise Web SDK

L’extension de balise Web SDK équivalente à cette commande est l’action [Rediriger avec identité](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md).
