---
title: mediaCollection
description: Configurez le SDK Web pour collecter des données relatives à l’utilisation des médias sur vos propriétés web.
source-git-commit: 1d1bb754769defd122faaa2160e06671bf02c974
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---


# `streamingMedia`

La variable `streamingMedia` vous aide à collecter des données relatives aux sessions multimédia sur votre site web.

Les données collectées peuvent inclure des informations sur les lectures multimédia, les pauses, les fins et d’autres événements connexes. Une fois ces données collectées, vous pouvez les envoyer à Adobe Experience Platform et/ou Adobe Analytics pour générer des rapports. Cette fonctionnalité offre une solution complète pour effectuer le suivi et comprendre le comportement de consommation des médias sur votre site web.

## Conditions préalables {#prerequisites}

Pour utiliser la variable `streamingMedia` du SDK Web, vous devez respecter les conditions préalables suivantes :

* Vérifiez que vous avez accès à Adobe Experience Platform et/ou Adobe Analytics.
* Vous devez utiliser le SDK Web version 2.20.0 ou ultérieure. Voir [Présentation de l’installation du SDK Web](../../install/overview.md) pour découvrir comment installer la dernière version.
* Activez la variable **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** pour le flux de données que vous utilisez.
* Assurez-vous que le schéma utilisé par votre flux de données comprend les champs de schéma Media Collection.
* Configurez la fonction Média en flux continu dans la configuration du SDK Web, comme illustré dans cette page, soit par le biais de la fonction [extension de balise](#tag-extension) ou au moyen de la variable [Bibliothèque JavaScript](#library).

## Configuration de médias en continu à l’aide de l’extension de balise SDK Web {#tag-extension}

Pour configurer les médias en continu dans l’extension de balise du SDK Web, procédez comme suit.

1. Connexion à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur le [!UICONTROL SDK Web Adobe Experience Platform] carte.
1. Configurez la variable **[!UICONTROL Média en flux continu]** comme décrit dans la section [Page de configuration de l’extension de balise SDK Web](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## Configuration de médias en flux continu à l’aide de la bibliothèque JavaScript du SDK Web {#library}

Pour configurer la diffusion multimédia en continu dans le SDK Web, utilisez les propriétés décrites ci-dessous.

Lorsque vous appelez la fonction `configure` , ajoutez la commande `streamingMedia` .

```js
alloy("configure", {
    streamingMedia: {
        channel: "video channel",
        playerName: "test player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Propriété | Type | Obligatoire | Description |
|---------|----------|---------|---------|
| `channel` | Chaîne | Oui | Nom du canal sur lequel la collecte de médias en continu a lieu. Exemple : `Video channel`. |
| `playerName` | Chaîne | Oui | Nom du lecteur multimédia. |
| `appVersion` | Chaîne | Non | Version de l’application du lecteur multimédia. |
| `mainPingInterval` | Nombre entier | Non | Fréquence des pings pour le contenu principal, en secondes. La valeur par défaut est `10`. Les valeurs peuvent être comprises entre `10` to `50` secondes.  Si aucune valeur n’est spécifiée, la valeur par défaut est utilisée lors de l’utilisation de la variable [sessions suivies automatiquement](../createmediasession.md#automatic). |
| `adPingInterval` | Nombre entier | Non | Fréquence des pings pour le contenu de la publicité, en secondes. La valeur par défaut est `10`. Les valeurs peuvent être comprises entre `1` to `10` secondes. Si aucune valeur n’est spécifiée, la valeur par défaut est utilisée lors de l’utilisation de la variable [sessions suivies automatiquement](../createmediasession.md#automatic). |
