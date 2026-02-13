---
title: Paramètres de remplacement de la configuration du flux de données
description: Modifier les paramètres de configuration lorsque certaines conditions sont remplies
exl-id: 68227148-3d74-4807-836c-14acd8a9c1dc
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 3%

---

# Paramètres de remplacement de la configuration du flux de données {#config-overrides}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_overrides"
>title="Remplacements de la configuration des trains de données"
>abstract="Déclenchez de manière conditionnelle différents comportements de flux de données sans avoir besoin d’un flux de données distinct. La définition de toute configuration de train de données côté client remplace pour un environnement dans cette section remplace toute configuration de train de données dynamique côté serveur et les règles pour cet environnement."

Les remplacements de flux de données vous permettent de définir des configurations supplémentaires pour vos flux de données, qui sont transmises à Edge Network via le SDK Web. Cette fonctionnalité vous permet de déclencher de manière conditionnelle différents comportements de flux de données sans créer de flux de données ni modifier vos paramètres existants.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Datastream configuration overrides]** .

Le remplacement de la configuration du train de données comporte deux étapes :

1. Tout d’abord, vous devez définir le remplacement de votre configuration de train de données lors de la [configuration d’un train de données](/help/datastreams/configure.md) dans l’interface utilisateur des trains de données. Consultez [Remplacements de la configuration des trains de données](/help/datastreams/overrides.md) dans la documentation sur les trains de données pour obtenir des instructions sur la configuration des remplacements.
1. Après avoir configuré le remplacement du flux de données dans l’interface utilisateur des flux de données, vous pouvez configurer l’extension de balise.

Les remplacements de flux de données doivent être configurés pour chaque environnement. Les environnements de développement, d’évaluation et de production ont tous des remplacements distincts. Vous pouvez copier les paramètres de remplacement dans n’importe quel environnement souhaité :

![Image montrant les remplacements de la configuration du train de données à l’aide de la page d’extension de balise Web SDK.](../assets/datastream-overrides.png)

Par défaut, les remplacements de la configuration du train de données sont désactivés. L’option **[!UICONTROL Match datastream configuration]** est sélectionnée par défaut.

![L’interface utilisateur de l’extension de balise Web SDK affichant la configuration du flux de données remplace le paramètre par défaut.](../assets/datastream-override-default.png)

Pour activer les remplacements de train de données dans l’extension de balise, sélectionnez **[!UICONTROL Enabled]** dans le menu déroulant.

![L’interface utilisateur de l’extension de balise Web SDK affiche le paramètre Remplacements de la configuration des trains de données activés.](../assets/datastream-override-enabled.png)

Après avoir activé les remplacements de la configuration du train de données, vous pouvez configurer les remplacements pour chaque service décrit ci-dessous. Ces paramètres de remplacement de train de données remplacent toutes les configurations et règles de train de données côté serveur pour l’environnement sélectionné.

## Adobe Analytics

Remplacez le routage des données par le service Adobe Analytics.

![Image de l’interface utilisateur de l’extension de balise Web SDK montrant les paramètres de remplacement du flux de données Adobe Analytics.](../assets/datastream-override-analytics.png)

* **[!UICONTROL Enabled]**/**[!UICONTROL Disabled]** : active ou désactive le routage des données vers Adobe Analytics.
* **[!UICONTROL Report suites]** : identifiants des suites de rapports de destination dans Adobe Analytics. La valeur doit être une suite de rapports de remplacement préconfigurée (ou une liste de suites de rapports séparées par des virgules) de votre configuration de train de données. Ce paramètre remplace les suites de rapports principales.
* **[!UICONTROL Add Report Suite]** : sélectionnez cette option pour ajouter des suites de rapports supplémentaires.

## Adobe Audience Manager

Remplacez le routage des données par Adobe Audience Manager.

![Image de l’interface utilisateur de l’extension de balise Web SDK montrant les paramètres de remplacement du flux de données Adobe Audience Manager.](../assets/datastream-override-audience-manager.png)

* **[!UICONTROL Enabled]**/**[!UICONTROL Disabled]** : active ou désactive le routage des données vers Adobe Audience Manager.
* **[!UICONTROL Third-party ID sync container]** : ID du conteneur de synchronisation des identifiants tiers de destination dans Audience Manager. La valeur doit être un conteneur secondaire préconfiguré de votre configuration de train de données et remplace le conteneur principal.

## Adobe Experience Platform

Remplacez le routage des données par Adobe Experience Platform.

![Image de l’interface utilisateur de l’extension de balise Web SDK montrant les paramètres de remplacement du flux de données Adobe Experience Platform.](../assets/datastream-override-experience-platform.png)

* **[!UICONTROL Enabled]**/**[!UICONTROL Disabled]** : active ou désactive le routage des données vers Adobe Experience Platform.
* **[!UICONTROL Event dataset]** : identifiant du jeu de données d’événement de destination dans le Adobe Experience Platform. La valeur doit être un jeu de données secondaire préconfiguré de votre configuration de train de données.
* **[!UICONTROL Offer Decisioning]** : activer ou désactiver le routage des données vers le service [!DNL Offer Decisioning].
* **[!UICONTROL Edge Segmentation]** : activer ou désactiver le routage des données vers le service [!DNL Edge Segmentation].
* **[!UICONTROL Personalization Destinations]** : activer ou désactiver le routage des données vers les destinations de personnalisation.
* **[!UICONTROL Adobe Journey Optimizer]** : activer ou désactiver le routage des données vers [!DNL Adobe Journey Optimizer].

## Transfert d’événement côté serveur Adobe

Remplacez le routage des données par le service Transfert d’événement côté serveur d’Adobe.

![Image de l’interface utilisateur de l’extension de balise Web SDK montrant les paramètres de remplacement du flux de données de transfert d’événement côté serveur Adobe.](../assets/datastream-override-ssf.png)

* **[!UICONTROL Enabled]**/**[!UICONTROL Disabled]** : active ou désactive le routage des données vers le service de transfert d’événement côté serveur d’Adobe.

## Adobe Target {#target}

Remplacez le routage des données par Adobe Target.

![Image de l’interface utilisateur de l’extension de balise Web SDK montrant les paramètres de remplacement du flux de données Adobe Target.](../assets/datastream-override-target.png)

* **[!UICONTROL Enabled]**/**[!UICONTROL Disabled]** : active ou désactive le routage des données vers Adobe Target.
