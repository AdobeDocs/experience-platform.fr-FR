---
title: Paramètres de configuration du streaming multimédia
description: Personnalisez la manière dont l’extension de balise Web SDK collecte les données de médias en flux continu.
exl-id: f486d729-b7ad-4720-8399-71495cb9c57e
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 4%

---

# Paramètres de configuration du streaming multimédia {#streaming-media}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_streamingmedia"
>title="Streaming de médias"
>abstract="Détermine la manière dont les données multimédia en flux continu sont collectées pendant les sessions de lecture multimédia."

La fonctionnalité de collecte de médias vous permet de collecter des données relatives aux sessions de médias, telles que les lectures de médias, les pauses, les fins de session et d’autres événements associés. Une fois collectées, vous pouvez envoyer ces données à Adobe Experience Platform ou Adobe Analytics pour générer des rapports. Cette fonctionnalité fournit une solution complète pour suivre et comprendre le comportement de consommation des médias sur votre site web.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Streaming media]** .

![Image montrant les paramètres de collection de médias de l’extension de balise Web SDK dans l’interface utilisateur des balises](../assets/media-collection.png)

## Conditions préalables

Pour utiliser le composant Streaming Media du Web SDK, vous devez remplir les conditions préalables suivantes :

* Assurez-vous d’avoir accès à Adobe Experience Platform ou Adobe Analytics.
* Activez l’option **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** pour le flux de données que vous utilisez.
* Assurez-vous que le schéma utilisé par votre flux de données comprend les champs de schéma Media Collection.
* Configurez la fonction Streaming Media dans l’extension de balises Web SDK, comme illustré sur cette page.

## [!UICONTROL Channel]

Nom du canal sur lequel la collecte de médias a lieu. Par exemple : `Video channel`. Toute valeur de chaîne est valide.

## [!UICONTROL Player Name]

Nom du lecteur multimédia que votre propriété utilise pour la lecture multimédia.

## [!UICONTROL Application Version]

Version de l’application du lecteur multimédia que votre propriété utilise pour la lecture multimédia.

## [!UICONTROL Main ping interval]

Fréquence des pings pour le contenu principal, en secondes. La valeur par défaut est `10`. Les valeurs peuvent aller de `10` à `50` secondes. Si aucune valeur n’est spécifiée, la valeur par défaut est utilisée lors de l’utilisation de [sessions suivies automatiquement](/help/collection/js/commands/createmediasession.md#automatic).

## [!UICONTROL Ad ping interval]

Fréquence des pings pour le contenu publicitaire, en secondes. La valeur par défaut est `10`. Les valeurs peuvent aller de `1` à `10` secondes. Si aucune valeur n’est spécifiée, la valeur par défaut est utilisée lors de l’utilisation de [sessions suivies automatiquement](/help/collection/js/commands/createmediasession.md#automatic).
