---
title: Envoi de données à Adobe Audience Manager
seo-title: Envoi de données à Adobe Audience Manager avec le SDK Web Adobe Experience Platform
description: Découvrez comment envoyer des données à Adobe Audience Manager avec le SDK Web Experience Platform
seo-description: Découvrez comment envoyer des données à Adobe Audience Manager avec le SDK Web Experience Platform
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Audience Manager] sur la [!DNL Experience Platform Edge Network]

Le Adobe Experience Platform [!DNL Web SDK] est intégré à Adobe Audience Manager et prend en charge l’envoi et la réception de données à partir de [!DNL Audience Manager]destinations de cookies et d’URL, ainsi que la synchronisation des identifiants.

## Activation [!DNL Audience Manager]

Pour activer [!DNL Audience Manager] cette fonction, vous devez effectuer les opérations suivantes :

- Activez [!DNL Audience Manager] la configuration [de votre](../../fundamentals/edge-configuration.md)bord.
- Activez ou désactivez les destinations de cookie et d’URL.
- Spécifiez votre Conteneur de synchronisation des identifiants pour les synchronisations de partenaires externes (facultatif).

## Synchronisation des identités

Le SDK Web Adobe Experience Platform prend en charge la possibilité de déclarer les ID de client et leurs états d’authentification par le biais de la commande [sendEvent](../../fundamentals/identity.md#syncing-identities) .

Choisissez vos espaces de nommage dans les Espaces de nommage [](../../../identity/../identity-service/namespaces.md) Identity Service pour indiquer le contexte auquel une identité se rapporte, en utilisant les valeurs de la colonne Identity Symbol :

![Vue de l’interface utilisateur Espaces de nommage](../../../assets/edge_namespaceUI_identity-symbol.png)

En tant que client d’Audience Manager, toutes vos sources de données existantes qui utilisent le type d’ID : L&#39;Espace de nommage d&#39;identité est automatiquement associé à plusieurs périphériques. Pour trouver l&#39;Espace de nommage d&#39;identité correspondant à votre source de données d&#39;Audience Manager, connectez-vous au Adobe Experience Platform et accédez à la section Identités.

Toute nouvelle source [!DNL Audience Manager] de données qui utilise le type d’ID : Un Espace de nommage d&#39;identité est généré sur plusieurs périphériques. Les types d’ID de source de données Cookie et ID de publicité de périphérique ne sont pas pris en charge actuellement. De plus, tout Espace de nommage d&#39;identité créé dans Adobe Experience Platform génère une source de données correspondante, mais notez que la méthode syncIdentity ne prend en charge que les symboles d&#39;identité de l&#39;Espace de nommage. [!DNL Audience Manager]
