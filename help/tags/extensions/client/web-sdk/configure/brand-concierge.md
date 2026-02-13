---
title: Paramètres de configuration de Brand Concierge
description: Configurez la persistance de session et les délais d’expiration de diffusion pour la conversation Brand Concierge.
exl-id: d5c0bdf7-563d-4e0e-9b1b-71e2fa783e29
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 15%

---

# Paramètres de configuration de Brand Concierge {#brand-concierge}

>[!AVAILABILITY]
>
>Brand Concierge pour le SDK Web est actuellement en version **bêta**. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_brandconcierge"
>title="Brand Concierge"
>abstract="Paramètres de configuration lors de l’utilisation de Brand Concierge sur votre propriété"

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
