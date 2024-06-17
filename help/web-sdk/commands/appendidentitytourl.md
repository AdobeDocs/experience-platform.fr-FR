---
title: appendIdentityToUrl
description: Proposer des expériences personnalisées plus précisément entre les applications, le web et les domaines.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: 153c5bae42c027c25a38a8b63070249d1b1a8f01
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---

# `appendIdentityToUrl`

La variable `appendIdentityToUrl` vous permet d’ajouter un identifiant d’utilisateur à l’URL en tant que chaîne de requête. Cette action vous permet de transférer l’identité d’un visiteur entre les domaines, ce qui empêche la duplication du nombre de visiteurs pour les jeux de données qui incluent à la fois des domaines ou des canaux. Il est disponible sur le SDK Web versions 2.11.0 ou ultérieures.

La chaîne de requête générée et ajoutée à l’URL est `adobe_mc`. Si le SDK Web ne trouve pas d’ECID, il appelle la variable `/acquire` point d’entrée pour en générer un.

>[!NOTE]
>
>Si le consentement n’a pas été fourni, l’URL de cette méthode est renvoyée inchangée. Cette commande s’exécute immédiatement ; elle n’attend pas la mise à jour du consentement.

## Ajout d’une identité à l’URL à l’aide de l’extension SDK Web {#extension}

L’ajout d’une identité à une URL est effectué sous la forme d’une action au sein d’une règle dans l’interface des balises de collecte de données Adobe Experience Platform.

1. Connexion à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez la variable [!UICONTROL Extension] du champ déroulant vers **[!UICONTROL SDK Web Adobe Experience Platform]**, puis définissez la variable [!UICONTROL Type d’action] to **[!UICONTROL Redirection vers une identité]**.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre workflow de publication.

Cette commande est généralement utilisée avec une règle spécifique qui écoute les clics et vérifie les domaines souhaités.

+++Critères d’événement de règle

Déclenche lorsqu’une balise d’ancrage comporte une balise `href` Cliquez sur la propriété .

* **[!UICONTROL Extension]** : Core
* **[!UICONTROL Type d’événement]**: cliquez sur
* **[!UICONTROL Lorsque l’utilisateur clique sur]**: éléments spécifiques
* **[!UICONTROL Éléments correspondant au sélecteur CSS]**: `a[href]`

![Événement de règle](../assets/id-sharing-event-configuration.png)

+++

Condition de +++règle

Déclenche uniquement sur les domaines de votre choix.

* **[!UICONTROL Type de logique]**: régulier
* **[!UICONTROL Extension]** : Core
* **[!UICONTROL Type de condition]**: comparaison de valeurs
* **[!UICONTROL Opérateur de gauche]**: `%this.hostname%`
* **[!UICONTROL Opérateur]**: Matches Regex
* **[!UICONTROL Opérateur de droit]**: expression régulière qui correspond aux domaines de votre choix. Par exemple : `adobe.com$|behance.com$`

![Condition de règle](../assets/id-sharing-condition-configuration.png)

+++

Action +++Rule

Ajoutez l’identité à l’URL.

* **[!UICONTROL Extension]** : SDK Web Adobe Experience Platform
* **[!UICONTROL Type d’action]**: redirection avec identité

![Action de règle](../assets/id-sharing-action-configuration.png)

+++

## Ajout d’une identité à l’URL à l’aide de la bibliothèque JavaScript du SDK Web

Exécutez la variable `appendIdentityToUrl` avec une URL comme paramètre. La méthode renvoie une URL dont l’identifiant est annexé en tant que chaîne de requête.

```js
alloy("appendIdentityToUrl",document.location);
```

Vous pouvez ajouter un écouteur d’événement pour tous les clics reçus sur la page et vérifier si l’URL correspond à l’un des domaines souhaités. Dans ce cas, ajoutez l’identité à l’URL et redirigez l’utilisateur.

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

Si vous décidez [gérer les réponses](command-responses.md) avec cette commande, l’objet de réponse contient **`url`**, la nouvelle URL avec les informations d’identité ajoutées en tant que paramètre de chaîne de requête.
