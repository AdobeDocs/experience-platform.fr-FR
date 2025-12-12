---
title: Paramètres de configuration de Personalization
description: Configurez les paramètres de personnalisation dans l’extension de balise Web SDK.
source-git-commit: 9a617b6e97aec22a6726266f2628bd2c2a05da19
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# Paramètres de configuration de Personalization

Cette section de configuration vous permet de déterminer comment masquer certaines parties de la page lors du chargement du contenu personnalisé. Lorsqu’ils sont configurés correctement, ces paramètres garantissent que vos visiteurs voient le contenu personnalisé approprié.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Personalization]** .

![Image montrant les paramètres de personnalisation de l’extension de balise Web SDK dans l’interface utilisateur des balises](../assets/web-sdk-ext-personalization.png)

Les options disponibles sont les suivantes :

## [!UICONTROL Migrate Target from at.js to the Web SDK]**

Utilisez cette option pour permettre à Web SDK de lire et d’écrire les `mbox` hérités et les cookies `mboxEdgeCluster` utilisés par les bibliothèques `at.js` 1.x ou 2.x. Ce paramètre permet de conserver les profils des visiteurs intacts lorsqu’ils se déplacent entre les pages à l’aide de Web SDK ou de `at.js` sur le même site Web. Si aucune `at.js` n’est implémentée sur votre site, il n’est pas nécessaire d’activer cette case à cocher. La bibliothèque JavaScript équivalente à cette case à cocher est [`targetMigrationEnabled`](/help/collection/js/commands/configure/targetmigrationenabled.md).

Lors de l’activation de cette option, veillez à activer également le [`overrideMboxEdgeServer`](https://experienceleague.adobe.com/fr/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver) dans `targetGlobalSettings()`.

## [!UICONTROL Prehiding style] {#prehiding-style}

L’éditeur de style de masquage préalable vous permet de définir des règles CSS personnalisées pour masquer des sections spécifiques d’une page. Lorsque la page est chargée, le SDK Web utilise ce style pour masquer les sections à personnaliser, récupérer la personnalisation, puis annuler le masquage des sections de page personnalisées. Ce workflow permet aux visiteurs de voir le contenu personnalisé sans voir le processus de récupération de la personnalisation se charger ou scintiller. La bibliothèque JavaScript équivalente à cet éditeur de code est [`prehidingStyle`](/help/collection/js/commands/configure/prehidingstyle.md).

## [!UICONTROL Prehiding snippet] {#prehiding-snippet}

Cette section n’est pas un paramètre de configuration direct, mais plutôt un emplacement pratique où vous pouvez obtenir du code d’implémentation. Implémentez ce fragment de code de masquage préalable dans la balise `<head>` de votre site pour masquer le contenu souhaité pendant le chargement de la bibliothèque Web SDK.

>[!IMPORTANT]
>
>Lors de l’utilisation du fragment de code de masquage préalable, Adobe recommande d’utiliser la même règle CSS entre le fragment de code de masquage préalable et le style de masquage préalable.

## [!UICONTROL Enable personalization storage]

Case à cocher qui permet au SDK Web de stocker les événements de personnalisation. dans l’espace de stockage local du navigateur. Il s’avère utile lorsque vous souhaitez suivre les expériences que le visiteur a vues à travers les chargements de page.

## [!UICONTROL Auto click collection for Adobe Journey Optimizer]

Un menu déroulant qui détermine à quel moment le SDK Web collecte automatiquement les clics sur le contenu renvoyé par Adobe Journey Optimizer.

* **[!UICONTROL Always]** : permet de collecter toutes les interactions avec les propositions.
* **[!UICONTROL Decorated elements only]** : collecte uniquement les interactions sur les éléments ayant des attributs HTML `data-aep-click-label` ou `data-aep-click-token`.
* **[!UICONTROL Never]** : ne collectez pas les interactions avec les propositions.

La bibliothèque JavaScript équivalente à ce menu déroulant est [`autoCollectPropositionInteractions.AJO`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md). Sa valeur par défaut est [!UICONTROL Always].

## [!UICONTROL Auto click collection for Adobe Target]

Un menu déroulant qui détermine à quel moment le SDK Web collecte automatiquement les clics sur le contenu renvoyé par Adobe Target.

* **[!UICONTROL Always]** : permet de collecter toutes les interactions avec les propositions.
* **[!UICONTROL Decorated elements only]** : collecte uniquement les interactions sur les éléments ayant des attributs HTML `data-aep-click-label` ou `data-aep-click-token`.
* **[!UICONTROL Never]** : ne collectez pas les interactions avec les propositions.

La bibliothèque JavaScript équivalente à ce menu déroulant est [`autoCollectPropositionInteractions.TGT`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md). Sa valeur par défaut est [!UICONTROL Never].
