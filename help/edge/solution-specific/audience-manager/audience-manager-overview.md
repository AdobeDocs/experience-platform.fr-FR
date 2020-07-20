---
title: Envoi de données à l'Adobe Audience Manager
seo-title: Envoi de données à l'Adobe Audience Manager avec le SDK Web Adobe Experience Platform
description: Découvrez comment envoyer des données à l'Adobe Audience Manager avec le SDK Web Experience Platform
seo-description: Découvrez comment envoyer des données à l'Adobe Audience Manager avec le SDK Web Experience Platform
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# [!DNL Audience Manager] sur la [!DNL Experience Platform Edge Network]

L’Adobe Experience Platform [!DNL Web SDK] est intégré à l’Adobe Audience Manager et prend en charge l’envoi et la réception de données à partir de [!DNL Audience Manager]destinations, de cookies et d’URL, ainsi que la synchronisation des identifiants.

## Activation [!DNL Audience Manager]

Pour activer [!DNL Audience Manager] cette fonction, vous devez effectuer les opérations suivantes :

- Activez [!DNL Audience Manager] la configuration [de votre](../../fundamentals/edge-configuration.md)bord.
- Activez ou désactivez les destinations de cookie et d’URL.
- Spécifiez votre Conteneur de synchronisation des identifiants pour les synchronisations de partenaires externes (facultatif).

## Synchronisation des identités

L&#39;Adobe Experience Platform [!DNL Web SDK] prend en charge la possibilité de déclarer les ID de client et leurs états d&#39;authentification via la commande [SyncIdentity](../../fundamentals/identity.md) .

La méthode syncIdentity utilise des Espaces de nommage [](../../../identity/../identity-service/namespaces.md) Identity Service pour indiquer le contexte auquel une identité se rapporte. En tant que [!DNL Audience Manager] client, toutes vos sources de données existantes qui utilisent le type d’ID : Les périphériques croisés auront automatiquement un [!DNL Identity Namespace]lien correspondant. Pour trouver le code correspondant [!DNL Identity Namespace] pour votre [!DNL Audience Manager Data Source]site, connectez-vous à l’Adobe Experience Platform et accédez à la [!DNL Identities] section.

![Vue de l’interface utilisateur Espaces de nommage](../../../assets/edge_configuration_identity.png)

Ici, vous pouvez rechercher votre source de données par nom. [!DNL Audience Manager] La méthode syncIdentity utilise le symbole d&#39;identité pour indiquer l&#39;Espace de nommage.

Toute nouvelle source [!DNL Audience Manager] de données qui utilise le type d’ID : Un Espace de nommage d&#39;identité est généré sur plusieurs périphériques. Les types d’ID de source de données Cookie et ID de publicité de périphérique ne sont pas pris en charge actuellement. De plus, tout Espace de nommage d&#39;identité créé dans l&#39;Adobe Experience Platform génère une source de données correspondante, mais notez que la méthode syncIdentity ne prend en charge que les symboles d&#39;identité de l&#39;Espace de nommage. [!DNL Audience Manager]
