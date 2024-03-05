---
title: getIdentity
description: Obtenez l’identité d’un visiteur sans envoyer de données d’événement.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# `getIdentity`

La variable `getIdentity` permet d’obtenir un identifiant visiteur sans envoyer de données d’événement. Lorsque vous exécutez le `sendEvent` , le SDK Web obtient automatiquement l’identité du visiteur s’il n’est pas déjà présent.

Si vous avez besoin d’appels distincts pour générer un identifiant visiteur et envoyer des données, vous pouvez utiliser cette commande.

## Obtention de l’identité à l’aide de l’extension de balise SDK Web

L’extension de balise SDK Web ne propose pas cette commande via l’interface utilisateur de l’extension de balise. Utilisez l’éditeur de code personnalisé à l’aide de la syntaxe de la bibliothèque JavaScript.

## Obtention de l’identité à l’aide de la bibliothèque JavaScript du SDK Web

Exécutez la variable `getIdentity` lors de l’appel de votre instance configurée du SDK Web. Les options suivantes sont disponibles lors de la configuration de cette commande :

* **`namespaces`**: un tableau d’espaces de noms. La valeur par défaut est `["ECID"]`. Les valeurs valides incluent : `["ECID"]`, `null`, ou `undefined`.
* **`edgeConfigOverrides`**: [objet de remplacement de la configuration du flux de données](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## Objet de réponse

Si vous décidez [gérer les réponses](command-responses.md) avec cette commande, les propriétés suivantes sont disponibles dans l’objet de réponse :

* **`identity.ECID`**: chaîne contenant l’ECID du visiteur.
* **`edge.regionID`**: nombre entier représentant la région réseau Edge que le navigateur a atteinte lors de l’acquisition d’une identité. Il est identique à l’indicateur d’emplacement de l’Audience Manager héritée.
