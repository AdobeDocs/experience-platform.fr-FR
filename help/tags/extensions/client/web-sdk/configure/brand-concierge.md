---
title: Paramètres de configuration de Brand Concierge
description: Configurez la persistance de session et les délais d’expiration de diffusion pour la conversation Brand Concierge.
exl-id: d5c0bdf7-563d-4e0e-9b1b-71e2fa783e29
source-git-commit: 9f7464b78da9615bf6966e34eb129150a481fb5f
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 21%

---

# Paramètres de configuration de Brand Concierge {#brand-concierge}

>[!AVAILABILITY]
>
>Brand Concierge pour le SDK Web est actuellement en version **bêta**. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_brandconcierge"
>title="Brand Concierge"
>abstract="Paramètres de configuration lors de l’utilisation de Brand Concierge sur votre propriété."

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

## [!UICONTROL Collect sources]

Case à cocher qui collecte les sources si un utilisateur a accédé à la page à partir d’un lien dans une conversation Brand Concierge. Décoché par défaut. Si cette option est activée, la bibliothèque vérifie le paramètre de chaîne de requête `adobe_brand_concierge_source` et renseigne sa valeur dans `xdm.channel.referringSource`.
