---
title: Paramètres de configuration de Brand Concierge
description: Configurez la persistance de session et les délais d’expiration de diffusion pour la conversation Brand Concierge.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 15%

---

# Paramètres de configuration de Brand Concierge

>[!AVAILABILITY]
>
>Brand Concierge pour le SDK Web est actuellement en version **bêta**. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

La section **[!UICONTROL Brand Concierge]** vous permet de contrôler le comportement des sessions de conversation Brand Concierge dans l’extension de balise Web SDK.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Brand Concierge]** .

Les options disponibles sont les suivantes :

## [!UICONTROL Sticky conversation session]

Une case à cocher qui conserve les sessions Brand Concierge sur plusieurs chargements de page à l’aide d’un cookie de session. Par défaut, cette option est désactivée. Voir [`conversation`](/help/collection/js/commands/configure/conversation.md) dans la documentation de la bibliothèque JavaScript pour obtenir des conseils sur la définition de cette valeur.

## [!UICONTROL Stream timeout (seconds)]

Durée maximale d’attente, en secondes, des blocs de flux de conversation avant de déclencher une erreur de temporisation. La valeur par défaut est de `10` secondes.
