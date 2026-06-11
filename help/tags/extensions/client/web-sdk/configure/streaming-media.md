---
title: Paramètres de configuration des médias en streaming
description: Personnalisez la manière dont l’extension de balise Web SDK collecte les données de médias en flux continu.
exl-id: f486d729-b7ad-4720-8399-71495cb9c57e
TQID: https://experienceleague.adobe.com/Oimv345d5pcvdhA0O4JyayB1Z5ZXXGGak-9tWgkA1Nk
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: ca3d6bf4-a4af-4944-936b-8de1eb09f149id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 60dfb3bf6044036be567e46c3807b48408ea3477
workflow-type: tm+mt
source-wordcount: 339
ht-degree: 10%

---

# Paramètres de configuration des médias en streaming {#streaming-media}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_streamingmedia"
>title="Médias en streaming"
>abstract="Détermine la manière dont les données des médias en streaming sont collectées pendant les sessions de lecture multimédia."

La fonctionnalité de collecte de médias vous permet de collecter des données relatives aux sessions de médias, telles que les lectures de médias, les pauses, les fins de session et d’autres événements associés. Une fois collectées, vous pouvez envoyer ces données à Adobe Experience Platform ou Adobe Analytics pour générer des rapports. Cette fonctionnalité fournit une solution complète pour suivre et comprendre le comportement de consommation des médias sur votre site web.

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configurer]** sur la vignette [!UICONTROL Adobe Experience Platform Web SDK].
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Médias en flux continu]**.

![Image montrant les paramètres de collection de médias de l’extension de balise Web SDK dans l’interface utilisateur des balises](../assets/media-collection.png)

## Conditions préalables

Pour utiliser le composant Streaming Media du Web SDK, vous devez remplir les conditions préalables suivantes :

* Assurez-vous d’avoir accès à Adobe Experience Platform ou Adobe Analytics.
* Activez l’option **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** pour le flux de données que vous utilisez.
* Assurez-vous que le schéma utilisé par votre flux de données comprend les champs de schéma Media Collection.
* Configurez la fonction Streaming Media dans l’extension de balises Web SDK, comme illustré sur cette page.

## [!UICONTROL Canal]

Nom du canal sur lequel la collecte de médias a lieu. Par exemple : `Video channel`. Toute valeur de chaîne est valide.

## [!UICONTROL Nom du lecteur]

Nom du lecteur multimédia que votre propriété utilise pour la lecture multimédia.

## [!UICONTROL Version de l’application]

Version de l’application du lecteur multimédia que votre propriété utilise pour la lecture multimédia.

## [!UICONTROL Intervalle de ping principal]

Fréquence des pings pour le contenu principal, en secondes. La valeur par défaut est `10`. Les valeurs peuvent aller de `10` à `50` secondes. Si aucune valeur n’est spécifiée, la valeur par défaut est utilisée lors de l’utilisation de [sessions suivies automatiquement](/help/collection/js/commands/createmediasession.md#automatic).

## [!UICONTROL Intervalle de ping des annonces]

Fréquence des pings pour le contenu publicitaire, en secondes. La valeur par défaut est `10`. Les valeurs peuvent aller de `1` à `10` secondes. Si aucune valeur n’est spécifiée, la valeur par défaut est utilisée lors de l’utilisation de [sessions suivies automatiquement](/help/collection/js/commands/createmediasession.md#automatic).
