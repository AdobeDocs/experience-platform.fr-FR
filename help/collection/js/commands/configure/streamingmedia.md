---
title: streamingMedia
description: Configurez le SDK Web pour collecter des données relatives à l’utilisation des médias sur vos propriétés web.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 8%

---

# `streamingMedia`

Le composant `streamingMedia` vous permet de collecter des données relatives aux sessions multimédia sur votre site web.

Les données collectées peuvent inclure des informations sur les lectures de médias, les pauses, les terminaisons et d’autres événements associés. Une fois collectées, vous pouvez envoyer ces données à Adobe Experience Platform ou Adobe Analytics pour générer des rapports. Cette fonctionnalité fournit une solution complète pour suivre et comprendre le comportement de consommation des médias sur votre site web.

## Conditions préalables

Pour utiliser le composant `streamingMedia` de Web SDK, les prérequis sont les suivants :

* Assurez-vous d’avoir accès à Adobe Experience Platform ou Adobe Analytics.
* Vous devez utiliser Web SDK version 2.20.0 ou ultérieure. Voir la [présentation de l’installation de Web SDK](../../install/overview.md) pour savoir comment installer la dernière version.
* Activez l’option **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** pour le flux de données que vous utilisez.
* Assurez-vous que le schéma utilisé par votre flux de données comprend les champs de schéma Media Collection.
* Configurez la fonction Streaming Media dans le SDK Web, comme illustré sur cette page.

Lors de l’appel de la commande `configure`, ajoutez l’objet `streamingMedia` .

```js
alloy("configure", {
    streamingMedia: {
        channel: "Video channel",
        playerName: "Example player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Propriété | Type | Obligatoire | Description |
| --- | --- | --- | --- |
| **`channel`** | Chaîne | Oui | Nom du canal sur lequel la collecte de médias en flux continu est effectuée. Exemple : `Video channel`. |
| **`playerName`** | Chaîne | Oui | Nom du lecteur multimédia. |
| **`appVersion`** | Chaîne | Non | Version de l’application du lecteur multimédia. |
| **`mainPingInterval`** | Nombre entier | Non | Fréquence des pings pour le contenu principal, en secondes. La valeur par défaut est `10`. Les valeurs peuvent aller de `10` à `50` secondes.  Si aucune valeur n’est spécifiée, la valeur par défaut est utilisée lors de l’utilisation de [sessions suivies automatiquement](../createmediasession.md#automatic). |
| **`adPingInterval`** | Nombre entier | Non | Fréquence des pings pour le contenu publicitaire, en secondes. La valeur par défaut est `10`. Les valeurs peuvent aller de `1` à `10` secondes. Si aucune valeur n’est spécifiée, la valeur par défaut est utilisée lors de l’utilisation de [sessions suivies automatiquement](../createmediasession.md#automatic). |

## Configuration des médias en flux continu à l’aide de l’extension de balise Web SDK

Ces paramètres peuvent être configurés dans l’extension de balise Web SDK à l’aide des [ Paramètres de configuration des médias en flux continu ](/help/tags/extensions/client/web-sdk/configure/streaming-media.md).
