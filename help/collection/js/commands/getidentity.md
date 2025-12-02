---
title: getIdentity
description: Obtenir l’identité d’un visiteur sans envoyer de données d’événement.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: aea46e3804d315c1237fc853540771f1b5c2b767
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 2%

---

# `getIdentity`

Lorsque vous exécutez la commande [`sendEvent`](sendevent/overview.md), le Web SDK récupère automatiquement l’identité du visiteur si elle n’est pas déjà présente. La commande `getIdentity` permet d’obtenir un identifiant visiteur sans envoyer de données d’événement. Si vous avez besoin d’appels distincts pour générer un identifiant visiteur et envoyer des données, vous pouvez utiliser cette commande.

La commande `getIdentity` passe par le flux suivant pour récupérer le `ECID`.

1. Vous utilisez le SDK Web pour appeler `getIdentity` ou [`appendIdentityToUrl`](appendidentitytourl.md).
1. Web SDK attend que les informations de consentement soient fournies.
1. Web SDK vérifie si l&#39;espace de noms `ECID` a été demandé lors de l&#39;appel. Par défaut, l’espace de noms `ECID` est toujours inclus.
1. Web SDK lit le cookie `kndctr` et renvoie sa valeur sous la forme `ECID`, s’il existe. Cette fonction renvoie uniquement la valeur `ECID`, mais pas la `regionId`.
1. Si le cookie d’identité `kndctr` n’est pas défini ou si l’espace de noms `"CORE"` a été demandé, Web SDK effectue une requête à l’Edge Network.
1. Edge Network renvoie à la fois le `ECID` et le `regionId` (et le `CORE ID`, le cas échéant).

Exécutez la commande `getIdentity` lors de l’appel de votre instance configurée de Web SDK. Les options suivantes sont disponibles lors de la configuration de cette commande :

* **`namespaces`** : tableau d’espaces de noms. La valeur par défaut est `["ECID"]`. Autres valeurs prises en charge :
   * `["CORE"]`
   * `["ECID","CORE"]`
   * `null`
   * `undefined`

  Vous pouvez demander `"ECID"` et `"CORE ID"` en même temps. Exemple : `"namespaces": ["ECID","CORE"]`.

* **`edgeConfigOverrides`** : un [objet de remplacement de configuration de train de données](configure/edgeconfigoverrides.md).

```js
alloy("getIdentity",{
  // This command retrieves both ECID and CORE IDs
  "namespaces": ["ECID","CORE"] 
});
```

## Objet de réponse

Si vous décidez de [gérer les réponses](command-responses.md) avec cette commande, les propriétés suivantes sont disponibles dans l’objet de réponse :

* **`identity.ECID`** : chaîne contenant l’ECID du visiteur.
* **`identity.CORE`** : chaîne contenant l’ID CORE du visiteur.
* **`edge.regionID`** : un entier qui représente la région Edge Network visitée par le navigateur lors de l’acquisition d’une identité. Il est identique à l’indicateur d’emplacement Audience Manager hérité.

```js
// Get the visitor's ECID
alloy('getIdentity').then(result => {
  console.log(result.identity.ECID);
});
```

## Obtention de l’identité à l’aide de l’extension de balise Web SDK

L’extension de balise Web SDK n’offre pas cette commande via l’interface utilisateur de l’extension de balise. Utilisez l’éditeur de code personnalisé à l’aide de la syntaxe de la bibliothèque JavaScript.
