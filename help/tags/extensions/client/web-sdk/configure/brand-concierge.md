---
title: Paramètres de configuration de Brand Concierge
description: Configurez les paramètres souhaités pour la conversation Brand Concierge.
exl-id: d5c0bdf7-563d-4e0e-9b1b-71e2fa783e29
source-git-commit: 60dfb3bf6044036be567e46c3807b48408ea3477
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 12%

---

# Paramètres de configuration de Brand Concierge {#brand-concierge}

>[!AVAILABILITY]
>
>Brand Concierge pour le SDK Web est actuellement en version **bêta**. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_brandconcierge"
>title="Brand Concierge"
>abstract="Paramètres de configuration lors de l’utilisation de Brand Concierge sur votre propriété."

La section **&#x200B;**&#x200B;vous permet de contrôler le comportement des sessions de conversation Brand Concierge dans l’extension de balise Web SDK.

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configurer]** sur la vignette [!UICONTROL Adobe Experience Platform Web SDK].
1. Faites défiler l’écran jusqu’à la section **&#x200B;**.

Les options suivantes sont disponibles. Pour obtenir des paramètres de bibliothèque JavaScript équivalents, consultez [`conversation`](/help/collection/js/commands/configure/conversation.md) dans la documentation de Web SDK.

## [!UICONTROL Région]

Champ de texte qui achemine les demandes de conversation Brand Concierge vers un centre de données spécifique au lieu du centre disponible le plus proche. La plupart des organisations n’ont pas besoin de définir cette valeur. Définissez-le uniquement si les événements de conversation n’arrivent pas au centre de données souhaité.

Ce paramètre affecte uniquement les événements de conversation ; les commandes d’événement d’envoi standard ne sont pas affectées. `va7`, `or2` ou `irl1` sont des exemples de valeurs possibles.

## [!UICONTROL Session de conversation persistante]

Une case à cocher qui conserve les sessions Brand Concierge sur plusieurs chargements de page à l’aide d’un cookie de session. Par défaut, cette option est désactivée.

## [!UICONTROL Délai d’expiration du flux (secondes)]

Durée maximale d’attente, en secondes, des blocs de flux de conversation avant de déclencher une erreur de temporisation. La valeur par défaut est de `10` secondes.

## [!UICONTROL Collecter des sources]

Case à cocher qui collecte les sources si un utilisateur a accédé à la page à partir d’un lien dans une conversation Brand Concierge. Décoché par défaut. Si cette option est activée, la bibliothèque vérifie le paramètre de chaîne de requête `adobe_brand_concierge_source` et renseigne sa valeur dans `xdm.channel.referringSource`.
