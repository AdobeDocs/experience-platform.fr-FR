---
title: getIdentity
description: Obtenez l’identité d’un visiteur sans envoyer de données d’événement.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

La commande `getIdentity` vous permet d’obtenir un identifiant visiteur sans envoyer de données d’événement. Lorsque vous exécutez la commande `sendEvent`, le SDK Web obtient automatiquement l’identité du visiteur s’il n’est pas déjà présent.

Si vous avez besoin d’appels distincts pour générer un identifiant visiteur et envoyer des données, vous pouvez utiliser cette commande.

## Obtention de l’identité à l’aide de l’extension de balise SDK Web

L’extension de balise SDK Web ne propose pas cette commande via l’interface utilisateur de l’extension de balise. Utilisez l’éditeur de code personnalisé à l’aide de la syntaxe de la bibliothèque JavaScript.

## Obtention de l’identité à l’aide de la bibliothèque JavaScript du SDK Web

Exécutez la commande `getIdentity` lors de l’appel de votre instance configurée du SDK Web. Les options suivantes sont disponibles lors de la configuration de cette commande :

* **`namespaces`** : un tableau d’espaces de noms. La valeur par défaut est `["ECID"]`. Les valeurs valides sont `["ECID"]`, `null` ou `undefined`.
* **`edgeConfigOverrides`** : un [objet de remplacement de configuration de la banque de données](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## Objet de réponse

Si vous décidez de [gérer les réponses](command-responses.md) avec cette commande, les propriétés suivantes sont disponibles dans l’objet de réponse :

* **`identity.ECID`** : chaîne contenant l’ECID du visiteur.
* **`edge.regionID`** : nombre entier représentant la région de l’Edge Network que le navigateur a atteinte lors de l’acquisition d’une identité. Il est identique à l’indicateur d’emplacement de l’Audience Manager héritée.
