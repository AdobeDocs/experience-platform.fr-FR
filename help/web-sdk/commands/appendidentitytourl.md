---
title: appendIdentityToUrl
description: Diffusez des expériences personnalisées plus précisément entre les applications, le web et les domaines.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: 7c262e5819f8e3488c5ddd5a0221d1c52c28c029
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---

# `appendIdentityToUrl`

La commande `appendIdentityToUrl` vous permet d’ajouter un identifiant utilisateur à l’URL sous la forme d’une chaîne de requête. Cette action vous permet de transférer l’identité d’un visiteur ou d’une visiteuse entre les domaines, ce qui empêche le décompte de visiteurs en double pour les jeux de données qui incluent les deux domaines ou canaux. Il est disponible dans les versions 2.11.0 ou ultérieures de Web SDK.

La chaîne de requête générée et ajoutée à l’URL est `adobe_mc`. Si le SDK Web ne trouve pas d’ECID, il appelle le point d’entrée `/acquire` pour en générer un.

>[!NOTE]
>
>Si le consentement n’a pas été fourni, l’URL de cette méthode est renvoyée sans modification. Cette commande s’exécute immédiatement ; elle n’attend pas une mise à jour du consentement.

## Ajout d’une identité à une URL à l’aide de l’extension Web SDK {#extension}

L’ajout d’une identité à une URL est effectué en tant qu’action dans une règle de l’interface des balises de la collecte de données Adobe Experience Platform.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]**, puis définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Rediriger avec une identité]**.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre workflow de publication.

Cette commande est généralement utilisée avec une règle spécifique qui écoute les clics et vérifie les domaines souhaités.

+++Critères d’événement de règle

Se déclenche lorsqu’un utilisateur clique sur une balise d’ancrage avec une propriété `href`.

* **[!UICONTROL Extension]** : Core
* **[!UICONTROL Type d’événement]** : cliquez sur
* **[!UICONTROL Lorsque l&#39;utilisateur clique sur]** : Eléments spécifiques
* **[!UICONTROL Éléments correspondant au sélecteur CSS]** : `a[href]`

![Événement de règle](../assets/id-sharing-event-configuration.png)

+++

+++Condition de règle

Déclenche uniquement sur les domaines souhaités.

* **[!UICONTROL Type de logique]** : Standard
* **[!UICONTROL Extension]** : Core
* **[!UICONTROL Type de condition]** : comparaison de valeurs
* **[!UICONTROL Opérande de gauche]** : `%this.hostname%`
* **[!UICONTROL Operator]** : Correspond à l’expression régulière
* **[!UICONTROL Opérande droit]** : expression régulière correspondant aux domaines souhaités. Par exemple : `adobe.com$|behance.com$`

![Condition de règle](../assets/id-sharing-condition-configuration.png)

+++

+++Action de règle

Ajoutez l’identité à l’URL.

* **[!UICONTROL Extension]** : SDK Web Adobe Experience Platform
* **[!UICONTROL Type d’action]** : redirection avec identité

![Action de la règle](../assets/id-sharing-action-configuration.png)

+++

## Ajout d’une identité à une URL à l’aide de la bibliothèque JavaScript Web SDK

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
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => {document.location = result.url;});
});
```

## Objet de réponse

Si vous décidez de [gérer les réponses](command-responses.md) avec cette commande, l’objet de réponse contient **`url`**, la nouvelle URL avec des informations d’identité ajoutées comme paramètre de chaîne de requête.
