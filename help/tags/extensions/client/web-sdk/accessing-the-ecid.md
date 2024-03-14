---
title: Accès à l’ECID
description: Découvrez comment accéder à l’ID d’Experience Cloud à partir de la préparation de données ou des balises.
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e01dfcf3cccea589083a23171f4b8d9ecad58233
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%

---


# Accès à l’ECID

La variable [!DNL Experience Cloud Identity (ECID)] est un identifiant persistant attribué à un utilisateur lorsqu’il visite votre site web. Dans certains cas, vous pouvez préférer accéder à la variable [!DNL ECID] (pour l’envoyer à un tiers, par exemple). Un autre cas d’utilisation consiste à définir la variable [!DNL ECID] dans un champ XDM personnalisé, en plus de l’avoir dans la carte d’identité.

Vous pouvez accéder à l’ECID via [Préparation de données pour la collecte de données](../../../../datastreams/data-prep.md) (recommandé) ou au moyen de balises .

## Accès à l’ECID via la préparation des données (méthode préférée) {#accessing-ecid-data-prep}

Si vous souhaitez définir l’ECID dans un champ XDM personnalisé, en plus de l’avoir dans la carte d’identité, vous pouvez le faire en définissant la variable `source` à l’emplacement suivant :

```js
xdm.identityMap.ECID[0].id
```

Définissez ensuite la cible sur un chemin XDM où le champ est de type `string`.

![](./assets/access-ecid-data-prep.png)

## Balises

Si vous devez accéder à la variable [!DNL ECID] côté client, utilisez l’approche des balises comme décrit ci-dessous.

1. Vérifiez que votre propriété est configurée avec [séquencement des composants de règle](../../../ui/managing-resources/rules.md#sequencing) activée.
1. Créez une règle. Cette règle doit être utilisée exclusivement pour capturer la variable [!DNL ECID] sans aucune autre action importante.
1. Ajouter un [!UICONTROL Bibliothèque chargée] à la règle.
1. Ajouter un [!UICONTROL Code personnalisé] l’action sur la règle avec le code suivant (en supposant que le nom que vous avez configuré pour l’instance du SDK soit `alloy` et il n’existe pas déjà d’élément de données du même nom) :

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Enregistrez la règle.

Vous devriez alors pouvoir accéder au [!DNL ECID] dans les règles suivantes à l’aide de `%ECID%` ou `_satellite.getVar("ECID")`, comme pour tout autre élément de données.
